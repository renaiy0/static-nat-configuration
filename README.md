# static-nat-configuration
# 🌐 NAT Configuration Project

<div align="center">
  <img src="https://img.shields.io/badge/Cisco-Packet%20Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white" alt="Cisco Packet Tracer"/>
  <img src="https://img.shields.io/badge/Status-In%20Progress-yellow?style=for-the-badge" alt="Status"/>
  <img src="https://img.shields.io/badge/Network-NAT-blue?style=for-the-badge" alt="NAT"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License"/>
</div>

<br/>

<p align="center">
  <em>A simple Network Address Translation (NAT) implementation using Cisco Packet Tracer, demonstrating how private networks can access public networks while maintaining security isolation.</em>
</p>

---

## 📋 Overview

<table>
<tr>
<td width="60%">

This project demonstrates a **basic NAT setup** where:

- 🔒 Private network devices (PC1 & PC2) with IPs `10.10.10.1` and `10.10.10.2`
- 🌐 Can access public network (`30.30.30.1`) through NAT
- 🚫 Cannot directly ping each other's private IPs from outside
- ⚙️ Router configured with static IP addressing

</td>
<td width="40%">

```
┌─────────────┐
│ Private Net │
│ 10.10.10.0  │
└──────┬──────┘
       │
   [Router NAT]
       │
┌──────┴──────┐
│ Public Net  │
│ 30.30.30.0  │
└─────────────┘
```

</td>
</tr>
</table>

---

## 🎯 Project Goals

<div align="center">

| Goal | Description |
|:----:|:------------|
| 🎓 | Demonstrate basic NAT functionality |
| 🔐 | Show network isolation between private and public networks |
| 💻 | Practice static IP configuration on Cisco routers |
| 🛡️ | Understand how NAT provides security through address translation |

</div>

---

## 📁 Files in this Repository

<details open>
<summary><b>Click to expand file details</b></summary>
<br/>

| File | Preview | Description |
|------|:-------:|-------------|
| `cisco.pkt` | 📦 | Main Cisco Packet Tracer topology file |
| `staticonfig.png` | <img src="staticonfig.png" width="100"/> | Static IP configuration on router |
| `PROOFthatPC1and2cantpingingprivateIP.png` | <img src="PROOFthatPC1and2cantpingingprivateIP.png" width="100"/> | Proof that NAT is working - PC1 and PC2 cannot ping private IPs but can reach public IP |
| `progress1.png` | <img src="progress1.png" width="100"/> | CLI configuration progress screenshot |

</details>

---

## 🔧 Network Topology

<div align="center">

```mermaid
graph LR
    A[PC1<br/>10.10.10.1] -->|Private| R[Router<br/>NAT Gateway]
    B[PC2<br/>10.10.10.2] -->|Private| R
    R -->|Public| C[Public Host<br/>30.30.30.1]
    
    style A fill:#e1f5ff,stroke:#01579b,stroke-width:2px
    style B fill:#e1f5ff,stroke:#01579b,stroke-width:2px
    style R fill:#fff3e0,stroke:#e65100,stroke-width:3px
    style C fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px
```

</div>

---

## 📸 Complete Configuration Process

### 1️⃣ Static IP Configuration
<div align="center">
  <img src="staticonfig.png" alt="Static Config" width="800px"/>
  <p><em><b>Router static IP configuration</b> - Setting up interface IP addresses for NAT gateway</em></p>
</div>

**What's happening here:**
- Configuring router interfaces with appropriate IP addresses
- Setting up the gateway between private (10.10.10.0/24) and public (30.30.30.0/24) networks
- Enabling interfaces and verifying connectivity

<br/>

### 2️⃣ CLI Configuration Progress
<div align="center">
  <img src="progress1.png" alt="CLI Progress" width="800px"/>
  <p><em><b>Active CLI configuration</b> - Configuring NAT rules and routing via command line interface</em></p>
</div>

**Configuration steps being performed:**
```cisco
Router(config)# interface g0/0
Router(config-if)# ip address 10.10.10.254 255.255.255.0
Router(config-if)# ip nat inside
Router(config-if)# no shutdown

Router(config)# interface g0/1
Router(config-if)# ip address 30.30.30.254 255.255.255.0
Router(config-if)# ip nat outside
Router(config-if)# no shutdown

Router(config)# ip nat inside source list 1 interface g0/1 overload
Router(config)# access-list 1 permit 10.10.10.0 0.0.0.255
```

<br/>

### 3️⃣ NAT Verification & Testing
<div align="center">
  <img src="PROOFthatPC1and2cantpingingprivateIP.png" alt="NAT Proof" width="800px"/>
  <p><em><b>Proof of NAT functionality</b> - Testing network isolation and public access</em></p>
</div>

<br/>

<table align="center">
<tr>
<td align="center" width="50%">

### ❌ Private Network Isolation

**Test: Ping Private IPs**
- PC1 → PC2 (10.10.10.2): ❌ **UNREACHABLE**
- PC2 → PC1 (10.10.10.1): ❌ **UNREACHABLE**

Shows "Destination host unreachable"

✅ **This is correct behavior!**

</td>
<td align="center" width="50%">

### ✅ Public Network Access

