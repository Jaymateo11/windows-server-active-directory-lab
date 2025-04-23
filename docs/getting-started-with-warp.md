# Getting Started with Warp.dev on Windows

## Prerequisites
- Windows 10 or 11  
- PowerShell 7.2 or later  
- WSL2 (e.g., Ubuntu) enabled and installed  
- Git Bash (optional, for Git workflows)

## Installing Warp
1. Download the latest Windows installer from https://warp.dev/download  
2. Right‑click the installer and choose **Run as administrator**  
3. Follow the prompts to complete installation  
4. Launch Warp from the Start menu

## Configuring Shells in Warp
1. In Warp, open **Settings** (gear icon) → **Preferences** → **Shells**  
2. Add or select:
   - **PowerShell 7+** (path: `C:\Program Files\PowerShell\7\pwsh.exe`)
   - **WSL** (choose your WSL distribution)
   - **Git Bash** (path: `C:\Program Files\Git\bin\bash.exe`)
3. Set your preferred default shell

## Enabling Beta Features
1. In **Settings** → **Features**  
2. Toggle on:
   - **Warp Drive** (for Workflows & Drive integration)
   - **Notebooks**
   - **AI Assist**

## Connecting Your Repository
1. Clone the lab repo if needed:
   ```powershell
   git clone https://github.com/Jaymateo11/windows-server-active-directory-lab.git
   ```
2. In Warp, click **Open Folder** and select the cloned repository directory  
3. Verify Git is configured:
   ```powershell
   git config user.name    # should output Jaymateo11
   git config user.email   # should output jatnielmateo3@gmail.com
   ```
4. In the Warp sidebar, click the **Drive** icon  
5. Click **Add Folder to Drive** and select your repo folder  
6. Confirm that the repo appears under **Warp Drive**

Once complete, you can start using Workflows, Notebooks, and AI features within this repository.

# Getting Started with Warp.dev on Windows

**Prerequisites**
- Windows 10 or 11
- PowerShell 7 or later
- WSL2 with a Linux distribution (e.g., Ubuntu) installed and set to WSL2
- Git Bash (from Git for Windows) installed (optional)

**Installation Steps**
1. Download the Warp installer for Windows from https://warp.dev/download
2. Right‑click the downloaded installer and choose **"Run as administrator"**
3. Follow the installer prompts to complete the installation

**Configuring Default Shells**
- Open Warp, go to **Settings** → **Startup**, and choose your default shell:
  - **PowerShell**: Select "PowerShell"
  - **WSL**: Ensure WSL2 is installed (`wsl --set-default-version 2`) and select your distribution (e.g., "Ubuntu")
  - **Git Bash**: Install Git for Windows and point Warp to the Git Bash executable
- Close and reopen Warp to apply changes

**Enabling Warp Drive, Notebooks, and AI**
1. In Warp, navigate to **Settings** → **Beta Features**
2. Enable:
   - Warp Drive
   - Notebooks
   - AI
3. Restart Warp if prompted

**Connecting Your Repository to Warp Drive**
1. If you haven’t already cloned the repository:
   ```bash
   git clone https://github.com/Jaymateo11/windows-server-active-directory-lab.git
   ```
2. In Warp, click **Open Folder** and select the local `windows-server-active-directory-lab` directory
3. In the Warp sidebar under **Drive**, verify that `windows-server-active-directory-lab` appears. If not, click **Link Folder to Drive** to add it

