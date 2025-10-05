# BridgeAI: Hybrid Knowledge Assistant for Low-Connectivity Environments

**Tagline:** Offline-first AI assistant that becomes smarter online  

BridgeAI is a hybrid AI assistant designed to deliver instant, offline responses while leveraging cloud-based intelligence for complex queries when internet connectivity is available. It ensures knowledge accessibility even in low-connectivity environments.  

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
- **Gap:** There is no hybrid, offline-first assistant that works on minimal hardware but leverages advanced AI when possible.

---

## Solution Overview
BridgeAI bridges this gap with three integrated layers:

1. **Offline Layer (LLaMA 2, Chat-Optimized Quantized Model)**  
   - Lightweight, quantized version of LLaMA 2 optimized for chat.  
   - Handles lightweight queries, FAQs, and factual questions instantly.  
   - Runs entirely locally in a Docker container.  
   - Provides **instant offline inference** with minimal latency.  

2. **Online Layer (LLaMA 3 via Cerebras API)**  
   - Cloud-hosted LLaMA 3 model for complex queries, long-context reasoning, and advanced computation.  
   - Lightning-fast inference powered by Cerebras Cloud.  
   - Enhances offline responses with detailed explanations, structured guidance, and references.  

3. **Docker MCP Gateway**  
   - Orchestrates queries between offline and online layers.  
   - Logs queries, caches responses, and handles offline fallback.  
   - Ensures seamless hybrid operation in a portable Docker container.  

---

## System Architecture

```mermaid
graph TD
    A["User Sends Query"] --> B["Frontend (React UI)"]
    B --> C["Backend (FastAPI) Receives Request"]
    C --> D["MCP Gateway Processes Query"]
    D --> E{"Internet Available?"}
    E -- Yes --> F["LLaMA 3 via Cerebras API"]
    E -- No --> G["LLaMA 2 Offline (Chat-Optimized Quantized)"]
    F --> H["MCP Gateway Returns Response"]
    G --> H
    H --> I["User Receives Response"]
Workflow & User Scenario
Step 1: User Submits Query
Example:

"Explain the environmental impact of microplastics on marine life and suggest mitigation strategies."

Step 2: Frontend & Backend Processing

User input is sent from the frontend (React UI) to the backend (FastAPI).

Backend forwards the request to MCP Gateway for routing.

Step 3: MCP Gateway Determines Online/Offline Handling

Checks internet availability and query cache.

Offline → LLaMA 2 chat-optimized quantized model provides instant responses.

Online → LLaMA 3 via Cerebras API performs advanced reasoning and lightning-fast inference.

Step 4: Response Logging & Enhancement

Offline answers are tagged and cached for future enhancement.

When connectivity is restored, cached offline queries are enriched by LLaMA 3 online, creating enhanced, detailed responses.

Step 5: User Receives Final Answer

Users see richer explanations, references, or structured guidance.

System notifies: “Your question has been enhanced with additional insights.”

Handling Internet Outages
Offline-only scenario:

LLaMA 2 chat-optimized model provides instant, local answers.

MCP Gateway logs queries for later enhancement.

When connectivity returns:

LLaMA 3 via Cerebras API enriches offline responses.

Hybrid workflow ensures continuity with minimal user disruption.

Unique Features
LLaMA 2 = Offline survival brain, chat-optimized, quantized, instant inference.

LLaMA 3 = Online superbrain via Cerebras API, lightning-fast reasoning.

Docker MCP Gateway = Orchestrator, query logger, and metadata manager.

Fully hybrid workflow = resilient, smart, portable.

Tracks queries, caches responses, and enhances answers intelligently.

Suggested Use Cases
Research Assistant (Students & NGOs)

Offline: Curriculum, project briefs, or reports.

Online: Summaries, citations, next-step guidance.

Education Assistant (Rural Schools)

Offline: Subject Q&A, flashcards.

Online: Adaptive lesson plans, quizzes, concept explanations.

Civic Knowledge Portal

Offline: FAQs about schemes, forms, procedures.

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
