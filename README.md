# 🔍 PacketLens

> A real-time CLI network traffic analyzer for Kali Linux — built with Python, Scapy, and Rich.

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat-square&logo=python)
![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-red?style=flat-square&logo=linux)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
![Root](https://img.shields.io/badge/Requires-Root-critical?style=flat-square)

---

## 📡 What is PacketLens?

PacketLens is a live network traffic analyzer that runs directly in your terminal. It captures packets in real time, breaks them down by protocol, identifies the most active IP pairs, and automatically flags suspicious activity like port scans and ARP spoofing.

Built for penetration testers, security researchers, and anyone who wants visibility into their network traffic without the overhead of a GUI tool like Wireshark.

---

## ✨ Features

- 📊 **Live Dashboard** — real-time stats: packet counts, data rates, protocol breakdown
- 🔥 **Top Talkers** — most active IP pairs and ports updated live
- 🚨 **Alert Engine** — detects port scans (15+ ports from one source) and ARP spoofing
- 🔍 **BPF Filters** — standard Wireshark-style filters to focus on specific traffic
- 💾 **Export** — save full capture sessions to JSON or CSV
- ⏱ **Auto-stop** — stop after N packets or N seconds

---

## 🛠 Installation

**1. Clone the repo:**
```bash
git clone https://github.com/trendelinemorina1/packetlens.git
cd packetlens
```

**2. Install dependencies:**
```bash
sudo pip3 install -r requirements.txt --break-system-packages
```

---

## 🚀 Usage

```bash
sudo python3 packetlens.py
```

> ⚠️ Root privileges are required for raw packet sniffing.

---

## ⚙️ Options

| Flag | Description | Example |
|------|-------------|---------|
| `-i` / `--iface` | Network interface to sniff | `-i eth0` |
| `-f` / `--filter` | BPF packet filter | `-f "tcp port 80"` |
| `-c` / `--count` | Stop after N packets | `-c 500` |
| `-t` / `--timeout` | Stop after N seconds | `-t 60` |
| `--export` | Export format: json or csv | `--export json` |
| `--out` | Output filename | `--out capture` |
| `--no-ui` | Disable live dashboard | `--no-ui` |

---

## 💡 Examples

**Monitor HTTP traffic:**
```bash
sudo python3 packetlens.py -i eth0 -f "tcp port 80"
```

**Watch DNS queries for 30 seconds:**
```bash
sudo python3 packetlens.py -f "udp port 53" -t 30
```

**Detect port scans (run nmap in another terminal):**
```bash
sudo python3 packetlens.py -i lo
# in another terminal:
nmap -p 1-50 127.0.0.1
```

**Capture 500 packets and export to JSON:**
```bash
sudo python3 packetlens.py -c 500 --export json --out session
```

**Monitor a specific host:**
```bash
sudo python3 packetlens.py -f "host 192.168.1.50"
```

---

## 🚨 Security Alerts

| Alert | Trigger |
|-------|---------|
| `[PORT SCAN]` | Single IP hits more than 15 unique ports |
| `[ARP SPOOF]` | IP address changes its MAC address in an ARP reply |

---

## 📖 Full Tutorial

👉 [trendelinemorina1.github.io/packetlens/tutorial.html](https://trendelinemorina1.github.io/packetlens/tutorial.html)

---

## ⚖️ Disclaimer

This tool is intended for **authorized use only**. Only use PacketLens on networks and systems you own or have explicit permission to test. Unauthorized network sniffing may be illegal in your jurisdiction.

---

## 🧰 Built With

- [Scapy](https://scapy.net/) — packet capture and analysis
- [Rich](https://github.com/Textualize/rich) — terminal UI and live dashboard

---

*Made for Kali Linux · Python 3.8+*
