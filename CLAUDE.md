# Hardware Security Key Management

Owner: amj@mqqn.net
Platform: pypi.org (expanding to other services over time)

## Project Purpose

Track and manage physical hardware security keys (FIDO2/WebAuthn) and recovery codes
across services. Started with PyPI 2FA setup; will grow to cover multiple services
and locations.

## Architecture

Plain TOML files for now. Future: Rust CLI tool for querying and managing inventory.

### Files

- `keys.toml` — Inventory of all physical security keys (model, connector, location, status, nickname)
- `registrations.toml` — Which keys are registered to which services/accounts
- `recovery-usage.toml` — Tracks recovery code consumption (NOT the codes themselves)
- `codes.txt` — **SENSITIVE**: Actual recovery codes. Must be in .gitignore.

### Naming Convention

Keys are named after characters from Kurosawa's Seven Samurai (七人の侍),
each carrying one kanji from 温故知新 (onkochishin: "study the old to understand the new"):

| Nickname  | Key ID       | Model | Kanji | Meaning          |
|-----------|-------------|-------|-------|------------------|
| Kambei    | titan-k51t-1 | K51T  | 温 on  | to warm, review  |
| Kyuzo     | titan-k40t-1 | K40T  | 故 ko  | the old, past    |
| Heihachi  | titan-k40t-2 | K40T  | 知 chi | to know          |
| Kikuchiyo | titan-k52t-1 | K52T  | 新 shin| the new          |

Future keys: draw from remaining samurai (Gorobei, Shichiroji, Katsushiro)
or other Kurosawa films.

## Security Rules

- NEVER commit `codes.txt` or any file containing actual recovery codes
- NEVER store secrets, passwords, or tokens in tracked files
- Recovery-usage.toml tracks *metadata* about code usage, not the codes
- keys.toml does NOT contain any secret material (serial numbers are physical identifiers, not secrets)

## Git Setup

- `.gitignore` must exclude: `codes.txt`, `*.secret`, `.env`
- Public-safe files: `keys.toml`, `registrations.toml`, `recovery-usage.toml`, `CLAUDE.md`

## Future Plans

- Rust CLI tool for querying key inventory and registration status
- Multi-service expansion (GitHub, npm, cloud providers, etc.)
- Multi-location key cache tracking
- Recovery code rotation reminders
