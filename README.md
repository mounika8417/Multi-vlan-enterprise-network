# Multi-VLAN Small Enterprise Network with Inter-VLAN Routing

A network design and simulation project built in **Cisco Packet Tracer**, demonstrating VLAN segmentation and inter-VLAN routing using the **Router-on-a-Stick** method.

---

## 📌 Overview

This project simulates a small enterprise network divided into four departments using VLANs. A single router interface with 802.1Q subinterfaces handles all inter-department routing, connected to a core switch that fans out to two access-layer switches.

---

## 🗺️ Topology

```
                         [ R1 ]
                           |
                      G0/0 (Trunk)
                           |
                         [SW1]          ← Core Switch
                        /     \
                  Trunk         Trunk
                 /                 \
            [SW2]                [SW3]
        Access Switch          Access Switch
       /            \          /           \
  VLAN 20        VLAN 30   VLAN 40       VLAN 10
   (HR)           (IT)    (Guest)        (Mgmt)
```

---

## 📋 VLAN Design

| VLAN | Name       | Subnet           | Gateway        |
|------|------------|------------------|----------------|
| 10   | Management | 192.168.10.0/24  | 192.168.10.1   |
| 20   | HR         | 192.168.20.0/24  | 192.168.20.1   |
| 30   | IT         | 192.168.30.0/24  | 192.168.30.1   |
| 40   | Guest      | 192.168.40.0/24  | 192.168.40.1   |

---

## 🔧 Technologies & Concepts Used

- **VLANs** — Layer 2 network segmentation by department
- **802.1Q Trunking** — Carrying multiple VLANs over a single link
- **Router-on-a-Stick** — Inter-VLAN routing via subinterfaces on one physical interface
- **Access & Trunk Ports** — Proper port mode configuration on all switches
- **SVI (Switched Virtual Interface)** — Management IP addresses on each switch
- **PortFast** — Spanning-tree optimization on access ports

---

## 🖥️ Device Summary

| Device | Role              | Key Interfaces                          |
|--------|-------------------|-----------------------------------------|
| R1     | Router (RotS)     | G0/0.10, G0/0.20, G0/0.30, G0/0.40     |
| SW1    | Core Switch       | Fa0/1 → R1, Fa0/2 → SW2, Fa0/3 → SW3  |
| SW2    | Access (HR / IT)  | Fa0/2–6 = VLAN 20, Fa0/7–12 = VLAN 30  |
| SW3    | Access (Guest / Mgmt) | Fa0/2–6 = VLAN 40, Fa0/7–12 = VLAN 10 |

---

## ✅ What Was Verified

- All subinterfaces on R1 are `up/up`
- `show vlan brief` shows all 4 VLANs active on respective switches
- `show interfaces trunk` confirms trunk links carry correct VLANs
- PCs within the same VLAN can communicate
- PCs across VLANs can communicate through R1 (inter-VLAN routing works)
- Management VLAN accessible on all switches via SVI

---

## 📁 Repository Contents

```
├── README.md
├── configs/
│   ├── R1-router.txt
│   ├── SW1-core-switch.txt
│   ├── SW2-access-switch.txt
│   └── SW3-access-switch.txt
└── topology/
    └── multi-vlan-network.pkt      ← Packet Tracer file
```

---

## 🚀 How to Run

1. Open `topology/multi-vlan-network.pkt` in Cisco Packet Tracer
2. Configs are pre-applied — use the CLI to explore each device
3. Test connectivity using the **Packet Tracer ping tool** or PC command prompt

---

## 📚 Skills Demonstrated

`Networking` `VLANs` `Cisco IOS` `Packet Tracer` `Inter-VLAN Routing` `Trunking` `Router-on-a-Stick` `Layer 2 Switching`
