# 🏓 PongBot

> **AI-Powered Table Tennis Broadcast Production Engine**  
> Turn raw match footage into TV-ready sports broadcasts with automated ball tracking, physics event spotting, ITTF scoring, and official WTT-style graphics.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Next.js 16](https://img.shields.io/badge/Next.js-16-black.svg)](https://nextjs.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.110%2B-teal.svg)](https://fastapi.tiangolo.com/)

---

## What is PongBot?

PongBot is an end-to-end computer vision and sports broadcast suite designed for table tennis clubs, tournaments, content creators, and broadcast producers. 

Instead of requiring manual scorekeeping, specialized multi-camera tracking hardware, or post-production video editing teams, PongBot takes a single match video recording and automatically:
- **Tracks players and ball motion** across rallies using custom computer vision models.
- **Identifies table bounces, paddle strikes, and net hits** through real-time physics modeling.
- **Enforces official ITTF rules** (11-point games, service rotation, deuce / win-by-two logic).
- **Renders TV-style broadcast overlays** complete with player names, national flags, serving indicators, and match statistics.
- **Merges original match audio** and produces a television-ready 1080p export.

---

## Project Repositories

PongBot is designed with a clean, decoupled microservices architecture split across three repositories:

| Repository | Purpose | Primary Tech |
| :--- | :--- | :--- |
| 🧠 **[pongbot-engine](https://github.com/nelson-david/pongbot-engine)** | Core Computer Vision, physics detection, ITTF rules state machine, and video overlay renderer. | Python, YOLOv8, OpenCV, PyTorch, FFmpeg |
| ⚡ **[pongbot-server](https://github.com/nelson-david/pongbot-server)** | High-performance backend API handling uploads, asynchronous worker queues, and Server-Sent Event (SSE) telemetry streaming. | FastAPI, Uvicorn, Python, Sentry |
| 🖥️ **[pongbot-client](https://github.com/nelson-david/pongbot-client)** | Broadcast control dashboard featuring progressive section disclosure, live terminal streaming, and export modals. | Next.js 16, TypeScript, Tailwind CSS |

---

## Architecture Flow

```
   Raw Match Video (.mp4 / .mov)
                 │
                 ▼
      ┌─────────────────────┐
      │   pongbot-client    │  Next.js 16 Web Dashboard
      └──────────┬──────────┘
                 │ Multipart Upload + SSE Stream
                 ▼
      ┌─────────────────────┐
      │   pongbot-server    │  FastAPI Asynchronous Gateway
      └──────────┬──────────┘
                 │ Thread Pool Worker
                 ▼
      ┌─────────────────────┐
      │   pongbot-engine    │  CV Pipeline & Rules Engine
      │  ├─ YOLOv8 Vision   │  Player & ball detection
      │  ├─ Physics Spotter │  Bounces & paddle hits
      │  ├─ ITTF Rules      │  Official 11-point scoring
      │  └─ WTT Renderer    │  Broadcast overlay & FFmpeg audio merge
      └──────────┬──────────┘
                 │
                 ▼
   Rendered Broadcast Video (1080p MP4) + Match Telemetry Report
```

---

## Quick Links & Documentation

For installation instructions, API references, and deployment guides, visit the respective repository:

- [pongbot-engine Documentation](https://github.com/nelson-david/pongbot-engine#readme)
- [pongbot-server Documentation](https://github.com/nelson-david/pongbot-server#readme)
- [pongbot-client Documentation](https://github.com/nelson-david/pongbot-client#readme)

---

## Author
**David Ogwu-Nelson** — [GitHub](https://github.com/nelson-david)

## License
This project is licensed under the MIT License.
