# Networking Portfolio

Hands-on networking labs I've built while working toward a career in network engineering. Each folder contains the lab file (or saved device configs for emulator labs), a topology screenshot, and a short write-up explaining what it is and what I learned building it.

**Currently working toward:** Cisco CCNA, with a focus on hands-on labs and network automation.

## Labs

- **[Exploring Switch CAM Tables](switch-cam-table-learning/)** — Generated ARP and ICMP traffic between two Linux hosts and watched an IOS-XE switch (CML) learn their MACs on the right ports, cross-checking each CAM entry against the host's `ifconfig`. Then flushed the dynamic entries with `clear mac address-table dynamic` and let live traffic rebuild them. Includes notes on instant re-learning and why the switch CAM table and the host ARP cache are separate.
- **[Switch Interfaces and the CAM Table](switch-interfaces-cam-table/)** — Read-only audit of an aggregation switch on Cisco IOS-XE (CML): port roles from descriptions, duplex/speed and error-counter health checks, and MAC address table lookups to find each device's port and spot the trunk uplink to the core. Verified against every completion check with captured show output. Includes a troubleshooting note on NX-OS vs IOS command syntax.
- **[District Shop Bring-Up](district-shop-bring-up/)** — Took two access switches and an edge router from factory state to a hardened, manageable baseline on Cisco IOS-XE (CML): hostnames, MOTD banner, enable secret, encrypted console/VTY passwords with SSH-only VTY, port descriptions, management SVIs and default gateway. Verified with saved configs, a reload test, and pings to the gateway. Includes a troubleshooting write-up on catching a pasted `copy` command that never saved the config.
- **[Wireless Router and Client](wireless-router-and-client/)** — Built and secured a SOHO home network in Cisco Packet Tracer: cable-modem internet, DHCP addressing, a WPA2-secured wireless LAN, and both wired and wireless clients reaching the internet. Graded 100%. Includes a troubleshooting write-up on diagnosing and recovering from an admin-credential lockout.
- **[Connected Devices](connecting-devices/)** — Connecting and configuring end devices in Cisco Packet Tracer and verifying end-to-end connectivity across the topology.
- **[Intro to Packet Tracer](intro-to-packet-tracer/)** — First lab: learning the Packet Tracer environment and building a basic working topology from the ground up.

## Tools used
Cisco Packet Tracer · Cisco CML (IOS-XE) · GNS3 · Wireshark · VirtualBox · Git

*(more labs added as I complete them)*

---
*Built as a self-directed learning portfolio. Every lab here is something I can walk through and explain.*
