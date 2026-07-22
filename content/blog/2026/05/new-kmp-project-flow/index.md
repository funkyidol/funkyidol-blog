---
title: Starting a Production Kotlin Multiplatform Project with a Spec-Driven Agentic Workflow
date: 2026-05-09
draft: false
summary: A field note on spending two days setting up a production-intended Kotlin Multiplatform project before writing meaningful product code.
description: A field note on spending two days setting up a production-intended Kotlin Multiplatform project before writing meaningful product code.
tags:
  - kotlin-multiplatform
  - android
  - agentic-workflow
  - spec-driven-development
  - software-architecture
  - engineering-process
feature: kmp_project_flow.jpeg
featureAlt: Photo of the notepad with handwritten text showing the flow of steps
---
# Starting a Production Kotlin Multiplatform Project with a Spec-Driven Agentic Workflow

The following post is a field notes post about the process I followed for a new Kotlin Multiplatform project that I want to ship as a product soon.

I am embracing the whole agentic development workflow with this project, but I did not want it to become a vibe-coded POC that I would have to trash or rewrite in the near future.

It has to be built properly.  
It has to work with confidence, as intended.  
It has to be maintainable.

I wanted to pour in all my years of experience into this project and make something I could be proud of, even if I might not write every single line myself. It needs to look like it was built by a thoughtful team, not assembled randomly by prompts.

I could have easily hit the ground running with a vibe-coded project. But from my recent experience with agentic coding, I have had enough insight to know that you cannot just let an LLM run amok and expect a well-built solution.

It has to be guided. 
It has to be guard-railed. 
It has to be nudged and corrected continuously. 
**Most of all, it cannot be trusted blindly.**

For this project, I wanted a clear specification, a scoped implementation path, a task breakdown and an agentic workflow that could help me build without constantly expanding the project in random directions.

Not a perfect process. Not a universal template. Just the flow I used to move from idea to a serious, buildable foundation.

## Why I did not start with code

One of the biggest risks with AI-assisted development is that it makes starting feel deceptively easy. I have created many experimental projects in recent months where this made life much easier. This website itself started off as a vibe-coded project.

You can ask an agent to create the app structure, generate screens, add navigation, wire dependencies, create test files and suggest architecture. In a few minutes, the project looks active. There are files. There is code. There is movement.

But movement is not the same as progress.

For a production project, the hard part is rarely just "writing the code". The harder questions are about direction. What exactly are we building? What is the first usable version? What should be deferred? What assumptions are risky? Which parts need architectural care now and which parts can stay simple?

It is all about product-first thinking and mindset.

If those decisions are not made clearly, AI tools tend to amplify ambiguity. They produce more surface area before the product shape is stable.

Since I knew exactly where things could go wrong, I decided to start by putting in proper foundational work.

The rough flow looked like this:

```text
Requirement analysis and brainstorming
→ Create PRD
→ Create alpha implementation plan
→ Break down tasks and create a task tracker
→ Create project from starter template
→ Set up AGENTS.md using the PRD as guidance
→ Create sub-agents for manager, developer, tester and designer roles
→ Run a scope audit and break the initial scope into smaller milestones
→ Update helper agents and coding skills for implementation and review
→ Add core dependencies for DI, logging, navigation and testing
```

This took about two days.

At the end of it, I did not have a flashy demo. But I had something more useful for this stage: a clear vision of what needed to be built and how.

## The PRD became the anchor

The first real artifact I created was the PRD.

I did not treat it as a corporate document or a formality. I treated it as the anchor for the entire project. The PRD captured what the product is supposed to do, who it is for, what the initial version should include and **what should deliberately stay out of scope.**

That last part matters a lot.

When working with agents, the problem is rarely lack of ideas. It is too many ideas. Agents are very good at suggesting "also add this" or "you may want to support that". Sometimes those suggestions are useful, but early in a project they can quickly turn a focused build into a giant mess.

