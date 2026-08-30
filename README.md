Day 01 — Packet Tracer Introduction

Tool: Cisco Packet Tracer Goal: Get comfortable navigating Packet Tracer and reading an enterprise-style topology.

The topology

A two-site enterprise network with a New York Branch and a Tokyo Branch connected across a simulated WAN ("The Internet"):

Each branch has a 2960 switch, a 2911 router, and a 5505 ASA firewall at its edge.
The New York side has two PCs; the Tokyo side has two servers.
A remote laptop connects in over the WAN, and an attacker node sits off the internet cloud (a reminder of why the edge firewalls are there).
What I did / learned
Navigated the Packet Tracer workspace — selecting devices, panning the canvas, and opening device configuration windows.
Identified each device type and its role in a branch-to-branch design (access switch → router → edge firewall → WAN).
Read interface link states: links show green when both ends are up, and red when an interface is still administratively down (the default for router/ASA interfaces until configured). This is an intro/exploration file, so unconfigured links are expected.
Started practicing an OSI-layer read: checking whether a link is up at Layer 1 (interface on?) before looking higher.
Takeaway

This was about orientation, not configuration — learning the tool and recognizing the shape of a real enterprise network before building one from scratch in later labs. 
# networking-portfolio
