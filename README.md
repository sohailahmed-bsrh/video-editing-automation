<div align="center">

<h1>Automated Video Processing & Subtitle Generation Pipeline</h1>

<img src="https://readme-typing-svg.herokuapp.com?font=Inter&weight=800&size=22&duration=3000&pause=1000&color=6366F1&center=true&vCenter=true&width=800&lines=Automated+Video+Processing;Whisper+Speech-to-Text+Subtitling;MoviePy+Video+Assembly;FastAPI+%2B+React+Interface" alt="Typing Header" />

<p><strong>Programmatic Video Processing, Audio Extraction, Whisper Subtitling, and MoviePy Rendering</strong></p>

<p>
  <a href="https://skillicons.dev"><img src="https://skillicons.dev/icons?i=python,fastapi,react,vite,ts,tailwind,github&theme=dark" alt="Skills" /></a>
</p>

<p>
  <a href="#overview">Overview</a> &bull;
  <a href="#system-architecture">Architecture</a> &bull;
  <a href="#visual-showcase-gallery">Visual Gallery</a> &bull;
  <a href="#core-capabilities">Capabilities</a> &bull;
  <a href="#installation--setup">Installation</a> &bull;
  <a href="#author--contact-information">Author</a>
</p>

</div>

---
## Overview

The Video Editing Automation framework automates repetitive video editing workflows. Given raw video files, the pipeline extracts audio tracks, performs speech transcription with OpenAI Whisper, generates synchronized animated subtitle overlays, applies video speed curves, and renders final composite videos using MoviePy and FFmpeg.

---

## Visual Showcase Gallery

<table width="100%" align="center">
  <tr>
    <td align="center"><b>Application Interface & Processing Hero</b><br><sub>Vite & React frontend interface communicating with FastAPI video processing backend.</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="frontend/src/assets/hero.png" alt="Video Hero Screen" width="700"/></td>
  </tr>
</table>

---

## System Architecture

```mermaid
flowchart TD
    A[Raw Video File Upload: MP4 / MOV] --> B[Audio Stream Extraction via FFmpeg]
    B --> C[OpenAI Whisper Automated Transcription]
    C --> D[Timestamp-Synchronized Subtitle Segments]
    D --> E[Animated Subtitle Graphic Generator]
    A --> F[MoviePy Video Compositor Engine]
    E --> F
    F --> G[Video Compression & Final MP4 Export]
```

---

## Technology Stack

| Layer | Technologies |
| :--- | :--- |
| Backend Server | FastAPI, Python 3.10+, Uvicorn |
| Media Processing | MoviePy, FFmpeg, Whisper |
| Frontend Interface | React, TypeScript, Vite, Tailwind CSS |

---

## Installation & Setup

```bash
# Clone the repository
git clone https://github.com/sohailahmed-bsrh/video-editing-automation.git
cd video-editing-automation

# Setup backend
cd backend
pip install -r requirements.txt
python main.py

# Setup frontend
cd ../frontend
npm install
npm run dev
```
---

## Author & Contact Information

<table width="100%" align="center">
  <tr>
    <td align="center" style="padding: 20px;">
      <h3>Sohail Ahmed</h3>
      <p><strong>Full-Stack Artificial Intelligence & Computer Vision Engineer</strong></p>
      <p>
        <a href="https://sohail.devsil.com"><img src="https://img.shields.io/badge/Live_Portfolio-sohail.devsil.com-0052FF?style=for-the-badge&logo=google-chrome&logoColor=white" alt="Portfolio"/></a>
        <a href="https://github.com/sohailahmed-bsrh"><img src="https://img.shields.io/badge/GitHub-Profile-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"/></a>
        <a href="https://linkedin.com/in/sohail-ahmed-dev"><img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/></a>
        <a href="mailto:sohail.bsrh@gmail.com"><img src="https://img.shields.io/badge/Email-Contact_Me-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"/></a>
      </p>
      <p><em>Available for technical roles in Artificial Intelligence, Computer Vision, and Full-Stack Engineering.</em></p>
      <hr style="border: 0; height: 1px; background: #30363d; margin: 15px 0;">
      <small>Repository: <code>sohailahmed-bsrh/video-editing-automation</code> &bull; Distributed under the MIT License.</small>
    </td>
  </tr>
</table>
