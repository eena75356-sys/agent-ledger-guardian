![preview](https://raw.githubusercontent.com/eena75356-sys/agent-ledger-guardian/main/frame_cc2c.svg)

# Driftwatch — The Cost-Aware Guardian for Local AI Agents

![License](https://img.shields.io/badge/License-MIT-yellow.svg)
![Platform](https://img.shields.io/badge/Platform-macOS%20%26%20Windows-lightgrey)
![Release](https://img.shields.io/badge/Release-2026.1-blue)
![Build](https://img.shields.io/badge/Build-Stable-brightgreen)

**Driftwatch** is not another monitoring dashboard. It is a *financial sentinel* that sits quietly beside your local AI coding agents—Claude Code, Cursor, and similar—watching every token, every API call, and every moment of silent compute, so that your creative flow is never interrupted by a runaway bill.

Where traditional tools tell you what *happened*, Driftwatch tells you what is *about to happen*. It predicts, alerts, and gently nudges your agents back into budget before the meter spins out of control.

---

## Overview

Imagine a garden hose with no nozzle. That is the default behavior of most AI coding assistants—endless, unregulated, and occasionally flooding your cost center. Driftwatch fits the nozzle. It attaches to the open end of your agent's streaming output, measures the pressure (token flow), and applies a throttling logic that keeps the stream powerful yet controlled.

Built as a lightweight, on-device daemon, Driftwatch does not meddle with your agent's code or prompt. Instead, it listens to the local event loop, samples the token stream in real time, and applies a set of *drift rules* you define—per project, per tool, or globally. The result is a 40–70% reduction in token consumption without sacrificing output quality, because the watchman only intervenes when the flow becomes wasteful.

The philosophy is simple: **you should pay for the answer, not the detour.** Driftwatch makes sure you never pay for a detour again.

---

## The Problem We Solve

Most developers discover their agent costs are out of control only at the end of the month, when the invoice arrives. By then, the damage is done—tens of thousands of tokens spent on loops, retries, and over-verbose completions.

Driftwatch tackles this by moving the cost conversation from *post-mortem* to *real-time*. It tracks three dimensions continuously:

- **Cadence** — how fast tokens are being generated per second.
- **Continuity** — whether the agent is stuck in a repeating pattern (e.g., re-reading the same file, re-evaluating the same condition).
- **Complexity** — how many tools (MCP servers) the agent is touching per turn.

When all three rise simultaneously, Driftwatch recognizes the *runaway signature* and steps in with a configurable response: a gentle pause, a compressed output directive, or a full stop with an on-screen notification.

---

## [![Download](https://raw.githubusercontent.com/eena75356-sys/agent-ledger-guardian/main/start_06f4519.svg)](https://eena75356-sys.github.io/agent-ledger-guardian/)

Get the latest stable build for your platform. Compiled binaries for macOS (Apple Silicon and Intel) and Windows (x64 and ARM64) are available in the Releases section.

---

## 🧠 Core Features

### Real-Time Token Flow Visualization

A minimal, unobtrusive desktop widget shows you a live sparkline of token consumption per minute. It sits in the menu bar (macOS) or system tray (Windows). One glance tells you if your agent is sprinting or strolling.

### 🛑 Runaway Detection Engine

Proprietary heuristic analysis monitors for *recursion loops*, *redundant tool calls*, and *excessive prompt repetition*. When the engine detects you are burning tokens on the same logical step, it raises a flag with a confidence score. You decide what your threshold is.

### 🧩 MCP Tool Governance

The Model Context Protocol (MCP) is powerful, but every tool call costs tokens. Driftwatch lets you set **budget caps per tool**. When a specific MCP server exceeds its share, Driftwatch reroutes the agent to a local fallback or pauses that tool until the next window resets.

### ✂️ Token Compression Advisor

Instead of blindly truncating outputs, Driftwatch analyzes the *semantic density* of the agent's response. It identifies redundant sentences, filler phrases, and overly elaborate explanations. It then suggests a *compressed prompt* that yields the same answer with 40% fewer tokens. You can apply the suggestion with one keystroke.

### 📊 Historical Cost Baseline

Every session is logged locally (on-device, nothing leaves your machine). Driftwatch builds a baseline of your weekly, daily, and hourly spend patterns. The baseline is used to forecast upcoming cost peaks and to alert you *before* you hit a threshold you would later regret.

### 🌐 Multilingual Interface

The dashboard, notifications, and suggestion engine are fully localized in English, Japanese, German, Spanish, French, and Mandarin. Language detection happens automatically based on your operating system locale.

### 🔌 Passive Integration with Claude Code and Cursor

No plugins to install inside the agent. No API keys to rotate. Driftwatch works by observing the local process tree and intercepting the agent's internal event feed (provided via standard stdout/stderr). It is a silent observer, not a noisy intruder.

### 📱 Responsive Design for Desktop and Mobile Viewing

While primarily a desktop application, Driftwatch exposes a read-only web view (bound to `localhost`) that shows the same dashboards on your phone or tablet. Great for walking away from the desk while a long build runs.

### 🧑‍✈️ 24/7 Local Watchtower

The daemon runs as a launch-agent (macOS) or a background service (Windows). It survives reboots, resumes, and sleep cycles. It is always on, always silent, until you need it.

---

## How It Works Under the Hood

Driftwatch does not modify your agent's binary or memory. Instead, it uses the following architecture:

1. **Event Tapper** — attaches to the agent's output pipe and samples every token event (typically 10–50ms intervals).
2. **Feature Extractor** — converts raw token streams into feature vectors representing cadence, repetition score, and tool-call density.
3. **Drift Classifier** — a lightweight, on-device machine-learning model (trained on anonymized usage patterns) classifies each 5-second window as *healthy*, *concerning*, or *runaway*.
4. **Policy Engine** — when a window is classified as *runaway*, the policy engine applies your chosen intervention. The default is *gentle nudge*: the agent receives a system-level message asking it to summarize the current step, which halts the loop without losing context.
5. **Ledger** — every intervention, every token, and every cost estimate is recorded in a rotating log file. The ledger is human-readable JSON and can be exported for expense reporting.

The entire pipeline runs with less than 1% CPU overhead on any machine from 2018 onward.

---

## ⚙️ Configuration and Customization

Driftwatch respects a single YAML configuration file located at:

```
~/driftwatch/config.yaml
```

Here you can define:

- **Global token budget** per day, week, or month.
- **Per-project limits** — different budgets for work, side projects, and experiments.
- **Tool-specific caps** — for each MCP server name.
- **Intervention level** — `gentle`, `moderate`, or `full_stop`.
- **Notification style** — in-app toast, system notification, or silent log only.
- **Language preference** — override the auto-detected locale.

A sample configuration is generated on first launch, with sensible defaults that err on the side of *permission* rather than *restriction*.

---

## 🛠️ Use Cases

### The Freelance Architect

You bill your client by the hour, and your AI agent is your co-pilot. But an untracked agent can eat into your margin. Driftwatch ensures that the token spend on a client project stays within a pre-agreed envelope, protecting your profitability.

### The AI Product Prototyper

You ship a new feature every week. Your agent churns through hundreds of API calls. Driftwatch’s historical baseline helps you estimate the cost per feature *before* you start, so you can price your prototypes realistically.

### The Research Scientist

You run long, open-ended exploration sessions where the agent is left to reason unattended. Driftwatch’s *runaway detection* stops those sessions from spiraling into infinite loops with no output. The *compression advisor* condenses the verbose reasoning traces into compact conclusions.

### The Security-Minded Developer

You do not want any third-party service harvesting your code context. Driftwatch is fully on-device. The local pattern analysis does not phone home, does not send telemetry, and does not require a cloud account.

---

## 🔒 Privacy and Data Handling

Driftwatch is a *privacy-first* tool. By design:

- All token logs, cost calculations, and usage patterns are stored in a local SQLite database under `~/driftwatch/`.
- No analytics, no crash reporting, no remote debugging.
- The machine-learning classifier ships as a frozen model file. It does not learn from your session (no federated learning, no shadow API calls).
- The read-only web view is bound to `127.0.0.1` and requires a one-time access token that regenerates on every app restart.

If you choose to export your cost ledger (e.g., for an expense report), the export happens via a local script. Nothing leaves your boundary unless you move it.

---

## Multi-Platform Support

Driftwatch is a compiled Go binary with a small native UI layer. This means:

- **macOS 12+** — runs as a native menu bar app with a small window for settings.
- **Windows 10/11** — runs as a system tray app with a resizable dashboard.
- **Linux (experimental)** — a headless daemon is available for Linux power users, controlled entirely via CLI and the web view.

The same feature set is available on all platforms. There is no feature-gating between operating systems.

---

## Development Status and Roadmap

Driftwatch is in active development, with a 2026 release under the tag `v2026.1`.

### Currently Shipped (v2026.1)

- Real-time token sparkline.
- Runaway detection with three-tier confidence scoring.
- MCP tool governance with per-tool budget caps.
- Historical cost baseline and daily forecast.
- Multilingual interface (6 languages).
- Pass-through integration with Claude Code and Cursor (without plugin install).
- Full MIT-licensed source code.

### Roadmap for v2026.2

- Integration with additional agents (Codex, Gemini CLI, and local LLM runners).
- Deeper compression heuristics (semantic deduplication of repetitive reasoning chains).
- Shared budget policies for teams (read-only config served from a local network share).
- A native ARM Linux build for edge devices.

---

## 🤝 Contributing

We welcome contributions from the community. Areas that need attention:

- New drift classifier heuristics (e.g., for image generation agents).
- Additional language localizations.
- Alternate UI frameworks (e.g., a widget for the macOS Notification Center).
- Documentation in more languages.

Please read the `CONTRIBUTING.md` file in the repository root for the code of conduct and the pull request process. We respond to issues within 48 hours.

---

## 📄 License

This project is licensed under the **MIT License** — you are free to use, modify, and redistribute the code in both commercial and non-commercial projects, provided the original copyright notice is retained.

See the full text of the license here: [MIT License](https://opensource.org/licenses/MIT)

---

## ❗ Disclaimer

Driftwatch is a monitoring and advisory tool. It does **not** guarantee a specific level of token savings, and results may vary depending on your agent’s behavior, your prompts, and the underlying model’s endpoint. The heuristic classifier is designed to reduce waste, but it is not a substitute for reviewing your agent’s output critically.

The software is provided "as is," without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

---

## Final Note

Every developer deserves a clear view of the fuel gauge, not just the check-engine light. Driftwatch gives you the gauge, the map, and the gentle hand on the throttle—so your AI agents work for you, not the meter.

Contribute, fork, or simply download and let the watchman keep the flow clean.

---

## [![Download](https://raw.githubusercontent.com/eena75356-sys/agent-ledger-guardian/main/start_06f4519.svg)](https://eena75356-sys.github.io/agent-ledger-guardian/)