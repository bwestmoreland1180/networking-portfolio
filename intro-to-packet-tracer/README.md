# Intro to Packet Tracer (Site-to-Site Topology Walkthrough)

**Tool:** Cisco Packet Tracer

**Goal:** First hands-on orientation in Packet Tracer — opening and reading a pre-built, two-site network to get familiar with the device icons, link types, and overall layout before building anything from scratch.

## The topology

Two branch sites connected across a simulated WAN:

- **New York Branch** — PC1 and PC02 → Switch1 → Router1 → ASA1 (firewall) → WAN link out to **"The Internet"** cloud. A standalone laptop (Laptop0) also connects directly into the Internet cloud.
- **Tokyo Branch** — Server1 and Server2 → Switch2 → ASA2 (firewall) → Router2 → WAN link into the same Internet cloud.
- The Internet cloud is the shared WAN link joining the New York and Tokyo edge routers.

## Takeaway

An orientation exercise: reading a multi-site topology (LAN switch → router → firewall → WAN cloud, repeated per site) and identifying device roles before doing any configuration work.

## Files

```
.
└── Packet Tracer Intro - Google Docs.pdf   # topology screenshot + notes (screenshot embedded in the PDF)
```
