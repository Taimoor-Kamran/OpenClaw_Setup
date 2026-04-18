# Pushing This to GitHub

This guide explains how to push your OpenClaw setup documentation to a GitHub repository.

---

## Prerequisites

- Git installed (`git --version` to check)
- A GitHub account
- GitHub CLI installed, OR an SSH key/personal access token set up

---

## If You Are Starting Fresh (No Local Repo Yet)

```bash
cd ~/openclaw-setup

# Initialize a git repo
git init

# Add all files
git add .

# Create the first commit
git commit -m "initial commit: openclaw setup docs"

# Link to your GitHub repo
git remote add origin https://github.com/Taimoor-Kamran/OpenClaw_Setup.git

# Push
git push -u origin main
```

---

## If the Repo Already Exists Locally

```bash
cd ~/openclaw-setup

# Stage all new and changed files
git add .

# Commit with a message
git commit -m "add full documentation"

# Push to GitHub
git push
```

---

## Authenticating with GitHub

When you run `git push` for the first time, GitHub will ask for credentials.

### Option A — GitHub CLI (Easiest)

```bash
# Install GitHub CLI
sudo apt install gh

# Login
gh auth login
```

Follow the prompts. Choose **HTTPS** and authenticate via browser.

### Option B — Personal Access Token

1. Go to GitHub → Settings → Developer Settings → Personal Access Tokens → Tokens (classic)
2. Click **Generate new token**
3. Give it a name, set expiry, and check the **repo** scope
4. Copy the token

When git asks for your password, paste the token instead of your GitHub password.

### Option C — SSH Key

```bash
# Generate a key (skip if you already have one)
ssh-keygen -t ed25519 -C "your-email@example.com"

# Copy the public key
cat ~/.ssh/id_ed25519.pub
```

Paste it into GitHub → Settings → SSH and GPG Keys → New SSH Key.

Then change your remote to SSH:

```bash
git remote set-url origin git@github.com:Taimoor-Kamran/OpenClaw_Setup.git
```

---

## Checking What Will Be Pushed

```bash
# See what files changed
git status

# See what the changes look like
git diff

# See commit history
git log --oneline
```

---

## Updating Docs Later

Whenever you update a file:

```bash
git add docs/whatsapp.md       # add specific file
# OR
git add .                       # add everything

git commit -m "update whatsapp troubleshooting steps"
git push
```

---

## Repo Link

This project is hosted at:
**https://github.com/Taimoor-Kamran/OpenClaw_Setup**