**This is where I apply first-principles thinking.** 
What's the core of the problem I'm trying to solve? 
Why will anyone come back to use the app? 
How can I reduce the product to a one line problem statement?

The PRD gave me a reference point. Whenever I moved into planning, task breakdown, or agent instructions, I could come back to the same source of truth. Does this belong in the first version? Is this part of the user journey? Is this a real requirement or just an attractive distraction?

Writing this document also gave me a good picture of where the product could go in the future, what direction I might take it in and what features I could add later. But I documented those outside the PRD to keep the PRD focused on the task at hand.

This clarity made the next steps easier.

## From product intent to implementation plan

After the PRD, I created an alpha implementation plan.

The distinction between the PRD and the implementation plan was important for me. The PRD described the product intent. The implementation plan described how I wanted to approach the first serious version.

For a Kotlin Multiplatform project, early technical choices matter. Project structure, shared modules, platform boundaries, navigation, dependency injection, persistence, logging and testing setup can either support the project or slow it down. But it is also easy to over-engineer too early.

The implementation plan helped me decide what deserved attention immediately and what could wait.

I wanted enough structure to avoid future mess, but not so much structure that the project became architecture-heavy before the product had earned it. This is one of the central tradeoffs in serious project setup: move too fast and you create debt; design too much and you create drag.

The alpha plan was my attempt to stay in the middle.
Ship ASAP, without regret.

## Breaking work down before assigning it to agents

Once the alpha plan was ready, I broke it down into tasks and created a task tracker.

This was one of the most important things to have when working with AI agents, not just humans. Every meaningful piece of work should be broken down into an exact action item, or context drift can take your project into uncharted waters without you noticing.

**Agentic workflows work better when the work is bounded.** A vague task like "build the app" gives the agent too much room to invent structure, behavior and priorities. A smaller task with clear inputs and expected output is much easier to review.

For example, instead of asking an agent to "set up navigation", the task can specify the expected screens, whether the screens are placeholders or functional, where navigation state should live and what tests or compile checks should exist after the task.

That level of task clarity makes agent output easier to evaluate. It also keeps me in control of the product and architecture instead of letting the tool silently make decisions for me.

The task tracker became the bridge between planning and execution.

One important thing I also included in the task tracker was the **product and technical decisions** I needed to make. Which SDKs should I use? What screen flow should the user have? Which auth providers should I include?

This helped me in two ways:
- Have a clear order of decisions that need to be taken before a given task
- Have a clear record of what decision was taken and why

## Creating the project only after the shape was clearer

Only after the PRD, implementation plan and task breakdown were in place did I create the actual Kotlin Multiplatform project.

I used a starter template because I did not want to spend time fighting the same setup problems every KMP project has: Gradle configuration, module layout, shared code setup, Compose wiring, platform entry points and test source sets. The official sources are usually up to date in that sense.

But I also did not want the template to become the architecture.

By the time I created the project, I had enough clarity to shape the template around the product instead of shaping the product around the template. The starter gave me a baseline. The PRD and implementation plan gave me direction.

## AGENTS.md as project memory

The next major step was creating an `AGENTS.md` file. This is where the agentic part of the project starts.

The main purpose of this file is to give every agent call a very clear set of instructions regarding the project requirements, architectural guidance, important considerations, custom test/lint scripts, important documents like the PRD, implementation plan, task tracker and more.

Without a file like this, every agent interaction starts from scratch. With it, the project has persistent context that can guide future work.

Hence, it was not as simple as calling `/init` on my CLI. The agents file created from this command is never super helpful. It typically contains no clear instruction, just a basic project intro, codebase structure and generic platform instructions.

My agents files are usually more targeted. Almost hand-crafted. And continuously improved, since they form the bedrock of the whole agent interaction.

I have a lot more to say about the `AGENTS.md` file, which I will cover in more detail in a future post.

## Creating sub-agents for different modes of thinking

After setting up the main project guidance, **I created sub-agents with specific responsibilities: manager, designer, developer and tester.**

