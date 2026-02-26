## VoyageX AI — Self-Hosting Guide

Host VoyageX AI on your ship computer or local server for offline access.


### System Requirements

| | Minimum | Recommended |
|:--|:--|:--|
| **OS** | Windows 10, macOS 13, Ubuntu 20.04 | Windows 11, macOS 14+, Ubuntu 22.04 LTS |
| **CPU** | Quad-core 2.5 GHz | 8-core 3 GHz+ |
| **RAM** | 8 GB | 16 GB+ |
| **Storage** | 5 GB SSD | 20 GB+ SSD |
| **Browser** | Chrome 119+, Edge 119+ | Chrome latest |

### Installation

**1 · Download the App**

Download `web.zip` from the [latest release](https://github.com/voyagexai/app/releases/latest) and unzip:

```bash
unzip web.zip
```

You'll get a `web/` folder — this is the complete app.

**2 · Install Node.js**

Download **Node.js LTS** from [nodejs.org](https://nodejs.org) and install it.

```bash
node -v && npm -v   # verify install
```

**3 · Start the Server**

Open **PowerShell** (Windows) or **Terminal** (macOS / Linux) in the folder containing `web/`:

```bash
npx serve web/ --set-headers "Cross-Origin-Opener-Policy=same-origin,Cross-Origin-Embedder-Policy=require-corp"
```

**4 · Open the App**

Open **Chrome** or **Edge** and go to `http://localhost:3000`

> [!NOTE]
> The app runs entirely from your local machine — no internet required after first setup.

### Onboard Network Access

Once the server is running, crew devices on the same network can access the app via the host computer's IP.

**Find your local IP**

```bash
ipconfig          # Windows  →  IPv4 Address
ifconfig          # macOS / Linux  →  inet
```

**Share this address with crew devices**

```
http://192.168.x.x:3000
```

**Windows firewall** — allow port `3000`:

```
Settings → Windows Defender Firewall → Allow an app → Node.js
```

> [!IMPORTANT]
> All devices must be on the same local network (LAN or Wi-Fi). No internet required.

### Updating

```bash
# 1. Stop the server
Ctrl + C

# 2. Download latest web.zip → github.com/voyagexai/app/releases/latest
# 3. Replace the web/ folder
# 4. Restart
npx serve web/ --set-headers "Cross-Origin-Opener-Policy=same-origin,Cross-Origin-Embedder-Policy=require-corp"
```

### Troubleshooting

| Symptom | Fix |
|:--|:--|
| **Blank screen** | `F12` → Network → `index.html` → verify `Cross-Origin-Opener-Policy` and `Cross-Origin-Embedder-Policy` headers are present |
| **Crew devices can't connect** | Allow port `3000` in firewall; confirm all devices are on the same network |
| **App won't load** | Use Chrome 119+ or Edge 119+ — Firefox is not supported |
| **WASM error** | Must be served from `localhost` or HTTPS — plain HTTP on a remote IP will not work |
