---
allowed-tools: Bash, Read, Write, Edit
description: Analyze chat history to extract knowledge from errors and solutions
---

## Your task
Perform a retrospective analysis of the conversation to extract valuable knowledge from errors encountered and solutions implemented.

### Step 1: Analyze the conversation
Review the conversation history and identify:
- **Errors encountered:** Error messages, exceptions, failures
- **Solutions implemented:** Code fixes, configuration changes, workarounds
- **Decisions made:** Technical choices with rationale
- **Lessons learned:** Best practices, patterns discovered
- **Context:** Framework, language, environment details

Focus on extracting:
```
1. Problem → Solution pairs
2. Code examples with explanations
3. Prevention strategies
4. Root cause analysis
```

### Step 2: For each identified knowledge item:

#### A. Check if already exists in KB
```bash
cd .kb/shared && python tools/kb.py search "<error关键词或问题描述>" && cd -
```

#### B. Determine scope
Ask yourself:
- **Is this universal?** (docker, universal, python, postgresql, javascript, vps)
  - Generic pattern applicable across projects?
  - Library/framework tool issue?
  - Best practice or standard approach?

- **Or project-specific?** (project, domain, framework)
  - Business logic specific to this project?
  - Internal URLs, secrets, or infrastructure?
  - Domain-specific knowledge?

Use `sharing_criteria` from `.kb/context/PROJECT.yaml` if available.

### Step 3: Create knowledge entries

For each valuable knowledge item, create a YAML entry following this format:

```yaml
version: "1.0"
category: "category-name"
last_updated: "2026-01-11"

errors:
  - id: "SCOPE-NNN"  # e.g., DOCKER-024, PYTHON-123
    title: "Error Title or Problem Description"
    severity: "high"  # critical | high | medium | low
    scope: "python"   # universal | python | javascript | docker | postgresql | vps
    problem: |
      Detailed description of what went wrong.
      Include error messages, stack traces, and context.
    solution:
      code: |
        # Solution code here
        # Include imports, configuration, etc.
      explanation: |
        How the solution works.
        Why it fixes the problem.
    prevention: |
      How to prevent this issue in the future.
    tags:
      - "keyword1"
      - "keyword2"
```

### Step 4: Save entries

**For Project KB (project-specific):**
```bash
# Save to .kb/project/knowledge/<category>-<name>.yaml
```

**For Shared KB (universal):**
```bash
# Save to .kb/project/pending/<category>-<name>.yaml
# Then submit via GitHub Issue:
python .kb/shared/tools/kb_submit.py \
    --target shared \
    --file .kb/project/pending/<category>-<name>.yaml \
    --title "<title>" \
    --desc "<description>" \
    --domain <scope>
```

### Step 5: Validate entries
```bash
# Validate the created entry
python .kb/shared/tools/kb.py validate <path-to-yaml>
```

### Step 6: Report summary

Provide a formatted summary:

```markdown
## 📊 Retrospective Analysis Complete

### ✅ Knowledge Items Extracted: N

#### 1. [ID] Title
- **Scope:** universal/project
- **Severity:** high/medium/low
- **Saved to:** path/to/file.yaml
- **Action:** Created/Already exists

#### 2. [ID] Title
...

### 📈 Summary
- New entries created: N
- Already documented: N
- Project-specific: N
- Universal candidates: N

### 🎯 Next Steps
1. Review created entries
2. Edit if needed: <paths>
3. Submit universal entries to Shared KB: <commands>
```

## Best Practices

**✅ Extract:**
- Errors with non-obvious solutions
- Solutions that required research/debugging
- Configuration patterns that work
- Best practices discovered
- Anti-patterns to avoid

**❌ Skip:**
- Trivial issues (typos, syntax errors)
- Project-specific business logic details
- Secrets, passwords, sensitive data
- Temporary workarounds
- Issues already well-documented

**💡 Tips:**
- Be specific in error descriptions
- Include complete, runnable code examples
- Explain WHY the solution works
- Add prevention strategies
- Use clear, searchable titles
- Add relevant tags for discoverability

## Example Output

```markdown
## 📊 Retrospective Analysis Complete

### ✅ Knowledge Items Extracted: 3

#### 1. [DOCKER-046] Healthcheck Timeout Too Short
- **Scope:** docker
- **Severity:** high
- **Problem:** Container marked healthy before database ready
- **Saved to:** .kb/project/pending/docker-healthcheck-timeout.yaml
- **Action:** Created (submit to Shared KB)

#### 2. [PYTHON-127] FastAPI WebSocket Connection State
- **Scope:** python
- **Severity:** medium
- **Problem:** WebSocket connections not closing properly
- **Saved to:** .kb/project/pending/fastapi-websocket-state.yaml
- **Action:** Created (submit to Shared KB)

#### 3. Project-specific: Stripe Webhook Signature
- **Scope:** project
- **Severity:** high
- **Saved to:** .kb/project/knowledge/stripe-webhook-signature.yaml
- **Action:** Created (local only)

### 📈 Summary
- New entries created: 3
- Already documented: 0
- Project-specific: 1
- Universal candidates: 2

### 🎯 Next Steps
1. Review the 3 created entries
2. Submit universal entries:
   ```bash
   python .kb/shared/tools/kb_submit.py --target shared --file .kb/project/pending/docker-healthcheck-timeout.yaml --title "Docker compose healthcheck fix" --domain docker
   python .kb/shared/tools/kb_submit.py --target shared --file .kb/project/pending/fastapi-websocket-state.yaml --title "FastAPI WebSocket connection state" --domain python
   ```
```

Execute these steps using the available tools. Analyze the conversation thoroughly and extract all valuable knowledge items.
