---
allowed-tools: Bash(git *), Bash(python *)
description: Check Shared Knowledge Base status and available updates
---

## Context
- Current directory: !`pwd`
- KB exists: !`test -d .kb/shared && echo "yes" || echo "no"`

## Your task
Check Shared Knowledge Base status in this project:

### Step 1: Check if KB is installed
```bash
if [ -d ".kb/shared" ]; then
    echo "✅ Installed: True"
else
    echo "❌ Installed: False"
    echo "💡 Run /kb-init to install Shared KB"
    exit 0
fi
```

### Step 2: Get version from CHANGELOG.md
```bash
head -1 .kb/shared/CHANGELOG.md | grep -oP '(?<=\[)\d+\.\d+\.\d+(?=\])'
```

### Step 3: Get entry count
```bash
cd .kb/shared && python tools/kb.py stats | grep "Total Entries:" && cd -
```

### Step 4: Get last update date
```bash
git -C .kb/shared log -1 --format=%ci
```

### Step 5: Check for available updates
```bash
git -C .kb/shared fetch origin
git -C .kb/shared log HEAD..origin/main --oneline | head -5
```

Execute these steps using the Bash tool and display the results in a formatted way.
