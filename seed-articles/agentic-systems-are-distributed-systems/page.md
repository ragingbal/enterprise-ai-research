---
title: "Agentic Systems: A Distributed Systems Problem"
description: Agentic systems, particularly in autonomous enterprise backends, are
  fundamentally a distributed systems challenge rather than a workflow problem. Treating
  them as such is crucial for achieving scalable and auditable autonomy.
tags:
- agentic systems
- distributed systems
- autonomy
- microservices
- swarm computing
- orchestration
- A2A communication
---

# Agentic Systems Don’t Have a Workflow Problem. They Have a Distributed Systems Problem.

Much of today’s thinking about agentic systems—particularly in the context of autonomous enterprise backend platforms—starts from the wrong abstraction.

We start with workflows.

We talk about agents as if they are steps in a flowchart.\
We design orchestration graphs.\
We invent DSLs that look suspiciously like BPMN with an LLM bolted on.

And then we are surprised when these systems collapse under scale, complexity, or audit requirements.

This is a category error.

Agentic systems are not primarily a workflow problem. They are a distributed systems problem. Until we treat them as such, enterprise‑grade autonomy will remain fragile, opaque, and fundamentally unscalable.

---

## The Workflow Trap

Workflow‑centric thinking assumes three things:

1. A predefined execution path
2. A central orchestrator
3. Deterministic execution semantics

These assumptions work tolerably well for batch jobs, ETL pipelines, and CRUD‑heavy microservice choreography.

They fail the moment you introduce agents.

Why?

Because agents are not steps. They are actors.

Agents are:

* Autonomous
* Stateful
* Internally non‑deterministic
* Long‑lived in intent, even if their processes are ephemeral

The moment you have more than one agent, you no longer have a workflow.

You have a distributed system.

---

## The Persistent Category Error in Agent Design

There is a recurring mistake in how agent systems are designed and discussed:

We think of agent‑to‑agent (A2A) communication as “chat between models.”

This framing is intuitive—and deeply misleading.

In reality, A2A communication has far more in common with microservices talking to each other under partial failure than with conversational interfaces.

As soon as agents interact, you inherit all the classic distributed systems problems:

* Causality
* Retries
* Duplication
* Partial failure
* Ordering
* Observability
* Auditability

Most A2A protocols today ignore this.

They optimize for immediacy, not history.

And history is where systems break.

---

## Why Predefined Orchestration Fails

Traditional orchestration assumes you can specify the control plane up front.

Agents violate this assumption by design.

They may discover new sub‑tasks dynamically.\
They may defer action based on evolving context.\
They may operate concurrently, competitively, or redundantly.\
They may revise earlier conclusions.

Trying to force this behaviour into a static workflow graph is like trying to model the internet as a single call stack.

The result is brittle systems that work in demos and fail in production.

The alternative is not better workflows.

The alternative is emergent orchestration.

---

## From Workflows to Swarms

If agentic systems are a distributed systems problem, the natural architectural endpoint is not orchestration. It is swarm computing.

A swarm‑based agentic platform has three defining properties.

---

### 1. Mixed Determinism

Not everything should be an agent.

Most things shouldn’t be.

A scalable agentic system deliberately combines:

* Deterministic microservices\
  For validation, enforcement, enrichment, persistence, and guarantees.

* Non‑deterministic agents\
  For reasoning, planning, interpretation, and decision‑making under uncertainty.

Agents think.\
Microservices execute.

The capability of the system emerges from their interaction, not from pretending everything is an agent.

---

### 2. Event‑First Communication

In a swarm, actors do not call each other directly.

They emit events.\
They consume events.

They react to what they observe, not to who sent it.

Communication happens through events interlinked by correlation identifiers, not through predefined call graphs or orchestration plans.

There is:

* No central orchestrator
* No global workflow definition
* No single source of truth for control flow

Instead, orchestration emerges from the event topology itself.

What happens next is defined by which actors are listening, what state they carry, and how they interpret the event history so far.

This is not chaos.

This is how distributed systems actually work.

---

### 3. History as a First‑Class Primitive

Swarm systems treat history as infrastructure, not metadata.

Every meaningful action produces an event of record.\
Every decision can be reconstructed from prior state.\
Every agent’s behavior is explainable after the fact.

This requires:

* Durable event logs (for example, Kafka)
* Strong correlation semantics
* Explicit causality tracking
* Reproducible state transitions

Without this, autonomy becomes an excuse for opacity.

---

## Why Most Agent Platforms Break at Enterprise Scale

Most current agent frameworks were designed for:

* Single‑process execution
* Short‑lived interactions
* Human‑in‑the‑loop supervision
* Minimal compliance and audit requirements

Enterprises need the opposite:

* Long‑running autonomous behavior
* Partial failure tolerance
* Auditability by default
* Deterministic replay
* Change control via GitOps
* Clear operational ownership

These properties cannot be bolted on later.

They must be native to the platform.

---

## The Case for a Swarm Computing Platform

This is why we argue for a swarm computing platform for autonomous enterprise backends.

At a high level:

* Agents and microservices are first‑class actors
* Actors are dynamically launched and executed in containers
* All communication happens via CloudEvents over Kafka
* Correlation, not orchestration, defines system behavior

The platform provides the harness that individual actors should not have to reinvent:

* Auditability
* Logging
* State management
* Context transfer
* Retry semantics
* Observability
* GitOps‑based deployment and evolution

Agents get autonomy without being allowed to bypass operational reality.

---

## Emergence Is Not Optional

If your agentic system does not allow for emergent behavior, it is not truly agentic.

And if it allows emergence without the infrastructure to observe, constrain, and explain it, it is not enterprise‑ready.

Swarm architectures accept emergence as inevitable—and then design for it.

---

## A Final Reframe

Stop asking:

“How do we design better workflows for agents?”

Start asking:

“What does a distributed system look like when some of its nodes can think?”

The answer is not orchestration.

The answer is a swarm.
