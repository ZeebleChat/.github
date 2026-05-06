<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=36&duration=4000&pause=1000&color=58A6FF&center=true&vCenter=true&multiline=true&width=600&height=90&lines=ZEEBLE;Chat+Without+Compromise." alt="Zeeble Chat" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-open_beta-58A6FF?style=for-the-badge" />
  <img src="https://img.shields.io/badge/version-0.1.11-brightgreen?style=for-the-badge" />
  <img src="https://img.shields.io/badge/next-0.2.0-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/license-Apache--2.0-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Rust-000000?style=for-the-badge&logo=rust&logoColor=white" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" />
  <img src="https://img.shields.io/badge/Tauri-24C8DB?style=for-the-badge&logo=tauri&logoColor=white" />
</p>

<p align="center">
  <b>A self-hostable chat platform with real-time messaging, voice channels, and a universal identity system.</b><br/>
  <sub>Built with Rust, React 19, and Tauri 2. Deploy anywhere. Own your data. Keep your identity.</sub>
</p>

<p align="center">
  <a href="https://zeeble.xyz"><b>🌐 zeeble.xyz</b></a> ·
  <a href="https://github.com/ZeebleChat/Client/releases"><b>⬇️ Download Client</b></a> ·
  <a href="http://198.160.26.90:8081/join/zbl-3spzdzkj"><b>💬 Join the Zeeble Server</b></a> ·
  <a href="https://status.zeeble.xyz"><b>📡 Status</b></a> ·
  <a href="#-contributing"><b>🤝 Contribute</b></a>
</p>

---

## Navigation

