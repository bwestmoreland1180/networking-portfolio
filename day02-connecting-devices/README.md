Day 02 — Connecting Devices (Cabling & Media Selection)

Tool: Cisco Packet Tracer Goal: Connect a multi-site topology using the correct cable type and medium for each link — choosing between copper straight-through, copper crossover, and fiber (multimode vs. single-mode) based on the devices and the distance involved. Auto MDI-X is assumed disabled, so cable type must be chosen manually.

The topology

Four routers (R1–R4) form the backbone, each branching down into a tree of switches, PCs, and a server:

R1–R2 (50 m), R1–R3 (3 km), R3–R4 (250 m) — router-to-router backbone links.
R2 and R4 each connect down to two access switches, which connect to lower switches, which connect to end devices (PCs / server).
Cabling logic

Two rules drove every cable choice:

Cable type (Auto MDI-X disabled):

Same device types (switch↔switch, router↔router) → crossover
Different device types (router↔switch, switch↔PC, switch↔server) → straight-through

Medium (driven by distance):

Copper Ethernet is limited to 100 m → fine for short LAN links
Beyond 100 m requires fiber
Multimode fiber for shorter/mid-range runs; single-mode for long distance
Cabling decision table
Link	Distance	Devices	Cable chosen	Why
R1–R2	50 m	router↔router	Copper crossover	Same device type; within 100 m
R1–R3	3 km	router↔router	Single-mode fiber	Far beyond copper limit; long-haul distance
R3–R4	250 m	router↔router	Multimode fiber	Beyond 100 m copper limit; mid-range distance
R2–SW1 / R2–SW2	LAN	router↔switch	Copper straight-through	Different device types
R4–SW5 / R4–SW6	LAN	router↔switch	Copper straight-through	Different device types
SW1–SW2 / SW5–SW6	LAN	switch↔switch	Copper crossover	Same device type
SW1–SW3 / SW2–SW4 / SW5–SW7 / SW6–SW8	LAN	switch↔switch	Copper crossover	Same device type
SW3–PC1 / SW4–PC2 / SW7–PC3	LAN	switch↔PC	Copper straight-through	Different device types
SW8–SRV1	LAN	switch↔server	Copper straight-through	Different device types
Troubleshooting note

Initially miscabled the router-to-switch links (R2–SW1, R2–SW2) with crossover cables. Diagnosed the error by noticing the switch-side ports stayed down (red) — a link that's cabled with the wrong type won't come up even on the switch end. Corrected to straight-through cables (router and switch are different device types), which brought the switch-side ports up (green).

Expected link states at this stage
Switch-to-switch, switch-to-PC/server links: up (green) on both ends — switch/PC ports are enabled by default.
Router-to-switch links: switch end up (green), router end down (red) — router interfaces are administratively shut down by default.
Router-to-router links: down (red) on both ends — same reason.

The remaining red ports are expected and correct for a physical-layer lab; they come up in later labs once interfaces are enabled (no shutdown) and addressed via the CLI.

Takeaway

This lab is about Layer 1 decision-making: matching cable type to device pairing and medium to distance. The key skill demonstrated is not just connecting devices, but diagnosing and correcting a miscabled link by reading port status — a core troubleshooting habit.
