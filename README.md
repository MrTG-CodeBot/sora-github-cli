<div align="center">

<img src="sora.jpeg" alt="Sora Logo" width="130" height="130" style="border-radius: 20px; box-shadow: 0 8px 24px rgba(0,0,0,0.3);" />

# 🚀 Sora - GitHub CLI Manager

### Simple, Fast, and Cross-Platform GitHub Repository Management

[![Version](https://img.shields.io/badge/version-2.1.0-blue.svg)](https://github.com/MrTG-CodeBot/sora-github-cli/releases)
[![Python](https://img.shields.io/badge/python-3.6+-3776AB.svg?logo=python&logoColor=white)](https://www.python.org/downloads/)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS%20%7C%20Termux-blueviolet.svg)](#-installation)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Stars](https://img.shields.io/github/stars/MrTG-CodeBot/sora-github-cli?style=social)](https://github.com/MrTG-CodeBot/sora-github-cli/stargazers)
[![Issues](https://img.shields.io/github/issues/MrTG-CodeBot/sora-github-cli)](https://github.com/MrTG-CodeBot/sora-github-cli/issues)

[Live Documentation](https://mrtg-codebot.github.io/sora-github-cli/) •
[Features](#-features) •
[Installation](#-installation) •
[Quick Start](#-quick-start) •
[Command Reference](#-command-reference) •
[Troubleshooting](#-troubleshooting)

</div>

---

## 📖 Overview

**Sora** is a lightweight command-line interface (CLI) that simplifies GitHub repository and file operations. Designed for developers who prefer staying in their terminal, Sora allows you to upload folders recursively, read remote source code, inspect repository analytics, and manage branches directly without complex Git setup.

> [!TIP]
> **Version 2.1.0** features a zero-restart cross-platform configuration engine (`~/.sora/config.json`) with full support for **Windows**, **Linux**, **macOS**, and **Android (Termux)**.

---

## ✨ Features

<table>
<tr>
<td width="50%" valign="top">

### 📂 Repository Management
- ✅ **List Repositories** - Filter by public, private, or sort by stars/updated
- ✅ **Create Repositories** - Instant private or public repos with descriptions
- ✅ **Repository Analytics** - View stars, watchers, forks, size, and branches
- ✅ **Rename & Update** - Modify names, descriptions, or toggle visibility
- ✅ **Delete Safely** - Interactive confirmation guards prevent accidental deletion

</td>
<td width="50%" valign="top">

### 📄 File Operations & Code
- ✅ **Direct Folder Push** - Upload entire folder trees recursively
- ✅ **Remote File Inspection** - Read code in stdout via `sora cat`
- ✅ **Browse Trees** - List repository files without cloning
- ✅ **API Pull** - Download and extract repo archives directly
- ✅ **Branch Support** - List all active branches and commit SHAs
- ✅ **Smart Retries** - Built-in exponential backoff handles network drops

</td>
</tr>
</table>

---

## 🚀 Installation

### Prerequisites
- **Python 3.6+** installed on your system
- A **GitHub Personal Access Token** with the `repo` scope

### 🪟 Windows (Command Prompt & PowerShell)

```powershell
# 1. Clone repository
git clone https://github.com/MrTG-CodeBot/sora-github-cli.git
cd sora-github-cli

# 2. Install dependency
pip install requests

# 3. Add to User PATH or copy sora.cmd into your Python Scripts directory
# Run sora anywhere without typing python!
sora --version
```

### 📱 Android (Termux)

```bash
# 1. Install Python, Git & Dependencies
pkg update && pkg install python git -y
pip install requests

# 2. Install Sora into Termux bin
curl -o $PREFIX/bin/sora https://raw.githubusercontent.com/MrTG-CodeBot/sora-github-cli/main/sora
chmod +x $PREFIX/bin/sora

# 3. Verify
sora --version
```

### 🐧 Linux (Ubuntu / Debian / Arch)

```bash
# 1. Download to system bin
sudo curl -o /usr/local/bin/sora https://raw.githubusercontent.com/MrTG-CodeBot/sora-github-cli/main/sora
sudo chmod +x /usr/local/bin/sora

# 2. Install dependency
pip install requests
```

### 🍏 macOS

```bash
# 1. Download to executable path
sudo curl -o /usr/local/bin/sora https://raw.githubusercontent.com/MrTG-CodeBot/sora-github-cli/main/sora
sudo chmod +x /usr/local/bin/sora

# 2. Install dependency
pip3 install requests
```

---

## 🎯 Quick Start

### 1. Generate Your Token
1. Go to [GitHub Settings → Tokens](https://github.com/settings/tokens).
2. Click **Generate new token (classic)**.
3. Select the `repo` scope (Full control of repositories).
4. Copy your token (starts with `ghp_`).

### 2. Configure Token (Works Everywhere)
Sora saves your token locally in `~/.sora/config.json`. **No terminal restart required**:

```bash
sora --set-token YOUR_GITHUB_TOKEN
```

### 3. Verify Authentication
```bash
sora --check-account
```

Output:
```text
✓ Connected as: MrTG-CodeBot
```

---

## 📚 Command Reference

### 🏠 Repository Management

| Command | Synopsis | Description |
|---------|----------|-------------|
| `repos` | `sora repos [--visibility {all,public,private}] [--limit N]` | List repositories with stats & visibility |
| `create` | `sora create <name> [--private] [--desc "text"]` | Create a new GitHub repository |
| `stats` | `sora stats <repo>` | Display detailed stars, forks, issues & metadata |
| `view` | `sora view <repo>` | Show repository URLs and general info |
| `rename` | `sora rename <old-name> <new-name>` | Rename a repository |
| `update` | `sora update <repo> [--desc "text"] [--public \| --private]` | Update repo description or toggle visibility |
| `delete` | `sora delete <repo> [--force]` | Delete a repository permanently |

### 📁 File & Code Operations

| Command | Synopsis | Description |
|---------|----------|-------------|
| `push` | `sora push <repo> [path] [--target remote/] [-m "msg"]` | Upload a file or folder recursively |
| `pull` | `sora pull <repo> [--dest path] [--branch name]` | Download and extract repository archive |
| `ls` | `sora ls <repo> [--path dir/] [--files-only]` | Browse directory contents remotely |
| `cat` | `sora cat <repo> <file> [--raw]` | Print remote file contents directly to terminal |
| `rm` | `sora rm <repo> <path> [-m "msg"] [--force]` | Delete a remote file or directory |

### 🌲 Git Operations

| Command | Synopsis | Description |
|---------|----------|-------------|
| `branches` | `sora branches <repo>` | List all branches and latest commit SHAs |

---

## 💡 Practical Examples

### 1. Instant Project Backup
Download any repository as a clean zip and extract it without installing Git:
```bash
sora pull Muzic-x --dest ./backup-muzic
```

### 2. Deploy a Build Folder
Upload a compiled distribution directory to a remote repository folder:
```bash
sora push my-website ./dist --target build/ -m "Deploy v2.1.0 release"
```

### 3. Inspect Remote Code in Seconds
Check configuration or documentation files without cloning:
```bash
sora cat my-project package.json
```

### 4. Create and Initialize a Private Repo
```bash
sora create backend-service --private --desc "Microservices API"
sora push backend-service ./src -m "Initial commit"
```

---

## ⚙️ How Authentication Works

Sora searches for credentials using this resolution hierarchy:

```text
1. CLI Flag (--token <TOKEN>)
      ↓
2. Local Config File (~/.sora/config.json)
      ↓
3. Environment Variable ($GITHUB_TOKEN)
```

> [!NOTE]
> Config files are stored with `chmod 600` permissions (owner read/write only) on POSIX systems (Linux, macOS, Termux) and locally in `%USERPROFILE%\.sora\` on Windows.

---

## 🐛 Troubleshooting

### `Invalid GitHub token` (HTTP 401)
- **Cause:** Token has expired, was revoked, or lacks `repo` scope.
- **Fix:** Generate a fresh token at [github.com/settings/tokens](https://github.com/settings/tokens) and run:
  ```bash
  sora --set-token YOUR_NEW_TOKEN
  ```

### `NameResolutionError / Failed to resolve api.github.com`
- **Cause:** Temporary network or DNS interruption.
- **Fix:** Verify internet connection or flush your DNS cache:
  ```powershell
  # Windows
  ipconfig /flushdns
  ```

### `'sora' is not recognized on Windows`
- **Fix:** Use the included `sora.cmd` launcher by adding the `sora-github-cli` directory to your User `PATH`, or copy `sora.cmd` into your Python `Scripts` directory (`%LOCALAPPDATA%\Programs\Python\Python3xx\Scripts`).

---

## 🤝 Contributing

Contributions, bug reports, and suggestions are welcome!

1. Fork the Project (`https://github.com/MrTG-CodeBot/sora-github-cli/fork`)
2. Create your Feature Branch (`git checkout -b feature/NewFeature`)
3. Commit your Changes (`git commit -m 'Add NewFeature'`)
4. Push to the Branch (`git push origin feature/NewFeature`)
5. Open a Pull Request

---

## 📜 License

Distributed under the **MIT License**. See [`LICENSE`](LICENSE) for more information.

---

## 👨‍💻 Author

**MrTG-CodeBot**
- 🌐 Portfolio: [amalnath.netlify.app](https://amalnath.netlify.app/)
- 🐙 GitHub: [@MrTG-CodeBot](https://github.com/MrTG-CodeBot)
- 💬 Discussions: [GitHub Discussions](https://github.com/MrTG-CodeBot/sora-github-cli/discussions)
