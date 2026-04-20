# F5agenttools — 基于 OpenCode 的 JARVIS AI 智能体工具集

专为 F5 BIG-IP 技术支持、网络分析和自主任务编排设计的 [OpenCode](https://opencode.ai) AI 智能体工具集，开箱即用，只需配置你自己的模型和 API Key。

---

## 📦 包含内容

| 文件 | 说明 |
|------|------|
| `agents/jarvis.md` | 🤖 **JARVIS** — 主控编排智能体，管理复杂任务、调度子智能体、处理 F5 技术支持工作流 |
| `agents/qkview_agent.md` | 🔍 **QkView 智能体** — 专注分析 F5 BIG-IP QkView 诊断文件，定位故障根因 |
| `agents/tshark_agent.md` | 🌐 **TShark 智能体** — 在 F5 BIG-IP 环境中进行网络抓包分析 |
| `agents/skill_creator.md` | 🛠️ **Skill 创建器** — 交互式创建和测试新的 OpenCode 技能与智能体 |
| `config/opencode.json` | ⚙️ **配置模板** — OpenCode 模型与 Provider 配置模板 |

---

## 🚀 快速开始

### 第一步：安装 OpenCode

```bash
curl -fsSL https://opencode.ai/install | bash
```

安装完成后重启终端，或执行以下命令使配置生效：

```bash
source ~/.zprofile   # macOS
source ~/.bashrc     # Linux
```

验证安装：

```bash
opencode --version
```

---

### 第二步：配置模型和 API Key

编辑 `config/opencode.json`，将占位符替换为你自己的值：

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

**常见 Provider 配置示例：**

<details>
<summary>▶ OpenAI（GPT-4o 等）</summary>

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
<summary>▶ Anthropic Claude</summary>

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
<summary>▶ 兼容 OpenAI 的 API（LiteLLM / Azure / 本地 Ollama 等）</summary>

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

---

### 第三步：复制文件到 OpenCode 配置目录

```bash
# 创建配置目录
mkdir -p ~/.config/opencode/agents

# 复制所有智能体文件
cp agents/*.md ~/.config/opencode/agents/

# 复制配置文件（如已有配置请先备份）
cp config/opencode.json ~/.config/opencode/opencode.json
```

---

### 第四步：启动 OpenCode

```bash
opencode
```

- 按 **Ctrl+A** 切换智能体
- 选择 **JARVIS** 开始使用 🎉

---

## 🤖 智能体详细介绍

### JARVIS — 主控编排智能体

JARVIS 是核心调度器，负责处理复杂的多步骤任务，将工作分发给专用子智能体并汇总结果。

**核心能力：**
- 📋 自主任务规划与进度追踪（TodoWrite）
- ⚡ 并行调度多个子智能体，大幅提升效率
- 🧠 F5 BIG-IP 专业知识库（LTM、ASM、APM、DNS、F5OS 等）
- 🔒 严格的循证推理机制，杜绝 AI 幻觉
- 🔐 PII 敏感信息安全处理

**适用场景：**
- F5 设备故障排查
- 多文件代码分析与开发
- 复杂技术问题研究与报告生成
- 自动化运维工作流

---

### 🔍 QkView 智能体 — F5 诊断文件分析

专门分析 F5 BIG-IP QkView 诊断压缩包，快速定位故障根因。

**核心能力：**
- 日志文件深度分析（含轮转日志 zgrep）
- 设备配置审查与对比
- 故障根因识别与分析
- 安全 IOC 检测
- 性能数据关联分析

**适用场景：**
- 设备宕机 / 故障排查
- 性能瓶颈分析
- 配置变更影响评估
- iHealth 诊断报告解读

---

### 🌐 TShark 智能体 — 网络抓包分析

专注于 F5 BIG-IP 环境的网络流量分析，支持 F5 Ethertrailer 字段解析和双侧流量关联。

**核心能力：**
- `.pcap` / `.pcapng` 抓包文件分析
- F5 Ethertrailer 字段提取与解析
- 客户端 ↔ 服务端双侧流量关联
- SSL/TLS 解密分析
- TCP 性能诊断（重传、窗口、RTT）
- HTTP 请求延迟定位

**适用场景：**
- 连接被 RST 重置问题
- SSL 握手失败排查
- 网络延迟与丢包分析
- 应用层响应慢定位

---

### 🛠️ Skill 创建器 — 自定义智能体工厂

交互式创建属于你自己的 OpenCode 技能（Skill）和智能体（Agent）。

**核心能力：**
- 交互式需求收集
- 生成符合规范的 Skill / Agent 文件
- 自动化 eval 基准测试
- 基于测试结果迭代优化
- 自动部署到正确路径

**适用场景：**
- 为特定业务场景定制专属智能体
- 封装团队内部知识为可复用 Skill
- 快速原型验证新的 AI 工作流

---

## 📂 目录结构

```
F5agenttools/
├── README.md               ← 英文说明
├── README_CN.md            ← 中文说明（本文件）
├── INSTALL.md              ← 详细安装指南
├── agents/
│   ├── jarvis.md           ← JARVIS 主控智能体
│   ├── qkview_agent.md     ← QkView 分析智能体
│   ├── tshark_agent.md     ← TShark 抓包分析智能体
│   └── skill_creator.md    ← Skill/Agent 创建工具
└── config/
    └── opencode.json       ← 配置模板（需填入你的 API Key）
```

---

## ❓ 常见问题

**Q：不知道 `baseURL` 填什么？**

| Provider | baseURL |
|----------|---------|
| OpenAI 官方 | `https://api.openai.com/v1/` |
| 本地 Ollama | `http://localhost:11434/v1/` |
| LiteLLM 代理 | `http://你的服务器:4000/openai/` |
| Azure OpenAI | `https://你的资源名.openai.azure.com/` |
| Anthropic | 不需要，使用 `@ai-sdk/anthropic` |

**Q：`context` 和 `output` 填多少？**

参考模型官方文档中的 context window 大小。不确定时可填 `context: 128000`，`output: 4096`，这适用于大多数主流模型。

**Q：可以同时配置多个模型吗？**

可以。在 `models` 对象里添加多个条目即可，OpenCode 启动时允许你选择使用哪个模型。

**Q：JARVIS 和 QkView/TShark 智能体是什么关系？**

JARVIS 是主控智能体，QkView 和 TShark 是它的子智能体。当你向 JARVIS 提交任务时，它会自动判断是否需要调用子智能体，无需手动切换。

**Q：这些智能体适合非 F5 场景吗？**

JARVIS 和 Skill 创建器是通用的，适合任何开发和技术支持场景。QkView 和 TShark 智能体专为 F5 BIG-IP 设计，其他场景下功能有限。

---

## 📋 系统要求

- [OpenCode](https://opencode.ai) 已安装
- 任意支持的 LLM Provider 的 API 访问权限（OpenAI、Anthropic、LiteLLM、Ollama 等）
- macOS 或 Linux

---

## 📄 许可证

MIT License — 自由使用、修改和分发。
