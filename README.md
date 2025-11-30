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

### Global Arguments (can be used with or without a subcommand)

*   **`--version`**
    *   **Use:** Displays the version of the GitHub CLI Manager.
    *   **Example:**
        ```bash
        sora --version
        ```

*   **`--check-account`**
    *   **Use:** Shows the GitHub username of the currently connected account.
    *   **Example:**
        ```bash
        sora --check-account
        ```

*   **`--show-local-repo`**
    *   **Use:** Detects and displays the GitHub repository name that the current local Git repository is connected to.
    *   **Important:** This command must be run within a directory that is a Git repository (i.e., contains a `.git` folder) and has a remote origin configured. If not, it will display an error.
    *   **Example:**
        ```bash
        # Navigate to your local Git repository first
        cd C:\path\to\your\repo
        sora --show-local-repo
        ```

### Subcommands

*   **`create <name> [--private] [--desc DESCRIPTION]`**
    *   **Use:** Creates a new GitHub repository.
    *   **Arguments:**
        *   `<name>`: The name of the new repository.
        *   `--private` (optional): Makes the repository private.
        *   `--desc` (optional): Provides a description for the repository.
    *   **Example:**
        ```bash
        sora create my-new-repo --private --desc "My awesome private project"
        ```

*   **`view <name>`**
    *   **Use:** Displays details about a specific GitHub repository.
    *   **Arguments:**
        *   `<name>`: The name of the repository to view.
    *   **Example:**
        ```bash
        sora view my-new-repo
        ```

*   **`delete <name>`**
    *   **Use:** Deletes a GitHub repository. **This action is irreversible.**
    *   **Arguments:**
        *   `<name>`: The name of the repository to delete.
    *   **Example:**
        ```bash
        sora delete my-old-repo
        ```

*   **`visibility <name> [--public | --private]`**
    *   **Use:** Changes the visibility of a repository (public or private).
    *   **Arguments:**
        *   `<name>`: The name of the repository.
        *   `--public`: Makes the repository public.
        *   `--private`: Makes the repository private.
    *   **Example:**
        ```bash
        sora visibility my-repo --public
        ```

*   **`upload <repo> [path] [--target TARGET_PATH] [-m MESSAGE]`**
    *   **Use:** Uploads a file, a folder, or the entire current directory to a specified repository. If `path` is omitted, it defaults to uploading the current directory (`.`).
    *   **Arguments:**
        *   `<repo>`: The name of the target repository.
        *   `[path]` (optional): Local file or folder path. Use '.' to upload the current directory.
        *   `--target` (optional): The target path inside the repository where the file/folder will be uploaded. If not provided, the file/folder will be uploaded to the root of the repository.
        *   `-m, --message` (optional): A custom commit message for the upload. If not provided, a default message like "Update <filename>" or "Create <filename>" will be used.
    *   **Examples:**
        ```bash
        # Upload all files in the current directory with a custom message
        sora upload my-repo -m "Initial commit of project files"

        # Upload a single file to the repository root with a custom message
        sora upload my-repo my_local_file.txt -m "Add important configuration file"

        # Upload a single file to a specific path within the repo with a custom message
        sora upload my-repo my_local_file.txt --target docs/my_remote_file.txt -m "Update documentation"

        # Upload a local folder to the repository root with a custom message
        sora upload my-repo my_local_folder -m "Upload new feature folder"

        # Upload a local folder to a specific path within the repo with a custom message
        sora upload my-repo my_local_folder --target project-files -m "Sync project files"
        ```

*   **`rm <repo> <path>`**
    *   **Use:** Deletes a file or recursively deletes a folder from the specified repository.
    *   **Arguments:**
        *   `<repo>`: The name of the target repository.
        *   `<path>`: The path of the file or folder inside the repository to delete.
    *   **Examples:**
        ```bash
        # Delete a single file
        sora rm my-repo docs/old_file.txt

        # Delete a folder (and its contents) recursively
        sora rm my-repo old-folder
        ```
