# 1.安装指南
从官方文档和生态来看，在 Cursor 里使用它主要有两大路径：
**CLI安装（官方推荐）** 和 **手动安装**

这里主要介绍官方安装步骤：

==前置条件：==
搜索脚本需要Python 3.x 环境支持
```
# 检查 Python 是否已安装
python3 --version

# macOS
brew install python3
```

参考链接 https://ui-ux-pro-max-skill.com/docs/cli-reference/
```
# 全局安装 CLI 工具
npm install -g uipro-cli
# 进入你的项目目录
cd /path/to/your/project
# 为指定 AI 助手安装技能

uipro init --ai claude # Claude Code
uipro init --ai cursor # Cursor
uipro init --ai windsurf # Windsurf
uipro init --ai antigravity # Antigravity (.agent + .shared)
uipro init --ai copilot # GitHub Copilot
uipro init --ai kiro # Kiro
uipro init --ai all # 所有 AI 助手
```
