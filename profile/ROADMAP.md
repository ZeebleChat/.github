# Zeeble Roadmap

This is a living document. Items move around as priorities shift — if you want to work on something here, open an issue or start a thread on [Zeeblings](https://github.com/ZeebleChat/Zeeblings).

---

## v0.2.0 — In Development

### Bug Fixes
- [ ] Display name does not update after change
- [ ] Client does not notify the user if their account was deleted or disabled
- [ ] Servers that are offline need a red dot indicator in the server list
- [ ] Channels cannot be reordered by click and drag
- [ ] Parental controls are not accessible through the main account

### Age Verification System
Four tiers of verification for servers that want to restrict access by age:

| Tier | Method | Notes |
|:---|:---|:---|
| Basic | Email age check | Email must be 5+ years old — requires 13+ to create, so a rough age signal |
| Standard | Email verified 18+ | Direct email-based 18+ confirmation |
| Moderate | Phone verification | Phone number required |
| High | Government ID | Scan ID, extract required info, immediately discard the image |

- [ ] Implement all four verification tiers
- [ ] Per-server verification level setting (owner chooses required tier)
- [ ] Server toggle: enable/disable new members joining

### Server Enhancements
- [ ] Server-level join toggle — enable or disable new members joining at any time
- [ ] Per-server verification requirement — owners choose which tier (email, phone, ID, etc.)
- [ ] External emoji support

### UI & Client
- [ ] Custom Tauri compatibility layer for smoother native performance

### Platform
- [ ] Community service — public server discovery with karma and ratings
- [ ] Packs service — texture pack distribution (emojis, animations, themes)
- [ ] Cloud service — managed server hosting

---

## Future — Enhancements

### Packs & Content System
- [ ] Soundboards, stickers, and custom emojis as part of the packs system
- [ ] Central sanitization server for validating and globalizing custom emojis, stickers, and soundboards before they enter the global pool
- [ ] Per-user pack downloads — users choose which packs to install instead of inheriting everything globally (avoids the Discord emoji spam problem)
- [ ] Paid content — stickers, emojis, and soundboards that use hosted server space can be set as premium-only
- [ ] Boosts increase a server's quota of emojis, stickers, and soundboards
- [ ] Ratings and karma system for packs — 5 star rating plus written comments so the community can flag bot farms, MAP servers, and low quality content that would otherwise game star ratings
- [ ] Pack discovery via the community listing with karma, ratings, comments, and categories
- [ ] Per-server toggle for global content (turn global emojis/stickers on or off for a specific server)

### Child Accounts & Parental Controls
- [ ] Expanded parental controls accessible from the main account
- [ ] Granular restrictions per child account
- [ ] Child account age verification integration

> Child accounts are mostly done — remaining work is parental controls depth and age verification integration.

### Premium & Boost Features
- [ ] Custom fonts
- [ ] Additional premium perks (TBD)
- [ ] Additional boost rewards beyond current tiers (TBD)

### Community & Discovery
- [ ] Community server listing with karma and ratings
- [ ] Servers can opt into the public listing

---

## Future — Platform

- [ ] Mobile client
- [ ] Federation between independent PhaseLink instances
- [ ] Audit log for server admins
- [ ] Bot API — production-ready release (currently WIP since 0.1.0)
- [ ] Zeeblings plugin/extension system

---

## Done ✅

- [x] Real-time messaging (WebSocket)
- [x] Voice channels (LiveKit)
- [x] Direct messages
- [x] Friends system
- [x] Voice DMs
- [x] Role-based permissions
- [x] Invite system
- [x] File uploads
- [x] Beam identity system
- [x] Self-hosted support (PhaseLink)
- [x] Cloudflare tunnel support
- [x] Bot API foundation (v0.1.0)
- [x] Stripe premium subscriptions
- [x] Light / dark mode
- [x] Texture pack theming foundation
- [x] Message edit history — previous versions viewable, visible to staff, editor, and receiver
- [x] UI overhaul
- [x] Text chat improvements
- [x] Child accounts (mostly complete)

---

*Want to work on something? Open an issue in the relevant repo or start a discussion on [Zeeblings](https://github.com/ZeebleChat/Zeeblings).*
