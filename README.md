### BridgeAI: Hybrid Knowledge Assistant for Low-Connectivity Environments

**Tagline:** Offline-first AI assistant that becomes smarter online  

BridgeAI is a hybrid AI assistant designed to deliver instant, offline responses while leveraging cloud-based intelligence for complex queries when internet connectivity is available. It ensures knowledge accessibility even in low-connectivity environments.  

---

### Table of Contents
1. [Problem Statement](#problem-statement)  
2. [Solution Overview](#solution-overview)  
3. [System Architecture](#system-architecture)  
4. [Workflow & User Scenario](#workflow--user-scenario)  
5. [Handling Internet Outages](#handling-internet-outages)  
6. [Demo & Hackathon Presentation](#demo--hackathon-presentation)  
7. [Unique Features](#unique-features)  
8. [Suggested Use Cases](#suggested-use-cases)  
9. [Quick Start / Installation](#quick-start)  


---

### Problem Statement
- Communities such as students, researchers, NGOs, and local governments often face slow or unreliable internet connectivity.  
- Current AI assistants are either:  
  - **Fully cloud-based** → require fast, reliable internet.  
  - **Fully local** → limited intelligence and cannot handle large datasets.  
- **Gap:** There is no hybrid, offline-first assistant that works on minimal hardware but leverages advanced AI when possible.

---

### Solution Overview
BridgeAI bridges this gap with three integrated layers:

1. **Offline Layer (LLaMA)**  
   - Small, quantized version of LLaMA.  
   - Handles lightweight queries, simple facts, FAQs.  
   - Runs entirely locally in a Docker container.  

2. **Online Layer (Cerebras API)**  
   - Cloud-hosted model for complex questions, large-context reasoning, and advanced computation.  
   - Enhances answers when internet is available.  

3. **Docker MCP Gateway**  
   - Orchestrates queries between offline and online layers.  
   - Logs queries, caches responses, and handles offline fallback.  
   - Packages everything into a portable, deployable container.  

---

### System Architecture

<img width="2541" height="3840" alt="Untitled diagram _ Mermaid Chart-2025-10-05-105133" src="https://github.com/user-attachments/assets/c8bead61-beea-42fc-9798-8e4ffeffcbb4" />

---

### Workflow & User Scenario
**Step 1: User Submits Query**  
Example query:  
> "Explain the environmental impact of microplastics on marine life and suggest mitigation strategies."

**Step 2: MCP Gateway Intercepts Query**  
- Checks if internet is available.  
- Checks if query has been cached before.  
- Routes query: offline-first if no internet, online via Cerebras if available.  

**Step 3: Offline Handling (LLaMA)**  
- LLaMA provides instant, simplified responses from preloaded data.  
- Response may be less detailed or approximate.  
- Metadata marks this as an offline-limited answer.  

**Step 4: Online Enhancement (Cerebras API)**  
- Once internet is restored, MCP detects previously answered queries that were offline-limited.  
- Sends them to Cerebras API for full processing.  
- Caches detailed responses locally and marks them as “enhanced online response.”  

**Step 5: User Receives Improved Answer**  
- Users can see richer explanations, references, or structured guidance.  
- System notifies: “Your question has been enhanced with additional insights.”  

---

### Handling Internet Outages
- Offline-only scenario:  
  - LLaMA answers from preloaded data.  
  - MCP logs queries needing later enhancement.  
  - Users get instant responses even if simplified.  
- When connectivity returns:  
  - Cerebras API enriches previously limited answers.  
  - Hybrid workflow ensures continuity.  

---


### Unique Features
- LLaMA = Offline survival brain.  
- Cerebras = Cloud superbrain.  
- Docker MCP = Orchestrator + metadata manager.  
- Fully hybrid workflow = resilient, smart, portable  
- Tracks queries, logs, and enhanced responses intelligently.  

---

### Suggested Use Cases
1. **Research Assistant (Students & NGOs)**  
   - Offline: Curriculum, project briefs, or reports.  
   - Online: Summaries, citations, next-step guidance.  

2. **Education Assistant (Rural Schools)**  
   - Offline: Subject Q&A, flashcards.  
   - Online: Adaptive lesson plans, quizzes, concept explanations.  

3. **Civic Knowledge Portal**  
   - Offline: FAQs about schemes, forms, procedures.  
   - Online: Tailored instructions, multi-source summaries, templates.  

---

### `QUICKSTART.md`

```markdown
#  BridgeAI Quick Start

## Prerequisites
- Docker Desktop: https://www.docker.com/products/docker-desktop/  
- Python 3.11+ (if running locally)  
- Cerebras API Key: https://cloud.cerebras.ai/

---

## Setup (Windows Example)
```bash
# Run setup
setup.bat
# This downloads LLaMA model (~4GB) and configures environment

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


