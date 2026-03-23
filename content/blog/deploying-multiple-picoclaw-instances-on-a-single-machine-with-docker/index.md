---
title: Deploying Multiple PicoClaw Instances on a Single Machine with Docker
date: 2026-03-13
summary: How to run two PicoClaw Docker Compose deployments on one machine by removing fixed container names, separating repo state, and using explicit project names.
feature: "monika-borys-DStJr8oJurw-unsplash.jpg"
featureAlt: "Photo of two different coloured lobsters"
description: "How I ran two PicoClaw deployments on one machine: remove fixed container names, use separate repo state, and start each stack with explicit Docker Compose project names."
tags: 
  - docker
  - docker-compose
  - picoclaw
  - self-hosting
  - devops
---
## Context and goal

If you have not used it yet, [PicoClaw](https://picoclaw.ai/) is a lightweight way to run AI agents locally with tools, a workspace, and long running workflows. I liked that balance because it was practical to try on a personal laptop without building a large platform first.

My goal was simple from the start: run **two PicoClaw instances** on one machine. I wanted one instance for experimentation and one instance that stayed stable for my wife. I first tried a single repo with two instances. That approach quickly failed because both agents touched shared repo state and the Docker setup became harder to reason about.

I moved to duplicate repos and treated each deployment as an independent unit:

- `~/picoclaw` for my instance
- `~/picoclaw-2` for my wife's instance

This post covers what blocked parallel runs and the exact setup that worked.

## The Compose setup that caused the conflict

My original Compose file was:

```yaml
services:
  picoclaw-agent:
    image: docker.io/sipeed/picoclaw:latest
    container_name: picoclaw-agent
    volumes:
      - ./data:/root/.picoclaw

  picoclaw-gateway:
    image: docker.io/sipeed/picoclaw:latest
    container_name: picoclaw-gateway
    volumes:
      - ./data:/root/.picoclaw
```

Each repo had its own `./data`, which was good. The real blocker was `container_name`: Docker container names are global on the host, not scoped to the repo directory.

## Why two instances would not run in parallel

### 1. The `container_name` values collided globally

Both repos tried to create:

- `picoclaw-agent`
- `picoclaw-gateway`

So the second stack failed immediately.

### 2. Shared bot credentials can also conflict

Even after fixing Docker naming, gateway deployments can still conflict if both instances use the same Telegram bot token. One token usually expects one active polling client, so each always on gateway should use its own token.

### 3. Ports can become a problem later

My setup did not expose host ports, so this was not the first issue. If you later add `ports:` for a UI or endpoint, those host ports also need to be unique per instance.

## The key fix

The most useful change was to remove `container_name` completely.

```yaml
services:
  picoclaw-agent:
    image: docker.io/sipeed/picoclaw:latest
    volumes:
      - ./data:/root/.picoclaw

  picoclaw-gateway:
    image: docker.io/sipeed/picoclaw:latest
    volumes:
      - ./data:/root/.picoclaw
```

This hands naming back to Docker Compose.

Without `container_name`, Compose generates names using the project name, for example:

- `picoclaw1-picoclaw-gateway-1`
- `picoclaw2-picoclaw-gateway-1`

Project names also separate networks and named volumes, so they are the clean way to run multiple deployments of the same stack on one machine.

## How I set up the second repo

### 1. Keep two separate repos

- `~/picoclaw` for my instance
- `~/picoclaw-2` for my wife's instance

### 2. Remove `container_name` in both repos

In each `docker/docker-compose.yml`, remove:

```yaml
container_name: picoclaw-agent
container_name: picoclaw-gateway
```

If you also use `docker-compose.full.yml`, remove the matching `container_name` lines there too.

### 3. Keep data and config separate per repo

Simple setup:

```bash
docker/data
```

With mounted config:

```bash
config/config.json
```

### 4. Start each stack with an explicit project name

From repo one:

```bash
docker compose -f docker/docker-compose.yml -p picoclaw1 --profile gateway up -d
```

From repo two:

```bash
docker compose -f docker/docker-compose.yml -p picoclaw2 --profile gateway up -d
```

This keeps service names unchanged in Compose while giving each stack a separate Docker identity.

## Commands I kept handy

Inspect running containers:

```bash
docker ps --format "table {{.Names}}\t{{.Image}}\t{{.Status}}"
```

Follow logs for my instance:

```bash
docker compose -f docker/docker-compose.yml -p picoclaw1 logs -f picoclaw-gateway
```

Follow logs for my wife's instance:

```bash
docker compose -f docker/docker-compose.yml -p picoclaw2 logs -f picoclaw-gateway
```

Stop my stack:

```bash
docker compose -f docker/docker-compose.yml -p picoclaw1 down
```

Stop the second stack:

```bash
docker compose -f docker/docker-compose.yml -p picoclaw2 down
```

## Why this works well with Docker Desktop

I mainly use terminal commands for initial setup. After that, Docker Desktop is easier to use because the two stacks appear as separate Compose projects. That matches the operational goal: one stable instance and one flexible instance.

## OpenAI OAuth on the second repo

I wanted auth state to stay local to the second repo. Because the service entrypoint is `picoclaw agent`, I overrode entrypoint for login:

```bash
docker compose -f docker/docker-compose.yml run --rm \
  --entrypoint picoclaw \
  picoclaw-agent \
  auth login --provider openai --device-code
```

Then I verified it:

```bash
docker compose -f docker/docker-compose.yml run --rm \
  --entrypoint picoclaw \
  picoclaw-agent \
  status
```

This keeps OAuth state tied to the second repo's mounted PicoClaw directory.

## What I learned

Filesystem duplication and Docker isolation are different things. Copying a repo gives separate files, but runtime identity still depends on Compose project and container definitions.

`container_name` feels helpful for one stack and becomes friction for two.

Duplicate repos are a valid tradeoff when the priority is preserving one known good deployment while experimenting in another.

## The setup I am keeping

- one repo per PicoClaw instance
- separate data and config per repo
- no `container_name` in Compose
- explicit project names such as `picoclaw1` and `picoclaw2`
- Docker Desktop for routine operation, terminal for setup tasks

This is less elegant on paper than one shared repo, but it matches the practical goal of stability plus safe experimentation.
