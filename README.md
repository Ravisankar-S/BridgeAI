# BridgeAI: Hybrid Knowledge Assistant for Low-Connectivity Environments

**Tagline:** Online-first AI assistant with automatic offline fallback

BridgeAI is a hybrid AI assistant that delivers high-quality, cloud-powered responses when internet connectivity is available while providing instant, offline answers through a lightweight local model when connectivity is limited. It ensures knowledge accessibility even in low-connectivity environments.  

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
BridgeAI bridges this gap using **three integrated layers**:

1. **Online Layer (LLaMA 3 via Cerebras API)**  
   - Handles complex queries, long-context reasoning, and advanced computation.  
   - Lightning-fast inference powered by Cerebras Cloud.  
   - Provides enhanced answers with structured guidance, references, and deep reasoning.  

2. **Offline Layer (LLaMA 2, Chat-Optimized Quantized Model)**  
   - Lightweight, quantized version optimized for chat.  
   - Handles FAQs, factual questions, and lightweight queries when connectivity is unavailable.  
   - Runs locally in a Docker container with instant inference.  

3. **Docker MCP Gateway**  
   - Orchestrates queries between online and offline layers.  
   - Detects network availability and switches automatically to offline fallback.  
   - Logs queries, caches responses, and ensures seamless hybrid operation.  

---

## System Architecture

### Architecture Overview
BridgeAI consists of five main layers:

1. **Frontend Layer**: React-based UI for query input and response display.  
2. **Backend Layer**: FastAPI service receives requests and forwards them to MCP Gateway.  
3. **MCP Gateway Layer**:  
   - Decision engine for online/offline routing  
   - Query logging and caching  
   - Metadata management  
4. **AI Models Layer**:  
   - **Online:** LLaMA 3 via Cerebras API  
   - **Offline:** LLaMA 2 Chat-Optimized Quantized model (Dockerized)  
5. **Persistence Layer**: Stores logs, cached responses, and user preferences.  

---

### Diagram 
<img width="1941" height="3840" alt="Untitled diagram _ Mermaid Chart-2025-10-05-113759" src="https://github.com/user-attachments/assets/97142c47-eb93-467c-9c80-3057630f1c12" />

    

    
Flow Description
User Query: Submitted via frontend.
Backend Routing: FastAPI forwards the query to MCP Gateway.

Online-First Decision:

Internet available → LLaMA 3 online handles query.

Internet unavailable → LLaMA 2 offline handles query.

Response Handling: Gateway sends response back to frontend.

Logging & Caching: Offline responses cached and optionally enriched when online.

Workflow & User Scenario
Example Query:
"The number of world cups won by argentina."

Steps:

User submits query via React UI.

Backend sends query to MCP Gateway.

MCP Gateway checks connectivity → online first, offline fallback.

Response is returned to frontend.

Offline responses are logged for optional later enhancement.

Handling Internet Outages
Offline Mode: LLaMA 2 chat-optimized model provides instant local answers.

Caching: Queries are stored locally for enrichment when connectivity is restored.

Online Enhancement: Once online, cached responses can be enriched by LLaMA 3 for detailed reasoning.

Unique Features
Online-first, offline-fallback ensures optimal performance in any connectivity scenario.

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

Offline: Forms, schemes, procedural guidance.

Online: Tailored instructions, multi-source summaries, templates.

Quick Start / Installation
Prerequisites
Docker Desktop: https://www.docker.com/products/docker-desktop

Python 3.11+ (if running locally)

Cerebras API Key: https://cloud.cerebras.ai/

Setup (Windows Example)
bash
Copy code
# Run setup
setup.bat
# Downloads LLaMA 2 model (~4GB) and configures environment

# Start the app
start.bat
# Builds Docker images (~5-10 min) and opens browser
Docker Commands
bash
Copy code
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
License: MIT License – see LICENSE file for details

Developed by: Team Cyber_Samurais for WeMakeDevs FutureStack GenAI Hackathon 2025
