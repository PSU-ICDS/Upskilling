---
layout: default
title: LiteLLM API Access
description: Learn how to set up API access to the large language models (LLMs) running on a Grace Hopper node on Roar.
nav_order: 2
---

# LiteLLM API Access

The Institute for Computational and Data Sciences (ICDS) has deployed a self-hosted large language model (LLM) service with application programming interface (API) access, designed to integrate with a user's coding agent (sometimes called a harness or agentic coding tool) to support tasks such as code generation, refactoring, and debugging. The service is currently available for alpha testing and runs on an NVIDIA Grace Hopper node on Roar, Penn State's high-performance computing cluster, behind a LiteLLM proxy.

The sections below describe how to configure OpenCode and Claude Code to use ICDS-hosted models, and how to call the API directly from your own code.

## Prerequisites

This guide assumes the following:

1. You have a valid API key.
   - To request an API key, please email us at [icds@psu.edu](mailto:icds@psu.edu).
2. You are on the Penn State network or are connected to [the Penn State virtual private network (VPN)](https://pennstate.service-now.com/kb?sys_kb_id=050f3d564781c750fb179df4126d43c2&id=kb_article_view).

### Check your connection

Before setting up a coding agent, confirm that you can reach the ICDS service and that your key works. Replace `PASTE-YOUR-API-KEY-HERE` with your key.

macOS / Linux:

```bash
curl -H "Authorization: Bearer PASTE-YOUR-API-KEY-HERE" https://ai.hpc.psu.edu:4000/v1/models
```

Windows PowerShell (type `curl.exe`, not `curl`):

```powershell
curl.exe -H "Authorization: Bearer PASTE-YOUR-API-KEY-HERE" https://ai.hpc.psu.edu:4000/v1/models
```

What the result means:

- **A list of models** (including `Laguna-XS-2.1`): everything works. Continue to the next section.
- **The command hangs or says it could not connect:** you are probably not on the Penn State network. Connect to the VPN and try again.
- **An error mentioning "401" or "authentication":** the service is reachable, but your key was not accepted. Check that you copied the whole key, or email [icds@psu.edu](mailto:icds@psu.edu).

> **Note:** This command saves your key in your terminal history. On a shared computer, clear your history afterward. In the macOS / Linux terminal, run `history -c`. In PowerShell, run `Clear-History`, then delete the saved history file with `Remove-Item (Get-PSReadLineOption).HistorySavePath`.

## Setting up a coding agent

Our current instructions support using two different coding agents: OpenCode and Claude Code. If you set up a separate coding agent, please consider adding directions here or submitting them in your feedback.

Both setups below save your settings in the agent's **default configuration file**, so the agent uses the ICDS models every time you start it. If you already use one of these agents with another provider, the steps include making a backup copy of your existing configuration first, so you can switch back later.

### OpenCode

These instructions are for OpenCode 2, the current version.

#### Step 1: Install OpenCode

Open a terminal and run the command for your system.

macOS / Linux (recommended install script):

```bash
curl -fsSL https://opencode.ai/v2/install | bash
```

macOS with Homebrew (alternative):

```bash
brew install anomalyco/tap/opencode-v2
```

Any system with Node.js already installed (alternative):

```bash
npm install -g @opencode/cli
```

Windows: we recommend installing inside [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/windows/wsl/install) using the macOS / Linux command above. OpenCode 2 does not support Windows package managers such as Chocolatey or Scoop. To install natively on Windows instead, download [the OpenCode 2 zip file for Windows (x64)](https://opencode.ai/update/api/latest/cli/opencode/opencode-windows-x64.zip), unzip it, and place `opencode.exe` in a folder on your PATH (the list of folders Windows searches for commands). Other Windows downloads are listed in the [OpenCode 2 installation docs](https://opencode.ai/v2/docs/).

When the install finishes, open a new terminal window and run:

```bash
opencode --version
```

It should print a version starting with `2.x`. If it prints `1.x`, you still have OpenCode 1 installed. OpenCode 1 and OpenCode 2 both use the `opencode` command and cannot be installed side by side; see the [OpenCode 2 docs](https://opencode.ai/v2/docs/) for how to switch.

#### Step 2: Configure OpenCode for ICDS

OpenCode reads its settings from a fixed location in your home folder. These commands create that folder if needed, back up any existing configuration file, and open the file in a text editor.

macOS / Linux / WSL:

```bash
mkdir -p ~/.config/opencode
[ -f ~/.config/opencode/opencode.json ] && cp -n ~/.config/opencode/opencode.json ~/.config/opencode/opencode.json.backup
nano ~/.config/opencode/opencode.json
```

Windows (PowerShell), for native Windows installs only:

```powershell
New-Item -ItemType Directory -Force "$HOME\.config\opencode" | Out-Null
if ((Test-Path "$HOME\.config\opencode\opencode.json") -and -not (Test-Path "$HOME\.config\opencode\opencode.json.backup")) { Copy-Item "$HOME\.config\opencode\opencode.json" "$HOME\.config\opencode\opencode.json.backup" }
notepad "$HOME\.config\opencode\opencode.json"
```

> **Back up first:** If you already had a configuration file, the commands above saved a copy as `opencode.json.backup` in the same folder. If a backup already exists, they leave it alone, so running these commands again will not overwrite your original. The next step replaces the file's contents. To return to your old setup later, copy the backup over `opencode.json`.

Delete anything already in the file, paste in the following JSON (JavaScript Object Notation), then replace `PASTE-YOUR-API-KEY-HERE` with your key (keep the quotation marks):

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "icds": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "ICDS",
      "options": {
        "baseURL": "https://ai.hpc.psu.edu:4000/v1",
        "apiKey": "PASTE-YOUR-API-KEY-HERE"
      },
      "models": {
        "Laguna-XS-2.1": {
          "name": "Laguna XS 2.1"
        },
        "gpt-oss-20b": {
          "name": "gpt-oss 20B"
        }
      }
    }
  },
  "model": "icds/Laguna-XS-2.1"
}
```

Save the file. In nano: press Ctrl+O, then Enter to save, then Ctrl+X to exit. In Notepad: File > Save.

> **Tip:** Use a plain-text editor like nano, Notepad, or VS Code. Word processors (and TextEdit on macOS) can turn straight quotation marks (") into curly quotes, which breaks the file.

#### Step 3: Start OpenCode and verify

In your terminal, move into the folder you want to work in, then start OpenCode:

```bash
cd path/to/your/project
opencode
```

To confirm OpenCode can see the ICDS models, run this in a separate terminal window:

```bash
opencode models
```

The list should include `icds/Laguna-XS-2.1` and `icds/gpt-oss-20b`. Then ask OpenCode a simple question, such as "What files are in this folder?" If it answers, you are connected.

#### Troubleshooting OpenCode

- **`opencode models` does not list the ICDS models:** OpenCode may not have read your configuration file. Check that the file is saved at `~/.config/opencode/opencode.json` (on native Windows, `$HOME\.config\opencode\opencode.json`) and that it is valid JSON. To check the JSON, run `python3 -m json.tool ~/.config/opencode/opencode.json` (on Windows, `python -m json.tool "$HOME\.config\opencode\opencode.json"`). If it prints an error, look for a missing comma, a missing quotation mark, or curly quotes.
- **OpenCode says it could not connect, or a request times out:** confirm that you are on the Penn State network or VPN, then run the command in [Check your connection](#check-your-connection) again.
- **An error mentioning "401" or "authentication":** check that you pasted your whole key between the quotation marks after `"apiKey"`, with no extra spaces.
- **The settings seem to be ignored:** run `opencode --version`. If it prints `1.x`, you are running OpenCode 1, not OpenCode 2. See Step 1.

### Claude Code

#### Step 1: Install Claude Code

Open a terminal and run the command for your system. You do not need administrator rights.

macOS / Linux / WSL (recommended native installer):

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Windows PowerShell (your prompt starts with `PS C:\`):

```powershell
irm https://claude.ai/install.ps1 | iex
```

Windows Command Prompt (your prompt starts with `C:\`, without `PS`):

```bat
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

