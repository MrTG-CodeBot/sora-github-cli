<div align="center">

<img src="sora.jpeg" alt="Sora Logo" width="150" height="150" />

# 🚀 Sora - GitHub CLI Manager

### Simple, Powerful, and User-Friendly GitHub Repository Management

[![Version](https://img.shields.io/badge/version-2.1.0-blue.svg)](https://github.com/MrTG-CodeBot/sora-github-cli/releases)
[![Python](https://img.shields.io/badge/python-3.6+-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Stars](https://img.shields.io/github/stars/MrTG-CodeBot/sora-github-cli?style=social)](https://github.com/MrTG-CodeBot/sora-github-cli/stargazers)
[![GitHub Issues](https://img.shields.io/github/issues/MrTG-CodeBot/sora-github-cli)](https://github.com/MrTG-CodeBot/sora-github-cli/issues)

[Features](#-features) •
[Installation](#-installation) •
[Quick Start](#-quick-start) •
[Documentation](#-documentation) •
[Contributing](#-contributing)

</div>

---

## 📖 Overview

**Sora** is a powerful command-line interface (CLI) tool that simplifies GitHub repository management. Whether you're uploading files, reading code, managing repositories, or exploring branches, Sora provides an intuitive and efficient way to interact with GitHub without leaving your terminal.

### Why Sora?

- 🎯 **Simple & Intuitive** - Clean commands that just make sense
- ⚡ **Fast & Efficient** - Optimized API calls with automatic retry logic
- 🎨 **Beautiful Output** - Color-coded, emoji-rich terminal display
- 🛡️ **Safe Operations** - Confirmation prompts for destructive actions
- 🔄 **Smart Retry** - Exponential backoff for network errors
- 📦 **Feature-Rich** - 10+ powerful features for complete GitHub management

---

## ✨ Features

<table>
<tr>
<td width="50%">

### 📂 Repository Management
- ✅ List all your repositories
- ✅ Create new repositories
- ✅ View repository details
- ✅ Rename repositories
- ✅ Update repository settings
- ✅ Delete repositories
- ✅ Show detailed statistics

</td>
<td width="50%">

### 📄 File Operations
- ✅ List repository contents
- ✅ Read file contents directly
- ✅ Upload files & folders
- ✅ Delete files & folders
- ✅ Download repositories
- ✅ Branch management
- ✅ Smart path handling

</td>
</tr>
</table>

### 🔥 Advanced Features

| Feature | Description |
|---------|-------------|
| 🔄 **Auto Retry** | Automatic retry with exponential backoff for network failures |
| 📊 **Rich Statistics** | Detailed repo stats including stars, forks, and engagement |
| 🌲 **Branch Support** | List and work with different branches |
| 🎨 **Color Output** | Beautiful, color-coded terminal output with icons |
| 📦 **Bulk Operations** | Upload/delete multiple files with progress tracking |
| 🛡️ **File Validation** | Automatic file size checks (100MB limit) |
| 💾 **Smart Caching** | Optimized API usage for faster operations |
| ⚙️ **Flexible Config** | Support for both inline tokens and environment variables |

---

## 🚀 Installation

### Prerequisites

- **Python 3.6+** installed on your system
- A **GitHub Personal Access Token** with `repo` permissions

### Step 1: Get the Script

Download or clone this repository:

```bash
# Using git
git clone https://github.com/MrTG-CodeBot/sora-github-cli.git
cd sora-github-cli

# Or download directly
curl -O https://raw.githubusercontent.com/MrTG-CodeBot/sora-github-cli/main/sora
```

### Step 2: Make it Executable (Linux/macOS)

```bash
chmod +x sora
```

### Step 3: Add to PATH (Run Sora Globally)

**Linux / macOS:**
```bash
chmod +x sora
sudo mv sora /usr/local/bin/
```

**Android (Termux):**
```bash
chmod +x sora
cp sora $PREFIX/bin/
```

**Windows:**
Run `sora.cmd` or add the script directory to your User `PATH`.

### Step 4: Install Dependencies

```bash
pip install requests
```

---

## 🎯 Quick Start

### 1. Get Your GitHub Token

1. Go to [GitHub Settings → Tokens](https://github.com/settings/tokens)
2. Click "Generate new token (classic)"
3. Give it a name (e.g., "Sora CLI")
4. Select scopes: `repo` (Full control of private repositories)
5. Click "Generate token"
6. **Copy the token** (you won't see it again!)

### 2. Save Your Token (All Platforms)

Works automatically on **Windows**, **Linux**, **macOS**, and **Termux (Android)** without restarting your terminal:

```bash
sora --set-token YOUR_GITHUB_TOKEN
```

### 3. Verify Authentication

```bash
sora --check-account
```

Output:
```
✓ Connected as: YourUsername
```

### 4. Start Using Sora!

```bash
# List your repositories
sora repos

# Create a new repository
sora create my-awesome-project --private --desc "My new project"

# Upload files
sora push my-repo ./my-project

# Download a repository
sora pull my-repo --dest ./downloads
```

---

## 📚 Documentation

### Commands Overview

#### 🏠 Repository Management

```bash
# List all repositories
sora repos
sora repos --visibility private
sora repos --sort created --limit 10

# Create a repository
sora create <name> [--private] [--desc "description"]

# View repository details
sora view <repo>

# Show detailed statistics
sora stats <repo>

# Rename a repository
sora rename <old-name> <new-name>

# Update repository settings
sora update <repo> --desc "New description"
sora update <repo> --private
sora update <repo> --public

# Delete a repository
sora delete <repo>
sora delete <repo> --force
```

#### 📁 File Operations

```bash
# List repository contents
sora ls <repo>
sora ls <repo> --path src/
sora ls <repo> --files-only
sora ls <repo> --folders-only

# Read file contents
sora cat <repo> <file-path>
sora cat <repo> README.md --raw

# Upload file or folder
sora push <repo> <local-path>
sora push <repo> ./file.txt --target remote/path/
sora push <repo> ./folder -m "Upload project files"

# Delete file or folder
sora rm <repo> <path>
sora rm <repo> old-folder --force

# Download repository
sora pull <repo>
sora pull <repo> --dest ./downloads
sora pull <repo> --branch develop
```

#### 🌲 Branch Management

```bash
# List all branches
sora branches <repo>
```

#### 🔐 Authentication

```bash
# Check current user
sora --token YOUR_TOKEN --check-account

# Save token (Windows)
sora --set-token YOUR_TOKEN
sora --set-token YOUR_TOKEN --scope system
```

### Command Reference Table

| Command | Description | Example |
|---------|-------------|---------|
| `repos` | List repositories | `sora repos --visibility private` |
| `create` | Create repository | `sora create my-app --private` |
| `view` | View repo info | `sora view my-repo` |
| `stats` | Show statistics | `sora stats my-repo` |
| `rename` | Rename repository | `sora rename old new` |
| `update` | Update settings | `sora update my-repo --desc "text"` |
| `delete` | Delete repository | `sora delete my-repo` |
| `ls` | List contents | `sora ls my-repo --path src/` |
| `cat` | Read file | `sora cat my-repo README.md` |
| `push` | Upload files | `sora push my-repo ./folder` |
| `rm` | Delete files | `sora rm my-repo old-file.txt` |
| `pull` | Download repo | `sora pull my-repo --dest ./dl` |
| `branches` | List branches | `sora branches my-repo` |

---

## 💡 Usage Examples

### Example 1: Create and Setup a New Project

```bash
# Create a new private repository
sora create my-new-project --private --desc "My awesome new project"

# Upload your project files
sora push my-new-project ./my-project -m "Initial commit"

# Verify the upload
sora ls my-new-project
```

### Example 2: Download and Explore a Repository

```bash
# Download repository
sora pull username/repo --dest ./my-downloads

# View repository statistics
sora stats username/repo

# List branches
sora branches username/repo

# Read a specific file
sora cat username/repo package.json
```

### Example 3: Update Repository Settings

```bash
# Update description
sora update my-repo --desc "A better description"

# Make repository public
sora update my-repo --public

# Rename repository
sora rename old-name new-name
```

### Example 4: Clean Up Old Files

```bash
# List repository contents
sora ls my-repo

# Delete old files
sora rm my-repo old-folder --force
sora rm my-repo deprecated.txt
```

### Example 5: Bulk Operations

```bash
# Upload entire project folder
sora push my-repo ./my-project -m "Upload all project files"

# Download multiple repos (using loop)
for repo in repo1 repo2 repo3; do
  sora pull $repo --dest ./backups/$repo
done
```

---

## 🎨 Output Examples

### Beautiful Terminal Output

```bash
$ sora repos --limit 3

ℹ Fetching your repositories (all)...

📚 Your Repositories (3)
────────────────────────────────────────────────────────────
🌍 my-awesome-project [JavaScript] ⭐12
   A cool web application built with React
   https://github.com/username/my-awesome-project

🔒 private-repo [Python]
   Internal project management tool
   https://github.com/username/private-repo

🌍 sora-cli [Python] ⭐5
   GitHub CLI manager
   https://github.com/username/sora-cli
────────────────────────────────────────────────────────────
```

```bash
$ sora stats my-repo

ℹ Fetching statistics for 'username/my-repo'...

📊 Statistics for username/my-repo
──────────────────────────────────────────────────────────────
  General:
    Description:  My awesome repository
    Visibility:   🌍 Public
    Created:      2024-01-15
    Updated:      2024-12-17
    Size:         2.45 MB
    Language:     Python

  Engagement:
    ⭐ Stars:      42
    👁  Watchers:   12
    🔱 Forks:      8
    ⚠  Issues:     3

  Branches:
    Default:      main

  URLs:
    Web:          https://github.com/username/my-repo
    Clone:        https://github.com/username/my-repo.git
──────────────────────────────────────────────────────────────
```

---

## ⚙️ Configuration

### Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `GITHUB_TOKEN` | Your GitHub Personal Access Token | `ghp_xxxxxxxxxxxxx` |

### Setting the Token

**Option 1: Use the built-in command (Windows)**
```bash
sora --set-token YOUR_TOKEN
```

**Option 2: Set environment variable manually**

**Windows (PowerShell):**
```powershell
[System.Environment]::SetEnvironmentVariable('GITHUB_TOKEN', 'your_token', 'User')
```

**Linux/macOS (add to ~/.bashrc or ~/.zshrc):**
```bash
export GITHUB_TOKEN="your_token_here"
```

---

## 🤝 Contributing

We love contributions! Whether it's bug reports, feature requests, or code improvements, all contributions are welcome.

### How to Contribute

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/amazing-feature`)
3. **Commit your changes** (`git commit -m 'Add amazing feature'`)
4. **Push to the branch** (`git push origin feature/amazing-feature`)
5. **Open a Pull Request**

### Reporting Issues

Found a bug or have a suggestion? Please [open an issue](https://github.com/MrTG-CodeBot/sora-github-cli/issues/new) with:

- 🐛 Clear description of the bug
- 📝 Steps to reproduce
- 💻 Expected vs actual behavior
- 🖼️ Screenshots (if applicable)

### Feature Requests

Have an idea for a new feature? We'd love to hear it! [Create a feature request](https://github.com/MrTG-CodeBot/sora-github-cli/issues/new) and describe:

- 🎯 What problem it solves
- 💡 How it should work
- 🌟 Why it's useful

---

## 📋 Requirements

- **Python:** 3.6 or higher
- **Dependencies:**
  - `requests` - For GitHub API calls
- **GitHub:** Personal Access Token with `repo` scope

---

## 🐛 Troubleshooting

### Common Issues

#### "Invalid token or connection issue"
- **Solution:** Check your GitHub token is valid and has `repo` permissions
- Re-generate token at: https://github.com/settings/tokens

#### "Repository not found"
- **Solution:** Check the spelling (GitHub is case-sensitive)
- Ensure you have access to the repository

#### "File too large (>100MB)"
- **Solution:** GitHub has a 100MB file size limit
- Consider using Git LFS for large files

#### "Connection error"
- **Solution:** Check your internet connection
- Sora will automatically retry with exponential backoff

---

## 📜 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2024 MrTG-CodeBot

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```

---

## 🎯 Roadmap

### Planned Features

- [ ] 🔍 Search repositories
- [ ] 📌 Pin/unpin repositories
- [ ] 🏷️ Manage repository topics
- [ ] 👥 Manage collaborators
- [ ] 🔑 SSH key management
- [ ] 📊 Advanced analytics
- [ ] 🔔 Notifications support
- [ ] 🌐 Multi-account support
- [ ] 📱 Config file support
- [ ] 🎨 Customizable themes

---

## 🌟 Show Your Support

If you find Sora useful, please consider:

- ⭐ **Starring the repository**
- 🐦 **Sharing with others**
- 💬 **Providing feedback**
- 🤝 **Contributing to the project**

---

## 👨‍💻 Author

**MrTG-CodeBot**

- 🌐 Website: [amalnath.netlify.app](https://amalnath.netlify.app/)
- 🐙 GitHub: [@MrTG-CodeBot](https://github.com/MrTG-CodeBot)
- 📧 Email: [Create an issue](https://github.com/MrTG-CodeBot/sora-github-cli/issues)

---

## 🙏 Acknowledgments

- Thanks to all [contributors](https://github.com/MrTG-CodeBot/sora-github-cli/graphs/contributors)
- Inspired by the need for a simple, powerful GitHub CLI tool
- Built with ❤️ using Python and GitHub API

---

## 📚 Related Projects

- [GitHub CLI (gh)](https://cli.github.com/) - Official GitHub CLI
- [hub](https://hub.github.com/) - Git wrapper for GitHub

---

## 📞 Support

Need help? We're here for you!

- 📖 **Documentation:** [View Docs](https://mrtg-codebot.github.io/sora-github-cli/)
- 🐛 **Issues:** [Report a Bug](https://github.com/MrTG-CodeBot/sora-github-cli/issues)
- 💬 **Discussions:** [Join the Discussion](https://github.com/MrTG-CodeBot/sora-github-cli/discussions)
- 🌐 **Website:** [amalnath.netlify.app](https://amalnath.netlify.app/)

---

<div align="center">
**[⬆ Back to Top](#-sora---github-cli-manager)**

</div>

