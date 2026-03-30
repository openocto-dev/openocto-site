---
title: "Deep Dive: The OpenOcto Persona System"
description: "How personas work under the hood — YAML configs, system prompts, voice settings, and how to create your own custom persona."
date: "2026-03-15"
tags: ["technical", "personas"]
author: "Rocket Dev"
---

The persona system is what makes OpenOcto unique. While other assistants give you one fixed personality, OpenOcto lets you choose — or create — the perfect character for your needs.

## Anatomy of a Persona

Each persona is a directory containing:

```
personas/hestia/
├── persona.yaml        # Configuration
├── system_prompt.md    # AI system prompt
├── avatar.png          # Avatar for UI
└── sounds/             # Custom activation sounds
    ├── activate.wav
    └── deactivate.wav
```

## The YAML Configuration

```yaml
name: "Hestia"
display_name: "Hestia"
description: "Warm home keeper. Caring, calm, patient."

wakeword: "hey_hestia"
wakeword_threshold: 0.5

voice:
  engine: "piper"
  model: "en_US-amy-medium"
  length_scale: 1.05  # Slightly slower — calmer

personality:
  tone: "warm"
  verbosity: "balanced"
  humor: "gentle"
  formality: "informal"

skills:
  - media_control
  - smart_home
  - reminders
  - cooking_assistant
```

## Built-in Personas

| Persona | Role | Tone | Best For |
|---------|------|------|----------|
| Hestia | Home Keeper | Warm, caring | Family, daily tasks |
| Metis | Strategic Advisor | Concise, strategic | Business, planning |
| Nestor | Wise Mentor | Patient, thorough | Education, kids |
| Sofia | Companion | Empathetic, soft | Reflection, support |
| Argus | Guardian | Serious, attentive | Security, monitoring |
| Octo | Default | Friendly, universal | Quick start |

## Creating Your Own

1. Create a new directory under `personas/`
2. Write a `persona.yaml` with your configuration
3. Craft a `system_prompt.md` that defines behavior
4. Optionally add an avatar and custom sounds
5. Restart OpenOcto — your persona appears in the wizard

The community can share personas through the upcoming marketplace. Your custom creation could help thousands of users.