| | Section | Description |
|---|:---|:---|
| 🧭 | [What is Zeeble?](#-what-is-zeeble) | Overview and philosophy |
| 🏗️ | [Architecture](#-architecture) | Full system design and service map |
| 📦 | [Repositories](#-repositories) | Project breakdown |
| ✨ | [Features](#-features) | Client and server capabilities |
| 🔧 | [Tech Stack](#-tech-stack) | Technologies used |
| 🚀 | [Quick Start](#-quick-start) | Get up and running |
| 🔌 | [API Overview](#-api-overview) | REST and WebSocket reference |
| 🪪 | [Beam Identities](#-beam-identity-system) | Universal identity format |
| ⚙️ | [Configuration](#-configuration) | Server settings reference |
| 🗺️ | [Roadmap](#-roadmap) | What's coming next |
| 🤝 | [Contributing](#-contributing) | How to get involved |

---

## 🧭 What is Zeeble?

Zeeble is a **self-hostable messaging platform** that gives communities Discord-level features with full data ownership. Run it on your own hardware, connect with the official desktop client, and keep your identity across every server — self-hosted or cloud.

> *"Communication should be instant, secure, and beautifully simple."*

**Already live at [zeeble.xyz](https://zeeble.xyz) — currently in open beta.**

### Why Zeeble?

| | Discord | Slack | TeamSpeak | Revolt/Stoat | Root | Matrix/Element | **Zeeble** |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Self-hostable | ❌ | ❌ | ✅ | ✅ | ❌ | ✅ | ✅ |
| Managed cloud hosting | ✅ | ✅ | ❌ | Partial | ✅ | ❌ | 🚧 WIP |
| Voice + text in one app | ✅ | Partial | Voice only | ✅ | ✅ | ✅ | ✅ |
| Open source backend | ❌ | ❌ | ❌ | ✅ | ❌ | ✅ | ✅ |
| Texture packs & custom themes | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |
| Bot / extension API | ✅ | ✅ | ❌ | Partial | Community apps | ✅ | 🚧 WIP |
| 18+ server age verification | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ (v0.2.0) |
| No user caps on self-hosted | ❌ | ❌ | ✅ | ✅ | ❌ | ✅ | ✅ |
| Client app under 50MB RAM | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ | ✅ |
| Easy setup for non-technical users | ✅ | ✅ | Partial | Partial | ✅ | ❌ | ✅ |

---

## 🏗️ Architecture

Zeeble has two deployment paths — **Zeeble Cloud** (managed, hosted by Zeeble) and **Self-Hosted** (PhaseLink on your own hardware). Both share the same client and auth layer.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                          ZEEBLE ECOSYSTEM                               │
└─────────────────────────────────────────────────────────────────────────┘

  ┌──────────────────────────┐
  │      DESKTOP CLIENT      │
  │   React 19 + TypeScript  │
  │   Tauri 2 + Vite         │
  │   Custom Tauri Layer     │
  │   Light / Dark / Packs   │
  └────────────┬─────────────┘
               │
               │  WSS / HTTPS
               ▼
  ┌────────────────────────────────────────────────────────────────────┐
  │                        ZEEBLE CLOUD                                │
  │                                                                    │
  │  ┌──────────────┐  ┌──────────────┐  ┌──────────┐  ┌──────────┐  │
  │  │  AUTH       │  │  DM SERVER   │  │  CLOUD   │  │  PACKS   │  │
  │  │  Auth Server │  │  Direct Msgs │  │  Managed │  │  Texture │  │
  │  │  JWT / Stripe│  │  Friends     │  │  Servers │  │  Emojis  │  │
  │  │  Payments    │  │  Voice DMs   │  │  LiveKit │  │  Themes  │  │
  │  └──────┬───────┘  └──────┬───────┘  └────┬─────┘  └────┬─────┘  │
  │         │                 │               │              │        │
  │  ┌──────┴─────────────────┴───────────────┴──────────────┴──────┐ │
  │  │                      COMMUNITY                                │ │
  │  │              Public Server Discovery                          │ │
  │  └──────────────────────────────┬────────────────────────────────┘ │
  │                                 │                                  │
  │  ┌──────────────────────────────▼────────────────────────────────┐ │
  │  │                        POSTGRESQL                             │ │
  │  │              Primary · Backup · All cloud services            │ │
  │  └───────────────────────────────────────────────────────────────┘ │
  └────────────────────────────────────────────────────────────────────┘

  ┌────────────────────────────────────────────────────────────────────┐
  │                      SELF-HOSTED (PhaseLink)                       │
  │                                                                    │
  │  ┌──────────────┐  ┌──────────────┐  ┌──────────┐                 │
  │  │    CADDY     │  │   LIVEKIT    │  │  SQLITE  │                 │
  │  │  Auto-TLS    │  │  Voice/Video │  │  Local   │                 │
  │  │  CF Tunnels  │  │  + Redis     │  │  DB      │                 │
  │  └──────────────┘  └──────────────┘  └──────────┘                 │
  │                                                                    │
  │  Connects to: Zbeam (auth) · Desktop Client                        │
  │  Runs its own: LiveKit · SQLite · Caddy                            │
  └────────────────────────────────────────────────────────────────────┘
```

---

## 📦 Repositories

| Repository | Language | Status | Description |
|:---|:---|:---:|:---|
| [**Client**](https://github.com/ZeebleChat/Client) | TypeScript 73% | ✅ Active | Desktop client — React 19, Tauri 2, custom Tauri layer, LiveKit voice, Stripe, markdown, GIF picker, role permissions, texture pack support |
| [**Server (PhaseLink)**](https://github.com/ZeebleChat/Server) | Rust 99% | ✅ Active | Core self-hosted chat server — Axum REST + WebSocket, SQLite, Caddy, Docker Compose, bot API with Ed25519 JWT |
| [**DM-server**](https://github.com/ZeebleChat/DM-server) | Rust | ✅ Released | Direct messages, friends system, voice DMs |
| [**Zeeblings**](https://github.com/ZeebleChat/Zeeblings) | — | 💬 Discussions | Community discussion board |
| [**.github**](https://github.com/ZeebleChat/.github) | Config | ✅ Active | Org config, issue templates, workflows |

---

## ✨ Features

### Client

| Feature | Details |
|:---|:---|
| Real-time messaging | WebSocket-powered instant communication |
| Voice channels | LiveKit-powered voice rooms with screen sharing |
| Text channels | Markdown rendering + GIF picker (Tenor) |
| Direct messages | Private messaging with voice DM support |
| Server management | Create, join, and configure servers |
| Role-based permissions | Granular access control |
| Friend system | Friends list with DM integration |
| Texture packs | Custom emojis, animations, and themes — everything except layout |
| Themes | Light mode, dark mode, plus full custom color themes via packs |
| Premium subscriptions | Stripe-powered paid tiers ($5/mo) |
| Server boosts | Boost servers to unlock public pack slots |
| Self-hostable | Connect to any PhaseLink server, not just zeeble.xyz |
| Lightweight | Under 50MB RAM — no Electron bloat |

### Server (PhaseLink)

| Feature | Details |
|:---|:---|
| REST API | Full CRUD for channels, messages, members, invites, roles |
| WebSocket | Real-time message streaming with JSON frames |
| Bot API | Create bots, send messages, read channels via REST + WS — work in progress since 0.1.0 |
| Auto-TLS | Caddy handles Let's Encrypt automatically |
| SQLite | Zero-config database, auto-migrations on startup |
| Cloudflare tunnels | Built-in tunnel support for public URLs without port forwarding |
| File uploads | Configurable max size (default 8MB, up to 1GB) |
| Invite system | Expiry, max uses, human-readable landing pages |
| Beam identities | Universal user IDs across the whole Zeeble network |
| Server lock | Owner authentication required on every startup |
| No user caps | Run as many users as your hardware supports |

---

## 🔧 Tech Stack

<p align="center">
  <img src="https://skillicons.dev/icons?i=rust,typescript,react,vite,tauri,docker,sqlite,postgres,redis,linux&theme=dark&perline=10" />
</p>

### Cloud Backend

| Component | Technology | Purpose |
|:---|:---|:---|
| Zbeam | Rust + Axum | Auth server — JWT, Stripe payments, premium |
| DM Server | Rust | Direct messages, friends, voice DMs |
| Cloud | Rust | Managed server hosting (like Discord server creation) |
| Packs | Rust | Texture pack distribution — emojis, animations, themes |
| Community | Rust | Public server discovery |
| PostgreSQL | — | Primary data store for all cloud services |
| PostgreSQL (backup) | — | Automated backup instance |

### Self-Hosted Backend

| Component | Technology | Purpose |
|:---|:---|:---|
| PhaseLink | Rust + Axum | Core chat server (REST + WebSocket) |
| Caddy | Go | Auto-TLS reverse proxy + Cloudflare tunnel |
| LiveKit | Go | Voice and video rooms |
| LiveKit API | Go | Token bridge for client auth |
| Redis | C | LiveKit state + caching |
| SQLite | C | Local database |

### Frontend

| Component | Technology | Purpose |
|:---|:---|:---|
| UI | React 19 + TypeScript | Desktop client interface |
| Build | Vite | Fast dev server and bundler |
| Desktop | Tauri 2 | Native app wrapper (Windows/Mac/Linux) |
| Tauri Layer | Custom | Zeeble-specific Tauri compatibility and performance layer |
| Voice | LiveKit SDK | Voice/video integration |
| Payments | Stripe | Premium subscriptions |
| Security | DOMPurify | XSS sanitization |

---

## 🚀 Quick Start

### Run the Desktop Client

Download a prebuilt release from [GitHub Releases](https://github.com/ZeebleChat/Client/releases) — available for Windows, Mac, and Linux.

Or build from source:

```bash
git clone https://github.com/ZeebleChat/Client.git
cd Client
npm install
npm run dev          # browser dev mode
npm run tauri dev    # desktop app
```

### Self-Host with PhaseLink

```bash
git clone https://github.com/ZeebleChat/Server.git
cd Server
# Edit phaselink.yaml with your owner credentials and public URL
docker compose up -d
```

Caddy handles TLS automatically. For public access without port forwarding, Cloudflare tunnel support is built in.

> **Requirements:** Docker + Docker Compose. Voice support (LiveKit + Redis) is included in the default `docker-compose.yml`.

---

## 🔌 API Overview

### REST Endpoints

| Category | Endpoints |
|:---|:---|
| Auth | `GET /health`, `POST /admin/unlock` |
| Channels | `GET/POST /channels`, `PATCH/DELETE /channels/:id` |
| Messages | `GET/POST /channels/:id/messages`, `PATCH/DELETE /messages/:id` |
| Files | `POST /upload`, `GET /attachments/:id` |
| Members | `GET /members`, `PATCH /account/status` |
| Invites | `GET/POST /invites`, `DELETE /invites/:code`, `POST /invites/:code/redeem` |
| Roles | `GET /roles`, `PUT/DELETE /roles/:user_id` |
| Voice | `GET /voice/token`, `GET /voice/rooms` |
| Bots | `POST/GET /bots`, `DELETE /bots/:id` |

### WebSocket Protocol

Connect to `wss://yourdomain.com/ws` — all frames are JSON.

| Direction | Message Types |
|:---|:---|
| Client → Server | `auth`, `join`, `message`, `edit_message`, `delete_message`, `leave`, `ping` |
| Server → Client | `pong`, `message`, `message_edited`, `message_deleted`, `activated`, `error` |

---

## 🪪 Beam Identity System

Zeeble uses **beam identities** — one identity that follows you across every server on the network, self-hosted or cloud.

| Account Type | Separator | Example | Notes |
|:---|:---:|:---|:---|
| Primary | `»` | `alice»k4mx9` | Main account, auto-assigned tag |
| Alt | `§` | `alice§ab1cd` | Alt accounts |
| Child | `♦` | `alice♦xyz99` | Managed sub-accounts |
| Bot | `λ` | `MyBotλ00001` | Bot accounts via Bot API |

Display names are 1–12 characters (lowercase). Tags are 5 random alphanumeric characters assigned at registration. Premium users can set a custom tag.

---

## ⚙️ Configuration

All server settings live in `phaselink.yaml`. Most settings hot-reload without restart.

| Setting | Default | Reload | Description |
|:---|:---|:---:|:---|
| `port` | `4000` | Restart | Internal listen port |
| `db_path` | `zeeble.db` | Restart | SQLite database path |
| `public_url` | `http://localhost:4000` | Live | Base URL for invite links |
| `max_message_length` | `4000` | Live | Max characters per message |
| `max_upload_size` | `8MB` | Live | Max file upload size |
| `invites_anyone_can_create` | `true` | Live | Allow any member to create invites |

---

## 🗺️ Roadmap

### v0.2.0 — In Development

This is a major update — nearly every part of the platform is getting work. Big enough that it was originally versioned 0.1.12; renamed to 0.2.0 to reflect the actual scope.

**Community & Discovery**
- [ ] Community service — public server discovery page
- [ ] Packs service — texture pack distribution (emojis, animations, custom themes)
- [ ] ID verification for 18+ server gating

**UI & Client**
- [ ] Major UI overhaul across the desktop client
- [ ] Custom Tauri compatibility layer — Zeeble-specific integration for smoother native performance
- [ ] Text chat improvements

**Platform**
- [ ] Cloud service — managed server hosting

### Future
- [ ] Mobile client
- [ ] Federation between independent PhaseLink instances
- [ ] Audit log for server admins
- [ ] Zeeblings plugin/extension system

---

## 🤝 Contributing

Zeeble is actively looking for contributors across all areas — Rust backend, TypeScript/React frontend, infrastructure, documentation, and testing. No experience level is too junior and no contribution is too small.

### Where to Start

**Not sure where to begin?** Check the [open issues](https://github.com/ZeebleChat/Server/issues) — anything tagged `good first issue` or `help wanted` is fair game.

**Want to discuss ideas or ask questions?** Head to [Zeeblings](https://github.com/ZeebleChat/Zeeblings) — that's our community discussion board — or join the [Zeeble server](http://198.160.26.90:8081/join/zbl-3spzdzkj) directly.

**Want to work on something specific?** Open an issue first so we can discuss it before you spend time on it.

### How to Contribute

1. **Fork** the repository you want to contribute to
2. **Create** a feature branch — `git checkout -b feature/your-feature`
3. **Commit** your changes — `git commit -m 'Add: your feature description'`
4. **Push** — `git push origin feature/your-feature`
5. **Open a Pull Request** — describe what you changed and why

### Areas That Need Help

| Area | Repo | What's needed |
|:---|:---|:---|
| Rust backend | Server / DM-server | API endpoints, performance, tests |
| React/TypeScript | Client | UI features, accessibility, bug fixes |
| Infrastructure | Server | Docker, deployment guides, CI/CD |
| Documentation | All | Setup guides, API docs, tutorials |
| Testing | All | Unit tests, integration tests |

### Development Setup

```bash
# Backend (requires Rust stable)
git clone https://github.com/ZeebleChat/Server.git
cd Server
cargo build

# Frontend (requires Node 18+)
git clone https://github.com/ZeebleChat/Client.git
cd Client
npm install && npm run dev
```

---

## 📄 License

Licensed under the **Apache License 2.0** — see [LICENSE](LICENSE) for details.

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=2&height=60&section=footer" width="100%" />
</p>

<p align="center">
  <sub>Built in the open · <a href="https://zeeble.xyz">zeeble.xyz</a> · Open Beta</sub>
</p>
