<div align="center">

# 🚀 VS Code in Termux — Complete Setup Guide (2026)

**Run a fully functional VS Code development environment on Android — no PC required.**

[![Skynet](https://img.shields.io/badge/Made%20with%20%E2%9D%A4%EF%B8%8F%20by-Skynet-0A0A23?style=for-the-badge&logo=heart&logoColor=FF6B6B)](https://github.com/skynetfc)
[![Project](https://img.shields.io/badge/Project-Atlantia--Empire-7B2CBF?style=for-the-badge&logo=github)](https://github.com/skynetfc/Atlantia-Empire)
[![Platform](https://img.shields.io/badge/Platform-Termux-000000?style=for-the-badge&logo=linux&logoColor=FFFFFF)](https://termux.dev/)
[![Editor](https://img.shields.io/badge/Editor-VS%20Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=FFFFFF)](https://code.visualstudio.com/)
[![License](https://img.shields.io/badge/License-MIT-F7DF1E?style=for-the-badge)](https://github.com/skynetfc/Atlantia-Empire/blob/main/LICENSE)
[![Version](https://img.shields.io/badge/Version-2026.07-blue?style=for-the-badge)](https://github.com/skynetfc/Atlantia-Empire/releases)

---

> 🔗 **Check out our new project:** [github.com/skynetfc/Atlantia-Empire](https://github.com/skynetfc/Atlantia-Empire)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [System Requirements](#-system-requirements)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
  - [Step 1: Update Termux Packages](#step-1-update-termux-packages)
  - [Step 2: Install Dependencies](#step-2-install-dependencies)
  - [Step 3: Install Code-Server](#step-3-install-code-server)
  - [Step 4: Configure Code-Server](#step-4-configure-code-server)
  - [Step 5: Start Code-Server](#step-5-start-code-server)
  - [Step 6: Access VS Code](#step-6-access-vs-code)
- [Extensions](#-extensions)
- [Development Environments](#-development-environments)
- [Background Operation](#-background-operation)
- [External Access](#-external-access)
- [Features](#-features)
- [Example Projects](#-example-projects)
- [Troubleshooting](#-troubleshooting)
- [Performance Tips](#-performance-tips)
- [Storage Integration](#-storage-integration)
- [Security](#-security)
- [Resources](#-resources)

---

## 🎯 Overview

This guide provides a complete, production-ready setup for running **VS Code** inside **Termux** on Android devices. Whether you're coding on the go, learning new languages, or building full-stack applications — this setup delivers a professional-grade development experience directly from your mobile device.

> **Target:** Android 10+ | **Termux 0.118+** | **Code-Server 4.x**

---

## 💻 System Requirements

### Storage

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| Termux Base | 200 MB | 500 MB |
| Code-Server | 500 MB | 1.0 GB |
| Node.js Runtime | 100 MB | 200 MB |
| Python Environment | 50 MB | 100 MB |
| Build Toolchain | 300 MB | 500 MB |
| VS Code Extensions | 100 MB | 300 MB |
| Project Workspace | 500 MB | 2.0 GB |
| **Total** | **~1.75 GB** | **~4.6 GB** |

> ⚠️ **Recommendation:** Maintain at least **5 GB** of free storage for optimal performance and future expansion.

### Hardware

| Specification | Minimum | Recommended |
|---------------|---------|-------------|
| RAM | 3 GB | 6 GB+ |
| Android Version | 10 (API 29) | 13+ (API 33+) |
| Processor | ARM64 | ARM64 (8-core) |
| Free Storage | 3 GB | 5 GB |

---

## 📦 Prerequisites

1. **Install Termux from F-Droid**
   > ⚠️ **Do not use the Google Play Store version** — it is outdated and no longer maintained.
   - Download F-Droid: [https://f-droid.org/](https://f-droid.org/)
   - Search for and install **Termux**

2. **Install Termux:API** (optional, recommended for extended functionality)
   - Available on F-Droid alongside Termux

---

## 🔧 Installation

### Step 1: Update Termux Packages

Ensure your package index and installed packages are current:

```bash
pkg update && pkg upgrade -y
```

> 💾 **Storage impact:** ~50–100 MB

---

### Step 2: Install Dependencies

Install the core toolchain required for development:

```bash
pkg install -y nodejs python git wget curl build-essential
```

> 💾 **Storage impact:** ~400–600 MB

**Installed components:**
- `nodejs` — JavaScript runtime & npm
- `python` — Python 3 interpreter & pip
- `git` — Version control
- `wget` / `curl` — Network utilities
- `build-essential` — GCC, make, and compilation tools

---

### Step 3: Install Code-Server

**Code-Server** is the official open-source VS Code distribution for remote development, running entirely in the browser.

#### Method A: npm (Recommended)

```bash
npm install -g code-server
```

#### Method B: Official Installer Script

```bash
curl -fsSL https://code-server.dev/install.sh | sh
```

> 💾 **Storage impact:** ~500 MB – 1.0 GB

---

### Step 4: Configure Code-Server

Create the configuration directory and file:

```bash
mkdir -p ~/.config/code-server
```

```bash
cat > ~/.config/code-server/config.yaml << 'EOF'
bind-addr: 127.0.0.1:8080
auth: password
password: CHANGE_THIS_TO_A_STRONG_PASSWORD
cert: false
EOF
```

> 🔐 **Security:** Replace `CHANGE_THIS_TO_A_STRONG_PASSWORD` with a cryptographically strong password (16+ characters, mixed case, numbers, symbols).

**Configuration reference:**

| Key | Value | Description |
|-----|-------|-------------|
| `bind-addr` | `127.0.0.1:8080` | Localhost binding (secure default) |
| `auth` | `password` | Password-based authentication |
| `password` | `<your_password>` | Access credential |
| `cert` | `false` | TLS disabled (use reverse proxy for HTTPS) |

---

### Step 5: Start Code-Server

Launch the server:

```bash
code-server
```

**Expected output:**

```
[2026-07-09T10:00:00.000Z] info  code-server 4.95.3
[2026-07-09T10:00:00.000Z] info  Using config file ~/.config/code-server/config.yaml
[2026-07-09T10:00:00.000Z] info  HTTP server listening on http://127.0.0.1:8080/
[2026-07-09T10:00:00.000Z] info  Session server listening on ~/.local/share/code-server/code-server-ipc.sock
```

---

### Step 6: Access VS Code

1. Open your preferred browser (Chrome, Firefox, Brave, etc.)
2. Navigate to: **[http://127.0.0.1:8080](http://127.0.0.1:8080)**
3. Enter your configured password
4. ✅ **VS Code is now running on your Android device**

---

## 🧩 Extensions

Install the following essential extensions via the Extensions panel (`Ctrl+Shift+X`):

| Extension | Publisher | Purpose |
|-----------|-----------|---------|
| **Python** | Microsoft | Python language support, IntelliSense, debugging |
| **ESLint** | Microsoft | JavaScript/TypeScript linting |
| **Prettier** | Prettier | Code formatting |
| **Live Server** | Ritwick Dey | Local development server for web projects |
| **C/C++** | Microsoft | C and C++ language support |
| **Extension Pack for Java** | Microsoft | Java development toolkit |
| **GitLens** | GitKraken | Enhanced Git visualization |
| **Markdown All in One** | Yu Zhang | Markdown authoring support |

> 💾 **Storage impact:** ~10–50 MB per extension

---

## 🛠️ Development Environments

### Python

```bash
pkg install python
pip install --upgrade pip
```

> 💾 **Storage impact:** ~50–100 MB

**Verify installation:**
```bash
python --version
pip --version
```

---

### Node.js

Pre-installed with Step 2. Verify:

```bash
node --version   # v22.x.x
npm --version    # 10.x.x
```

---

### C / C++

```bash
pkg install clang
```

> 💾 **Storage impact:** ~200–300 MB

**Verify installation:**
```bash
clang --version
```

---

### Java

```bash
pkg install openjdk-21
```

> 💾 **Storage impact:** ~300–400 MB

**Verify installation:**
```bash
java --version
javac --version
```

---

### Web Development

```bash
npm install -g live-server
```

> 💾 **Storage impact:** ~20–30 MB

---

## 🔄 Background Operation

To maintain VS Code availability without keeping Termux in the foreground, use one of the following methods:

### Method 1: `nohup` (Recommended)

Run code-server detached from the terminal:

```bash
nohup code-server > ~/code-server.log 2>&1 &
```

**Stop the server:**
```bash
pkill code-server
```

**View logs:**
```bash
tail -f ~/code-server.log
```

---

### Method 2: Termux:Boot (Auto-start on Boot)

1. Install **Termux:Boot** from F-Droid
2. Create the boot directory:
   ```bash
   mkdir -p ~/.termux/boot
   ```
3. Create the startup script:
   ```bash
   cat > ~/.termux/boot/start-code-server.sh << 'EOF'
   #!/data/data/com.termux/files/usr/bin/bash
   termux-wake-lock
   nohup code-server > ~/code-server.log 2>&1 &
   EOF
   chmod +x ~/.termux/boot/start-code-server.sh
   ```
4. Reboot your device — code-server starts automatically

---

### Method 3: `tmux` Session Management

```bash
pkg install tmux
```

**Create and attach to a session:**
```bash
tmux new -s vscode
code-server
```

**Detach:** `Ctrl+B` then `D`  
**Reattach:** `tmux attach -t vscode`

---

### Prevent Android from Killing Termux

1. **Android Settings → Apps → Termux → Battery → Unrestricted**
2. **Disable battery optimization** for Termux
3. **Acquire wake lock** to keep CPU active:
   ```bash
   termux-wake-lock
   ```
4. **Release wake lock** when done:
   ```bash
   termux-wake-unlock
   ```

> ✅ **Best Practice:** Combine `nohup` + `termux-wake-lock` for maximum reliability.

---

## 🌍 External Access

To access VS Code from another device on the same local network:

1. **Identify your device's IP address:**
   ```bash
   ifconfig
   ```
   Look for the `wlan0` interface (e.g., `192.168.1.42`).

2. **Update the binding address:**
   ```bash
   nano ~/.config/code-server/config.yaml
   ```
   Change:
   ```yaml
   bind-addr: 0.0.0.0:8080
   ```

3. **Restart code-server**

4. **Access from another device:**
   ```
   http://YOUR_DEVICE_IP:8080
   ```

> ⚠️ **Security Warning:** Only expose code-server on trusted local networks. For remote access, use a VPN or SSH tunnel.

---

## ✨ Features

| Capability | Status | Notes |
|------------|--------|-------|
| Full VS Code Editor | ✅ Supported | All editing features, multi-cursor, Emmet |
| Integrated Terminal | ✅ Supported | Full bash/zsh access within editor |
| Git Integration | ✅ Supported | Clone, commit, push, pull, diff |
| Extensions Marketplace | ✅ Supported | Thousands of extensions available |
| Debugging | ✅ Supported | Python, Node.js, C++, Java |
| IntelliSense | ✅ Supported | Code completion, hover info, go-to-definition |
| File Explorer | ✅ Supported | Full filesystem navigation |
| Multi-language Support | ✅ Supported | 50+ programming languages |
| Remote Development | ✅ Supported | Access from any browser on the network |
| Themes & Customization | ✅ Supported | Full theme and settings sync |

---

## 🎯 Example Projects

### 1. Flask Web Application

```bash
mkdir -p ~/projects/flask-demo
cd ~/projects/flask-demo
pip install flask
```

**`app.py`:**
```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/')
def index():
    return jsonify({
        "message": "Hello from Termux VS Code!",
        "platform": "Android",
        "runtime": "Flask + Python"
    })

@app.route('/health')
def health():
    return jsonify({"status": "healthy"})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
```

**Run:**
```bash
python app.py
```

---

### 2. Express.js REST API

```bash
mkdir -p ~/projects/express-demo
cd ~/projects/express-demo
npm init -y
npm install express
```

**`server.js`:**
```javascript
const express = require('express');
const app = express();

app.use(express.json());

app.get('/', (req, res) => {
    res.json({
        message: 'Hello from Termux VS Code!',
        platform: 'Android',
        runtime: 'Node.js + Express'
    });
});

app.get('/health', (req, res) => {
    res.json({ status: 'healthy' });
});

app.listen(3000, '0.0.0.0', () => {
    console.log('🚀 Server running at http://0.0.0.0:3000');
});
```

**Run:**
```bash
node server.js
```

---

### 3. C++ Console Application

**`hello.cpp`:**
```cpp
#include <iostream>
#include <string>

int main() {
    std::string platform = "Termux on Android";
    std::cout << "Hello from " << platform << "!" << std::endl;
    std::cout << "Compiled with Clang in VS Code." << std::endl;
    return 0;
}
```

**Compile and run:**
```bash
clang++ -std=c++17 -O2 hello.cpp -o hello
./hello
```

---

## 🔧 Troubleshooting

### Connection Refused / localhost unreachable

| Check | Command |
|-------|---------|
| Is code-server running? | `pgrep -f code-server` |
| Correct port? | `cat ~/.config/code-server/config.yaml` |
| Restart Termux | Close all sessions and reopen |
| Restart code-server | `pkill code-server && code-server` |

---

### Extension Installation Fails

| Cause | Solution |
|-------|----------|
| No internet connection | Verify Wi-Fi / mobile data |
| ARM architecture limitation | Check extension compatibility |
| Outdated code-server | `npm update -g code-server` |
| Corrupted extension cache | `rm -rf ~/.local/share/code-server/extensions` |

---

### Insufficient Storage

```bash
# Clean package cache
pkg clean

# Remove unused dependencies
pkg autoremove -y

# Check code-server disk usage
du -sh ~/.config/code-server ~/.local/share/code-server

# List largest packages
dpkg-query -Wf '${Installed-Size}\t${Package}\n' | sort -n | tail -20
```

---

### Code-Server Crashes or Freezes

| Action | Command |
|--------|---------|
| Check available RAM | `free -h` |
| Kill all code-server processes | `pkill -9 code-server` |
| Update all packages | `pkg update && pkg upgrade -y` |
| Clear extension cache | `rm -rf ~/.local/share/code-server/CachedExtensionVSIXs` |
| Restart with minimal extensions | `code-server --disable-extensions` |

---

## ⚡ Performance Optimization

1. **Limit Open Tabs** — Keep only actively edited files open
2. **Disable Unused Extensions** — Uninstall or disable extensions not in use
3. **Use Lightweight Themes** — Prefer Dark+ or Light+ over heavy custom themes
4. **Manage Terminal Instances** — Close integrated terminals when not needed
5. **Regular Maintenance** — Run `pkg clean` weekly to reclaim space
6. **Enable File Exclusions** — Add `node_modules/`, `__pycache__/` to `files.exclude`
7. **Reduce Editor Font Size** — Smaller fonts improve rendering performance on mobile

---

## 💾 Storage Integration

Grant Termux access to Android shared storage:

```bash
termux-setup-storage
```

**Available mount points:**

| Path | Description |
|------|-------------|
| `~/storage/downloads` | Downloads folder |
| `~/storage/dcim` | Camera photos & videos |
| `~/storage/shared` | Internal storage root |
| `~/storage/music` | Music directory |
| `~/storage/movies` | Movies directory |
| `~/storage/pictures` | Pictures directory |

**Sync projects with Git:**
```bash
cd ~/projects/my-app
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/username/repo.git
git push -u origin main
```

---

## 🔒 Security Best Practices

| Practice | Implementation |
|----------|----------------|
| Strong Authentication | Use 16+ character passwords with mixed entropy |
| Network Isolation | Bind to `127.0.0.1` by default; avoid `0.0.0.0` on public networks |
| Encrypted Remote Access | Use WireGuard or OpenVPN instead of direct exposure |
| Regular Updates | `pkg upgrade` weekly to patch vulnerabilities |
| Minimal Permissions | Grant only required Android permissions to Termux |
| Secret Management | Never commit credentials; use `.env` files excluded from Git |
| Session Timeout | Restart code-server after extended idle periods |

---

## 📚 Resources

| Resource | Link |
|----------|------|
| Code-Server Documentation | [coder.com/docs/code-server](https://coder.com/docs/code-server/latest) |
| Termux Wiki | [wiki.termux.com](https://wiki.termux.com/) |
| VS Code Docs | [code.visualstudio.com/docs](https://code.visualstudio.com/docs) |
| F-Droid Repository | [f-droid.org](https://f-droid.org/) |
| Atlantia Empire Project | [github.com/skynetfc/Atlantia-Empire](https://github.com/skynetfc/Atlantia-Empire) |

---

<div align="center">

## 🌟 Created by Skynet

[![GitHub](https://img.shields.io/badge/GitHub-@skynetfc-181717?style=for-the-badge&logo=github)](https://github.com/skynetfc)
[![Project](https://img.shields.io/badge/Atlantia--Empire-7B2CBF?style=for-the-badge&logo=github)](https://github.com/skynetfc/Atlantia-Empire)

---

> 💡 **Note:** This setup is ideal for mobile development, learning, prototyping, and lightweight production workloads. For resource-intensive tasks (large builds, heavy ML training), a dedicated workstation remains recommended.

**If this guide helped you, please ⭐ star the repository!**

</div>
