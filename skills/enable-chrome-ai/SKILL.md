---
name: enable-chrome-ai
description: 修补 Chrome 本地用户数据（Local State 中的 is_glic_eligible、variations_country、variations_permanent_consistency_country）以启用 Chrome 内置 AI 功能（Gemini、AI 历史记录搜索、DevTools AI），无需清除数据或重装浏览器。当用户需要启用 Chrome 内置 AI / Gemini、AI 历史搜索或 DevTools AI，或遇到 Chrome 内置 AI 因地区/资格限制不可用、需要打补丁启用时使用本技能。来源仓库：https://github.com/lcandy2/enable-chrome-ai（MIT）。
---
# Enable Chrome AI

修补 Chrome 本地 profile 数据，启用 Chrome 内置 AI 功能（Gemini、AI 历史记录搜索、DevTools AI 创新功能），免清除数据、免浏览器 flag、免重装。

## 快速运行

1. 环境准备：Python 3.13+；安装依赖 `python -m pip install psutil`（或 `uv sync`）。
2. 运行：`python scripts/enable_chrome_ai.py`。
3. 脚本关闭 Chrome → 修补 → 自动重启 Chrome → 按 Enter 结束。

前置条件：以拥有 Chrome profile 的同一 OS 用户运行；Chrome 至少启动过一次（确保 `User Data/Local State` 已生成）。

## 修补内容

1. 自动探测 Windows / macOS / Linux 的 Chrome Stable / Canary / Dev / Beta 用户数据目录。
2. 关闭顶层 Chrome 进程（避免文件锁），记录其可执行路径。
3. 每个 `Local State` JSON 中：递归置所有 `is_glic_eligible=true`；根级 `variations_country="us"`；`variations_permanent_consistency_country=["<版本号>","us"]`。
4. 重启修补前正在运行的 Chrome。

## 核心注意事项

- `Local State` 不存在会失败——先启动一次 Chrome。
- 仅当能从进程探测到可执行路径时才自动重启 Chrome。
- macOS 按名称识别进程，可能终止超出"顶层"的范围；Linux 按可执行名 `chrome` 识别，构建名不同则可能关不掉（文件锁）。
- 脚本会写入现有 Chrome profile，介意先备份 `User Data`；非 Google 官方产品，风险自担。
- 只修补本地 profile JSON，不联网、不改系统配置。

## 详细参考

完整安装方式（uv / pip 分支）、平台细节与排查清单见 `references/readme-zh.md`（官方中文 README 整理）——需要完整步骤、平台差异或故障排查时读取；快速执行时无需加载。
