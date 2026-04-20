导览（windows系统）
本章节包括：
	完成 Git、Node.js 和 Claude Code 的安装
	配置 GLM 模型
	遇到的故障排除等
参考网站：
https://www.vibevibe.cn/Advanced/01-environment-setup/00-quick-start.html
https://code.claude.com/docs/zh-CN/setup#native-install-recommended
https://code.claude.com/docs/zh-CN/troubleshooting#windows-powershell
https://docs.bigmodel.cn/cn/coding-plan/tool/claude

# Claude code安装前置环境
## 安装GIT
下载地址：[https://registry.npmmirror.com/-/binary/git-for-windows/v2.52.0.windows.1/Git-2.52.0-64-bit.exe](https://registry.npmmirror.com/-/binary/git-for-windows/v2.52.0.windows.1/Git-2.52.0-64-bit.exe)

![[GIT.png|637]]

下载之后双击开始安装，**一直点"下一步"即可**。
## Node.js  安装
Claude Code 是基于 Node.js 开发的 CLI（命令行）工具，因此你的电脑上必须先安装 Node。
**下载地址**：[https://npmmirror.com/mirrors/node/v24.13.0/node-v24.13.0-x64.msi](https://npmmirror.com/mirrors/node/v24.13.0/node-v24.13.0-x64.msi)


![[Pasted image 20260420233911.png|718]]

下载后双击安装，**一直点"下一步"即可**（已安装可跳过）。

## 安装验证
如您不清楚PC上是否已经安装GIT、Node.js。可先通过终端查看。
具体步骤：
- 按 `win` + `R` 唤起运行窗口输入 `cmd` 打开终端或**Windows PowerShell**
- 在终端中输入
```
git --version
node -v
```
如果显示版本号，说明安装成功/已经安装。

# Claude安装
本次安装推荐本地安装。
**Windows PowerShell：**
```
irm https://claude.ai/install.ps1 | iex
```
命令输入后画面出现卡顿不是命令错误，是正在以国内网络访问`storage.googleapis.com` 下载，只需等待一段时间即可。
安装完成后，执行：

```
claude
```
如果看到 Claude Code 的欢迎界面，说明安装成功！

![[Pasted image 20260420235003.png|710]]

首次安装会出现两个初始化选项：
1.主题：根据个人爱好选择即可
2.claude付费模式选择：
1. Claude account with subscription (网页版订阅用户)
2. Anthropic Console account (API 开发者用户)
3. 3rd-party platform (第三方云平台用户)
选择模式之后Claude即正式安装完成，可以使用。

# GLM模型配置
在初始化Claude时选择了Anthropic Console account (API 开发者用户)的用户可以自己配置API key去使用Claude。
Claude Code 默认使用 Claude 官方模型，但你可以配置国内模型（如 GLM），更便宜且访问快，以下时配置步骤。
## 获取API key
访问 [智谱开放平台](https://open.bigmodel.cn/)，点击右上角的「注册/登录」按钮，按照提示完成账号注册流程。登录后，在个人中心页面，点击 [API Keys](https://bigmodel.cn/usercenter/proj-mgmt/apikeys)，创建一个新的 API Key。

![[Pasted image 20260421000211.png|618]]

![[Pasted image 20260421000308.png|654]]


## 安装小助手--一件配置
智谱平台为Claude单独适配了插件，只需输入`API key`即可自动配置。
在终端/PowerShell 中执行：
```
npx @z_ai/coding-helper
```
输入获取的`GLM key`，工具会自动完成所有配置。
官方文档
更多配置详情可参考 [GLM 官方文档 - Claude Code 配置指南](https://docs.bigmodel.cn/cn/coding-plan/tool/claude)。

## 开始使用Claude
配置完成后，进入一个您的代码工作目录，在终端中执行 `claude` 命令即可开始使用 **Claude Code**

> 若遇到「Do you want to use this API key」选择 Yes 即可

启动后选择信任 Claude Code 访问文件夹里的文件，如下：

![[Pasted image 20260421001129.png|724]]

# 常见故障和安装问题
详细文档参考官方文档：[Claude Code安装和使用中常见问题的解决方案](https://code.claude.com/docs/zh-CN/troubleshooting)
下列举我遇到的常见问题：
## 网络连接问题
当运行Claude时出现以下报错：
```
 Failed to connect to api.anthropic.com: ERR_BAD_REQUEST
 Please check your internet connection and network settings.
 Note: Claude Code might not be available in your country. Check supported countries at  https://anthropic.com/supported-countries
```
别担心，这是配置 Claude Code 时非常常见的一道门槛。这主要是**终端网络环境**的问题。
### **解决方案**：为 PowerShell 配置终端代理（最常见原因）
即使你的电脑已经开启了 VPN 或代理软件，Windows 的 PowerShell 终端默认是不会走系统代理的。这就导致 Claude Code 实际上是用国内/本地的直连网络去访问 `api.anthropic.com`，从而被拦截。
在终端中输入以下命令来**临时**设置代理环境变量。
具体的代理端口可通过你的代理软件查看。（比如 Clash 默认是 7890，v2ray 默认通常是 10808）
```
$env:HTTPS_PROXY="http://127.0.0.1:7890"
$env:HTTP_PROXY="http://127.0.0.1:7890"
```
## path问题
当运行Claude时出现以下报错：
```
`未找到命令：Claude` 或 `'Claude' 未被识别`
```
如果安装成功但运行 `claude` 时出现 `command not found` 或 `not recognized` 错误，则安装目录不在您的 PATH 中。您的 shell 在 PATH 中列出的目录中搜索程序，安装程序在 Windows 上放在 `%USERPROFILE%\.local\bin\claude.exe`。通过列出您的 PATH 条目并过滤 `local/bin` 来检查安装目录是否在您的 PATH 中：
在终端中输入：
```
$env:PATH -split ';' | Select-String 'local\\bin'
```
如果没有输出，将安装目录添加到您的用户 PATH：
```
$currentPath = [Environment]::GetEnvironmentVariable('PATH', 'User')
[Environment]::SetEnvironmentVariable('PATH', "$currentPath;$env:USERPROFILE\.local\bin", 'User')
```
重启您的终端以使更改生效。验证修复是否有效：
```
claude --version
```
