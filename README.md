# GitHub CLI Manager - Usage Guide

First, set your GitHub Personal Access Token:

```powershell
$env:GITHUB_TOKEN="YOUR_GITHUB_TOKEN"
```

This script provides a command-line interface for interacting with GitHub.

**Global Argument:**
  `--token`: Your GitHub Personal Access Token. This is required for authentication and can also be set via the `GITHUB_TOKEN` environment variable.

**Commands:**

*   **`create <name> [--private] [--desc DESCRIPTION]`**
    *   **Use:** Creates a new GitHub repository.
    *   **Example:**
        ```bash
        python git_hub.py --token YOUR_GITHUB_TOKEN create my-new-repo --private --desc "My awesome private project"
        ```

*   **`view <name>`**
    *   **Use:** Displays details about a specific GitHub repository.
    *   **Example:**
        ```bash
        python git_hub.py --token YOUR_GITHUB_TOKEN view my-new-repo
        ```

*   **`delete <name>`**
    *   **Use:** Deletes a GitHub repository. **This action is irreversible.**
    *   **Example:**
        ```bash
        python git_hub.py --token YOUR_GITHUB_TOKEN delete my-old-repo
        ```

*   **`visibility <name> [--public | --private]`**
    *   **Use:** Changes the visibility of a repository (public or private).
    *   **Example:**
        ```bash
        python git_hub.py --token YOUR_GITHUB_TOKEN visibility my-repo --public
        ```

*   **`upload <repo> <path> [--target TARGET_PATH]`**
    *   **Use:** Uploads a file or a folder to a specified repository.
    *   **Examples:**
        ```bash
        # Upload a single file
        python git_hub.py --token YOUR_GITHUB_TOKEN upload my-repo my_local_file.txt --target docs/my_remote_file.txt

        # Upload a folder
        python git_hub.py --token YOUR_GITHUB_TOKEN upload my-repo my_local_folder --target project-files
        ```

*   **`add-all <repo>`**
    *   **Use:** Uploads all files in the current directory (and its subdirectories, excluding common ignored directories) to the specified repository.
    *   **Example:**
        ```bash
        python git_hub.py --token YOUR_GITHUB_TOKEN add-all my-repo
        ```

*   **`rm-file <repo> <path>`**
    *   **Use:** Deletes a specific file from a repository.
    *   **Example:**
        ```bash
        python git_hub.py --token YOUR_GITHUB_TOKEN rm-file my-repo docs/old_file.txt
        ```
