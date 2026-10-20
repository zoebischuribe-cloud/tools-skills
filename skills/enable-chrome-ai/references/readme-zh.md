# Enable Chrome AI — 中文参考文档（官方 README 中文版整理）

> 来源：https://github.com/lcandy2/enable-chrome-ai（MIT）· 官方 `README.zh.md`（main 分支）
> 用途：SKILL.md 的精简版只保留执行要点；完整安装方式、平台细节与故障排查在本文件，按需读取。

在 Google Chrome 中启用 Gemini、AI 历史搜索、DevTools AI 等创新功能——无需清除数据或重新安装。
轻量 Python 脚本，通过修改本地 Chrome 配置（`variations_country`、`variations_permanent_consistency_country` 和 `is_glic_eligible`）启用浏览器内置 AI 功能，无需额外开关。

## 环境要求

- Python `3.13+`（见仓库 `.python-version` / `pyproject.toml`）
- 已安装 Google Chrome（Stable/Canary/Dev/Beta 任一）

## 快速开始（uv）

1. 安装 uv（一次性）：
   - Windows: `powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"`
   - macOS & Linux: `curl -LsSf https://astral.sh/uv/install.sh | sh`
   - 更多安装方式见 [uv 安装文档](https://docs.astral.sh/uv/getting-started/installation/)
2. 安装依赖（自动创建虚拟环境）：`uv sync`
3. 运行脚本：`uv run main.py`
4. 补丁过程中 Chrome 会被关闭；重启后按提示按 Enter 结束

## 快速开始（pip）

1. 创建并激活虚拟环境
2. 安装依赖：`python -m pip install psutil`
3. 运行：`python main.py`

## 脚本做了什么

- 自动定位 Windows / macOS / Linux 上的 Chrome Stable / Canary / Dev / Beta 用户数据目录
- 关闭顶层 Chrome 进程以避免文件锁，补丁后恢复
- 在 `Local State` 中递归查找并将所有 `is_glic_eligible` 设为 `true`
- 在 `Local State` 中将 `variations_country` 设为 `"us"`
- 在 `Local State` 中将 `variations_permanent_consistency_country` 设为 `["<版本号>", "us"]`
- 重启补丁前已运行的 Chrome 版本

## 已知限制 / 注意事项

- 脚本假设 `User Data/Local State` 已存在；若缺失可能直接失败（可先启动一次 Chrome 生成配置）
- 只有在能从进程信息中取到可执行文件路径时，脚本才会自动重启 Chrome
- macOS 上按进程名（`Google Chrome*`）识别，可能会终止不止"顶层"应用进程
- Linux 上按可执行文件名 `chrome` 识别；若发行版/安装方式使用其他名字，可能不会关闭 Chrome（从而仍可能有文件锁）
- 脚本会修改现有 Chrome 配置，介意可先备份 `User Data`
- 使用拥有该 Chrome 配置的同一系统用户运行，确保有写入权限
- 与 Google 无关，风险自担

## 许可与致谢

- 许可：MIT；转载或基于本研究二次创作需注明来源
- 致谢：原作者 lcandy2；仓库 fork 自 [show-copilot](https://github.com/hzkaai/show-copilot)
