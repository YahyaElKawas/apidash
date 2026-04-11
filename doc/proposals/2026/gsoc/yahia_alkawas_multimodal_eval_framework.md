# GSoC 2026 Proposal: Multimodal AI and Agent API Eval Framework

* **Candidate:** Yahia (Yaya) Alkawas 
* **Project:** #2 - Multimodal AI and Agent API Eval Framework
* **Mentor:** Ankit & Ashita

## Abstract
This project aims to develop an end-to-end evaluation framework within API Dash to benchmark Text, Image, and Voice AI models and Agents. The architecture focuses on a "dependency-lite" approach, ensuring the framework is easy to install for end-users while providing a professional, real-time benchmarking experience.

## Proposed Architecture
* **Frontend (React/TypeScript):** A dynamic UI for configuring request parameters and visualizing multimodal results.
* **Backend (Python):** A robust bridge to tools like `lm-harness` and `lighteval`.
* **Execution:** Utilizing Python's `subprocess` for background tasks and **Server-Sent Events (SSE)** for real-time log streaming to minimize user dependencies.

## Detailed 12-Week Timeline (350 Hours)
* Week 1-2 (Community Bonding): Finalize API contracts and refine the MCP integration.

* Week 3-4 (Core Infrastructure): Implement the Async Evaluation Runner and SSE transport layer.

* Week 5-6 (Multimodal Parsers): Build the specialized handlers for Audio/Video/PDF.

* Week 7 (Midterm): Deliver a fully functional end-to-end prototype.

* Week 8-10 (Testing & Edge Cases): Write 80%+ coverage unit tests and handle "large file" streaming issues.

* Week 11-12 (Documentation): Write a full developer guide and a "How to add a new model" tutorial.

## Experience
As a CS student at Cairo University and a security researcher at HackerOne, I have extensive experience building scalable, secure Full-Stack applications using Node.js, React, and Python.

## 🚀 Proof of Concept (PoC)

To demonstrate the feasibility of the real-time streaming architecture, I have developed a functional Proof of Concept. This PoC integrates the FastAPI backend with the React frontend to handle live execution logs.

**[▶️ Watch the PoC Demo Video on Google Drive](https://drive.google.com/file/d/1yU1CVqcSTt9s4fWjEeRO6JzHmB7sXRpY/view?usp=drive_link)**

### **Technical Highlights of the PoC:**
* **Real-Time Streaming:** Implemented **Server-Sent Events (SSE)** using FastAPI’s `StreamingResponse` to pipe live output from a Python subprocess directly to the UI.
* **Terminal UI Component:** Developed a custom React/TypeScript terminal component that handles high-frequency data updates with 0% to 100% progress tracking.
* **Architecture:** Proves the "dependency-lite" approach by avoiding heavy message brokers like Redis, ensuring the framework remains lightweight and portable.

### MCP Alignment Architecture
​Standardized Tooling: "I will utilize MCP to standardize how the evaluation framework connects to external 'Multimodal Tools' (e.g., Vision-to-Text APIs, Audio Analysis tools)."
​Agentic Testing: "By implementing an MCP-compatible server, the framework will be able to evaluate not just model outputs, but also the accuracy of tool-calls made by Agentic AI models."
​Interoperability: "This ensures that any MCP-compatible model or agent can be plugged into the API Dash evaluation pipeline without custom glue code."

## Functional Requirements (The "What")
Real-time Streaming: The system must push evaluation logs to the UI with less than 200ms latency using SSE.

Multimodal Support: The framework must support rendering and evaluating Image (PNG/JPG), Audio (MP3/WAV), Video (MP4), and Document (PDF) formats.

Model Comparison: Users should be able to trigger the same evaluation against two different models simultaneously for benchmarking.

Asset Management: The system must securely fetch assets from both local paths and remote URLs.

## Non-Functional Requirements (The "How")
Security (Sandboxing): All multimodal assets must be rendered within a sandboxed environment to prevent XSS attacks.

Extensibility: The architecture must allow adding new media types (e.g., 3D models) by only updating the MediaDispatcher.

Reliability: The backend must handle subprocess failures gracefully without crashing the main API thread.

Ease of Setup: The project must be containerized using Docker to ensure a "one-command" setup for other contributors.

## The Architecture Diagram:
https://drive.google.com/file/d/1OM71McSuhDZ3f_VWvAS1MPakyd1s4wKb/view?usp=drive_link

## Security & Robustness
How I will handle:
Network drops: By Implementing a client-side buffer for SSE.
Large Payloads: By Using Blob URLs instead of Base64 for videos to save browser memory.

## Testing:
* Pytest for the backend logic.
* Vitest/Playwright for the UI.
* Mocking: How you will test the framework without spending money on expensive AI API calls (using Mock LLM responses).

## Implementation Strategy:
To ensure project maintainability across different operating systems (Windows/macOS/Linux), I will include a .gitignore that excludes environment-specific folders and provide a requirements.txt for consistent dependency resolution. I have already validated the setup on Windows, ensuring that the FastAPI backend and React frontend can be launched with minimal environment friction.
