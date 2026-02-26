# VoyageX AI — Self-Hosting Guide

Host VoyageX AI on your ship computer or local server for offline access.

---

## Requirements

| | Minimum | Recommended |
|:--|:--|:--|
| **OS** | Windows 10, macOS 13, Ubuntu 20.04 | Windows 11, macOS 14+, Ubuntu 22.04 LTS |
| **CPU** | Quad-core 2.5 GHz | 8-core 3 GHz+ |
| **RAM** | 8 GB | 16 GB+ |
| **Storage** | 5 GB SSD | 20 GB+ SSD |
| **Browser** | Chrome 119+, Edge 119+ | Chrome latest |

---

## Quick Start

### 1. Install Node.js

Download and install Node.js LTS from [nodejs.org](https://nodejs.org).

> **Linux only**
> ```bash
> sudo apt update && sudo apt install -y nodejs npm
> ```

---

### 2. Download the App

**macOS / Linux**
```bash
cd ~/Downloads
curl -L $(curl -s https://api.github.com/repos/voyagexai/app/releases/latest | grep "browser_download_url" | grep ".zip" | cut -d '"' -f 4) -o voyagex.zip
unzip -o voyagex.zip
```

**Windows (PowerShell)**
```powershell
cd $HOME\Downloads
$url = (Invoke-RestMethod https://api.github.com/repos/voyagexai/app/releases/latest).assets[0].browser_download_url
Invoke-WebRequest $url -OutFile voyagex.zip
Expand-Archive -Force voyagex.zip
```

---

### 3. Start the Server

```bash
npx serve voyagex/build/web/
```

---

### 4. Open in Browser

Go to `http://localhost:3000` in Chrome or Edge.

> [!NOTE]
> No internet required after first setup.

---

## Onboard Access (LAN)

Once the server is running, other devices on the same network can access the app.

**Find your IP**
```bash
ipconfig getifaddr en0   # macOS
hostname -I              # Linux
ipconfig                 # Windows → IPv4 Address
```

**Open on any device**
```
http://192.168.x.x:3000
```

> [!IMPORTANT]
> Windows users may need to allow port `3000` in the firewall:
> `Settings → Windows Defender Firewall → Allow an app → Node.js`

---

## Updating

Stop the server and re-run from Step 2.

```bash
Ctrl + C
```

---

## Troubleshooting

| Symptom | Fix |
|:--|:--|
| **Blank screen** | `F12` → Network → `index.html` → check COOP/COEP headers |
| **Can't connect from LAN** | Allow port `3000` in firewall; confirm same network |
| **App won't load** | Use Chrome 119+ or Edge 119+ — Firefox not supported |
