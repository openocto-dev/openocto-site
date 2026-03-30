# OpenOcto Site — Technical Description

## Project Overview

This is the **landing page and blog** for **OpenOcto** — an open-source constructor for personal AI assistants with voice control, persona system, and full local privacy. The site lives at [openocto.dev](https://openocto.dev).

OpenOcto itself is a Python-based platform that enables users to build personalized AI assistants with custom character, voice, and behavior — running entirely on their hardware (Mac, Windows, Linux). This site serves as the public-facing marketing and documentation entry point.

## Tech Stack

- **Framework:** [Astro](https://astro.build/) v6.1+ with MDX integration
- **Language:** TypeScript
- **Styling:** Custom CSS design system (no Tailwind despite README mention — pure CSS variables)
- **Fonts:** Inter (Google Fonts)
- **Content:** Astro Content Collections (Markdown blog posts)
- **Node.js:** >= 22.12.0
- **Deployment target:** Cloudflare Pages / GitHub Pages

## Project Structure

```
openocto-site/
├── assets/                          # Source images (logos, hero banner)
│   ├── hero-banner.jpg
│   ├── logo-capitan.png
│   └── logo-clean.png
├── site/                            # Astro project root
│   ├── astro.config.mjs             # Astro config (MDX integration)
│   ├── package.json
│   ├── tsconfig.json
│   ├── public/                      # Static assets served at /
│   ├── dist/                        # Build output
│   └── src/
│       ├── content.config.ts        # Content collection schema
│       ├── styles/
│       │   └── global.css           # Design system (CSS variables, base styles)
│       ├── layouts/
│       │   ├── BaseLayout.astro     # Root layout (nav, footer, meta)
│       │   └── BlogPost.astro       # Blog post layout
│       ├── pages/
│       │   ├── index.astro          # Homepage (hero, features, personas, pipeline, roadmap, blog, community)
│       │   └── blog/
│       │       ├── index.astro      # Blog listing page
│       │       └── [...slug].astro  # Dynamic blog post pages
│       └── content/
│           └── blog/                # Blog posts (Markdown)
│               ├── introducing-openocto.md
│               ├── local-voice-pipeline.md
│               └── persona-system-deep-dive.md
├── README.md
├── .gitignore
└── AGENTS.md                        # This file
```

## Design System

Dark theme with navy/coral/teal palette:

| Token | Value | Usage |
|-------|-------|-------|
| `--bg` | `#0b1426` | Page background |
| `--bg-card` | `#111d35` | Card backgrounds |
| `--navy` | `#1a365d` | Primary navy |
| `--coral` | `#ff6b6b` | Accent (CTAs, highlights) |
| `--teal` | `#4fd1c5` | Secondary accent (links, badges) |
| `--text` | `#e2e8f0` | Body text |
| `--text-muted` | `#94a3b8` | Secondary text |
| `--max-width` | `1200px` | Content container |

Responsive breakpoints: 1024px (tablet), 768px (mobile).

## Homepage Sections

1. **Hero** — full-screen with background image, headline, CTA buttons, stats
2. **What is OpenOcto** — 2x2 grid of value proposition cards
3. **Features** — 3-column grid of feature cards (9 features)
4. **Personas** — 3-column grid showcasing 5 built-in personas + "Create Your Own"
5. **How It Works** — vertical pipeline visualization (5 steps: wake word → VAD → STT → AI → TTS)
6. **Roadmap** — 4-phase grid (MVP → Personas & Wizard → Mobile App → Ecosystem)
7. **Blog** — latest 3 posts from content collection
8. **Community** — GitHub, Discord, Telegram links

## Navigation

Fixed navbar with blur backdrop. Links: Features, Personas, How it works, Roadmap, Blog, Community, GitHub (external). Mobile hamburger menu toggle via vanilla JS.

## Content System

Blog uses Astro Content Collections with Markdown files in `src/content/blog/`. Each post has frontmatter with `title`, `date`, `description`. Posts are sorted by date descending. Dynamic routing via `[...slug].astro`.

## OpenOcto Core Context

The site promotes these key aspects of the OpenOcto platform:

- **Local voice pipeline:** Wake word (OpenWakeWord) → VAD (Silero) → STT (whisper.cpp) → AI → TTS (Piper/Silero) — all audio processed on-device
- **Persona system:** 6 built-in characters (Hestia, Metis, Nestor, Sofia, Argus, Octo) — each with unique personality, voice, wake word, and skills
- **AI backend agnosticism:** Claude, OpenAI, Ollama (offline), Gonka, OpenClaw
- **Cross-platform:** macOS, Windows, Linux
- **Privacy:** No audio leaves the device; only text goes to AI API (optional with local LLM)
- **Setup wizard:** Visual browser-based first-run configuration
- **Mobile app:** React Native companion (Phase 3)
- **Integrations:** Home Assistant, Telegram bot
- **License:** MIT

## Development

```bash
cd site
npm install
npm run dev      # Dev server
npm run build    # Production build → dist/
npm run preview  # Preview production build
```

## Author

[Rocket Dev](https://rocketdev.io)
