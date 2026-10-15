# Port_scanner

A tiny Python port scanner — one of the first things I wrote while
teaching myself networking and cybersecurity.

## What it does

Run it, type in an IP address or hostname, and it does a TCP connect
scan over 25 well-known ports, printing each port's service name and
whether it's **open**, **closed**, or **filtered**. Standard library
only — no dependencies. You can still read the whole thing in one
sitting, which makes it a decent learning artifact.

```bash
python3 port_scanner            # it asks for a target
python3 port_scanner 127.0.0.1  # or give it one directly
python3 port_scanner 127.0.0.1 --banner   # also grab service banners
```

**Only scan machines you own or have explicit permission to test.**
Start with `127.0.0.1` — your own machine is the intended target.

## Updated

The original (May 2026) was about 25 lines: sequential, 11 ports,
open ports only. It worked, but it was slow and it only told a third of
the story. This version keeps the same simple idea and fixes that:

- **Threaded.** Up to 32 workers instead of one port at a time — a
  firewalled host no longer costs a full second per port, serially.
- **25 well-known ports with service names**, not just the original 11.
- **Open / closed / filtered as three distinct states.** The original
  only reported *open*; closed and filtered were both just silence,
  even though those are different answers in reality.
- **Optional passive banner grab** (`--banner`) — it reads the banner a
  service volunteers, nothing more aggressive than that.
- **Friendly input validation** instead of tracebacks: empty targets,
  unresolvable hostnames, and CIDR ranges get a plain-English
  explanation of what to enter instead.

## This grew up → the QuantumCat SOC Toolkit

This script is one of three I wrote in May 2026 while teaching myself
cybersecurity. I eventually rebuilt all three properly and combined
them into a single desktop app — the **QuantumCat SOC Toolkit** — for
people who want the answers without the terminal time.

What the app version of the scanner adds:

- A GUI tab where results stream into a table live as the scan runs
- The other two tools built in: a live connection monitor with
  LOCAL/EXTERNAL tagging and top talkers, and a one-click snapshot
  triage report
- An **AI Analyst** tab that reads the findings and explains them in
  plain English — VERDICT → what looks normal → what deserves a
  second look → suggested next steps — running 100% locally via
  Ollama, with a built-in rule engine if you don't have Ollama
- Real installers: a Windows `.msi` that gives you a desktop shortcut
  and a Start Menu entry, plus a Linux `.deb` and a portable
  `.tar.gz`. Click the cat, the app opens — no terminal

It's $12, one-time. And it's honest about what it is: a
beginner-friendly scanning and triage tool, not an nmap or Wireshark
replacement. 100% local, no accounts, no telemetry. The full Python
source is included in the download.

→ https://quantumcatsoc.gumroad.com/l/quantumcat-soc-toolkit

The other two originals:
[Network-Monitor](https://github.com/Quantumcat-py/Network-Monitor) ·
[Snapshot-Report](https://github.com/Quantumcat-py/Snapshot-Report)