**Test: Ping Public IP**
- PC1 → Public (30.30.30.1): ✅ **SUCCESS**
- PC2 → Public (30.30.30.1): ✅ **SUCCESS**

NAT translation working correctly! 🎉

✅ **Private IPs are translated!**

</td>
</tr>
</table>

> **💡 What does this prove?**
> - Private addresses (10.10.10.x) are hidden from the public network
> - NAT router successfully translates private IPs to public IP (30.30.30.254)
> - Network isolation is maintained - devices cannot directly access each other's private addresses
> - Security through address translation is working as intended

---

## 🚀 Getting Started

### Prerequisites

<div align="center">

![Cisco](https://img.shields.io/badge/Cisco_Packet_Tracer-v7.0+-1BA0D7?style=flat-square&logo=cisco)
![Networking](https://img.shields.io/badge/Basic_Networking-Knowledge-orange?style=flat-square)
![IP](https://img.shields.io/badge/IP_Addressing-Required-red?style=flat-square)

</div>

### Installation Steps

```bash
# 1. Clone this repository
git clone https://github.com/renaiyd/nat-config.git

# 2. Navigate to the project directory
cd nat-config

# 3. Open cisco.pkt in Cisco Packet Tracer
```

---

## 📝 Step-by-Step Configuration Guide

<div align="center">

```
Step 1: Static IP      Step 2: NAT Rules      Step 3: Testing      Step 4: Verification
    ⬇️                      ⬇️                     ⬇️                    ⬇️
Configure router    →  Define inside/      →  Ping tests       →  Analyze results
interfaces             outside interfaces      from PCs              & confirm NAT
```

</div>

### Detailed Commands

<table>
<tr>
<td>

**Step 1: Configure Inside Interface**
```cisco
Router(config)# interface g0/0
Router(config-if)# ip address 10.10.10.254 255.255.255.0
Router(config-if)# ip nat inside
Router(config-if)# no shutdown
Router(config-if)# exit
```

</td>
<td>

**Step 2: Configure Outside Interface**
```cisco
Router(config)# interface g0/1
Router(config-if)# ip address 30.30.30.254 255.255.255.0
Router(config-if)# ip nat outside
Router(config-if)# no shutdown
Router(config-if)# exit
```

</td>
</tr>
<tr>
<td>

**Step 3: Configure NAT Overload (PAT)**
```cisco
Router(config)# ip nat inside source list 1 interface g0/1 overload
Router(config)# access-list 1 permit 10.10.10.0 0.0.0.255
```

</td>
<td>

**Step 4: Verify Configuration**
```cisco
Router# show ip nat translations
Router# show ip nat statistics
Router# show ip interface brief
```

</td>
</tr>
</table>

---

## 🔍 Understanding the Results

### What Each Screenshot Shows:

#### 📊 Static Config (`staticconfig.png`)
- Initial router configuration
- IP address assignment
- Interface status

#### ⚙️ Progress (`progress1.png`)
- Live CLI configuration
- Commands being entered
- Real-time setup process

#### ✅ Proof (`PROOFthatPC1and2cantpingingprivateIP.png`)
- Ping test results
- Network isolation verification
- Public network accessibility confirmation

---

## 🎓 Learning Outcomes

<div align="center">

| 📚 Topic | 🎯 Outcome | 🖼️ Shown In |
|:---------|:-----------|:------------|
| **NAT Translation** | Understand how NAT translates private IPs to public IPs | All screenshots |
| **Network Security** | Learn why NAT provides security through isolation | `PROOFthatPC1and2...png` |
| **Cisco IOS** | Practice configuring NAT via CLI | `progress1.png` |
| **Static IP** | Configure router interfaces properly | `staticconfig.png` |

</div>

---

## 🛠️ Troubleshooting

<details>
<summary><b>🔴 Common Issues & Solutions</b></summary>

### Issue 1: Cannot ping public IP
**Solution:** Check if NAT is configured correctly
```cisco
Router# show ip nat translations
Router# show running-config | include nat
```

### Issue 2: Private IPs can ping each other
**Solution:** Verify NAT inside/outside interfaces
```cisco
Router# show ip interface brief
```

### Issue 3: Router interfaces are down
**Solution:** Enable interfaces
```cisco
Router(config-if)# no shutdown
```

</details>

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

<div align="center">

[![Fork](https://img.shields.io/github/forks/renaiyd/nat-config?style=social)](https://github.com/renaiyd/nat-config/fork)
[![Star](https://img.shields.io/github/stars/renaiyd/nat-config?style=social)](https://github.com/renaiyd/nat-config)
[![Issues](https://img.shields.io/github/issues/renaiyd/nat-config)](https://github.com/renaiyd/nat-config/issues)

</div>

---

## 📞 Connect With Me

<div align="center">

[![GitHub](https://img.shields.io/badge/GitHub-renaiyd-181717?style=for-the-badge&logo=github)](https://github.com/renaiyd)
[![Email](https://img.shields.io/badge/Email-Contact-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:your-email@example.com)

</div>

---

## 📄 License

<div align="center">

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

Copyright © 2024 [@renaiyd](https://github.com/renaiyd)

</div>

---

<div align="center">

### ⭐ Star this repo if you find it helpful!

**Made with ❤️ and lots of ☕**

<img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png" width="100%"/>

</div>
