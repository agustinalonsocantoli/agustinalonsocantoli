<p>
  <h1 align="center"><b>Hi, I'm Agustin Alonso Cantoli 👋</b></h1>
</p>

  [![Matrix SVG](https://raw.githubusercontent.com/rodrigograca31/rodrigograca31/master/matrix.svg)](https://www.youtube.com/watch?v=SDkAGkd4NLc)

 <p>
  <h4 align="center"><b><i>Full Stack Developer from Argentina, based in Valencia, Spain. Cofounder of Supafactu. I build multi-tenant SaaS with Node.js and React, native Mac and iOS apps in Swift, and put local LLMs to work inside them.</i></b></h4>
</p>

<p align="center">
<br>

<a href="https://www.instagram.com/alonsoagus_/"><img src="https://img.shields.io/badge/instagram-%23E4405F.svg?&style=for-the-badge&logo=instagram&logoColor=white" alt="Instagram" /></a>&nbsp;
<a href="https://www.linkedin.com/in/agustin-alonso-cantoli-5a54a0182/"><img src="https://img.shields.io/badge/linkedin-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>&nbsp;
<a href="mailto:agustinalonsocantoli@gmail.com?subject=Hello%20Agustin"><img src="https://img.shields.io/badge/gmail-%23D14836.svg?&style=for-the-badge&logo=gmail&logoColor=white" alt="Gmail"/></a>&nbsp;
</p>

<br>

### 👨‍💻 &nbsp;What I do

- 🏢 Full Stack at Imagina Group, a training company. I build the platforms the business runs on: a multi-tenant ERP, the ProAcademy e-learning campus, a CRM and the internal invoicing tools
- 🧾 Cofounder of Supafactu, an invoicing SaaS for Spanish freelancers and small businesses, in production at [app.supafactu.com](https://app.supafactu.com)
- ⚙️ Backend in AdonisJS and FastAPI over PostgreSQL and Redis. Frontend in React with Mantine, and Next.js. Native macOS and iOS in Swift and SwiftUI
- 🧠 Local models on Apple Silicon: LoRA fine-tunes with MLX, frozen evals, a FastAPI gateway in front, served from a Mac Mini I run myself

<br>

### 🚀 &nbsp;Projects

#### [Terminalia](https://github.com/agustinalonsocantoli/terminalia) — free native SSH client for macOS · [terminalia.dev](https://terminalia.dev)

Swift 5, SwiftUI + AppKit. Imports your `~/.ssh/config` (ProxyJump, forwards, certificates), opens one OpenSSH ControlMaster session per server, and runs everything over that single connection: terminal, dual-pane SFTP browser, remote editor, tunnels, PM2 + Docker Compose panel, live logs, snippets and a ⌘K palette. Works without an account or telemetry; secrets live only in Keychain. Spanish and English. In-app updates with Sparkle since 1.3.0, and a [Homebrew tap](https://github.com/agustinalonsocantoli/homebrew-tap):

```sh
brew tap agustinalonsocantoli/tap && brew install --cask agustinalonsocantoli/tap/terminalia
```

#### Supafactu — invoicing and expenses for Spanish freelancers and SMBs · [app.supafactu.com](https://app.supafactu.com)

Cofounded, private code, in production. AdonisJS 7 + Lucid + PostgreSQL, BullMQ on Redis, Puppeteer PDFs, SSE through Transmit. React 19 + Vite + Mantine 8 + TanStack Query.

The AI part: the invoice chat turns plain Spanish into invoice JSON on a Qwen3-4B-Instruct LoRA I fine-tuned with MLX on my own Mac Mini. Synthetic dataset (1,200 train, 200 frozen test, zero customer data), adapters versioned and judged against the same frozen set (v4: 96.5% valid JSON, 94% intent, 94.8% fields). One LLM call per turn; reply templates are deterministic on the Adonis side. The expense scanner turns a photo or PDF into a structured expense with a local Qwen3-VL via mlx-vlm, 9 deterministic guards in front, 93.3% on the production eval with 0 hard failures. Both run behind a Python FastAPI gateway with Redis cache and rate limiting, Langfuse tracing and pydantic repair.

#### Caloia — meal photo to macros, iOS (in progress)

SwiftUI app with @Observable stores and no third-party dependencies, AdonisJS 7 API, Python FastAPI engine running Qwen3-VL-8B-4bit + my own LoRA through mlx-vlm. JSON output is forced by an llguidance grammar; kcal and macros come from a deterministic food database, never from the model. Trained on Nutrition5k, FoodSeg103 and MM-Food-100K. The model perceives, the database calculates.

#### At Imagina Group (private)

- 🏗️ **Multi-tenant ERP**: AdonisJS 7 rewrite of a v5 backend with strict API parity, pg-boss jobs, Gmail, Drive and Holded integrations, and an AI service with a provider interface and OpenAI behind it
- 🎓 **ProAcademy campus**: multi-tenant e-learning on PostgreSQL with schema-per-tenant isolation (`search_path` set per transaction), pg-boss queues, Stripe subscriptions, FUNDAE-compliant guides and diplomas as PDF, and a student support bot on the OpenAI Assistants API
- 📣 **CRM**: campaigns, funnels, Gmail and Pipedrive sync, email generation with OpenAI traced through Langfuse
- 🧾 **Supplier-invoice reconciliation**: upload, Gmail or zip → extraction with the OpenAI Responses API → Google Drive mirror → bank CSV matching
- 🖥️ **pm2-admin**: web panel for the Mac Mini's PM2 processes, log tail over SSE, alerts with an Uptime Kuma dead-man's switch
- 🕷️ **scrapling-api**: FastAPI scraping service (Scrapling, Redis job store, BFS crawl) that replaced Firecrawl
- 🛡️ **bot-guardian**: Python watcher that polls PM2 every 5 minutes, applies deterministic rules (crash loops, silence, memory, swap), then asks a local Qwen3-4B + own LoRA to explain the incident on Discord. The dataset came from 712k real log events reduced to 891 templates

#### Also

- [nexo-web](https://github.com/agustinalonsocantoli/nexo-web): Next.js 16 + React 19 + Tailwind v4 site for a CrossFit gym in Valencia, with a QR welcome questionnaire
- Cafecito: macOS menu-bar app that keeps the Mac awake through IOKit power assertions, Swift/SwiftUI
- [multi-tenant-node](https://github.com/agustinalonsocantoli/multi-tenant-node): Express + Sequelize schema-per-tenant reference from 2024, the pattern I later used at work
- Solidity: a hand-written ERC-721 marketplace with Foundry, a weekend interest

<br>

### 🤖 &nbsp;AI, the way I do it

- 📏 **Evaluate first.** A frozen test set exists before any training run. A model version is a release: numbered adapters, judged against the same set, promoted or rejected
- 🧱 **Deterministic rules first, LLM second.** Guards, templates and a database handle what must be exact; the model handles what needs language or vision
- 🍎 **Local when it pays off.** Qwen3 on MLX on a Mac Mini M4 Pro serves Supafactu, Caloia and bot-guardian. Hosted OpenAI where the ERP, CRM and reconciliation need it
- 🧭 **Spec-driven development** with Claude Code and MCP servers for persistent memory and a code graph. I design the system and review every line; the model does the typing
- 🔒 **Customer data never enters a training set**

![OpenAI](https://img.shields.io/badge/-OpenAI-05122A?style=flat&logo=openai)&nbsp;
![Claude](https://img.shields.io/badge/-Claude-05122A?style=flat&logo=anthropic)&nbsp;
![MCP](https://img.shields.io/badge/-MCP-05122A?style=flat&logo=modelcontextprotocol)&nbsp;
![Qwen](https://img.shields.io/badge/-Qwen-05122A?style=flat&logo=alibabacloud)&nbsp;
![MLX](https://img.shields.io/badge/-MLX-05122A?style=flat&logo=apple)&nbsp;
![Hugging Face](https://img.shields.io/badge/-Hugging%20Face-05122A?style=flat&logo=huggingface)&nbsp;
![n8n](https://img.shields.io/badge/-n8n-05122A?style=flat&logo=n8n)&nbsp;
![Discord](https://img.shields.io/badge/-Discord-05122A?style=flat&logo=discord)&nbsp;

<br>

### 🛠 &nbsp;Tech Stack

![TypeScript](https://img.shields.io/badge/-TypeScript-05122A?style=flat&logo=typescript)&nbsp;
![JavaScript](https://img.shields.io/badge/-JavaScript-05122A?style=flat&logo=javascript)&nbsp;
![Python](https://img.shields.io/badge/-Python-05122A?style=flat&logo=python)&nbsp;
![Swift](https://img.shields.io/badge/-Swift-05122A?style=flat&logo=swift)&nbsp;
![Node.js](https://img.shields.io/badge/-Node.js-05122A?style=flat&logo=nodedotjs)&nbsp;
![AdonisJS](https://img.shields.io/badge/-AdonisJS-05122A?style=flat&logo=adonisjs)&nbsp;
![Express](https://img.shields.io/badge/-Express-05122A?style=flat&logo=express)&nbsp;
![FastAPI](https://img.shields.io/badge/-FastAPI-05122A?style=flat&logo=fastapi)&nbsp;
![React](https://img.shields.io/badge/-React-05122A?style=flat&logo=react)&nbsp;
![Next.js](https://img.shields.io/badge/-Next.js-05122A?style=flat&logo=nextdotjs)&nbsp;
![Vite](https://img.shields.io/badge/-Vite-05122A?style=flat&logo=vite)&nbsp;
![Mantine](https://img.shields.io/badge/-Mantine-05122A?style=flat&logo=mantine)&nbsp;
![Tailwind CSS](https://img.shields.io/badge/-Tailwind%20CSS-05122A?style=flat&logo=tailwindcss)&nbsp;
![PostgreSQL](https://img.shields.io/badge/-PostgreSQL-05122A?style=flat&logo=postgresql)&nbsp;
![Redis](https://img.shields.io/badge/-Redis-05122A?style=flat&logo=redis)&nbsp;
![MongoDB](https://img.shields.io/badge/-MongoDB-05122A?style=flat&logo=mongodb)&nbsp;
![Docker](https://img.shields.io/badge/-Docker-05122A?style=flat&logo=docker)&nbsp;
![Stripe](https://img.shields.io/badge/-Stripe-05122A?style=flat&logo=stripe)&nbsp;
![OpenAI](https://img.shields.io/badge/-OpenAI-05122A?style=flat&logo=openai)&nbsp;
![HTML](https://img.shields.io/badge/-HTML-05122A?style=flat&logo=HTML5)&nbsp;
![CSS](https://img.shields.io/badge/-CSS-05122A?style=flat&logo=CSS3&logoColor=1572B6)&nbsp;
![Git](https://img.shields.io/badge/-Git-05122A?style=flat&logo=git)&nbsp;
![GitHub](https://img.shields.io/badge/-GitHub-05122A?style=flat&logo=github)&nbsp;

<br>

### 📊 &nbsp;GitHub stats

<p align="center">
<a href="https://github.com/agustinalonsocantoli">
<img height="180em" src="https://github-readme-stats.vercel.app/api?username=agustinalonsocantoli&show_icons=true&theme=tokyonight&include_all_commits=true&count_private=true"/>
<img height="180em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=agustinalonsocantoli&layout=compact&langs_count=8&theme=tokyonight"/>
</a>
</p>
