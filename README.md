# BridgeAI: Hybrid Knowledge Assistant for Low-Connectivity Environments

**Tagline:** Online-first AI assistant with offline fallback  

BridgeAI is a hybrid AI assistant designed to deliver high-quality, cloud-powered responses when internet connectivity is available while providing instant, offline answers through a lightweight model when connectivity is limited. It ensures knowledge accessibility even in low-connectivity environments.  

---

## Table of Contents
1. [Problem Statement](#problem-statement)  
2. [Solution Overview](#solution-overview)  
3. [System Architecture](#system-architecture)  
4. [Workflow & User Scenario](#workflow--user-scenario)  
5. [Handling Internet Outages](#handling-internet-outages)  
6. [Unique Features](#unique-features)  
7. [Suggested Use Cases](#suggested-use-cases)  
8. [Quick Start / Installation](#quick-start--installation)  
9. [License & Acknowledgments](#license--acknowledgments)  

---

## Problem Statement
- Communities such as students, researchers, NGOs, and local governments often face slow or unreliable internet connectivity.  
- Current AI assistants are either:  
  - **Fully cloud-based** → require fast, reliable internet.  
  - **Fully local** → limited intelligence and cannot handle large datasets.  
- **Gap:** There is no hybrid assistant that prioritizes advanced online reasoning but can fall back to offline mode when necessary.  

---

## Solution Overview
BridgeAI bridges this gap with three integrated layers:

1. **Online Layer (LLaMA 3 via Cerebras API)**  
   - Primary model for complex queries, long-context reasoning, and advanced computation.  
   - Lightning-fast inference powered by Cerebras Cloud.  
   - Provides enhanced answers with structured guidance, references, and deep reasoning.  

2. **Offline Layer (LLaMA 2, Chat-Optimized Quantized Model)**  
   - Lightweight, quantized version of LLaMA 2 optimized for chat.  
   - Handles lightweight queries, FAQs, and factual questions when connectivity is unavailable.  
   - Runs locally in a Docker container with instant inference.  

3. **Docker MCP Gateway**  
   - Orchestrates queries between online and offline layers.  
   - Automatically detects network availability and switches to offline fallback if needed.  
   - Logs queries, caches responses, and ensures seamless hybrid operation in a portable Docker container.  

---

## System Architecture

```mermaid
graph TD
    A["User Sends Query"] --> B["Frontend (React UI)"]
    B --> C["Backend (FastAPI) Receives Request"]
    C --> D["MCP Gateway Processes Query"]
    D --> E{"Internet Available?"}
    E -- Yes --> F["LLaMA 3 via Cerebras API (Online)"]
    E -- No --> G["LLaMA 2 Offline (Chat-Optimized Quantized)"]
    F --> H["MCP Gateway Returns Response"]
    G --> H
    H --> I["User Receives Response"]
Workflow & User Scenario
Step 1: User Submits Query
Example:

"Explain the environmental impact of microplastics on marine life and suggest mitigation strategies."

Step 2: Frontend & Backend Processing

Query is sent from the frontend (React UI) to the backend (FastAPI).

Backend forwards the request to MCP Gateway for routing.

Step 3: Online-First Handling

MCP Gateway first attempts to process the query using LLaMA 3 via Cerebras API.

If internet is unavailable or the request fails, the system falls back to LLaMA 2 offline.

Step 4: Response Logging & Enhancement

Offline responses are cached for future enhancement.

When connectivity is restored, cached offline queries are optionally enriched by LLaMA 3 online.

Step 5: User Receives Final Answer

Users see high-quality responses online and simplified, instant responses offline.

System notifies: “Your question has been enhanced with additional insights” once enriched.

Handling Internet Outages
Offline-only scenario:

LLaMA 2 chat-optimized model provides instant local answers.

MCP Gateway logs queries for later enhancement.

When connectivity returns:

LLaMA 3 via Cerebras API enriches previously offline responses.

Online-first workflow ensures users get the best response whenever possible.

Unique Features
Online-first, offline fallback ensures optimal performance in any connectivity scenario.

LLaMA 2 = Offline survival brain, chat-optimized, quantized, instant inference.

LLaMA 3 = Online superbrain via Cerebras API, lightning-fast reasoning.

Docker MCP Gateway = Orchestrator, query logger, and metadata manager.

Fully hybrid workflow = resilient, smart, portable.

Tracks queries, caches responses, and enhances answers intelligently.

Suggested Use Cases
Research Assistant (Students & NGOs)

Offline: Project briefs, reports, FAQs.

Online: Advanced summaries, citations, reasoning.

Education Assistant (Rural Schools)

Offline: Flashcards, Q&A.

Online: Adaptive lesson plans, quizzes, concept explanations.

Civic Knowledge Portal

Offline: Forms, schemes, and procedural guidance.

Online: Tailored instructions, multi-source summaries, templates.

Quick Start / Installation
markdown
Copy code
# BridgeAI Quick Start

## Prerequisites
- Docker Desktop: https://www.docker.com/products/docker-desktop/  
- Python 3.11+ (if running locally)  
- Cerebras API Key: https://cloud.cerebras.ai/

## Setup (Windows Example)
```bash
# Run setup
setup.bat
# Downloads LLaMA 2 model (~4GB) and configures environment

# Start the app
start.bat
# Builds Docker images (~5-10 min) and opens browser

# Docker Commands

# Start in foreground
docker-compose up

# Start in background
docker-compose up -d

# Stop all containers
docker-compose down

# Rebuild containers after changes
docker-compose up --build

# View logs
docker-compose logs -f
License & Acknowledgments
MIT License – see LICENSE for details

Developed by Team Cyber_Samurais for WeMakeDevs FutureStack GenAI Hackathon 2025

Acknowledgments: Meta (LLaMA), Cerebras, Docker, FastAPI, React, and community contributors
