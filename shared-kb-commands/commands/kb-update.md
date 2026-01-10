---
allowed-tools: Bash(git *), Bash(python *)
description: Update Shared Knowledge Base to the latest version
---

## Context
- Current directory: !`pwd`
- KB status: !`git -C .kb/shared log -1 --oneline`

## Your task
Update Shared Knowledge Base in this project:

### Step 1: Check if KB is installed
First, verify that `.kb/shared/` exists. If not, inform the user that KB is not installed and they should run `/kb-init` first.

### Step 2: Update submodule
```bash
git submodule update --remote .kb/shared
```

### Step 3: Rebuild index (if needed)
```bash
cd .kb/shared && python tools/kb.py index --force && cd -
```

### Step 4: Show update summary
```bash
git -C .kb/shared log -1 --oneline
```

Execute these steps using the Bash tool. After completion, inform the user that Shared KB has been successfully updated.
