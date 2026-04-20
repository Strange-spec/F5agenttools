# 安装指南（中文）

## 第一步：安装 OpenCode

```bash
curl -fsSL https://opencode.ai/install | bash
```

安装完成后重启终端，或执行：
```bash
source ~/.zprofile   # macOS zsh
# 或
source ~/.bashrc     # Linux bash
```

验证安装：
```bash
opencode --version
```

## 第二步：配置模型和 API Key

编辑 `config/opencode.json`，将以下占位符替换为你自己的值：

| 占位符 | 替换为 |
|--------|--------|
| `YOUR_PROVIDER_NAME` | 提供商名称，如 `openai`、`anthropic`、`my_llm` |
| `YOUR_API_BASE_URL` | API 地址，如 `https://api.openai.com/v1/` |
| `YOUR_API_KEY` | 你的 API Key |
| `YOUR_MODEL_NAME` | 模型名称，如 `gpt-4o`、`claude-sonnet-4-5` |

## 第三步：复制文件到 OpenCode 配置目录

```bash
# 创建目录
mkdir -p ~/.config/opencode/agents

# 复制 agents
cp agents/*.md ~/.config/opencode/agents/

# 复制配置文件（如已有配置请先备份）
cp config/opencode.json ~/.config/opencode/opencode.json
```

## 第四步：启动 OpenCode

```bash
opencode
```

- 按 **Ctrl+A** 切换 Agent
- 选择 **JARVIS** 开始使用

## 常见问题

**Q: 不知道 baseURL 填什么？**
- OpenAI 官方：`https://api.openai.com/v1/`
- Anthropic：不需要 baseURL，直接用 `@ai-sdk/anthropic` npm 包
- 本地 Ollama：`http://localhost:11434/v1/`
- LiteLLM 代理：`http://你的服务器地址:4000/openai/`

**Q: context 和 output 填多少？**
- 参考模型官方文档，填实际支持的 token 数
- 不确定时可填 `context: 128000`，`output: 4096`

**Q: 多个模型怎么配置？**
在 `models` 对象里添加多个条目即可，OpenCode 启动时可选择使用哪个模型。