Alternatives, if you prefer a package manager:

- macOS Homebrew: `brew install --cask claude-code`
- Windows WinGet: `winget install Anthropic.ClaudeCode`

On Windows, installing [Git for Windows](https://git-scm.com/downloads/win) is optional but recommended, so Claude Code can run Bash commands.

When the installer finishes, open a new terminal window and run `claude --version`. If it prints a version number, Claude Code is installed. If your terminal says `claude` is not found, see the [Claude Code installation troubleshooting guide](https://code.claude.com/docs/en/troubleshoot-install). For other install options, see the [Claude Code setup docs](https://code.claude.com/docs/en/setup).

> **Note:** You do not need a paid Anthropic account to use Claude Code with the ICDS models. Your ICDS API key takes the place of an Anthropic login. Do not start Claude Code yet; finish Step 2 first.

#### Step 2: Configure Claude Code for ICDS

Claude Code reads your personal settings from `settings.json` in the `.claude` folder in your home folder. These commands create that folder if needed, back up any existing settings file, and open the file in a text editor.

macOS / Linux / WSL:

```bash
mkdir -p ~/.claude
[ -f ~/.claude/settings.json ] && cp -n ~/.claude/settings.json ~/.claude/settings.json.backup
nano ~/.claude/settings.json
```

Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude" | Out-Null
if ((Test-Path "$HOME\.claude\settings.json") -and -not (Test-Path "$HOME\.claude\settings.json.backup")) { Copy-Item "$HOME\.claude\settings.json" "$HOME\.claude\settings.json.backup" }
notepad "$HOME\.claude\settings.json"
```

> **Back up first:** If you already use Claude Code (for example, with a Claude subscription), the commands above saved your current settings as `settings.json.backup` in the same folder. If a backup already exists, they leave it alone, so running these commands again will not overwrite your original. The next step replaces the file's contents, and afterward every Claude Code session will use the ICDS models. To return to your old setup, copy the backup over `settings.json`.

Delete anything already in the file, paste in the following, then replace `PASTE-YOUR-API-KEY-HERE` with your key (keep the quotation marks). If your file already has other settings you want to keep, such as permissions or hooks, merge the `env` and `model` entries below into your file instead of deleting it.

```json
{
  "env": {
    "CLAUDE_CODE_ATTRIBUTION_HEADER": "0",
    "ANTHROPIC_BASE_URL": "https://ai.hpc.psu.edu:4000",
    "ANTHROPIC_API_KEY": "PASTE-YOUR-API-KEY-HERE",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "Laguna-XS-2.1",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "Laguna-XS-2.1",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "Laguna-XS-2.1",
    "CLAUDE_CODE_AUTO_MODE_SERVER": "0",
    "CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS": "1",
    "CLAUDE_CODE_DISABLE_UNKNOWN_MODEL_WINDOW_ENFORCEMENT": "1"
  },
  "model": "Laguna-XS-2.1"
}
```

The three `ANTHROPIC_DEFAULT_..._MODEL` lines point Claude Code's built-in model names, which it also uses for small background tasks, at the ICDS model, so those requests do not fail.

> **Long sessions with gpt-oss-20b:** The last setting stops Claude Code from guessing a context window (how much conversation the model can hold at once) for models it does not recognize. gpt-oss-20b holds about half as much as Laguna-XS-2.1 (see [Which models are good for what?](#which-models-are-good-for-what)). In a long session with gpt-oss-20b, type `/compact` to summarize the conversation so far, or `/clear` to start fresh, before it runs out of room.

Save the file. In nano: press Ctrl+O, then Enter to save, then Ctrl+X to exit. In Notepad: File > Save.

> **Tip:** Use a plain-text editor like nano, Notepad, or VS Code. Word processors (and TextEdit on macOS) can turn straight quotation marks (") into curly quotes, which breaks the file.

#### Step 3: Start Claude Code and verify

In your terminal, move into the folder you want to work in, then start Claude Code:

```bash
cd path/to/your/project
claude
```

The first time you start it, Claude Code may ask whether you want to use the API key it found. Choose **Yes**. This is your ICDS key.

To confirm you are connected to ICDS, type `/status` and press Enter. The model should be `Laguna-XS-2.1` and the base URL should be `https://ai.hpc.psu.edu:4000`. To switch to the other ICDS model, type `/model gpt-oss-20b`. Then ask a simple question, such as "What files are in this folder?" If it answers, you are connected.

If Claude Code asks you to log in to an Anthropic account instead, see [Troubleshooting Claude Code](#troubleshooting-claude-code) below.

#### Troubleshooting Claude Code

If you have never set up Claude Code on your system, it will try to walk you through its onboarding, which may prevent access to the ICDS models. To skip onboarding, add the line `"hasCompletedOnboarding": true` to your `~/.claude.json` file using one of the options below.

> **Quit Claude Code first.** Claude Code rewrites `~/.claude.json` while it runs and can undo your change. Type `/exit` (or press Ctrl+C twice) before running any of these commands, then start Claude Code again afterward.

In Python (works on any system with Python installed). Start Python by typing `python3` (macOS / Linux) or `python` (Windows), paste these lines, then type `exit()`:

```python
import json, os
p = os.path.expanduser("~/.claude.json")
d = json.load(open(p)) if os.path.exists(p) else {}
d["hasCompletedOnboarding"] = True
json.dump(d, open(p, "w"), indent=2)
```

In the macOS / Linux terminal. This option needs the `jq` tool, which is included with recent versions of macOS. On Linux, you may need to install it first (for example, `sudo apt install jq`), or use the Python option instead.

```bash
f=~/.claude.json; [ -f "$f" ] || echo '{}' > "$f"
jq '.hasCompletedOnboarding = true' "$f" > "$f.tmp" && mv "$f.tmp" "$f"
```

In Windows PowerShell:

```powershell
$f = "$HOME\.claude.json"
if (Test-Path $f) { $d = Get-Content $f -Raw | ConvertFrom-Json } else { $d = [pscustomobject]@{} }
$d | Add-Member -NotePropertyName hasCompletedOnboarding -NotePropertyValue $true -Force
[IO.File]::WriteAllText($f, ($d | ConvertTo-Json -Depth 100), [Text.UTF8Encoding]::new($false))
```

## Using the API directly

You can also call the ICDS models from your own scripts. The service is OpenAI-compatible, so any tool or library that works with the OpenAI API can use it. Point it at the base URL `https://ai.hpc.psu.edu:4000/v1` and use your ICDS API key. The same prerequisites apply: you need your key, and you must be on the Penn State network or VPN.

### From the terminal

macOS / Linux:

```bash
curl https://ai.hpc.psu.edu:4000/v1/chat/completions \
  -H "Authorization: Bearer PASTE-YOUR-API-KEY-HERE" \
  -H "Content-Type: application/json" \
  -d '{"model": "Laguna-XS-2.1", "messages": [{"role": "user", "content": "Say hello in one sentence."}]}'
```

The reply is JSON. The model's answer is in the `content` field near the end.

### From Python

Install the OpenAI Python library once with `pip install openai`, then run:

```python
import os
from openai import OpenAI

client = OpenAI(
    base_url="https://ai.hpc.psu.edu:4000/v1",
    api_key=os.environ["ICDS_API_KEY"],
)

response = client.chat.completions.create(
    model="Laguna-XS-2.1",
    messages=[{"role": "user", "content": "Say hello in one sentence."}],
)
print(response.choices[0].message.content)
```

This example reads your key from an environment variable named `ICDS_API_KEY`, so the key never appears in your code. Set the variable in the same terminal before you run the script: on macOS / Linux, `export ICDS_API_KEY="PASTE-YOUR-API-KEY-HERE"`; in PowerShell, `$env:ICDS_API_KEY = "PASTE-YOUR-API-KEY-HERE"`. To use the other model, change `model` to `"gpt-oss-20b"`.

## Data privacy and storage

While Roar is approved for both Level 1 and Level 2 data, during the pilot, users should restrict their usage to Level 1 data, because ICDS staff will be making frequent configuration changes as they incorporate feedback from users. See [Penn State policies on information classification](https://security.psu.edu/awareness/icdt/).

### Keeping data local

- Because LiteLLM is preconfigured to call open-weight models running on Roar, your prompts and data are not sent to OpenAI, Anthropic, Google, Meta, or other third parties when using the hosted models. Please verify you are using the correct model before starting your work. In most coding agents, you can select your desired model with the `/model` command.
- It is possible that your coding tool will query the internet when completing a task, causing some data to go outside of the Roar system. To maintain complete control of what your coding tool is doing, consider switching to a mode that asks before acting. In Claude Code, press Shift+Tab to switch to plan mode. In OpenCode, press Tab to switch to the Plan agent.

### Keeping your access secure

Your API key should be protected with the same diligence as you would protect a password or a passkey. Do not share it with others and avoid putting it places where it may be saved by another system, such as git. The only places your key should appear are the configuration files described above. Keep those files out of git repositories, shared folders, and cloud-synced folders, and do not paste your key into a chat with the coding agent.

## FAQ

### Choosing models

#### Which models are good for what?

These models are available through the API:

| Model | Maximum Context Window | Inputs | Notes |
|:------|-----------------------:|:-------|:------|
| [Laguna-XS-2.1](https://huggingface.co/poolside/Laguna-XS-2.1) | 262,144 | Text only | Default model. Made by Poolside for software engineering and agentic coding. |
| [gpt-oss-20b](https://huggingface.co/openai/gpt-oss-20b) | 131,072 | Text only | OpenAI open-weight reasoning model with support for tool use. |

#### Why aren't bigger models available now?

ICDS aims to order a new graphics processing unit (GPU) cluster optimized for AI workflows soon. The new cluster will include more GPUs with more video memory (VRAM) and allow ICDS to serve larger local open-weight models to many more users. In the meantime, ICDS aims to help users develop experience working with small to medium-size open-weight models and welcomes feedback to inform future purchasing decisions.

#### Why aren't Qwen models available?

ICDS is still seeking permission to make Qwen models available to the ICDS community.

#### How can I request a specific model?

Please let us know through [the feedback options below](#how-can-i-provide-feedback) which models you would like and your intended use case. If you have a specific quantization in mind, feel free to include that information. Please also let us know whether you need low latency or intend for this model to be used primarily for batch processing where a higher latency would be acceptable.

### Purpose of ICDS AI-as-a-Service

#### Why is ICDS serving small to medium-size open-weight models when Penn State already has AI Studio providing access to frontier-class models?

Open-weight models have many advantages. Using open-weight models gives users more control. For example, users can:

- Select from specific models trained for specific purposes.
- Fine-tune an open-weight model on their own datasets for a specific purpose.
- Be confident that they'll be able to reprocess data consistently years later (even if commercial offerings change).
- Keep data on Penn State controlled systems for greater data privacy.

Additionally, local open-weight models have the potential to:

- Have lower latency than commercial cloud services, and
- Meet many needs more economically and more efficiently.

Through this pilot, users can begin to explore potential benefits and ICDS can gain experience to provide more robust open-weight AI-as-a-service offerings in the future.

#### Should I expect open-weight models to replace commercial AI models?

No. It seems likely that open-weight models will continue to trail the capabilities of the latest commercial, frontier models. As the gap between open and frontier models narrows, open-weight models may become more attractive, and ICDS anticipates that many users will want to use a combination of open-weight and frontier models.

### Feedback

#### How can I provide feedback?

Send email to [icds@psu.edu](mailto:icds@psu.edu) or complete [the ICDS AI feedback form](https://forms.cloud.microsoft/Pages/ResponsePage.aspx?id=RY30fNs9iUOpwcEVUm61Lr6d8HgUHz5EltDgI6iOfatURFJVS0xKREdWMlQ1MzJTTTFCTU44N1JBTy4u).

#### Why should I provide feedback?

The primary purpose of the pilot is to help ICDS better understand which use cases are likely to be common. We look forward to hearing which models and features are most useful to the ICDS community and which new models users would like to see added.
