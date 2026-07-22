---
title: "What Shipping a Product Is Teaching Me About Codex and OpenCode"
date: 2026-07-22T19:22:00+05:30
draft: false
summary: "A field note from building a product with Codex and OpenCode, focused on context, model control, subagents and code review."
description: "Hands-on observations from using Codex and OpenCode while shipping a product, including context limits, subagent routing, review depth and the GLM 5.2 plus DeepSeek V4 combination."
tags:
  - ai
  - coding-agents
  - developer-tools
  - ai-assisted-development
  - code-review
feature: "feature-image.png"
featureAlt: "A developer working at a laptop beside two luminous paths that represent compact and continuous coding workflows"
showTableOfContents: false
---

I am building something I am excited to ship soon. I cannot share much about the product yet, but the work has given me a useful stretch of concentrated time with both Codex and OpenCode.

My goal has not been to run a benchmark or declare a universal winner. I have been trying to keep momentum in a real codebase: understand unfamiliar parts, decide what to change, hand off bounded work, review the result and keep the larger product direction intact.

Work like that exposes differences that are easy to miss in a quick demo. A model can write a good first pass and still be frustrating if the surrounding workflow keeps losing the thread.

Here are the patterns I have noticed so far.

## Context is a product experience

The biggest difference for me has been context continuity.

In the Codex configuration I have been using, the context window is about 258K tokens. With OpenCode using DeepSeek V4, I have been working with a much larger 1M token window. Those numbers matter less as a specification than as a working experience: Codex has needed to compact the conversation after relatively small but meaningful pieces of work, while OpenCode has let more of the original discussion, codebase discovery and decisions remain available.

Compaction is not inherently bad. A clean summary can remove noise and make the next step clearer. The problem appears when the work is still unfolding and the compacted version loses the reason a choice was made, an edge case uncovered earlier or the boundary that was supposed to keep a change small.

While shipping, continuity is part of quality. I do not want to spend energy repeatedly reconstructing the same product context just because the session has crossed a threshold.

## Subagent routing needs to be predictable

Codex has strong subagent capabilities, but I have found its model selection hard to predict.

For small tasks, I have sometimes seen it send work to GPT 5.6 Sol with extra high reasoning. The output can be good, but the cost feels out of proportion to the task when I only need a quick, bounded investigation or a small edit. I want to decide when a difficult problem deserves an expensive reasoning pass and when a lighter model is enough.

OpenCode has felt more direct in this respect. I can make the model choice and keep that choice consistent across the work. Keeping that control changes how comfortable I am delegating. Small supporting tasks can stay small instead of unexpectedly becoming a premium reasoning job.

The underlying lesson is not that every task should use the cheapest model. Model routing is part of the engineering workflow, so the developer needs to understand it and be able to steer it.

## A selected model should stay selected

Relatedly, Codex has occasionally switched models in the middle of a conversation after I had manually selected one. I have found that disruptive because model choice affects more than response speed: cost, reasoning style, how much context I expect to retain and how I frame the task all change with it.

When I choose a model for a session, I am making a workflow decision. A tool can recommend a change or make the routing visible, but it should not quietly turn that decision into a surprise.

## Codex has the stronger review instinct

Codex has also shown a clear strength: its code review has found more issues for me than DeepSeek V4 has found in comparable work.

The difference is not only about spotting syntax errors or asking for more tests. The useful reviews have surfaced assumptions, edge cases and integration risks that were easy to miss while moving quickly. An agent needs to be demanding in exactly those places. Building speed is useful, but speed without a credible review loop simply moves the risk later in the process.

For now, I trust Codex more as a reviewer than as the place where I want every long running implementation conversation to live.

## The combination that is working for me

The most competitive setup in my current work has not been one model used for everything. GLM 5.2 and DeepSeek V4 have worked well together and have felt genuinely competitive with GPT 5.6 Sol for the tasks I have been giving them.

DeepSeek V4 has been especially useful when I need long context and sustained implementation flow. GLM 5.2 has been a strong companion for other coding tasks. Codex, meanwhile, remains valuable when I want a more critical code review pass before I treat a change as done.

I would not generalize that into a permanent ranking. Models move quickly, tool integrations change and the best choice depends on the codebase and the task. Still, the experience has made one preference clear: I want a workflow where model selection, context and delegation are explicit controls rather than hidden behavior.

## What I am taking into the launch

The product I am building is the priority, not the agent comparison. Yet the tools shape the way I think, decide and recover from mistakes while building it, so their behavior matters.

The best setup for me is not the one with the most impressive single model. I need a setup that lets me keep context when the work becomes complex, choose the right level of reasoning for the task and apply a rigorous review before shipping. Right now, I am using more than one tool and being deliberate about what each one is responsible for.

I will have more to say once the product is out. For now, this is the field note I wanted to preserve: agentic coding is becoming less about finding one winner and more about designing a workflow that keeps the human in control.
