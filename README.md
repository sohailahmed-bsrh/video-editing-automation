# Autonomous Video Editing & Cut Automation Engine

<p align="center">
  <a href="https://sohail.devsil.com"><strong>Portfolio</strong></a> | 
  <a href="https://github.com/sohailahmed-bsrh"><strong>GitHub Profile</strong></a> | 
  <a href="https://github.com/sohailahmed-bsrh/video-editing-automation"><strong>Source Repository</strong></a>
</p>

---

## Executive Summary & Problem Statement

Manual video editing for digital content, interviews, and educational lectures requires hours of repetitive labor: cutting silence, removing disfluencies ("um", "ah"), detecting scene changes, and aligning subtitles with millisecond precision. For high-volume content creators and media agencies, these manual tasks create production bottlenecks.

The Autonomous Video Editing Engine automates raw video post-production. By coordinating audio analysis, word-level speech recognition, scene boundary detection, and programmatic timeline assembly, the engine transforms raw recordings into polished, subtitle-synced video content without manual intervention.

<div align="center">
  <img src="frontend/src/assets/hero.png" width="750" alt="Autonomous Video Editing Dashboard"/>
  <p><em>Microservice pipeline for silence detection, automated cutting, and subtitle rendering.</em></p>
</div>

---

## Real-World Industry Applications

- **Podcast Post-Production**: Automatically truncates pauses, dead air, and speaker hesitation across multi-hour audio/video streams.
- **Short-Form Content Repurposing**: Converts long horizontal webinars and interviews into vertical (9:16) clips with burned-in dynamic captions.
- **Corporate Training Videos**: Standardizes internal video presentations by eliminating dead silence and aligning animated subtitles.
- **E-Learning & Course Creation**: Processes raw classroom lectures into concise, structured instructional modules.

---

## Technical Architecture & Engineering Walkthrough

The platform employs a decoupled asynchronous architecture separating client management from heavy compute rendering:

```
[Raw Video Upload] ──► [Node.js / Express API Gateway]
                                  │
                                  ▼
                        [Redis / BullMQ Job Queue]
                                  │
                                  ▼
                        [Python Worker Service]
                                  │
         ┌────────────────────────┼────────────────────────┐
         ▼                        ▼                        ▼
[Audio Silence Detector]  [Whisper Transcription]  [PySceneDetect Cuts]
(RMS Energy & Decibels)   (Word-Level Timestamps)  (HSV Scene Transitions)
         │                        │                        │
         └────────────────────────┼────────────────────────┘
                                  │
                                  ▼
                   [Timeline Decision Engine (EDL)]
                                  │
                                  ▼
            [FFmpeg / MoviePy Video Assembly & Subtitle Burn]
                                  │
                                  ▼
                 [Final Polished MP4 Video Asset]
```

### Step 1: Acoustic Silence Analysis
The Python worker (`backend/python-worker/app/audio_analysis/silence.py`) extracts the primary audio stream and evaluates acoustic energy levels. Using Root Mean Square (RMS) decibel thresholds and minimum pause durations (e.g., 600ms), it marks all silent intervals for non-destructive removal.

### Step 2: Speech-to-Text with Word Timestamps
The transcriber module (`backend/python-worker/app/transcription/transcriber.py`) runs OpenAI Whisper to extract text content, speaker shifts, and precise word boundaries with millisecond timestamps.

### Step 3: Visual Scene Boundary Detection
The visual scene module (`backend/python-worker/app/scene_detection/detector.py`) applies PySceneDetect algorithms (HSV color space thresholding) to track visual cut points, ensuring edits align with natural camera breaks.

### Step 4: Timeline Synthesis & Video Assembly
The timeline engine merges audio silences, scene cuts, and word boundaries into an Edit Decision List (EDL). MoviePy and direct FFmpeg subprocesses execute stream slicing, crossfade audio smoothing to avoid popping sounds, and dynamic text overlay generation.

### Step 5: Asynchronous Queue & Client Monitoring
Video rendering is CPU/GPU intensive. The Node.js orchestrator (`backend/src/app.ts`, `jobs.controller.ts`) enqueues render jobs into BullMQ, streaming progress back to the Vite web frontend via WebSocket status endpoints.

---

## Technology Stack & Implementation Specifications

| Component | Technology | Version | Architectural Function |
| :--- | :--- | :--- | :--- |
| **API Orchestrator** | Node.js / TypeScript | 20.x | Job dispatch, asset upload validation, WebSocket progress |
| **Worker Engine** | Python | 3.10+ | Heavy compute audio processing, Whisper, and FFmpeg tasks |
| **Speech Recognition** | OpenAI Whisper | Latest | Millisecond-accurate word timestamp generation |
| **Audio Analysis** | LibROSA / SciPy | Latest | Decibel-level energy calculation and silence detection |
| **Video Assembly** | MoviePy / FFmpeg | 4.x+ | Frame manipulation, stream concatenation, subtitle burning |
| **Scene Detection** | PySceneDetect | Latest | Content-aware visual transition identification |
| **Job Queue** | BullMQ / Redis | 5.x | Fault-tolerant asynchronous background task management |
| **Frontend Interface** | React.js / Vite | 18.x | Media preview, parameter configuration, and job monitoring |

---

## Installation & Setup Guide

### 1. Redis Queue Startup
```bash
docker run -d -p 6379:6379 redis:alpine
```

### 2. Python Worker
```bash
cd backend/python-worker
python -m venv venv
# Windows: venv\Scriptsctivate | Unix: source venv/bin/activate
pip install -r requirements.txt
python app/main.py
```

### 3. API Orchestrator & Frontend
```bash
cd backend
npm install
npm run dev

# In another terminal:
cd frontend
npm install
npm run dev
```

---

## Author & Contact Information

<table width="100%">
  <tr>
    <td width="150" align="center" valign="middle">
      <img src="https://avatars.githubusercontent.com/u/231165170?v=4" width="120" style="border-radius: 50%;" alt="Sohail Ahmed"/>
    </td>
    <td>
      <h3>Sohail Ahmed</h3>
      <p><strong>Senior Software Engineer & AI Systems Architect</strong></p>
      <p>Specializing in Full-Stack AI Application Development, Computer Vision, Deep Learning Pipelines, and Scalable Automation Architectures.</p>
      <p>
        <a href="https://sohail.devsil.com"><strong>Portfolio Website</strong></a> | 
        <a href="https://github.com/sohailahmed-bsrh"><strong>GitHub Profile</strong></a> | 
        <a href="https://www.linkedin.com/in/sohail-ahmed-devsil/"><strong>LinkedIn</strong></a> | 
        <a href="https://www.kaggle.com/sohail2411126"><strong>Kaggle</strong></a> | 
        <a href="https://x.com/ahmed241126"><strong>Twitter/X</strong></a> | 
        <a href="mailto:se906403@gmail.com"><strong>Email Contact</strong></a>
      </p>
    </td>
  </tr>
</table>
