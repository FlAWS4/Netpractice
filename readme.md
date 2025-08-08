# 🌐 NetPractice - Complete Network Configuration Guide

<div align="center">

![NetPractice](https://img.shields.io/badge/42-NetPractice-blue?style=for-the-badge&logo=42)
![HTML](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

**Master TCP/IP networking through interactive visual puzzles!**

</div>

---

## 📖 Table of Contents

- [🎯 Project Overview](#-project-overview)
- [🚀 Getting Started](#-getting-started)
- [🧠 Core Concepts](#-core-concepts)
- [🎮 How to Solve Levels](#-how-to-solve-levels)
- [📊 Network Components](#-network-components)
- [🔧 Configuration Patterns](#-configuration-patterns)
- [📝 Level Solutions Guide](#-level-solutions-guide)
- [🏆 Evaluation](#-evaluation)
- [📚 Resources](#-resources)

---

## 🎯 Project Overview

NetPractice is an interactive web-based training tool that teaches TCP/IP addressing through 10 progressively challenging network configuration scenarios.

### 🎪 The Analogy
Think of networking like a **postal system**:
- 🏠 **Houses** = Computers (Hosts)
- 🛣️ **Streets** = Networks  
- 🏢 **Post Offices** = Routers
- 📬 **Addresses** = IP Addresses
- 📮 **Mail Routes** = Routing Tables

---

## 🚀 Getting Started

### Installation
```bash
# Clone or download the NetPractice files
# Extract if compressed
tar -xf netpractice.tar

# Open the web interface
open index.html
# OR
firefox index.html
```

### Quick Start
1. 📝 Enter your login (or leave empty for practice mode)
2. 🎮 Click "Start!" 
3. 🧩 Solve levels 1-10
4. 💾 Export configs with "Get my config"
5. 📁 Submit all 10 JSON files to your repository

---

## 🧠 Core Concepts

### 🏠 IP Addresses = House Addresses

```
192.168.1.5
^^^^^^^^^ ^
Network   Host
(Street)  (House #)
```

**Visual Breakdown:**
```
┌─────────────┬─────┐
│ Network     │Host │
│ 192.168.1   │  5  │
│ (Street)    │(#)  │
└─────────────┴─────┘
```

### 🎭 Subnet Masks = Address Rules

| Mask | CIDR | Meaning | Example |
|------|------|---------|---------|
| `255.255.255.0` | `/24` | Last number = house | `192.168.1.X` |
| `255.255.0.0` | `/16` | Last 2 numbers = house | `192.168.X.Y` |
| `255.0.0.0` | `/8` | Last 3 numbers = house | `192.X.Y.Z` |

### 🛣️ Network Communication Rules

#### ✅ Same Network (Direct Communication)
```
🏠 192.168.1.5 ←────→ 🏠 192.168.1.10
   Same street = Can talk directly!
```

#### ❌ Different Networks (Need Router)
```
🏠 192.168.1.5 ──→ 🏢 Router ──→ 🏠 10.0.0.5
   Different streets = Need post office!
```

---

## 🎮 How to Solve Levels

### 🔍 Step-by-Step Approach

#### 1. **Analyze the Topology**
```
   🏠 Host A
    │
   ┌┴┐
   │R│ Router
   └┬┘
    │
   🏠 Host B
```

#### 2. **Identify Editable Fields**
- ⬜ **White fields** = You can edit
- ⬛ **Gray fields** = Fixed, can't change

#### 3. **Apply The Golden Rule**
> **Devices connected by a wire MUST be in the same network!**

#### 4. **Check Your Work**
- Click "Check again"
- Read error messages in logs
- Adjust and retry

---

## 📊 Network Components

### 🏠 Hosts (Computers)
```
┌─────────────────┐
│   Host A        │
│ IP: 192.168.1.5 │
│ Mask: /24       │
└─────────────────┘
```

### 🏢 Routers (Multi-Interface)
```
     Interface A1          Interface B1
   192.168.1.1 ├─────────┤ 10.0.0.1
               │ Router  │
               └─────────┘
     Network A              Network B
```

**Router Rules:**
- Each interface = Different network
- Router forwards between networks
- Each interface needs IP in its connected network

### ⬜ Switches (Same Network)
```
     🏠 Host A (192.168.1.5)
        │
    ┌───┴───┐
    │Switch │
    └───┬───┘
        │
     🏠 Host B (192.168.1.10)
```

All devices connected to switch = Same network

---

## 🔧 Configuration Patterns

### Pattern 1: **Direct Connection**
```
🏠 ─────── 🏠
A          B

Solution: Same network for both
A: 192.168.1.5/24
B: 192.168.1.10/24
```

### Pattern 2: **Switch Connection**
```
🏠 ─┐
A   │ ┌─────┐ ┌─ 🏠
    └─┤  S  ├─┘  B
      └─────┘

Solution: All same network
A: 192.168.1.5/24
B: 192.168.1.10/24
```

### Pattern 3: **Router Between Networks**
```
🏠 ──── 🏢 ──── 🏠
A      R       B

Solution: Two different networks
A: 192.168.1.5/24  │  R-A1: 192.168.1.1/24
                   │  R-B1: 10.0.0.1/24
B: 10.0.0.5/24     │
```

### Pattern 4: **Complex Multi-Router**
```
🏠 ── 🏢 ── 🏢 ── 🏠
A    R1   R2    B

Solution: Three networks
A: 192.168.1.5/24    R1-A1: 192.168.1.1/24
                     R1-R2: 192.168.2.1/24
                     R2-R1: 192.168.2.2/24  
B: 10.0.0.5/24       R2-B1: 10.0.0.1/24
```

---

## 📝 Level Solutions Guide

### 🎯 Level 1: Basic Host-to-Host
**Goal:** Direct communication between pairs

```
🏠 A ──── 🏠 B    🏠 C ──── 🏠 D

Strategy:
- Make A & B same network
- Make C & D same network
```

### 🎯 Level 2: Switch Introduction
**Goal:** Multiple hosts through switch

```
🏠 ─┐
    ├── ⬜ Switch
🏠 ─┘

Strategy: All hosts same network
```

### 🎯 Level 3: First Router
**Goal:** Router connecting two networks

```
🏠 ──── 🏢 ──── 🏠

Strategy:
- Left side: Network A
- Right side: Network B  
- Router: One interface per network
```

### 🎯 Levels 4-10: Progressive Complexity
- Multiple routers
- Routing tables
- Complex topologies
- Internet connections

---

## 🧮 Quick Calculation Reference

### Network Calculation
```
IP: 192.168.1.100
Mask: 255.255.255.0 (/24)

Network Address: 192.168.1.0
Broadcast: 192.168.1.255
Valid Host IPs: 192.168.1.1 - 192.168.1.254
```

### Subnet Examples
| Network | First Host | Last Host | Broadcast |
|---------|------------|-----------|-----------|
| `192.168.1.0/24` | `192.168.1.1` | `192.168.1.254` | `192.168.1.255` |
| `10.0.0.0/16` | `10.0.0.1` | `10.0.255.254` | `10.0.255.255` |
| `172.16.0.0/12` | `172.16.0.1` | `172.31.255.254` | `172.31.255.255` |

---

## 🎯 Universal Problem-Solving Formula

### The 4-Step Method

#### 1. 🔍 **IDENTIFY**
```bash
# What's connected to what?
Host A ──── Router ──── Host B
```

#### 2. 🧮 **CALCULATE**
```bash
# What networks exist?
Left side:  192.168.1.0/24
Right side: 10.0.0.0/24
```

#### 3. ✏️ **CONFIGURE**
```bash
# Assign IPs correctly
Host A:      192.168.1.10/24
Router-A1:   192.168.1.1/24
Router-B1:   10.0.0.1/24
Host B:      10.0.0.10/24
```

#### 4. 🗺️ **ROUTE**
```bash
# Set routing tables
Host A default gateway: 192.168.1.1
Host B default gateway: 10.0.0.1
```

---

## 🏆 Evaluation

### Defense Requirements
- ⏱️ **15 minutes** to solve **3 random levels** (6-10)
- 🚫 No external tools (calculator like `bc` allowed)
- 💡 Explain your solution process

### Submission Checklist
- [ ] 10 JSON config files (level01.json - level10.json)
- [ ] Files at repository root
- [ ] Used your login in the interface
- [ ] All levels successfully completed

---

## 🧠 Mental Models

### 🏠 The House Analogy
```
IP Address = House Address
Network = Street/Neighborhood  
Subnet Mask = Postal Zone Rules
Router = Post Office
Default Gateway = Local Post Office Address
```

### 🗺️ The Map Analogy
```
Routing Table = GPS Navigation
Destination = Where you want to go
Next Hop = Next turn on the route
Default Route (0.0.0.0/0) = "GPS: Go to main road for everything else"
```

---

## 📚 Resources

### Key Concepts to Master
- **Subnetting** - Dividing networks
- **CIDR Notation** - Network size representation  
- **Default Gateway** - Local router address
- **Routing Tables** - Path finding rules
- **Network vs Broadcast** - Address boundaries

### Common Pitfalls
- ❌ Different networks on same wire
- ❌ Wrong subnet masks
- ❌ Missing default routes
- ❌ Duplicate IP addresses
- ❌ Router interfaces in wrong networks

### Pro Tips
- 🎯 Start with fixed (gray) values as anchors
- 🔧 Use simple networks: `192.168.1.0/24`, `10.0.0.0/24`
- 🗺️ Router IPs usually end in `.1` (like `192.168.1.1`)
- 🎪 Default route destination is always `0.0.0.0/0`
- 📝 Work one connection at a time

---

<div align="center">

**Happy Networking!** 🌐✨

*Master the art of digital communication, one subnet at