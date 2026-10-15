# Port_scanner

A tiny Python port scanner — one of the first things I wrote while
teaching myself networking and cybersecurity.

## What it does

Run it, type in an IP address, and it does a TCP connect scan over 11
common ports with a 1-second timeout, printing the ones that are open.
Sequential, simple, standard library only (`socket`). It's about 25
lines and you can read the whole thing in one sitting, which makes it
a decent learning artifact.

## Run it

```bash
python3 port_scanner
```

**Only scan machines you own or have explicit permission to test.**
Start with `127.0.0.1` — your own machine is the intended target.

## Honest notes

- It only reports *open* ports. Closed and filtered ports are both
  just silence, even though those are different answers in reality.
- It's sequential, so it's slow — one port at a time, up to a second
  each.
- No service names, no banners. You get a port number and whatever you
  already know about what usually lives there.

## This grew up → the QuantumCat SOC Toolkit

This script is one of three I wrote in May 2026 while teaching myself
cybersecurity. I eventually rebuilt all three properly and combined
them into a single desktop app — the **QuantumCat SOC Toolkit** — for
people who want the answers without the terminal time.

What the app version of the scanner adds:

- A **threaded** scan (results stream in live instead of one port per
  second)
- **25 well-known ports with service names**, not just the 11
- **Open / closed / filtered** reported as three distinct states
- Optional **banner grabs** — it reads the banner a service volunteers,
  nothing more aggressive than that
- Friendly input validation instead of tracebacks
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
