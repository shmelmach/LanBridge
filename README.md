# LanBridge 2.0

> **Modern, self-hosted Windows Virtual LAN application (Radmin VPN alternative) with a sleek dark GUI, powered by AmneziaWG 3.1 and Xray VLESS + REALITY.**

---

### ⚠️ IMPORTANT NETWORK REQUIREMENT:
> ## **THE HOST MACHINE MUST HAVE A PUBLIC ("WHITE") IPv4 ADDRESS OR CONFIGURED PORT FORWARDING ON THE ROUTER.**
>
> **LANBRIDGE 2.0 RUNS DIRECTLY ON THE OWNER'S COMPUTER WITHOUT EXTERNAL CLOUD SERVERS, THIRD-PARTY ACCOUNTS, OR CENTRALIZED RELAYS.**
>
> - **FOR THE HOST (SERVER):** A PUBLIC IPv4 ADDRESS (STATIC OR DYNAMIC) OR ACCESS TO YOUR ROUTER'S PORT FORWARDING SETTINGS IS **STRICTLY REQUIRED**.
> - **FOR CONNECTING FRIENDS (CLIENTS):** NO PUBLIC IP OR ROUTER SETUP IS NEEDED. CLIENTS ONLY INITIATE AN OUTBOUND CONNECTION TO THE HOST'S IP, PORT, AND PASSWORD.

---

## 🌟 Overview

**LanBridge 2.0** is a full-featured desktop virtual local network tool designed for Windows 10 and Windows 11 x64. It allows gamers and teams to link remote computers into a single virtual subnet (`10.77.0.0/24`), providing zero-configuration multiplayer gameplay for games like **Minecraft Java Edition** as if all players were plugged into the same local switch.

Unlike legacy software, LanBridge 2.0 introduces modern censorship-resistant transport layers, native hardware packet routing, and a clean, responsive dark-mode user interface.

---

## 🚀 Key Features

- **Modern Dark UI (WPF / MVVM):** Styled with a clean, low-contrast dark palette, real-time participant cards, ping meters, and one-click controls.
- **Dual Anti-DPI VPN Transports:**
  - **AmneziaWG 3.1:** Hardened WireGuard implementation featuring junk packet obfuscation (`Jc`, `Jmin`, `Jmax`, `S1`, `S2`, `H1`–`H4`) to bypass UDP throttling and Deep Packet Inspection.
  - **Xray VLESS + REALITY:** Masks VPN traffic as legitimate TLS 1.3 web connections (masquerading as `www.microsoft.com`). Features an integrated **Layer-3 Virtual Switch** (`VirtualL3PacketRouter`) to route raw IPv4, TCP, UDP, and ICMP Ping packets seamlessly between clients.
- **Automated Minecraft Java LAN Discovery:**
  - **Multicast Relay:** Intercepts Minecraft's native UDP broadcast (`224.0.2.60:4445`) and replicates it across the virtual subnet. Remote friends see the open world directly in their **Multiplayer** menu under *"LAN World"*.
  - **Direct Connect Helper:** Auto-detects the dynamic port opened by Minecraft and displays a one-click copyable address (e.g. `10.77.0.1:51234`).
- **Dynamic Virtual IP Management (IPAM):**
  - Host is permanently assigned `10.77.0.1`.
  - Up to 10 simultaneous remote peers receive conflict-free addresses from `10.77.0.2` to `10.77.0.10`.
- **Hardened Security & Privacy:**
  - **Windows DPAPI:** Saved profile passwords are encrypted at rest using the Windows Data Protection API (`CurrentUser`).
  - **PBKDF2-HMAC-SHA256:** Network passwords are authenticated with 100,000 hash iterations and unique 16-byte cryptographic salts.
  - **TLS 1.3 Control Plane:** Handshakes, participant updates, and heartbeat probes travel through an encrypted control channel on TCP port `51820`. Private VPN keys are never transmitted to peers.
  - **Physical LAN Isolation:** Virtual traffic is completely isolated from the host's private home network (`192.168.x.x`).
- **Profile Manager:** Store own networks and saved connections in a local SQLite database with AES-256-GCM export/import options.

---

## 🛠️ Required Ports for Host Router (Port Forwarding)

If the host computer connects via a home Wi-Fi router, forward these ports to the host's local IP:

| Protocol | Port | Description |
| :--- | :--- | :--- |
| **TCP** | `51820` | Control Plane (Authentication & Heartbeat) |
| **UDP** | `51821` | AmneziaWG 3.1 VPN Transport |
| **TCP / UDP** | `51822` | Xray VLESS + REALITY Transport |

*(Friends connecting to you do **not** need to touch their routers).*

---

## 🎮 Quick Start Guide

### 1. Host (Game Creator)
1. Launch `LanBridge.exe`.
2. Click **"Create Network"**, enter a network name, password, and select your transport protocol (**AmneziaWG 3.1** or **Xray REALITY**).
3. Click the **"Router"** tab in the top bar to verify your public IPv4 address.
4. Share your **Public IP**, port `51820`, and password with your friends.
5. Open your world in Minecraft Java Edition and click **"Open to LAN"**.

### 2. Client (Joining Friend)
1. Launch `LanBridge.exe`.
2. Click **"Connect to Network"**, enter the host's IP address, port `51820`, and password.
3. Once connected, open Minecraft Java -> **"Multiplayer"**.
4. The host's world will automatically appear at the bottom of the list under **"LAN World"**!
