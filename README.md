# AI-Powered Hands-Free Computer Interaction 🖱️🎙️

A contactless human-computer interaction system that replaces the traditional mouse and keyboard with **head movement, eye blinks, mouth gestures, and voice commands** — enabling users to control a computer entirely hands-free.

Developed as a Major Project at **Rajiv Gandhi University of Knowledge Technologies (RGUKT), Basar**.

> **Author:** Yenugu Smitha

---

## 📖 Table of Contents

- [Introduction](#introduction)
- [System Overview](#system-overview)
- [Features](#features)
- [Benefits](#benefits)
- [System Architecture](#system-architecture)
- [Head + Eye + Mouth Tracking Module](#head--eye--mouth-tracking-module)
- [Voice Control Module](#voice-control-module)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Setup & Installation](#setup--installation)
- [Applications](#applications)
- [Future Scope](#future-scope)

---

## Introduction

Traditional input devices — the mouse and keyboard — require sustained physical effort and pose accessibility barriers for users with motor impairments, repetitive strain injuries, or situations where touching a device isn't practical (e.g. sterile environments).

**This project solves that problem** by enabling fully contactless computer interaction through a combination of:
- **Head movements** → cursor control
- **Eye blinks** → mouse clicks
- **Mouth gestures** → right-click action
- **Voice commands** → application control and dictation

The result is a touch-free alternative to conventional input devices, built using only a standard webcam and microphone — no specialized hardware required.

---

## System Overview

The system is composed of three core modules working together:

### 🎯 Head-Tracking Module
- Uses a webcam combined with **MediaPipe FaceMesh** for real-time gaze tracking
- Tracks the **nose tip landmark** and maps its movement to on-screen cursor coordinates
- Detects **blink-based clicks** (single and double) and **mouth-open gestures** (right-click)

### 🗣️ Speech-to-Text Module
- Converts spoken words into digital text directly inside editors, documents, or web applications
- Enables typing without a physical keyboard — useful for emails, notes, and general writing

### 🎤 Voice Command Module
- Captures speech via microphone
- Recognizes spoken commands such as *open file*, *switch window*, *close window*
- Executes the corresponding mouse and keyboard actions (clicks, scrolling, copy-paste, etc.)
- Provides **text-to-speech feedback** to confirm actions back to the user

### 🔗 System Integration
- Seamlessly connects the head-tracking and voice modules with the operating system
- Enables hands-free interaction across multiple software environments
- Designed to be scalable for use in healthcare, education, and industrial settings

---

## Features

| Feature | Description |
|---|---|
| 🖱️ Real-time Head Tracking | Gaze-based cursor control using facial landmark detection |
| 🎙️ Voice Command Processing | Open/close applications, navigate the OS by voice |
| ⌨️ Speech-to-Text | Hands-free dictation directly into editors and documents |
| 👄 Mouth-Open Gesture | Triggers a right-click action |
| ⚙️ Customizable Sensitivity & Commands | Tunable tracking sensitivity and configurable voice commands |
| 🖥️ Cross-platform Compatibility | Designed to work across different operating environments |

---

## Benefits

- **Hands-free productivity boost** — interact with a computer without lifting a finger
- **Hygienic interaction** — zero physical contact, ideal for sterile or shared-device environments
- **User comfort** — reduces repetitive strain associated with traditional mouse/keyboard use
- **Wide adaptability** — applicable across healthcare, education, gaming, and industrial settings
- **Accessibility** — empowers users with motor impairments to use computers independently

---

## System Architecture

```
┌──────────────────────┐        HTTP Requests        ┌──────────────────────┐
│   Frontend            │ ───────────────────────────▶│   Backend             │
│   (index.html)         │                              │   (Flask – server.py) │
│   UI with control      │ ◀─────────────────────────── │   Handles requests,   │
│   buttons               │                              │   runs eye & voice    │
└──────────────────────┘                              │   modules              │
                                                        └───────────┬───────────┘
                                                                    │
                                  ┌─────────────────────────────────┼─────────────────────────────────┐
                                  ▼                                                                    ▼
                  ┌──────────────────────────────┐                                  ┌──────────────────────────────┐
                  │  Head-Tracking Module          │                                  │  Voice Module                  │
                  │  (eye1.py)                      │                                  │  Executes spoken commands,     │
                  │  Uses MediaPipe & OpenCV         │                                  │  converts speech to text        │
                  │  to control the cursor           │                                  │                                  │
                  └──────────────────────────────┘                                  └──────────────────────────────┘
```

| Layer | Component | Responsibility |
|---|---|---|
| **Frontend** | `index.html` | User interface with control buttons |
| **Backend** | `server.py` (Flask) | Handles requests, orchestrates the eye-tracking and voice modules |
| **Head-Tracking** | `eye1.py` | Uses MediaPipe and OpenCV to control the cursor |
| **Voice Module** | — | Executes spoken commands and converts speech to text |

---

## Head + Eye + Mouth Tracking Module

This module is the core of the hands-free cursor experience:

1. Captures live video via **webcam**
2. Runs **MediaPipe FaceMesh** to detect facial landmarks
3. Tracks the **nose tip (landmark 1)** as the reference point for gaze direction
4. Maps the tracked gaze direction → **screen coordinates** for cursor movement
5. Interprets specific facial actions as input events:

| Gesture | Action |
|---|---|
| Left-eye blink | Single click |
| Right-eye blink | Double click |
| Mouth open | Right click |

---

## Voice Control Module

Handles all spoken interaction with the system:

1. **Captures speech** input via the microphone
2. **Recognizes commands** (e.g., opening applications, controlling the OS)
3. **Converts speech → text** for writing directly into documents and editors
4. **Integrates with the Flask backend** to actually execute the recognized commands
5. Provides **text-to-speech feedback** so the user knows their command was understood and executed

---

## Tech Stack

### Programming Languages & Frameworks
- **Python** — core implementation
- **Flask** — backend server and API handling
- **HTML, CSS, JavaScript** — frontend interface

### Libraries for Head Tracking
- **OpenCV** — webcam input and image processing
- **MediaPipe FaceMesh** — facial landmark detection (nose, lips, eyes)
- **pynput** — programmatic mouse control

### Libraries for Voice Control
- **SpeechRecognition** — speech-to-text conversion
- **Pyttsx3** — text-to-speech feedback
- **PyAutoGUI** — automates keyboard and mouse actions
- **SoundDevice + NumPy** — real-time audio recording

### System & Utility Tools
- **Subprocess / OS** — launching and managing applications
- **WMCTRL** *(Linux)* — focusing and managing windows
- **Wave** — handling audio recordings

---

## Project Structure

```
Hands-free-computer-interaction/
├── index.html          # Frontend UI with control buttons
├── server.py           # Flask backend — handles requests, runs eye & voice modules
├── eye1.py              # Head/eye/mouth tracking — MediaPipe + OpenCV cursor control
├── voice_module.py      # Voice command recognition & speech-to-text (module name may vary)
├── requirements.txt    # Python dependencies
└── README.md
```

> Note: exact filenames for the voice module may differ in the repository — refer to `server.py`'s imports to confirm which files are wired together.

---

## Setup & Installation

### Prerequisites
- Python 3.x
- A working webcam
- A working microphone
- (Linux only) `wmctrl` installed for window management features

### Installation

```bash
# Clone the repository
git clone https://github.com/smithayenugu/Hands-free-computer-interaction.git
cd Hands-free-computer-interaction

# Create and activate a virtual environment (recommended)
python -m venv venv
source venv/bin/activate      # macOS/Linux
venv\Scripts\activate         # Windows

# Install dependencies
pip install -r requirements.txt
```

### Running the Application

```bash
python server.py
```

Then open the frontend (`index.html`) in your browser, or navigate to the local server address printed in the terminal, and grant camera + microphone permissions when prompted.

---

## Applications

- **Assistive technology** for differently-abled users
- **Sterile environments** (hospitals, laboratories) where touchless interaction is preferred
- **Hands-free computing** in industrial setups
- **Gaming and interactive learning** experiences

---

## Future Scope

- Improve gaze-tracking accuracy and reduce cursor jitter in varying lighting conditions
- Expand the voice command vocabulary for more complex, multi-step OS actions
- Add gesture customization through a settings UI rather than hardcoded thresholds
- Package as a standalone cross-platform desktop application for easier installation

---

Built by Smitha
