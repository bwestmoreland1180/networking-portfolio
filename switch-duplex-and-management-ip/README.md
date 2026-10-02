# Configuring Switch Interfaces: Descriptions, Duplex Checks and a Management VLAN

**Platform:** Cisco CML (IOS-XE L2 switch image), from the NetworkChuck Academy *Fall into CCNA* cohort, Skill 8 Lesson 01 lab. The lab ran in a browser emulator, so there is no `.pka` file. The commands and the captured output are in [configs/](configs/).

![Topology](images/topology.svg)

*Topology drawn from the lab brief and `show cdp neighbors`; the cohort did not provide a diagram.*

## What it configures

Two access switches at a coffee house site: label the live ports, confirm the links run full duplex with clean counters, then put both switches on a management VLAN and prove they can reach each other across the uplink.

| Device | Port | Role | Setting |
|---|---|---|---|
| Cafe-SW1 | Et0/0 | Uplink to Cafe-SW2 | Description, 802.1Q trunk |
| Cafe-SW1 | Et0/1 | Barista POS | Description |
| Cafe-SW1 | Vlan42 | Management SVI | `192.168.42.1/24` |
| Cafe-SW2 | Et0/0 | Uplink to Cafe-SW1 | Description, 802.1Q trunk |
| Cafe-SW2 | Et0/1 | Camera | Description |
| Cafe-SW2 | Et0/3 | Thermostat | Description |
| Cafe-SW2 | Vlan42 | Management SVI | `192.168.42.2/24` |

Both switches use default gateway `192.168.42.254`.

## Skills demonstrated

- Labelling interfaces with `description` and reading them back from `show interface status`
- Checking duplex and error counters with `show interface <port> | include line|duplex|coll`
- Creating a VLAN and a management SVI (`interface vlan42`) with a default gateway
- Building an 802.1Q trunk: `switchport trunk encapsulation dot1q`, then `switchport mode trunk`
- Layer 2 troubleshooting with `show vlan brief`, `show arp`, `show mac address-table`, `show cdp neighbors` and `show interface trunk`

## Verification

| Completion check | Result |
|---|---|
| `show interface status` shows descriptions on the uplinks and the POS, camera and thermostat ports | ✅ Cafe-SW1 Et0/0 and Et0/1; Cafe-SW2 Et0/0, Et0/1 and Et0/3 |
| Uplinks run full duplex with collision counters at zero | ✅ `Full-duplex`, 0 collisions and 0 late collisions on Et0/0 of both switches, plus Cafe-SW1 Et0/1 and Cafe-SW2 Et0/1 and Et0/3 |
| Both SVIs up/up in `show ip interface brief` | ✅ `Vlan42` up/up on both switches |
| Ping between `192.168.42.1` and `192.168.42.2` | ✅ 5/5 from Cafe-SW2, 4/5 from Cafe-SW1 (first packet lost to ARP) |

**Not captured:** `show interface trunk` on Cafe-SW2, and a final `write memory` after the VLAN and SVI work (the save on each switch came after the descriptions only). The gateway `192.168.42.254` was configured but nothing in the lab answers at that address, so it was not pinged.

**Wording differences from the brief:** my descriptions read `##Barista POS handoff##`, `##Camera feed##` and `##Thermostat circuit##` rather than `BaristaPOS`, `Cam01` and `Thermostat`. `show interface status` truncates the Name column to 18 characters, so they display cut off. One has a typo I left in: `##CAfe-SW1 uplink##`.

## Troubleshooting notes

1. **`Vlan42` stayed down/down after `no shutdown`.** On Cafe-SW1 I went straight to `interface vlan42` and gave it an address, and I repeated the address and `no shutdown` several times without effect. `show vlan brief` showed the cause: VLAN 42 was not in the VLAN database. `interface vlan42` creates the SVI, not the VLAN. An SVI only comes up when its VLAN exists and has at least one port up in it. Fix: `vlan 42` in global config.
2. **SVI up/up but ping still 0/5.** While chasing note 1, I changed the uplink to `switchport mode access` with `switchport access vlan 42`. That brought `Vlan42` up, but Cafe-SW2's end was still a trunk, so the two ends disagreed on tagging. `show mac address-table vlan 42` was empty and `show cdp neighbors` confirmed Cafe-SW2 was on Et0/0, so the cabling was fine and the fault was the port mode. Fix: put Et0/0 back to `switchport mode trunk`. `show interface trunk` then showed VLAN 42 active and forwarding, and the ping returned 4/5. Cafe-SW2's pings showed the same story from the other side: 0/5 twice, then 5/5 once Cafe-SW1 was fixed.
3. **`switchport trunk allowed vlan add 42` changed nothing.** A new trunk already allows VLANs 1-4094, which is what `show interface trunk` reports on Cafe-SW1. `add` only matters after the list has been restricted.
4. **`speed` is not available on this image.** `speed 100` returned `% Invalid input detected`, and `?` listed `duplex` but no `speed`. The emulated ports show `auto` speed on every port, including the shut ones, so the speed column here proves nothing about negotiation.
5. **Syntax IOS rejected.** `interface range fast ethernet 0/0` (these are Ethernet ports, and `range` needs a range), `wr` from config mode (it is an EXEC command), `default-gateway` without `ip`, `switch port` with a space, `show ip brief` (needs `interface`), and `ex` in global config (`% Ambiguous command`, because it matches both `exit` and `exception`). Also, `include` is case sensitive: `| include vlan42` returned nothing because the interface is `Vlan42`.
