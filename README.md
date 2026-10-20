# tools-skills

通用工具类 AI Skills（非科研专用）——日常浏览器、系统与效率工具的 Agent 技能集。
General-purpose tool skills for AI agents (non-research): everyday browser, system, and productivity utilities.

## Skill Index

| Skill | Status | Purpose | Trigger keywords |
|-------|--------|---------|------------------|
| [`enable-chrome-ai`](skills/enable-chrome-ai/SKILL.md) | Stable | 修补 Chrome 本地配置（Local State）启用内置 Gemini / AI 历史搜索 / DevTools AI，免清除数据与重装 | "Chrome AI", "Gemini in Chrome", "enable chrome ai", "AI 历史搜索", "Chrome 内置 AI" |

## Installation

每个 `skills/*` 目录是一个可安装单元，结构为标准 `SKILL.md` + 可选 `references/`、`scripts/`。

### Codex / OpenClaw / QClaw

```bash
git clone https://github.com/zoebischuribe-cloud/tools-skills.git
mkdir -p ~/.codex/skills          # OpenClaw: ~/.openclaw/workspace/skills/
cp -R skills/enable-chrome-ai ~/.codex/skills/
```

### Claude Code

```bash
mkdir -p ~/.claude/agents
cp skills/enable-chrome-ai/SKILL.md ~/.claude/agents/enable-chrome-ai.md
```

确保 frontmatter 的 `name` / `description` 有效。

## License

MIT License（见仓库 `LICENSE`）。

**来源声明**：`enable-chrome-ai` 移植自 [lcandy2/enable-chrome-ai](https://github.com/lcandy2/enable-chrome-ai)（MIT），原作者 lcandy2，fork 自 [hzkaai/show-copilot](https://github.com/hzkaai/show-copilot)；重分发保留原版权声明（Copyright (c) 2026 citron），详见其目录内 `LICENSE`。
