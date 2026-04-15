---
title: "BettaFish: Multi-Agent Framework for Public Opinion Analysis"
description: BettaFish is an open-source framework that orchestrates multiple AI agents
  to analyze public opinion across diverse social platforms by synthesizing multimodal
  data and employing a debate engine for refined insights. It offers a one-click deployment
  system for parallel agent execution, suitable for software engineers building distributed
  systems.
tags:
- public opinion
- social media analysis
- AI agents
- orchestration
- multimodal analysis
- parallel processing
- LLMs
- agent-based systems
---

# BettaFish: Multi-Agent Architecture for Public Opinion Analysis – A Systems Engineer's Guide

**[BettaFish](https://github.com/666ghj/BettaFish "BettaFish Github")** is an open-source framework designed to break through information silos by orchestrating multiple AI agents to analyse public opinion across diverse social platforms. For software engineers building distributed systems, it demonstrates practical agentic orchestration at scale, coordinating specialised agents like microservices in a resilient, parallel workflow.\[1\]\[2\]

## Purpose and Overview

BettaFish addresses the core challenge of synthesising multimodal data from over 30 platforms—including Weibo, Xiaohongshu, Douyin, and international sites like Twitter and YouTube - into coherent public opinion insights. Traditional sentiment analysis tools fail here due to platform-specific data formats, multimodal content (text, images, videos), and echo chambers that bias single-source views. BettaFish's purpose is to provide a **one-click deployment system** that launches parallel agents to crawl, process, debate, and report findings, delivering balanced reports that capture consensus and divergence.

From a software engineering perspective, BettaFish embodies **agent orchestration principles**: centralised coordination with decentralised execution, akin to Kubernetes managing pods. Its Flask-based web interface serves as the entry point, Docker containerisation ensures portability, and a backend crawler handles real-time data ingestion. Key innovations include a **virtual debate forum** where agents iterate arguments to refine analysis, preventing LLM hallucinations through adversarial collaboration, and **parallel processing** for low-latency results on large datasets. The system supports configurable LLMs (e.g., GPT-4, Claude), making it extensible for enterprise monitoring or market research.\[1\]\[2\]\[3\]

The overview workflow is simple yet powerful: input a query (e.g., "public sentiment on EV adoption"), the orchestrator spins up four core agents—Query Agent, Media Agent, Forum Agent, Report Agent—each handling specialised tasks concurrently. Outputs converge into a polished report with sentiment scores, key themes, and evidence traces. This mirrors enterprise patterns like sequential-to-concurrent handoffs, achieving sub-minute turnaround for complex queries.\[2\]\[4\]

## Architecture

BettaFish's architecture follows a **hierarchical orchestration model**, balancing control and autonomy. At the apex is the **Flask orchestrator**, a lightweight web server that receives user queries via a clean UI, validates inputs, and launches agents via asynchronous processes. This central coordinator manages task decomposition, resource allocation (e.g., GPU for media processing), and progress tracking, much like a workflow engine in Apache Airflow but optimised for LLM agents.\[1\]\[3\]

The **agent layer** comprises four specialised agents, operating as loosely coupled services:

* **Query Agent**: Handles platform-specific searches, adapting to API quirks and rate limits across 30+ sources. It aggregates raw data streams, filtering noise with semantic relevance scoring.
* **Media Agent**: Processes multimodal content using Playwright for dynamic scraping and computer vision APIs for image/video analysis. This agent extracts embedded sentiment from non-text data, addressing a common blind spot in text-only pipelines.
* **Forum Agent**: The innovation core—a debate engine simulating adversarial discussions. Agents post "arguments" in rounds, critiquing each other's outputs to converge on robust insights, inspired by group chat patterns for consensus-building.\[2\]
* **Report Agent**: Synthesises outputs into structured Markdown reports, incorporating visualisations (via integrated tools) and traceability links back to sources.

Supporting this is the **data layer**: SQLite for session state (queries, agent outputs, debate logs), ensuring auditability and resumption after failures. The **communication bus** uses standardised JSON messages for inter-agent handoffs, enforcing protocols for context passing and error propagation, similar to gRPC in microservices.\[4\]

Scalability comes from **concurrent execution**: Agents run in parallel threads, with the orchestrator monitoring via heartbeat signals to handle stragglers or retries. Deployment via Docker Compose allows horizontal scaling, with config files for LLM endpoints and platform credentials. This design avoids single points of failure through agent-level fault tolerance— if one agent stalls, others proceed with partial data.\[3\]

## Inner Workings

Execution begins with query ingestion at the Flask endpoint, where the orchestrator parses intent and spins up agents in parallel, assigning workloads based on query type (e.g., heavy media to Media Agent). Each agent initialises with shared context (query, platform list, LLM keys), then executes independently.\[1\]

The Query Agent starts by fanning out searches, using platform-native APIs and browser automation for JavaScript-heavy sites. It normalises results into a unified schema (timestamp, author, content type, sentiment proxy), buffering up to configurable limits to manage memory.

Concurrently, the Media Agent ingests Query outputs, applying OCR for images, transcription for videos, and embedding models for cross-modal search. This step employs batch processing to optimise LLM calls, chunking content to fit token limits while preserving context.

The Forum Agent receives partial results from Query and Media, initiating debate rounds (typically 3-5 iterations). It simulates a chat room: Agent 1 proposes a sentiment hypothesis, Agent 2 critiques with counter-evidence, resolving via majority vote or LLM arbitrator. This adversarial loop refines accuracy, emulating human peer review and mitigating bias from isolated analysis.\[2\]\[4\]

Finally, the Report Agent aggregates forum outputs, computing aggregate metrics (e.g., sentiment polarity via weighted averages) and generating narrative summaries. Traceability is baked in—every claim links to source data—enabling engineers to debug or extend.

Throughout, the orchestrator oversees via polling: reallocating tasks on timeouts, logging state for observability, and surfacing errors in the UI. Extensibility shines in config-driven swaps (e.g., replace GPT with local Llama) and plugin agents for custom platforms. Performance bottlenecks, like LLM latency, are mitigated by caching embeddings and asynchronous I/O.\[3\]

For systems engineers, BettaFish reveals agent orchestration's power: emergent intelligence from simple rules, resilient to individual failures, and scalable via parallelism. It's a blueprint for production-grade agent swarms in monitoring or analytics pipelines.

* **\[1\]** <https://www.scriptbyai.com/bettafish-public-opinion-analysis-agent/> – Overview of BettaFish multi-agent system, features, and workflow (crawler clusters, forum engine, multimodal analysis).\[1\]

* **\[2\]** <https://betterstack.com/community/guides/ai/bettafish-multi-agent/> – Detailed agent roles (Query, Media, Insight Agents), forum debate mechanism, and architecture breakdown.\[2\]

* **\[3\]** <https://github.com/u0x01/bettafish/blob/main/README-EN.md> – Official GitHub README for technical specs, deployment, and core implementation details.\[3\]

* **\[4\]** <https://www.xugj520>
