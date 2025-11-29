# GitHub CLI Manager - Usage Guide

This script provides a command-line interface for interacting with GitHub.

## Setup

### 1. Set your GitHub Personal Access Token

It is highly recommended to set your GitHub Personal Access Token as an environment variable named `GITHUB_TOKEN`. This token is required for authentication with the GitHub API.

```powershell
$env:GITHUB_TOKEN="YOUR_GITHUB_TOKEN"
```

Replace `"YOUR_GITHUB_TOKEN"` with your actual GitHub Personal Access Token. For persistent storage, you can add this line to your PowerShell profile (type `$profile` in PowerShell to find its location).

Alternatively, you can provide the token with each command using the `--token` argument.

### 2. Add the script to your System PATH (Windows)

To be able to run `sora` commands directly from any terminal window, you need to add the directory containing the `sora` script to your system's `PATH` environment variable. This needs to be done once after cloning the repository.

1.  **Open PowerShell as Administrator:**
    *   Search for "PowerShell" in the Start menu.
    *   Right-click on "Windows PowerShell" and select "Run as administrator".

2.  **Navigate to your cloned repository directory:**
    ```powershell
    cd C:\Users\amaln\Downloads\github_cmd
    ```
    (Replace `C:\Users\amaln\Downloads\github_cmd` with the actual path to your cloned `github_cmd` directory.)

3.  **Add the current directory to your system's `PATH` permanently:**
    Execute the following command in the *Administrator PowerShell*:

    ```powershell
    [Environment]::SetEnvironmentVariable("Path", "$([Environment]::GetEnvironmentVariable("Path", "Machine"));$((Get-Location).Path)", "Machine")
    ```
    This command appends the current directory's full path to the system-wide `PATH` environment variable.

4.  **Restart PowerShell:**
    Close and reopen any PowerShell windows for the changes to take effect.

## Commands

*   **`create <name> [--private] [--desc DESCRIPTION]`**
    *   **Use:** Creates a new GitHub repository.
    *   **Example:**
        ```bash
        sora create my-new-repo --private --desc "My awesome private project"
        ```

*   **`view <name>`**
    *   **Use:** Displays details about a specific GitHub repository.
    *   **Example:**
        ```bash
        sora view my-new-repo
        ```

*   **`delete <name>`**
    *   **Use:** Deletes a GitHub repository. **This action is irreversible.**
    *   **Example:**
        ```bash
        sora delete my-old-repo
        ```

*   **`visibility <name> [--public | --private]`**
    *   **Use:** Changes the visibility of a repository (public or private).
    *   **Example:**
        ```bash
        sora visibility my-repo --public
        ```

*   **`upload <repo> <path> [--target TARGET_PATH]`**
    *   **Use:** Uploads a file or a folder to a specified repository.
    *   **Examples:**
        ```bash
        # Upload a single file
        sora upload my-repo my_local_file.txt --target docs/my_remote_file.txt

        # Upload a folder
        sora upload my-repo my_local_folder --target project-files
        ```

*   **`add-all <repo>`**
    *   **Use:** Uploads all files in the current directory (and its subdirectories, excluding common ignored directories) to the specified repository.
    *   **Example:**
        ```bash
        sora add-all my-repo
        ```

*   **`rm-file <repo> <path>`**
    *   **Use:** Deletes a specific file from a repository.
    *   **Example:**
        ```bash
        sora rm-file my-repo docs/old_file.txt
        ```
