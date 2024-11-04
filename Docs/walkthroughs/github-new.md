# Creating a New GitHub Account and Setting Up a Simple Development Environment for Node.js and TypeScript

This guide provides a step-by-step walkthrough for creating a GitHub account, setting up a development environment for Node.js and TypeScript, and configuring a Git client on Windows, macOS, Linux, and Android phones using Termux.

## Table of Contents
- [Creating a New GitHub Account and Setting Up a Simple Development Environment for Node.js and TypeScript](#creating-a-new-github-account-and-setting-up-a-simple-development-environment-for-nodejs-and-typescript)
  - [Table of Contents](#table-of-contents)
  - [Creating a GitHub Account](#creating-a-github-account)
    - [Visit GitHub:](#visit-github)
    - [Sign Up:](#sign-up)
    - [Verify Your Account:](#verify-your-account)
    - [Choose a Plan:](#choose-a-plan)
    - [Complete Setup:](#complete-setup)
    - [Set Up Your Profile (Optional):](#set-up-your-profile-optional)
  - [Setting Up the Development Environment](#setting-up-the-development-environment)
    - [Windows](#windows)
    - [macOS](#macos)
    - [Linux](#linux)
    - [Android (Termux)](#android-termux)
  - [Setting Up a Git Client](#setting-up-a-git-client)
    - [Windows](#windows-1)
    - [macOS](#macos-1)
    - [Linux](#linux-1)
    - [Android (Termux)](#android-termux-1)
  - [Basic Git Usage Guide](#basic-git-usage-guide)
  - [Resources](#resources)

## Creating a GitHub Account

### Visit GitHub:
- Go to GitHub's website.

### Sign Up:
- Click on the Sign up button in the top right corner.
- Enter your email address, choose a password, and select a username.

### Verify Your Account:
- Follow the on-screen instructions to verify your email address.

### Choose a Plan:
- Select a plan (Free is sufficient for most users).

### Complete Setup:
- Fill in additional information as prompted, such as your interests and whether you want to receive updates.

### Set Up Your Profile (Optional):
- You can add a profile picture and bio later.

## Setting Up the Development Environment

### Windows

1. Install Node.js:
   - Download the Windows installer from the Node.js official website.
   - Run the installer and follow the setup steps. Ensure you install npm (Node Package Manager).

2. Verify Installation (in Command Prompt or PowerShell):
   ```bash
   node -v
   npm -v
   ```

3. Install TypeScript:
   ```bash
   npm install -g typescript
   ```

4. Set Up a Simple Project:
   ```bash
   mkdir my-project
   cd my-project
   npm init -y
   tsc --init
   ```

### macOS

1. Install Homebrew (if not installed):
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. Install Node.js:
   ```bash
   brew install node
   ```

3. Verify Installation:
   ```bash
   node -v
   npm -v
   ```

4. Install TypeScript:
   ```bash
   npm install -g typescript
   ```

5. Set Up a Simple Project:
   ```bash
   mkdir my-project
   cd my-project
   npm init -y
   tsc --init
   ```

### Linux

1. Update Package List:
   ```bash
   sudo apt update
   ```

2. Install Node.js:
   ```bash
   sudo apt install nodejs npm
   ```

3. Verify Installation:
   ```bash
   node -v
   npm -v
   ```

4. Install TypeScript:
   ```bash
   npm install -g typescript
   ```

5. Set Up a Simple Project:
   ```bash
   mkdir my-project
   cd my-project
   npm init -y
   tsc --init
   ```

### Android (Termux)

1. Install Termux:
   - Download Termux from the F-Droid or Google Play Store.

2. Update Packages:
   ```bash
   pkg update
   pkg upgrade
   ```

3. Install Node.js:
   ```bash
   pkg install nodejs
   ```

4. Verify Installation:
   ```bash
   node -v
   npm -v
   ```

5. Install TypeScript:
   ```bash
   npm install -g typescript
   ```

6. Set Up a Simple Project:
   ```bash
   mkdir my-project
   cd my-project
   npm init -y
   tsc --init
   ```

## Setting Up a Git Client

### Windows

1. Install Git:
   - Download the Git installer from the Git official website.
   - Run the installer and select default options unless you have specific preferences.

2. Verify Installation:
   ```bash
   git --version
   ```

3. Configure Git:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your_email@example.com"
   ```

### macOS

1. Install Git:
   ```bash
   brew install git
   ```

2. Verify Installation:
   ```bash
   git --version
   ```

3. Configure Git:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your_email@example.com"
   ```

### Linux

1. Install Git:
   ```bash
   sudo apt install git
   ```

2. Verify Installation:
   ```bash
   git --version
   ```

3. Configure Git:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your_email@example.com"
   ```

### Android (Termux)

1. Install Git:
   ```bash
   pkg install git
   ```

2. Verify Installation:
   ```bash
   git --version
   ```

3. Configure Git:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your_email@example.com"
   ```

## Basic Git Usage Guide

1. Initialize a Repository
   ```bash
   git init
   ```

2. Add Files
   ```bash
   git add filename        # Add a specific file
   git add .               # Add all files in the current directory
   ```

3. Commit Changes
   ```bash
   git commit -m "Your commit message"
   ```

4. Check Status
   ```bash
   git status
   ```

5. View Commit History
   ```bash
   git log
   ```

6. Branching
   ```bash
   git checkout -b new-branch-name    # Create and switch to new branch
   git checkout main                  # Switch back to main branch
   ```

7. Merging Branches
   ```bash
   git merge branch-name
   ```

8. Cloning a Repository
   ```bash
   git clone https://github.com/username/repository.git
   ```

9. Pushing Changes
   ```bash
   git push origin branch-name
   ```

10. Pulling Changes
    ```bash
    git pull origin branch-name
    ```

## Resources
- Node.js Official Website
- TypeScript Official Website
- Git Official Documentation
- GitHub Docs
- Termux Wiki

This guide should provide you with a solid foundation for creating a GitHub account, setting up your development environment for Node.js and TypeScript, configuring a Git client, and using Git effectively across different platforms.