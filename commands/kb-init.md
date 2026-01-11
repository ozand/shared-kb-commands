---
allowed-tools: Bash(git *), Bash(mkdir *), Read, Write, Edit
description: Initialize Shared Knowledge Base in the current project
---

## Context
- Current directory: !`pwd`
- Git repository status: !`git status`
- Current user: !`whoami`

## Your task
Initialize Shared Knowledge Base in this project by following these steps:

### Step 1: Create .kb/ directory structure
```bash
mkdir -p .kb/context .kb/project/knowledge .kb/project/pending
```

### Step 2: Add Shared KB as git submodule
```bash
git submodule add https://github.com/ozand/shared-knowledge-base.git .kb/shared
git submodule update --init --recursive
```

### Step 3: Create PROJECT.yaml template
Create `.kb/context/PROJECT.yaml` with this template:
```yaml
meta:
  name: "Project Name"
  id: "project-slug"

stack:
  language: "python"
  framework: ""

sharing_criteria:
  universal_if:
    - "Generic Pattern"
    - "Library Fix"
    - "Tooling"
  project_specific_if:
    - "Business Logic"
    - "Secrets"
    - "Internal URLs"
```

### Step 4: Copy session-start hook
```bash
mkdir -p .claude/hooks
cp .kb/shared/.claude/hooks/session-start-kb-check.py .claude/hooks/
```

### Step 5: Commit changes
```bash
git add .kb .claude .gitmodules
git commit -m "Chore: Initialize Shared KB v5.1 integration"
```

Execute these steps using the Bash tool. After completion, inform the user that Shared KB has been successfully initialized.
