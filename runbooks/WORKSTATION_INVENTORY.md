# Xonaix Development Workstation Inventory

**Machine:** MCBEAST33  
**Owner:** Founder (Macman-1)  
**Captured:** 2025-12-24  
**Status:** ✅ GOLDEN STATE VERIFIED

---

## System

| Component | Value |
|-----------|-------|
| OS | Windows 11 Pro Insider |
| Build | 10.0.26220.0 |
| CPU Threads | 24 |
| Hostname | MCBEAST33 |

---

## Rust Toolchain

| Component | Version |
|-----------|---------|
| rustc | 1.92.0 (stable, default) |
| cargo | 1.92.0 |
| rustup | Latest |

### Installed Toolchains

- `stable-x86_64-pc-windows-msvc` (default)
- `nightly-x86_64-pc-windows-msvc`

### Installed Components

- clippy
- rustfmt
- rust-analyzer
- rust-src
- llvm-tools
- miri

### Installed Targets

- `x86_64-pc-windows-msvc`
- `wasm32-unknown-unknown`

### Cargo Tools

| Tool | Version | Purpose |
|------|---------|---------|
| cargo-audit | Latest | Security vulnerability scanning |
| cargo-deny | Latest | License/advisory compliance |
| cargo-nextest | Latest | Fast test runner |
| cargo-watch | Latest | File watching |
| cargo-expand | Latest | Macro expansion |
| cargo-sbom | Latest | SBOM generation |
| cargo-machete | Latest | Unused dependency detection |
| cargo-udeps | Latest | Unused dependency detection |
| just | 1.43.1 | Command runner |
| wasm-pack | Latest | WASM packaging |
| sqlx-cli | Latest | Database migrations |

---

## Node.js Ecosystem

| Component | Version |
|-----------|---------|
| Node.js | v24.11.1 |
| npm | 11.6.2 |
| pnpm | 10.25.0 |
| bun | 1.3.3 |
| TypeScript | 5.9.3 |

### Global Packages

- eslint
- prettier
- vercel
- railway-cli

---

## Git & GitHub

| Component | Version/Status |
|-----------|----------------|
| Git | 2.51.2.windows.1 |
| GitHub CLI | 2.83.1 |
| Authenticated | ✅ Macman-1 |
| SSH Key | Ed25519 (id_ed25519) |
| SSH to GitHub | ✅ Working |

### Git Configuration

```
user.name = (configured)
user.email = 130313181+Macman-1@users.noreply.github.com
```

---

## Docker & Containers

| Component | Version/Status |
|-----------|----------------|
| Docker Desktop | 29.1.2 |
| Docker Compose | v2.x |
| WSL2 Backend | ✅ Enabled |

### Running Containers

| Container | Image | Status |
|-----------|-------|--------|
| ollama | ollama/ollama | Up (persistent) |

### Ollama Models

| Model | Size | Purpose |
|-------|------|---------|
| qwen2.5-coder:7b | ~4.7GB | Tab autocomplete (fast) |
| qwen2.5-coder:32b | ~19GB | Local reasoning (powerful) |
| deepseek-coder-v2:16b | ~8.9GB | Backup/comparison |
| nomic-embed-text | ~274MB | Embeddings for Continue |

---

## IDEs & Editors

### VS Code

| Component | Value |
|-----------|-------|
| Version | 1.107.0 |
| Extensions | 38 installed |

#### Key Extensions

- rust-analyzer
- Continue (AI assistant)
- Claude Code
- Error Lens
- GitLens
- Even Better TOML
- Markdown Preview
- YAML
- Docker
- Remote - WSL

### Visual Studio

- Visual Studio Community 2026

---

## AI Development Tools

| Tool | Version/Status |
|------|----------------|
| Claude Desktop | Installed |
| Claude Code CLI | 2.0.75 |
| Continue | 1.5.21 |

### Continue Configuration

| Model | Provider | Role |
|-------|----------|------|
| GPT-5.2 | OpenAI | Primary |
| Claude Opus 4.5 | Anthropic | Primary |
| Grok 4.1 Fast | xAI | Primary |
| Gemini 3 Pro | Google | Secondary |
| qwen2.5-coder:7b | Ollama (local) | Autocomplete |
| qwen2.5-coder:32b | Ollama (local) | Chat |
| nomic-embed-text | Ollama (local) | Embeddings |

### Claude Desktop MCP Servers

