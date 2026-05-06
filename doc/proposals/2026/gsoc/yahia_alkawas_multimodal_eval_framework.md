## GSoC 2026 Proposal: Multimodal AI and Agent API Eval Framework
Candidate: Yahia (Yaya) Alkawas

Project: #2 - Multimodal AI and Agent API Eval Framework

Mentors: Ankit & Ashita

## Abstract
This project aims to deliver a real-time, dependency-light evaluation framework for multimodal and agentic AI systems within API Dash. Existing evaluation tools are often fragmented, batch-oriented, and difficult to integrate into developer workflows. This project unifies text, image, audio, video, and agent evaluation into a single streaming interface, enabling developers to benchmark models and tool-using agents in real time.
The framework will provide live evaluation logs with <200ms latency, side-by-side model comparison, and seamless integration via MCP-compatible interfaces. Success will be measured by complete multimodal support, real-time streaming performance, and extensible architecture for future model and modality additions.

## Proposed Architecture
Core Components
Frontend (React / TypeScript):
Interactive UI for configuring evaluation tasks, visualizing multimodal outputs, and streaming real-time logs.
Backend (Python / FastAPI):
Evaluation orchestrator integrating tools such as lm-harness and lighteval.
Execution Layer:
Python subprocess-based runner for evaluation tasks, combined with Server-Sent Events (SSE) for real-time streaming.

## Design Decisions & Tradeoffs
SSE vs WebSockets:
SSE is chosen for its simplicity, lower overhead, and suitability for one-way streaming of evaluation logs.
Subprocess vs Task Queue (Celery/Redis):
A subprocess-based approach avoids heavy infrastructure dependencies, aligning with the “dependency-lite” goal.
Blob URLs vs Base64:
Blob URLs are used for large media to reduce browser memory usage and improve performance.

## MCP Alignment Architecture
Standardized Tooling:
The framework will use MCP to standardize connections to external multimodal tools (e.g., vision APIs, speech models).
Agentic Evaluation:
The system will evaluate not only model outputs but also tool-calling behavior of agentic systems.
Interoperability:
Any MCP-compatible model or agent can be integrated without custom glue code.

Example Agent Evaluation Flow:

Capture tool calls via MCP interface
Validate correctness of tool selection
Compare expected vs actual outputs
Score both reasoning and execution

## Functional Requirements
Real-time Streaming:
Evaluation logs must be streamed to the UI with <200ms latency using SSE.
Multimodal Support:
Support rendering and evaluation of:
Images (PNG, JPG)
Audio (MP3, WAV)
Video (MP4)
Documents (PDF)
Model Comparison:
Support side-by-side evaluation of at least two models with synchronized inputs and unified scoring output.
Asset Management:
Support local files up to 100MB and remote URLs with streaming fetch.

## Non-Functional Requirements
Security:
Sandboxed rendering of all multimodal outputs
MIME validation and file-type enforcement
Sanitization of model outputs to prevent XSS
Extensibility:
New media types can be added via modular MediaDispatcher updates.
Reliability:
Subprocess failures must be isolated and handled gracefully.
Ease of Setup:
Docker-based “one-command” setup for contributors.


## Evaluation Metrics
Text Models:
Accuracy, semantic similarity, BLEU-like metrics
Image Models:
Caption relevance and embedding similarity (e.g., CLIP-based scoring)
Audio Models:
Transcription accuracy using Word Error Rate (WER)
Agentic Systems:
Tool-call accuracy
Task completion success rate
Step-wise latency


## Security & Abuse Prevention

Given my background in security research, I will ensure:

Isolation of rendered content using sandboxed environments
Validation of all user-provided and remote assets
Rate limiting for evaluation endpoints
Protection against prompt injection affecting agent evaluation
Safe handling of untrusted model outputs


