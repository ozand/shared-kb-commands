# Shared KB Commands Plugin - Installation Guide

This plugin provides slash commands (`/kb-init`, `/kb-update`, `/kb-status`) for Shared Knowledge Base management.

## What was created

### 1. User-level Plugin (Global)
**Location:** `T:\Code\shared-kb-plugins\shared-kb-commands\`

**Commands:**
- `/kb-init` - Initialize Shared KB in any project
- `/kb-update` - Update Shared KB to latest version
- `/kb-status` - Check Shared KB status

**Scope:** Works across ALL projects (user-level)

### 2. Project-level Plugin
**Location:** `T:\Code\shared-knowledge-base\.claude\plugins\shared-kb-commands\`

**Commands:**
- `/kb-update` - Update this repository
- `/kb-status` - Check repository status

**Scope:** Works only in shared-knowledge-base repository

**Note:** `/kb-init` is NOT included in project-level plugin since this repository IS the Shared KB.

---

## Installation

### Option 1: Install via Claude Code UI (Recommended)

1. **Restart Claude Code** to refresh plugins
2. Open Claude Code Settings
3. Go to Plugins section
4. Add local marketplace:
   - Name: `local`
   - Path: `C:\Users\ozand\.claude\plugins\marketplaces\local`
5. Install `shared-kb-commands` plugin
6. Commands will be available globally

### Option 2: Manual Installation

1. Copy plugin directory to global plugins:
```bash
cp -r "T:\Code\shared-kb-plugins\shared-kb-commands" "C:\Users\ozand\.claude\plugins\installed\shared-kb-commands"
```

2. Update `C:\Users\ozand\.claude\plugins\installed_plugins.json`:
```json
{
  "version": 2,
  "plugins": {
    "shared-kb-commands@local": [
      {
        "scope": "user",
        "installPath": "T:\\Code\\shared-kb-plugins\\shared-kb-commands",
        "version": "1.0.0",
        "installedAt": "2026-01-11T00:00:00.000Z",
        "lastUpdated": "2026-01-11T00:00:00.000Z"
      }
    ]
  }
}
```

3. Restart Claude Code

---

## Verification

### Test 1: Check project-level plugin (in shared-knowledge-base)
```bash
cd T:\Code\shared-knowledge-base
/kb-status
```
Expected: Shows repository status

### Test 2: Check user-level plugin (in any project)
```bash
cd C:\Temp\test-kb-project
/kb-status
```
Expected: Shows KB status or prompts to install

---

## Files Created

### User-level plugin:
```
T:\Code\shared-kb-plugins\
└── shared-kb-commands\
    ├── .claude-plugin\
    │   └── plugin.json
    ├── commands\
    │   ├── kb-init.md
    │   ├── kb-update.md
    │   └── kb-status.md
    └── README.md
```

### Project-level plugin:
```
T:\Code\shared-knowledge-base\
└── .claude\
    └── plugins\
        └── shared-kb-commands\
            ├── .claude-plugin\
            │   └── plugin.json
            └── commands\
                ├── kb-update.md
                └── kb-status.md
```

### Marketplace configuration:
```
C:\Users\ozand\.claude\plugins\marketplaces\local\
└── marketplace.json
```

### Project metadata:
```
T:\Code\shared-knowledge-base\
└── .kb\
    └── context\
        └── PROJECT.yaml
```

---

## Troubleshooting

### Commands not found

**Problem:** `/kb-init`, `/kb-update`, or `/kb-status` give "Unknown slash command"

**Solutions:**
1. Restart Claude Code
2. Check plugin is installed: Look in `C:\Users\ozand\.claude\plugins\installed_plugins.json`
3. Verify marketplace configuration: Check `C:\Users\ozand\.claude\plugins\marketplaces\local\marketplace.json`
4. Check plugin files exist: `ls "T:\Code\shared-kb-plugins\shared-kb-commands\commands"`

### Plugin loads but commands don't work

**Problem:** Plugin installed but commands fail

**Solutions:**
1. Check command files have correct YAML frontmatter
2. Check `allowed-tools` includes necessary tools (Bash, Read, Write, Edit)
3. Test with `/kb-status` first (simplest command)
4. Check Claude Code logs for errors

### Project-level plugin doesn't work in shared-knowledge-base

**Problem:** `/kb-status` doesn't work in shared-knowledge-base repository

**Solutions:**
1. Check plugin exists: `ls "T:\Code\shared-knowledge-base\.claude\plugins\shared-kb-commands\commands"`
2. Restart Claude Code in shared-knowledge-base directory
3. Verify `.claude/plugins/` is not in `.gitignore`

---

## Architecture

### Why Two Plugins?

**User-level plugin** provides commands for OTHER projects:
- Works in any project
- Used to initialize KB in new projects
- `/kb-init` creates `.kb/shared/` submodule

**Project-level plugin** provides commands for THIS repository:
- Works only in shared-knowledge-base
- This repository IS the Shared KB (no submodule needed)
- `/kb-update` pulls from git directly

### Command Mapping

| Command | User-level Plugin | Project-level Plugin |
|---------|------------------|---------------------|
| `/kb-init` | ✅ Available | ❌ Not needed |
| `/kb-update` | ✅ Updates submodule | ✅ Updates repo |
| `/kb-status` | ✅ Checks submodule | ✅ Checks repo |

---

## Next Steps

1. ✅ Plugins created
2. ✅ Marketplace configured
3. ✅ Project metadata created
4. ✅ Committed to shared-knowledge-base (commit: 09c8a94)
5. ⏳ Install plugin via Claude Code UI
6. ⏳ Test commands
7. ⏳ Update documentation if needed

---

## Support

**Repository:** https://github.com/ozand/shared-knowledge-base
**Documentation:** `T:\Code\shared-knowledge-base\docs\integration\BOOTSTRAP.md`

---

**Version:** 1.0.0
**Last Updated:** 2026-01-11
**Status:** Ready for installation
