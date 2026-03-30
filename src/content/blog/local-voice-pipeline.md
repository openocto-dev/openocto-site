---
title: "How OpenOcto Processes Voice 100% Locally"
description: "A deep dive into the local voice pipeline: OpenWakeWord, Silero VAD, whisper.cpp, and Piper TTS — no audio leaves your device."
date: "2026-03-20"
tags: ["technical", "privacy"]
author: "Rocket Dev"
---

Privacy is not a feature — it's a foundation. In OpenOcto, **all audio processing happens on your device**. Here's how the pipeline works.

## The Five Stages

### 1. Wake Word Detection (OpenWakeWord)

The assistant listens for a specific activation phrase. Each persona has its own wake word — "Hey Hestia", "Hey Argus", or whatever you configure. OpenWakeWord runs continuously on audio chunks of 80ms, using a lightweight TFLite model.

### 2. Voice Activity Detection (Silero VAD)

Once the wake word triggers, Silero VAD takes over. It monitors the audio stream and detects when you stop speaking — after 3-4 seconds of silence, recording stops. The 2MB ONNX model is incredibly accurate.

### 3. Speech-to-Text (whisper.cpp)

The recorded audio is transcribed locally using whisper.cpp — C++ bindings for OpenAI's Whisper model. On Apple Silicon with the `small` model, a 10-second clip transcribes in under 3 seconds. Multilingual support is excellent.

### 4. AI Processing

This is the **only stage** that may involve an external connection — sending the transcribed text to Claude, OpenAI, or another API. But even this is optional: with Ollama running a local LLM, the entire pipeline is fully offline.

### 5. Text-to-Speech (Piper TTS)

The AI response is converted back to speech using Piper TTS. Each persona has its own voice configuration — speed, pitch, and character. Responses are streamed sentence-by-sentence for minimal latency.

## Total Latency

| Stage | Time |
|-------|------|
| Wake word | Real-time |
| VAD silence | 3.5s (configurable) |
| STT | <3s for 10s audio |
| AI response | 1-5s (streaming) |
| TTS | <1s per sentence |
| **Total perceived** | **~5-8s** |

The key optimization is streaming: TTS starts speaking the first sentence while the AI is still generating the rest.

## No Telemetry, No Analytics

OpenOcto has zero telemetry, zero analytics, and zero audio logging by default. The code is open-source (MIT) — you can verify this yourself.