## Proof of Concept (PoC)
[Here it is](https://github.com/YahyaElKawas/Multimodal-Ai-Evaluation-Framework-PoC)


## 🚀 Technical Highlights on the PoC
Real-time streaming pipeline using FastAPI + SSE for incremental evaluation outputs
Multimodal support (image, audio, video, PDF) in a unified framework
Event observability with UUIDs and timestamps for traceability
Model-agnostic design enabling easy integration with different AI systems
Interactive React dashboard with real-time visualization, progress tracking, and structured outputs
Robust media handling (images, audio/video playback, PDF rendering with fallback)
Advanced testing strategy covering streaming, schema validation, UI updates, and performance
Configurable latency for realistic demos and fast, deterministic tests

[**Watch the PoC video here on google drive**](https://drive.google.com/file/d/1WtIKGQIpj3g1S5EEe8Pj-8myfXZvzRmZ/view?usp=drive_link&authuser=1)


## Detailed 12-Week Timeline (350 Hours)
* **Week 1–2 (Community Bonding)**
Finalized API contracts and data schemas
Defined evaluation pipeline interfaces
Completed MCP integration design
Set up development environment and contribution workflow

* **Week 3–4 (Core Infrastructure)**
Implemented async evaluation runner supporting concurrent jobs
Built SSE streaming system with reconnect support
Integrated subprocess execution with structured logging
Delivered CLI-based evaluation test harness

* **Week 5–6 (Multimodal Support)**
Implemented media handlers for Image, Audio, Video, and PDF
Built frontend rendering components for each modality
Integrated streaming asset loading for large files
Delivered working multimodal evaluation pipeline

* **Week 7 (Midterm Deliverable)**
End-to-end system:
Text + Image evaluation working
Real-time logs visible in UI
Single-model evaluation fully functional
Demonstration of full evaluation workflow

* **Week 8–9 (Model Comparison & Agent Evaluation)**
Implemented dual-model comparison pipeline
Added unified scoring system
Integrated MCP-based agent evaluation
Delivered agent tool-call tracking and scoring

* **Week 10 (Performance & Edge Cases)**
Optimized large file streaming and memory usage
Implemented retry and failure recovery mechanisms
Added SSE buffering and reconnection handling
Benchmarked latency and performance

* **Week 11 (Testing & Stabilization)**
Achieved ≥80% backend test coverage (Pytest)
Implemented frontend tests (Vitest / Playwright)
Added mock evaluation system to avoid API costs
Fixed edge cases and ensured system stability

* **Week 12 (Documentation & Finalization)**
Wrote developer documentation
Created “How to add a new model” guide
Documented architecture and extension points
Delivered final demo and contributor onboarding guide

## Testing Strategy
Backend: Pytest with unit and integration tests
Frontend: Vitest and Playwright
Mocking: Simulated LLM responses to avoid API costs
Performance Testing: Evaluate streaming latency and load handling

## Risks & Mitigation
Large file bottlenecks:
Use chunked streaming and progressive rendering
Model API instability:
Implement retry strategies and fallback mocks
SSE connection drops:
Auto-reconnect with buffered state recovery
Scope complexity:
Deliver features incrementally (text → image → full multimodal)

## Final Deliverables
Fully integrated multimodal evaluation framework in API Dash
Real-time streaming UI with terminal-style logs
MCP-compatible agent evaluation support
Dual-model benchmarking system
≥80% test coverage (frontend + backend)
Complete documentation and contributor guides
End-to-end demo showcasing framework capabilities

## Experience
I am a Computer Science student at Cairo University and preveiuly an active security researcher on HackerOne, where I have reported multiple vulnerabilities including logic flaws and input validation issues. I have experience building full-stack applications using React, Node.js, and Python, along with integrating APIs and designing testing pipelines. Also I have built ai projects during my study at Cairo University, This background directly aligns with building a secure, scalable, and extensible evaluation framework.

## Architecture Diagram
[Architecture Diagram for the project here](https://drive.google.com/file/d/1OM71McSuhDZ3f_VWvAS1MPakyd1s4wKb/view?usp=drive_link)