| Server | Status | Paths |
|--------|--------|-------|
| filesystem | ✅ Configured | D:/dev/xonaix/{foundation,core,web,ops} |
| github | ✅ Configured | PAT rotated 2025-12-24 |

---

## Security Tools

| Tool | Version |
|------|---------|
| trivy | 0.68.1 |
| gitleaks | 8.30.0 |

---

## Shell Environment

### PowerShell

| Component | Value |
|-----------|-------|
| Version | 7.5.4 |
| Profile | `$HOME\Documents\PowerShell\Microsoft.PowerShell_profile.ps1` |
| Oh My Posh | ✅ Installed |
| Theme | `$HOME\.config\ohmyposh\xonaix.omp.json` |

### Environment Variables

| Variable | Value |
|----------|-------|
| POSH_THEME | `$HOME\.config\ohmyposh\xonaix.omp.json` |
| CARGO_HOME | `$HOME\.cargo` |
| RUSTUP_HOME | `$HOME\.rustup` |
| EDITOR | `code` |

### Shell Aliases & Functions

| Alias | Command |
|-------|---------|
| `dev` | `cd D:\dev\xonaix` |
| `foundation` | `cd D:\dev\xonaix\foundation` |
| `core` | `cd D:\dev\xonaix\core` |
| `web` | `cd D:\dev\xonaix\web` |
| `ops` | `cd D:\dev\xonaix\ops` |
| `gs` | `git status` |
| `gp` | `git pull` |
| `gd` | `git diff` |
| `gl` | `git log --oneline -20` |
| `cb` | `cargo build` |
| `ct` | `cargo test` |
| `cc` | `cargo clippy` |
| `cr` | `cargo run` |
| `cn` | `cargo nextest run` |
| `xonaix-status` | System overview |

---

## Directory Structure

### Development Root

```
D:\dev\xonaix\
├── foundation\    ← xonaix-foundation (archived)
├── core\          ← xonaix-core (Rust workspace)
├── web\           ← xonaix-web (Astro site)
└── ops\           ← xonaix-ops (brand, docs)
```

### OneDrive (Source Materials)

```
D:\OneDrive - XonaiX Inc\Tech\xonaix_b5\
├── Xonaix_B8_5_4_FOUNDATION_PRISTINE\    ← Original specs
└── Xonaix_Phase0_Package\                ← Setup package
```

---

## GitHub Repositories

| Repository | URL | Status |
|------------|-----|--------|
| xonaix-foundation | github.com/xonaix/xonaix-foundation | 🔒 Archived |
| xonaix-core | github.com/xonaix/xonaix-core | ✅ Active |
| xonaix-web | github.com/xonaix/xonaix-web | ✅ Active |
| xonaix-ops | github.com/xonaix/xonaix-ops | ✅ Active |

---

## Verification Results

**Date:** 2025-12-24  
**Script:** `Verify-XonaixWorkstation.ps1`

| Category | Passed | Warnings | Failed |
|----------|--------|----------|--------|
| Environment Variables | 4 | 0 | 0 |
| PowerShell Configuration | 3 | 0 | 0 |
| Rust Toolchain | 8 | 0 | 0 |
| Git/GitHub | 5 | 0 | 0 |
| Docker/Ollama | 6 | 0 | 0 |
| Claude Desktop | 4 | 0 | 0 |
| Directory Structure | 5 | 0 | 0 |
| Security Tools | 2 | 0 | 0 |
| **TOTAL** | **36** | **0** | **0** |

**Status:** ✅ GOLDEN STATE VERIFIED

---

## Maintenance Notes

### SSH Key

- Type: Ed25519
- Location: `$HOME\.ssh\id_ed25519`
- Public key added to GitHub: 2025-12-24
- Passphrase: None (for dev convenience)

### Secrets Rotated

- GitHub PAT: Rotated 2025-12-24 (old one was exposed in diagnostics)
- Location: Claude Desktop MCP config

### Backup Locations

- OneDrive: `D:\OneDrive - XonaiX Inc\`
- Docker volumes: `D:\docker\data\`
- Ollama models: `D:\docker\ollama\models\`

---

## Change Log

| Date | Change |
|------|--------|
| 2025-12-24 | Initial golden state achieved |
| 2025-12-24 | SSH key generated, added to GitHub |
| 2025-12-24 | GitHub PAT rotated |
| 2025-12-24 | Oh My Posh theme installed |
| 2025-12-24 | All 4 repos cloned and initialized |

---

*This inventory is the system of record for the Xonaix development workstation.*
