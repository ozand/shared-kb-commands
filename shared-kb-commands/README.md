# Shared KB Commands

Slash commands for Shared Knowledge Base initialization and management.

## Commands

### `/kb-init`
Initialize Shared Knowledge Base in the current project.

**What it does:**
- Creates `.kb/` directory structure
- Adds Shared KB as git submodule
- Creates PROJECT.yaml template
- Copies session-start hook
- Commits changes

**Usage:**
```
/kb-init
```

### `/kb-update`
Update Shared Knowledge Base to the latest version.

**What it does:**
- Updates submodule to latest version
- Rebuilds search index
- Shows update summary

**Usage:**
```
/kb-update
```

### `/kb-status`
Check Shared Knowledge Base status and available updates.

**What it shows:**
- Installation status
- Current version
- Entry count
- Last update date
- Available updates

**Usage:**
```
/kb-status
```

## Installation

This plugin should be installed as a user-level plugin to work across all projects.

### Manual Installation

1. Register this repository as a local marketplace in Claude Code settings
2. Install the `shared-kb-commands` plugin
3. Commands will be available globally

## Requirements

- Git repository (for submodule management)
- Python 3.8+ (for KB tools)
- Network connection (for cloning submodule)

## About Shared Knowledge Base

Shared Knowledge Base is a centralized knowledge management system for AI agents and development teams, containing 149+ verified solutions for common software development errors across Python, JavaScript, Docker, PostgreSQL, and more.

**Repository:** https://github.com/ozand/shared-knowledge-base
**Version:** 5.1.7