The 'manager agent' helps with planning, sequencing, scope control and milestone clarity. 
The 'designer agent' helps review flows, usability and interaction quality. 
The 'developer agent' focuses on implementation. 
The 'tester agent' looks for missing cases, fragile assumptions and test coverage.

This separation is useful because a single agent often optimizes for forward motion. It wants to complete the requested task. But serious product work needs more than completion. It needs review, challenge, simplification and tradeoff analysis.

By creating sub-agents, I was trying to make those modes explicit. Reducing the scope of each sub-agent also allows for better session optimization and reduces context drift when running long or complex tasks.

By giving a very specific set of instructions to each sub-agent, you also get sharper scoping and more optimized token consumption. This prevents agents from doing things they are not supposed to do, which can lead to undesirable consequences. And because they are only doing very specific tasks, agents do not end up spending precious tokens on unnecessary work.

## The scope audit was the most valuable step

After the initial setup, I ran a scope audit.

This was the point where the process really proved useful.

Once the PRD, implementation plan, task tracker and agent roles were visible together, it became much easier to see that the initial scope was still too large. Nothing looked unreasonable in isolation. But as a whole, the first version had too much packed into it.

So I broke it down into smaller milestones.

This is a very normal product engineering moment. The first version always wants to become bigger. Every feature feels small. Every improvement feels sensible. Every "while we are here" feels efficient.

But production projects do not fail only because teams cannot build. They also fail because teams try to build too much before the product has enough feedback.

The scope audit helped me define what I should focus on first, so that I can start having people use the MVP and provide feedback.

Good thing I did. This alone made the two-day setup worth it.

## Improving the agents as the project became clearer

As the project became clearer, I updated the helper agents and their skill scope. I refined how they should write code, how they should analyze existing code, how they should approach tests and how they should avoid unnecessary expansion.

This felt similar to improving team onboarding material. The first version of the instructions is rarely perfect. But every planning decision, every scope cut and every architectural choice gives you better material to improve the workflow.

At this point, I was not just setting up the project. I was setting up the way the project should be worked on.

I pulled out a lot of the sub-agent-level instructions and converted them into `SKILLS.md` files:

- Design skills with focus on Material Design
- KMP skills
- Software architecture skills
- Unit testing skills
- UI automation testing skills
And so on..

If anything is a focus area, I created a skill for it. This allows agents and sub-agents to quickly find and follow specific instructions for that focus area and gain the laser focus needed to complete a task to the best of their ability.

## Dependencies came last

The final setup step was adding core dependencies for dependency injection, logging, navigation and test frameworks.

Normally, dependencies are one of the first things developers add. I have done that many times. Start the project, add the familiar libraries and then begin shaping the code.

This time, I wanted to delay that step until the product and implementation direction were clearer.

Dependencies should support decisions, not substitute for them.

By the time I added them, I had a better sense of the project’s initial milestones, architecture direction and testing expectations. That made the choices feel less automatic and more grounded. Additionally, it allowed me to skip dependencies that belonged to later milestones, reducing complexity and focusing only on the first `0.1_alpha` version.

## Why I focused on this for the first two days

The biggest reason for this setup is that AI-assisted development does not remove the need for engineering discipline. It increases the importance of it even further.

When implementation becomes faster, unclear thinking becomes more expensive. A weak requirement can turn into five unnecessary modules. A vague task can turn into a large diff that is hard to review. An undefined scope can become a product that looks busy but is not moving toward a clear first release.

For small experiments, that may be fine. Exploration is part of the point.

But for a production-intended project, I want a different workflow. I want the agents to operate inside a system of product intent, architecture direction, scoped milestones and review expectations.

That is what these two days were about.

Not ceremony for its own sake.  
Not process theatre.  
Not pretending that a solo or small-team project needs enterprise overhead.

Just enough structure to make the next phase safer, faster and easier to reason about.

The code will come next. But before the code, I wanted the project to have a shape.