# ISOFlex Hub - Git Setup Guide

## 📋 Prerequisites

Make sure you have:
- Git installed: `git --version`
- GitHub account created
- New repository created on GitHub

---

## 🚀 Initial Setup Commands

### Step 1: Organize Your Files

First, create a new directory and organize files:

```bash
# Create project directory
mkdir isoflex-hub
cd isoflex-hub

# Copy/move your downloaded files here:
# - isoflex-hub.html → rename to index.html
# - 3d-ncm-dashboard.html → rename to 3d.html
# - README.md
# - package.json
# - .gitignore
# - DEPLOYMENT.md
```

### Step 2: Initialize Git

```bash
# Initialize git repository
git init

# Add all files
git add .

# First commit
git commit -m "Initial commit: ISOFlex Manufacturing Hub v1.0"
```

### Step 3: Connect to GitHub

**Replace `YOUR_USERNAME` and `YOUR_REPO` with your actual GitHub username and repo name:**

```bash
# Add remote origin
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git

# Verify remote
git remote -v

# Push to GitHub
git branch -M main
git push -u origin main
```

---

## 📝 Common Git Commands

### Making Changes

```bash
# Check status
git status

# Add specific file
git add filename.html

# Add all changes
git add .

# Commit with message
git commit -m "Add new feature"

# Push to GitHub
git push
```

### Viewing History

```bash
# See commit history
git log

# See recent commits (short)
git log --oneline -10

# See changes in a file
git diff filename.html
```

### Branches (For Future Features)

```bash
# Create new branch
git checkout -b feature/coa-module

# Switch branches
git checkout main

# Merge branch into main
git checkout main
git merge feature/coa-module

# Delete branch after merge
git branch -d feature/coa-module
```

---

## 🔄 Workflow for Updates

### Daily Development Flow:

```bash
# 1. Pull latest changes (if working with others)
git pull

# 2. Make your changes to files
# ... edit code ...

# 3. See what changed
git status
git diff

# 4. Stage changes
git add .

# 5. Commit with descriptive message
git commit -m "Updated NCM module with new filters"

# 6. Push to GitHub (triggers Cloudflare auto-deploy)
git push
```

---

## 🏷️ Versioning Best Practices

### Semantic Versioning

Use tags for releases:

```bash
# Tag current version
git tag -a v1.0.0 -m "Initial release"

# Push tags to GitHub
git push --tags

# List all tags
git tag
```

### Version Format: `v1.0.0`
- **Major** (1.x.x): Breaking changes
- **Minor** (x.1.x): New features, backward compatible
- **Patch** (x.x.1): Bug fixes

---

## 🐛 Troubleshooting

### "Permission denied" error

If you see authentication errors:

**Option 1: HTTPS with Token**
```bash
# Generate personal access token on GitHub:
# Settings → Developer settings → Personal access tokens → Tokens (classic)
# Use token as password when prompted
```

**Option 2: SSH (Recommended)**
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your_email@example.com"

# Copy public key
cat ~/.ssh/id_ed25519.pub

# Add to GitHub: Settings → SSH and GPG keys → New SSH key

# Change remote to SSH
git remote set-url origin git@github.com:YOUR_USERNAME/YOUR_REPO.git
```

### "Repository not found"

```bash
# Check remote URL
git remote -v

# Fix if wrong
git remote set-url origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
```

### Merge Conflicts

```bash
# Pull latest
git pull

# If conflicts, edit files to resolve
# Look for <<<<<<< HEAD markers

# After resolving
git add .
git commit -m "Resolved merge conflicts"
git push
```

---

## 📦 .gitignore Explained

Your `.gitignore` file prevents committing:
- `node_modules/` - Dependencies (reinstall with `npm install`)
- `.env` - Secret keys and passwords
- `dist/` - Build outputs
- `.DS_Store` - Mac system files

---

## 🌿 Branch Strategy (Future)

When your team grows:

### Main Branches:
- `main` - Production code (always deployable)
- `develop` - Integration branch for features

### Feature Branches:
- `feature/coa-upload`
- `feature/silo-monitoring`
- `bugfix/ncm-date-filter`

### Workflow:
1. Create feature branch from `develop`
2. Make changes and commit
3. Open Pull Request to `develop`
4. Review and test
5. Merge to `develop`
6. When stable, merge `develop` to `main`

---

## 🔍 Useful Git Aliases

Add these to `~/.gitconfig` for shortcuts:

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual 'log --oneline --graph --all'
```

Now use: `git st` instead of `git status`, etc.

---

## 📚 Learning Resources

### Git Basics
- Official docs: https://git-scm.com/doc
- Interactive tutorial: https://learngitbranching.js.org/
- Cheat sheet: https://education.github.com/git-cheat-sheet-education.pdf

### GitHub Specific
- GitHub Docs: https://docs.github.com
- Actions (CI/CD): https://github.com/features/actions

---

## ✅ Quick Reference

```bash
# Setup (once)
git init
git remote add origin <URL>
git push -u origin main

# Daily workflow
git pull              # Get updates
git add .             # Stage changes
git commit -m "msg"   # Commit
git push              # Deploy

# Check status anytime
git status
git log --oneline
```

---

**Now give me your GitHub repo URL and I'll give you the exact commands to run!** 🚀
