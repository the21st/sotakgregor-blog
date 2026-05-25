---
title: "Where Does Your Agent's Shared State Live?"
description: "Where the shared state lives – client or server – is one of the most consequential decisions when building an AI agent into a cloud product. It shapes review flows, autonomy, and what the agent can even see."
pubDate: "2026-05-25"
---

For the past few weeks I've been stuck on a design problem. We're building a feature that lets users edit their documents with our AI agent. We're in a regulated industry, so a review flow is a hard requirement – and every design I sketched felt wrong. The UX flows didn't work. The architecture felt forced. I couldn't figure out why.

Think about a Jupyter notebook: you've run a dozen cells, transformed some data, have a bunch of state living in memory, and you ask an agent to help debug something. A server-side agent has no idea what's in your kernel. It can't see what you see. That gap between what you're looking at and what the agent can access – that's the shared state problem. And where that shared state lives turns out to be one of the more consequential decisions in building agentic products.

That question shapes a lot of product decisions that follow.

## Two paradigms

Worth noting upfront: this is a decision that only exists for cloud products. For fully local apps with no backend – like Claude Code (in the terminal) running on your machine – there's no question to answer. The only state that exists is on your local machine, so the agent can always see it. The interesting design space is when there's a server involved.

There are basically 2 ways to build an agentic app today.

The first is a **client-side agent**. Notion AI is a good example. The AI runs inference in the cloud like everything else, but the state it works on lives in your browser – or at least, behaves as if it does. Here's where Notion is a useful, slightly unintuitive example. Notion is a server-side app – all your pages live in their database. But when Notion's AI edits a document, those edits live purely in your browser until you accept them. Which means, practically, you can't ask Notion's AI to rewrite a page and then close the tab. The agent can't finish without you. Despite being a cloud product, its AI editing model is local in the way that matters.

The second is a **server-side agent**. The Linear agent works this way. You can kick it off from Slack, and it goes and edits tickets, creates issues, does its thing – all while you're doing something else. The state it works on lives in the database. You don't have to be there. Its changes are applied immediately without a review.

The distinction that matters isn't where the LLM runs. It's where the shared context lives.

## The review flow is the tell

I noticed this first when I tried to build a review flow.

The approve/reject/modify review flow feels like the obvious UI for AI editing. This experience is native to the local agent model. Git gives it to you for free: the diff is just there, approval is a pull request. Notion gets it too, because edits are local until accepted.

With a server-side agent working on state that isn't a git repo or a local buffer, you have to engineer that entire experience yourself. Implementing drafts, managing the agent's version against the user's version, building the diff UI, keeping the client in sync. That complexity is the unavoidable cost of reaching for a UX pattern that doesn't naturally fit the paradigm you're in.

## Downstream effects

The review flow is the most visible consequence, but the state question influences other things too.

What can the agent actually *see*? If a user has unsaved local changes and asks the agent for help, a server-side agent is blind to that. It only knows what's been committed to the database. This creates a subtle trust problem: the user assumes the agent has full context, and it doesn't.

There's also the proactive agent question. If you want your agent to act on new data without being invoked (e.g. detecting an anomaly and automatically running a diagnostic) it needs access to state at all times. That requires server-side. You can't build a background agent on local state.

## Three paths when the paradigm doesn't fit

If you want a review flow but your state lives server-side, three options open up:

The **hybrid approach** is what Notion AI does: pass local state to the agent as context, get back a structured patch, render the diff on the client. It works, and you get the review flow. But the agent can't iterate autonomously, it can't run code on its own, and you end up bolting complexity everywhere.

The **live edits approach** skips drafts entirely and leans on versioning – the agent edits directly, and if you don't like it, you roll back. Linear works roughly this way. Simplest mental model by far. Not great if you're building for regulated industries where "just undo it" isn't a sufficient safety net. And no review step before changes land.

The **full server-side model with a review layer** resolves the mismatch cleanly: move all drafts to the server, give the agent its own working copy, build the review layer on top. The right long-term architecture if you want both autonomous agents and a proper review flow. I'm not aware of a product that fully does this today – if you know of one, I'd really love to hear about it.

## Ask it early

Any team building an agent for their cloud product will hit this fork.

Ask it first: where does the shared state live, and does that fit the product experience I'm trying to build? If you want a review flow, make sure your answer gets you one without a fight. If you want proactive agents, make sure the state is somewhere the agent can always reach.
