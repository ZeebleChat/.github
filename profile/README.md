<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=32&duration=4000&pause=1000&color=58A6FF&center=true&vCenter=true&multiline=true&width=600&height=80&lines=ZEEBLE+CHAT;Connect.+Converse.+Create." alt="Zeeble Chat" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-actively_building-brightgreen?style=for-the-badge" alt="Status" />
  <img src="https://img.shields.io/badge/license-Apache--2.0-blue?style=for-the-badge" alt="License" />
  <img src="https://img.shields.io/badge/Rust-000000?style=for-the-badge&logo=rust&logoColor=white" alt="Rust" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Tauri-24C8DB?style=for-the-badge&logo=tauri&logoColor=white" alt="Tauri" />
</p>

<p align="center">
  <b>A self-hostable chat platform with real-time messaging, voice channels, and a bot API.</b>
  <br />
  <sub>Built with Rust, React, and Tauri. Deploy anywhere. Own your data.</sub>
</p>

<br />

---

## Navigation

| Section | Description |
| :--- | :--- |
| [What is Zeeble?](#-what-is-zeeble) | Overview and philosophy |
| [Architecture](#-architecture) | System design and data flow |
| [Repositories](#-repositories) | Project breakdown |
| [Client Features](#-client-features) | Desktop app capabilities |
| [Server Features](#-server-features) | Backend capabilities |
| [Tech Stack](#-tech-stack) | Technologies used |
| [Quick Start](#-quick-start) | Get up and running |
| [API Overview](#-api-overview) | REST and WebSocket reference |
| [Beam Identities](#-beam-identity-system) | User identification format |
| [Configuration](#-configuration) | Server settings reference |
| [Contributing](#-contributing) | How to help |

---

## What is Zeeble?

Zeeble is a **self-hostable messaging platform** that gives you the power of Discord-like communication with full control over your data. Run it on your own server, connect with the official desktop client, and never worry about vendor lock-in again.

> _"Communication should be instant, secure, and beautifully simple."_

---

## Architecture

```
                    +----------------------------------------------+
                    |              ZEEBLE ECOSYSTEM                 |
                    +----------------------------------------------+

  +---------------------+
  |   DESKTOP CLIENT    |
  |  React 19 + TS      |
  |  Tauri 2 + Vite     |
  |  LiveKit (voice)    |
  |  Stripe (premium)   |
  +----------+----------+
             |  WSS / HTTPS
             v
  +---------------------+         +--------------------------+
  |      CADDY :443     |-------->|    PHASELINK :4000       |
  |  Auto-TLS + Proxy   |         |  Rust / Axum Server      |
  |  WebSocket Upgrade  |         |  REST + WebSocket API    |
  +---------------------+         |  SQLite Database         |
                                  |  Bot API + Ed25519 JWT   |
                                  +------------+-------------+
                                               |
                    +--------------------------+----------------------+
                    v                          v                      v
          +-----------------+      +------------------+    +-----------------+
          |    LIVEKIT      |      |   LIVEKIT-API    |    |     REDIS       |
          |  Voice / Video   |      |  Token Bridge    |    |  State / Cache  |
          |  :7880-7882      |      |  :3000           |    |  :6379          |
          +-----------------+      +------------------+    +-----------------+
```

---

## Repositories

| Repository | Language | Description |
| :--- | :--- | :--- |
| [**Client**](https://github.com/ZeebleChat/Client) | TypeScript 73% | Official desktop client with React 19, Tauri 2, LiveKit voice, Stripe payments, markdown rendering, GIF picker, friend system, and role-based permissions |
| [**Server**](https://github.com/ZeebleChat/Server) | Rust 99% | PhaseLink backend with Axum REST + WebSocket API, SQLite, Caddy auto-TLS, Docker Compose, LiveKit integration, and bot API with Ed25519 JWT auth |
| [**DM-server**](https://github.com/ZeebleChat/DM-server) | Coming Soon | Dedicated direct messaging service |
| [**Zeeblings**](https://github.com/ZeebleChat/Zeeblings) | Coming Soon | Extensions, plugins & integrations |
| [**.github**](https://github.com/ZeebleChat/.github) | Config | Organization config, issue templates & workflows |

---

## Client Features

| Feature | Details |
| :--- | :--- |
| Real-time messaging | WebSocket-powered instant communication |
| Voice channels | LiveKit-powered voice rooms with screen sharing |
| Text channels | Markdown rendering + GIF picker (Tenor) |
| Server management | Create, join, and configure servers |
| Role-based permissions | Granular access control |
| Friend system | Direct messages and social connections |
| Premium subscriptions | Stripe integration for paid tiers |
| Theming | Light and dark mode support |
| Self-hostable | Connect to any Zeeble server, not just zeeble.xyz |

---

## Server Features

| Feature | Details |
| :--- | :--- |
| REST API | Full CRUD for channels, messages, members, invites, roles |
| WebSocket | Real-time message streaming with JSON frames |
| Bot API | Create bots, send messages, read channels via REST + WS |
| Auto-TLS | Caddy handles Let's Encrypt automatically |
| SQLite | Zero-config database, auto-migrations on startup |
| File uploads | Configurable max size (default 8MB, supports up to 1GB) |
| Invite system | Expiry, max uses, human-readable landing pages |
| Beam identities | Unique user identifiers with display name + tag format |
| Server lock | Owner authentication required on every startup |

---

## Tech Stack

<p align="center">
  <img src="https://skillicons.dev/icons?i=rust,typescript,react,vite,tauri,docker,sqlite,redis,caddy,git,github,linux&theme=dark&perline=12" alt="Tech Stack" />
</p>

### Backend

| Component | Technology | Purpose |
| :--- | :--- | :--- |
| PhaseLink | Rust + Axum | Core chat server (REST + WebSocket) |
| Caddy | Go | Auto-TLS reverse proxy |
| LiveKit | Go | Voice and video rooms |
| Redis | C | LiveKit state management |
| SQLite | C | Primary data store |

### Frontend

| Component | Technology | Purpose |
| :--- | :--- | :--- |
| UI | React 19 + TypeScript | Desktop client interface |
| Build | Vite | Fast dev server and bundler |
| Desktop | Tauri 2 | Native app wrapper |
| Voice | LiveKit SDK | Voice/video integration |
| Payments | Stripe | Premium subscriptions |
| Security | DOMPurify | XSS sanitization |

---

## Quick Start

### Client

```bash
git clone https://github.com/ZeebleChat/Client.git
cd Client
npm install
npm run dev          # browser dev mode
npm run tauri dev    # desktop app
```

### Server

```bash
git clone https://github.com/ZeebleChat/Server.git
cd Server
# Edit phaselink.yaml with your owner credentials
docker compose up -d
```

---

## API Overview

### REST Endpoints

| Category | Endpoints |
| :--- | :--- |
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

Connect to `wss://yourdomain.com/ws` -- all frames are JSON.

| Direction | Message Types |
| :--- | :--- |
| Client to Server | `auth`, `join`, `message`, `edit_message`, `delete_message`, `leave`, `ping` |
| Server to Client | `pong`, `message`, `message_edited`, `message_deleted`, `activated`, `error` |

---

## Beam Identity System

Zeeble uses **beam identities** instead of traditional user IDs.

| Account Type | Separator | Example |
| :--- | :---: | :--- |
| Primary | `>>` | `alice>>k4mx9` |
| Alt | `S` | `aliceS>ab1cd` |
| Child | `>` | `alice>xyz99` |
| Bot | `A` | `MyBotA00001` |

Display names are 1-12 characters (lowercase). Tags are 5 random alphanumeric characters assigned at registration.

---

## Configuration

All server settings live in `phaselink.yaml`. Most settings hot-reload without restart.

| Setting | Default | Reload | Description |
| :--- | :--- | :--- | :--- |
| `port` | `4000` | Restart | Internal listen port |
| `db_path` | `zeeble.db` | Restart | SQLite database path |
| `public_url` | `http://localhost:4000` | Live | Base URL for invite links |
| `max_message_length` | `4000` | Live | Max characters per message |
| `max_upload_size` | `8MB` | Live | Max file upload size |
| `invites_anyone_can_create` | `true` | Live | Allow any member to create invites |

---

## Contributing

We welcome contributions! Here's how to get started:

1. **Fork** the repository
2. **Create** your feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

---

## License

This project is licensed under the **Apache License 2.0** -- see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=60&section=footer" width="100%" />
</p>

<p align="center">
  <sub>Built with passion by the Zeeble Team</sub>
</p>
