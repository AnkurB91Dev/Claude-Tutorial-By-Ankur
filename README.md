# 🤖 Claude Tutorial By Ankur

> A hands-on, notebook-driven guide to **everything Claude can do** — from basic API calls to autonomous multi-agent pipelines.

[![Anthropic](https://img.shields.io/badge/Powered%20by-Anthropic-blue?style=flat-square)](https://www.anthropic.com)
[![Python](https://img.shields.io/badge/Python-3.10%2B-yellow?style=flat-square)](https://www.python.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

---

## 📚 Table of Contents

- [About](#-about)
- [Setup](#-setup)
- [Features Covered](#-features-covered)
  - [Core API](#-core-api)
  - [Tool Use / Function Calling](#-tool-use--function-calling)
  - [Vision & Multimodal](#-vision--multimodal)
  - [Extended Thinking](#-extended-thinking)
  - [Prompt Caching](#-prompt-caching)
  - [Streaming](#-streaming)
  - [Batch API](#-batch-api)
  - [Files API](#-files-api)
  - [Memory & Context Management](#-memory--context-management)
  - [Agents & Multi-Agent Systems](#-agents--multi-agent-systems)
  - [MCP — Model Context Protocol](#-mcp--model-context-protocol)
  - [Claude Code CLI](#-claude-code-cli)
  - [Models Overview](#-models-overview)
- [Notebooks](#-notebooks)
- [Contributing](#-contributing)

---

## 🎯 About

This repository is a **complete learning resource** for developers building with the Claude API. Each feature is explored in a dedicated Jupyter notebook with real working examples, explanations, and best practices.

Whether you're building a chatbot, a document analyzer, an autonomous agent, or a full MCP-powered tool ecosystem — you'll find a working example here.

---

## ⚙️ Setup

```bash
# 1. Clone the repo
git clone https://github.com/AnkurB91Dev/Claude-Tutorial-By-Ankur.git
cd Claude-Tutorial-By-Ankur

# 2. Install dependencies
pip install anthropic python-dotenv

# 3. Add your API key
echo 'ANTHROPIC_API_KEY="your-key-here"' > .env

# 4. Launch Jupyter
jupyter notebook
```

> 🔑 Get your API key at [console.anthropic.com](https://console.anthropic.com)

---

## 🚀 Features Covered

### 🔌 Core API

The foundation of everything. Learn how to send messages, manage conversation history, and control model behavior.

| Topic | Description |
|---|---|
| Basic requests | Send your first message to Claude |
| System prompts | Shape Claude's persona and behavior |
| Multi-turn conversations | Build stateful chat with message history |
| Temperature & sampling | Control creativity vs. determinism |
| Max tokens | Manage response length and cost |
| Stop sequences | Define custom stopping conditions |

---

### 🛠️ Tool Use / Function Calling

Give Claude the ability to call your own functions, APIs, and services.

| Topic | Description |
|---|---|
| Defining tools | JSON Schema-based tool definitions |
| Single tool calls | Claude decides when and how to call a tool |
| Parallel tool calls | Claude calls multiple tools simultaneously |
| Tool result handling | Feed results back into the conversation |
| Forced tool use | Require Claude to always call a specific tool |
| Computer use | Let Claude control a desktop environment |

```python
tools = [{
    "name": "get_weather",
    "description": "Get current weather for a city",
    "input_schema": {
        "type": "object",
        "properties": {"city": {"type": "string"}},
        "required": ["city"]
    }
}]
```

---

### 👁️ Vision & Multimodal

Claude can see images, read PDFs, and understand documents — not just text.

| Topic | Description |
|---|---|
| Image input (base64) | Send images directly in the message |
| Image input (URL) | Reference publicly hosted images |
| PDF understanding | Analyze documents, reports, and papers |
| Multi-image reasoning | Compare or analyze multiple images at once |
| Screenshot analysis | Understand UI screenshots and diagrams |

---

### 🧠 Extended Thinking

Unlock Claude's deepest reasoning capabilities for hard problems.

| Topic | Description |
|---|---|
| Enabling thinking | Add a `thinking` block to complex requests |
| Budget tokens | Control how much Claude "thinks" |
| Streaming thinking | Stream reasoning tokens in real time |
| When to use thinking | Math, logic, planning, multi-step problems |

```python
response = client.messages.create(
    model="claude-opus-4-7",
    max_tokens=16000,
    thinking={"type": "enabled", "budget_tokens": 10000},
    messages=[{"role": "user", "content": "Solve this step by step..."}]
)
```

---

### ⚡ Prompt Caching

Dramatically cut latency and cost by caching large, reusable context.

| Topic | Description |
|---|---|
| Cache control headers | Mark content blocks as cacheable |
| System prompt caching | Cache large system prompts |
| Document caching | Cache entire PDFs or knowledge bases |
| Cache hit metrics | Measure savings via usage stats |
| Multi-turn cache reuse | Persist cache across a conversation |

> 💰 Cache hits cost **~90% less** than uncached input tokens.

---

### 🌊 Streaming

Get responses token-by-token for a real-time, ChatGPT-like experience.

| Topic | Description |
|---|---|
| Basic streaming | Stream text deltas as they arrive |
| Streaming tool calls | Handle tool use events in a stream |
| Streaming thinking blocks | Real-time extended reasoning |
| Async streaming | Non-blocking streams with `asyncio` |

---

### 📦 Batch API

Process thousands of requests offline at half the cost.

| Topic | Description |
|---|---|
| Creating batches | Submit up to 100k requests in one call |
| Polling for results | Check batch status and retrieve output |
| Error handling | Handle per-request failures gracefully |
| Cost savings | ~50% cheaper than synchronous requests |

---

### 📁 Files API

Upload files once, reuse them across many requests without re-uploading.

| Topic | Description |
|---|---|
| Uploading files | Store PDFs, images, and documents |
| Referencing files | Use `file_id` in message content |
| Managing files | List and delete uploaded files |
| Use cases | RAG, document QA, repeated analysis |

---

### 🧩 Memory & Context Management

Strategies for handling long conversations and large knowledge bases.

| Topic | Description |
|---|---|
| Context window limits | Understanding token budgets per model |
| Conversation summarization | Compress history to stay within limits |
| External memory (vector DB) | Retrieve relevant context on demand |
| Sliding window patterns | Keep only the most recent N turns |

---

### 🤖 Agents & Multi-Agent Systems

Build autonomous agents that plan, reason, use tools, and delegate to sub-agents.

| Topic | Description |
|---|---|
| ReAct loop | Think → Act → Observe cycles |
| Agentic tool use | Agents that call tools autonomously |
| Subagents | Orchestrator delegates to specialist agents |
| Agent SDK | Build production-grade agents with the SDK |
| Human-in-the-loop | Pause for approval at critical steps |
| Error recovery | Agents that retry and self-correct |

```
Orchestrator Agent
    ├── Research Agent    (web search, document reading)
    ├── Code Agent        (write, execute, debug code)
    └── Writer Agent      (summarize, format, publish)
```

---

### 🔗 MCP — Model Context Protocol

MCP is an open standard that lets Claude connect to external tools and data sources via a standardized interface.

| Topic | Description |
|---|---|
| MCP server setup | Build and run your own MCP server |
| Connecting Claude | Wire Claude to an MCP server |
| Built-in MCP servers | Filesystem, GitHub, Google Drive, Slack |
| Custom MCP tools | Expose your own APIs as MCP tools |
| MCP in Claude Code | Use MCP servers inside the CLI |

---

### 💻 Claude Code CLI

Claude Code is Anthropic's official CLI — an AI coding assistant that lives in your terminal.

| Feature | Description |
|---|---|
| `/help` | List all available slash commands |
| `/review` | AI code review of current changes |
| `/init` | Generate a `CLAUDE.md` for your project |
| `Hooks` | Run shell commands on Claude events |
| `MCP servers` | Connect tools directly to the CLI |
| `Permissions` | Fine-grained allow/deny tool policies |
| `Custom slash commands` | Define your own `/commands` |
| `IDE integration` | VS Code & JetBrains extensions |
| `Headless mode` | Run Claude Code in CI/CD pipelines |
| `Multi-agent` | Spawn and coordinate sub-agents |

---

### 🧬 Models Overview

| Model | ID | Best For |
|---|---|---|
| **Claude Opus 4.7** | `claude-opus-4-7` | Most capable, complex reasoning, agents |
| **Claude Sonnet 4.6** | `claude-sonnet-4-6` | Balanced speed + intelligence |
| **Claude Haiku 4.5** | `claude-haiku-4-5-20251001` | Fast, lightweight, high-volume tasks |

---

## 📓 Notebooks

| # | Notebook | Topics |
|---|---|---|
| 001 | [001_requests.ipynb](001_requests.ipynb) | Basic API requests |
| 002 | *(coming soon)* | Tool use & function calling |
| 003 | *(coming soon)* | Vision & multimodal |
| 004 | *(coming soon)* | Extended thinking |
| 005 | *(coming soon)* | Prompt caching |
| 006 | *(coming soon)* | Streaming |
| 007 | *(coming soon)* | Batch API |
| 008 | *(coming soon)* | Agents & multi-agent systems |
| 009 | *(coming soon)* | MCP integration |

---

## 🤝 Contributing

Found a bug or want to add a notebook? PRs are welcome!

1. Fork the repo
2. Create a feature branch: `git checkout -b feature/my-topic`
3. Commit your changes
4. Open a pull request

---

<p align="center">Made with ❤️ by <a href="https://github.com/AnkurB91Dev">Ankur</a> | Powered by <a href="https://www.anthropic.com">Anthropic Claude</a></p>
