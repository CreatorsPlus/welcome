# Creating a New GitHub Account and Development Environment Setup

A comprehensive guide for setting up GitHub, Node.js, and TypeScript across different platforms.

## Table of Contents
- [Creating a New GitHub Account and Development Environment Setup](#creating-a-new-github-account-and-development-environment-setup)
  - [Table of Contents](#table-of-contents)
  - [Creating a GitHub Account](#creating-a-github-account)
    - [Visit GitHub](#visit-github)
    - [Sign Up](#sign-up)
    - [Complete Setup](#complete-setup)
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
    - [Essential Commands](#essential-commands)
    - [Branch Operations](#branch-operations)
    - [Remote Operations](#remote-operations)
  - [Resources](#resources)

## Creating a GitHub Account

### Visit GitHub
1. Go to [GitHub's website](https://github.com)

### Sign Up
1. Click the "Sign up" button in the top right corner
2. Enter your email address
3. Choose a password
4. Select a username

### Complete Setup
1. Verify your email address following on-screen instructions
2. Choose a plan (Free is sufficient for most users)
3. Fill in additional information as prompted
4. Optional: Add a profile picture and bio

## Setting Up the Development Environment

### Windows

1. **Install Node.js**
   ```bash
   # Download from Node.js official website
   # Run installer and follow setup steps
   
   # Verify installation
   node -v
   npm -v
   ```

2. **Install TypeScript**
   ```bash
   npm install -g typescript
   ```

3. **Set Up Project**
   ```bash
   mkdir my-project
   cd my-project
   npm init -y
   tsc --init
   ```

### macOS

1. **Install Homebrew**
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. **Install Node.js**
   ```bash
   brew install node
   
   # Verify installation
   node -v
   npm -v
   ```

3. **Install TypeScript**
   ```bash
   npm install -g typescript
   ```

4. **Set Up Project**
   ```bash
   mkdir my-project
   cd my-project
   npm init -y
   tsc --init
   ```

### Linux

1. **Update Package List**
   ```bash
   sudo apt update
   ```

2. **Install Node.js**
   ```bash
   sudo apt install nodejs npm
   
   # Verify installation
   node -v
   npm -v
   ```

3. **Install TypeScript**
   ```bash
   npm install -g typescript
   ```

4. **Set Up Project**
   ```bash
   mkdir my-project
   cd my-project
   npm init -y
   tsc --init
   ```

### Android (Termux)

1. **Install Termux** from F-Droid or Google Play Store

2. **Update Packages**
   ```bash
   pkg update
   pkg upgrade
   ```

3. **Install Node.js**
   ```bash
   pkg install nodejs
   
   # Verify installation
   node -v
   npm -v
   ```

4. **Install TypeScript**
   ```bash
   npm install -g typescript
   ```

5. **Set Up Project**
   ```bash
   mkdir my-project
   cd my-project
   npm init -y
   tsc --init
   ```

## Setting Up a Git Client

### Windows
1. Download Git installer from the [Git official website](https://git-scm.com/)
2. Run installer with default options
3. Configure Git:
   ```bash
   git --version
   git config --global user.name "Your Name"
   git config --global user.email "your_email@example.com"
   ```

### macOS
```bash
# Install Git via Homebrew
brew install git

# Verify and configure
git --version
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

### Linux
```bash
# Install Git
sudo apt install git

# Verify and configure
git --version
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

### Android (Termux)
```bash
# Install Git
pkg install git

# Verify and configure
git --version
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

## Basic Git Usage Guide

### Essential Commands

1. **Initialize Repository**
   ```bash
   git init
   ```

2. **Add Files**
   ```bash
   git add filename    # Add specific file
   git add .           # Add all files
   ```

3. **Commit Changes**
   ```bash
   git commit -m "Your commit message"
   ```

4. **Check Status**
   ```bash
   git status
   ```

5. **View History**
   ```bash
   git log
   ```

### Branch Operations

1. **Create & Switch Branches**
   ```bash
   git checkout -b new-branch-name    # Create and switch
   git checkout main                  # Switch to main
   ```

2. **Merge Branches**
   ```bash
   git merge branch-name
   ```

### Remote Operations

1. **Clone Repository**
   ```bash
   git clone https://github.com/username/repository.git
   ```

2. **Push Changes**
   ```bash
   git push origin branch-name
   ```

3. **Pull Changes**
   ```bash
   git pull origin branch-name
   ```

## Resources

- [Node.js Official Website](https://nodejs.org/)
- [TypeScript Official Website](https://www.typescriptlang.org/)
- [Git Official Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com/)
- [Termux Wiki](https://wiki.termux.com/)