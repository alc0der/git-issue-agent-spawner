# git-issue-agent-spawner

**Proof of Concept**: Orchestrating AI agents with issue-as-code practice.

A minimal post-commit hook for [git-issue](https://github.com/dspinellis/git-issue) that automatically launches AI agents when issues are assigned to them. While the script supports multiple AI tools (claude, gpt, copilot), it has been primarily tested with [Gemini](https://github.com/reugn/gemini-cli).

## Overview

This hook detects when an issue is assigned to an AI agent (gemini, claude, gpt, or copilot) and automatically starts the agent in a background session to work on the issue.

## Installation

To install the hook, you can either copy it manually or use `curl` or `wget` to download it directly from GitHub.

### Manual Installation

Copy the post-commit hook to your `.issues/.git/hooks/` directory:

```bash
cp ./hooks/post-commit path/to/git-issue/enabled-repo/.issues/.git/hooks/
chmod +x .issues/.git/hooks/post-commit
```
> Replace `path/to/git-issue/enabled-repo` with your repo path

### Using `curl` or `wget`

```bash
# Using curl
curl -o .issues/.git/hooks/post-commit https://raw.githubusercontent.com/alc0der/git-issue-agent-spawner/main/hooks/post-commit
chmod +x .issues/.git/hooks/post-commit

# Using wget
wget -O .issues/.git/hooks/post-commit https://raw.githubusercontent.com/alc0der/git-issue-agent-spawner/main/hooks/post-commit
chmod +x .issues/.git/hooks/post-commit
```
> Replace `path/to/git-issue/enabled-repo` with your repo path

## Usage

The hook triggers automatically when you assign an issue to an AI agent using git-issue's native commands:

```bash
# From the parent directory (not .issues)
git issue assign <issue-id> <agent-name>
```

Supported agents: `gemini` (tested), `claude`, `gpt`, `copilot` (experimental support)

The agent will start in a tmux or screen session in the background.

## Uninstallation

Remove the hook:

```bash
rm .issues/.git/hooks/post-commit
```

## Files

- `hooks/post-commit` - The git hook that detects AI agent assignments

## Requirements

- [git-issue](https://github.com/dspinellis/git-issue)
- Bash shell
- [tmux](https://github.com/tmux/tmux) or screen (for background sessions)
- AI agent CLI tools ([gemini](https://github.com/google-gemini/gemini-cli), claude, gpt, or copilot)
