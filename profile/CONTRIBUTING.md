# Contributing to Zeeble

First off — thanks for wanting to help. Zeeble is built in the open and contributions from anyone are welcome, whether it's a bug fix, a new feature, a documentation improvement, or just asking a question that helps us explain something better.

---

## Before You Start

**Have a question?** Head to [Zeeblings](https://github.com/ZeebleChat/Zeeblings) (our community discussion board) or join the [Zeeble server](http://198.160.26.90:8081/join/zbl-3spzdzkj) directly.

**Found a bug?** [Open an issue](https://github.com/ZeebleChat/Server/issues/new) — describe what happened, what you expected, and how to reproduce it.

**Want to work on something?** Check the [open issues](https://github.com/ZeebleChat/Server/issues) first. Anything tagged `good first issue` or `help wanted` is actively looking for someone to pick it up.

---

## Contribution Flow

The right approach depends on the size of the change:

**Small changes** (bug fixes, typos, minor improvements, documentation) — just fork, make your change, and open a PR. No need to file an issue first.

**Medium or large changes** (new features, refactors, anything that touches multiple files or services) — open an issue first and describe what you want to do. This saves you from spending time on something that might conflict with work already in progress or go in a different direction than planned.

If you're unsure which category your change falls into, open an issue anyway. It's always better to check than to spend a week on a PR that needs a full rethink.

---

## Setting Up

### Backend (PhaseLink / Rust services)

Requires Rust stable or nightly — either works.

```bash
git clone https://github.com/ZeebleChat/Server.git
cd Server
cargo build
cargo test
```

### Frontend (Desktop Client)

Requires Node 18+. For the full desktop app you'll also need the [Tauri prerequisites](https://tauri.app/start/prerequisites/) for your OS.

```bash
git clone https://github.com/ZeebleChat/Client.git
cd Client
npm install
npm run dev          # browser dev mode
npm run tauri dev    # full desktop app
```

### Running the Full Stack Locally

The easiest way to get everything running together is Docker Compose:

```bash
cd Server
docker compose up -d
```

This starts PhaseLink, LiveKit, Redis, and Caddy. Edit `phaselink.yaml` to set your owner credentials and `public_url` before starting.

---

## Making Changes

1. **Fork** the repo you're working in
2. **Create a branch** — use a clear name like `fix/message-edit-crash` or `feature/role-color-picker`
3. **Make your changes**
4. **Write or update tests** — PRs without tests for new or changed behaviour will be asked to add them before merging
5. **Run the test suite** before opening a PR:

```bash
# Rust
cargo test

# Frontend
npm run test
```

6. **Open a Pull Request** — fill out the description, explain what changed and why, and link any related issues

---

## Pull Request Guidelines

- Keep PRs focused — one thing per PR is easier to review and faster to merge
- Write a clear title: `Fix: channel list not updating on role change` beats `fixed some stuff`
- If your PR is a work in progress, open it as a **Draft PR** so it's visible but not up for full review yet
- Be responsive to review feedback — PRs that go quiet get closed eventually

---

## Code Style

**Rust:** Run `cargo fmt` and `cargo clippy` before committing. CI will catch lint errors.

**TypeScript:** Run `npm run lint` before committing.

There's no formal style guide beyond what the linters enforce — just write readable code and leave comments where something isn't obvious.

---

## What Needs Help

Not sure where to plug in? Here's where things are actively needed:

| Area | Repo | Notes |
|:---|:---|:---|
| Bot API | Server | WIP since 0.1.0 — needs significant work to be production-ready |
| Rust backend | Server / DM-server | Backends are in good shape — mainly needs a code review pass, cleanup, and test coverage |
| React / TypeScript | Client | UI features, accessibility, bug fixes |
| Infrastructure | Server | Docker improvements, deployment guides, CI/CD |
| Documentation | All | Setup guides, API docs, self-hosting tutorials |
| Testing | All | Unit tests, integration tests across all services |

The Bot API in particular is a great area for someone who wants to own a significant piece of the platform — it's been mostly untouched since 0.1.0 and there's a lot of room to shape it.

---

## Services Overview

Zeeble is split across several repos. Here's a quick map so you know where things live:

| Repo | What it does |
|:---|:---|
| [Server (PhaseLink)](https://github.com/ZeebleChat/Server) | Core self-hosted chat server — REST + WebSocket, SQLite, Caddy, Docker |
| [Client](https://github.com/ZeebleChat/Client) | Desktop app — React 19, Tauri 2, LiveKit, Stripe |
| [DM-server](https://github.com/ZeebleChat/DM-server) | Direct messages, friends system, voice DMs |
| [Zeeblings](https://github.com/ZeebleChat/Zeeblings) | Community discussion board — questions, ideas, RFCs |
| [.github](https://github.com/ZeebleChat/.github) | Org config, issue templates, workflows |

---

## Code of Conduct

Be respectful. Zeeble is a community project and everyone contributing deserves to be treated well regardless of experience level. Harassment, discrimination, or bad faith behaviour will result in removal from the project.

---

*Questions? Join the [Zeeble server](http://198.160.26.90:8081/join/zbl-3spzdzkj) or open a thread on [Zeeblings](https://github.com/ZeebleChat/Zeeblings).*
