# GitHub CLI Manager - Usage Guide

This script provides a command-line interface for interacting with GitHub.

## Setup

### 1. GitHub Personal Access Token (`GITHUB_TOKEN`)

To use this CLI, you need a GitHub Personal Access Token (PAT). This token is required for authentication with the GitHub API and should have the necessary `repo` scopes to manage your repositories.

#### How to get a GitHub Personal Access Token:
1.  Go to your GitHub account `Settings`.
2.  In the left sidebar, click on `Developer settings`.
3.  Click on `Personal access tokens` -> `Tokens (classic)`.
4.  Click `Generate new token`.
5.  Give your token a descriptive name (e.g., "sora-cli-token").
6.  **Select the `repo` scope** (this grants full control of private and public repositories, which is needed for all CLI functions). You may also want to select `workflow` if you plan to update GitHub Actions workflows.
7.  Click `Generate token`.
8.  **Copy the generated token immediately!** You will not be able to see it again.

#### Where to add the `GITHUB_TOKEN`:

It is highly recommended to set your GitHub Personal Access Token as an environment variable named `GITHUB_TOKEN`.

*   **Temporarily (for the current PowerShell session):**
    ```powershell
    $env:GITHUB_TOKEN="YOUR_GITHUB_TOKEN"
    ```
    Replace `"YOUR_GITHUB_TOKEN"` with your actual GitHub Personal Access Token.

*   **Persistently (across PowerShell sessions):**
    Add the line above to your PowerShell profile. To find your profile path, type `$profile` in PowerShell. If the file doesn't exist, create it using `New-Item -Path $profile -ItemType File -Force`.

Alternatively, you can provide the token with each command using the `--token` argument: `python sora --token YOUR_GITHUB_TOKEN view my-repo`.

### 2. Add the script's folder path to the System PATH (Windows)

To be able to run `sora` commands directly from any terminal window without prefixing `python`, you need to add the directory containing the `sora` script to your system's `PATH` environment variable. This needs to be done once after cloning the repository.

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

### 3. Add the `sora` function to your PowerShell Profile (`Microsoft.PowerShell_profile.ps1`)

To seamlessly run `sora {command}` directly in PowerShell (without needing to type `python sora`), add the following function to your PowerShell profile file.

1.  **Open your PowerShell profile:**
    In your PowerShell terminal, type `$profile` and press `Enter`. This will show you the full path to your profile file (e.g., `C:\Users\YourUsername\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1`).

2.  **Create the profile file if it doesn't exist:**
    If the file path returned by `$profile` indicates the file doesn't exist, create it using:
    ```powershell
    New-Item -Path $profile -ItemType File -Force
    ```

3.  **Edit the profile file:**
    Open the profile file in a text editor.

4.  **Add the `sora` function:**
    Paste the following function block into the end of your profile file:
    ```powershell
    function sora {
        python C:\Users\amaln\Downloads\github_cmd\sora @args
    }
    ```
    **Important:** Ensure `C:\Users\amaln\Downloads\github_cmd\sora` is the **correct and absolute path** to your `sora` script.

5.  **Save the file and restart PowerShell:**
    Save the changes to the profile file, then close and reopen all your PowerShell windows for the function to be loaded.

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
