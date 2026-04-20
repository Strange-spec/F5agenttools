# F5agenttools — JARVIS AI Agent Toolkit for OpenCode

A ready-to-use collection of AI agents and configuration for [OpenCode](https://opencode.ai), specialized for F5 BIG-IP technical support, network analysis, and autonomous task orchestration.

## What's Included

| File | Description |
|------|-------------|
| `agents/jarvis.md` | 🤖 **JARVIS** — Primary orchestrator agent. Manages complex tasks, delegates to subagents, handles F5 support workflows |
| `agents/qkview_agent.md` | 🔍 **QkView Agent** — Specialized for analyzing F5 BIG-IP QkView diagnostic files |
| `agents/tshark_agent.md` | 🌐 **TShark Agent** — Network packet capture analysis in F5 BIG-IP environments |
| `agents/skill_creator.md` | 🛠️ **Skill Creator** — Interactively creates and tests new OpenCode skills and agents |
| `config/opencode.json` | ⚙️ **Config Template** — OpenCode provider/model configuration template |

## Quick Start

### Step 1: Install OpenCode

```bash
# macOS / Linux
curl -fsSL https://opencode.ai/install | bash
```

### Step 2: Configure Your Model & API Key

Edit `config/opencode.json`, replace the placeholders:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "YOUR_PROVIDER_NAME": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "YOUR_PROVIDER_NAME",
      "options": {
        "baseURL": "YOUR_API_BASE_URL",
        "apiKey": "YOUR_API_KEY"
      },
      "models": {
        "YOUR_MODEL_NAME": {
          "name": "YOUR_MODEL_NAME",
          "limit": {
            "context": 190000,
            "output": 32000
          }
        }
      }
    }
  }
}
```

**Examples for common providers:**

<details>
<summary>OpenAI</summary>

```json
{
  "provider": {
    "openai": {
      "npm": "@ai-sdk/openai",
      "name": "openai",
      "options": {
        "apiKey": "sk-xxxxxxxxxxxxxxxx"
      },
      "models": {
        "gpt-4o": {
          "name": "gpt-4o",
          "limit": { "context": 128000, "output": 16000 }
        }
      }
    }
  }
}
```
</details>

<details>
<summary>Anthropic Claude</summary>

```json
{
  "provider": {
    "anthropic": {
      "npm": "@ai-sdk/anthropic",
      "name": "anthropic",
      "options": {
        "apiKey": "sk-ant-xxxxxxxxxxxxxxxx"
      },
      "models": {
        "claude-sonnet-4-5": {
          "name": "claude-sonnet-4-5",
          "limit": { "context": 190000, "output": 32000 }
        }
      }
    }
  }
}
```
</details>

<details>
<summary>Any OpenAI-Compatible API (LiteLLM, Azure, local Ollama, etc.)</summary>

```json
{
  "provider": {
    "my_provider": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "my_provider",
      "options": {
        "baseURL": "http://localhost:4000/openai/",
        "apiKey": "your-key-here"
      },
      "models": {
        "llama3": {
          "name": "llama3",
          "limit": { "context": 128000, "output": 8000 }
        }
      }
    }
  }
}
```
</details>

### Step 3: Copy Files to OpenCode Config Directory

```bash
# Create OpenCode config directories
mkdir -p ~/.config/opencode/agents

# Copy agents
cp agents/*.md ~/.config/opencode/agents/

# Copy config (backup your existing config first if you have one)
cp config/opencode.json ~/.config/opencode/opencode.json
```

### Step 4: Launch OpenCode

```bash
opencode
```

Switch between agents with **Ctrl+A** (or the agent switcher), and select **JARVIS** to start!

---

## Agent Details

### 🤖 JARVIS (Primary Agent)
The main orchestrator. Handles complex multi-step tasks by delegating to specialized subagents. Features:
- Autonomous task planning with TodoWrite
- Parallel subagent execution
- F5 BIG-IP expert knowledge
- Strict evidence-based reasoning (no hallucination)
- PII-safe handling

### 🔍 QkView Agent (Subagent)
Analyzes F5 BIG-IP QkView diagnostic archives:
- Log analysis (including rotated logs)
- Configuration review
- Root cause identification
- Security IOC detection

### 🌐 TShark Agent (Subagent)
Network packet capture expert:
- `.pcap` / `.pcapng` file analysis
- F5 Ethertrailer field extraction
- Client-side ↔ Server-side flow correlation
- SSL/TLS decryption
- TCP performance diagnostics

### 🛠️ Skill Creator (Primary Agent)
Create your own skills and agents:
- Interactively gathers requirements
- Generates standards-compliant skill files
- Runs eval/benchmark testing
- Iterates based on test results

---

## Requirements

- [OpenCode](https://opencode.ai) installed
- API access to any supported LLM provider (OpenAI, Anthropic, LiteLLM, Ollama, etc.)
- macOS or Linux

---

## License

MIT License — free to use, modify, and distribute.
