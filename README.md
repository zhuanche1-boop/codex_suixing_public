# Codex 随行 · Codex Companion

Your computer works. You stay connected.

非官方 Codex 安卓伴侣：手机查看电脑会话、下发任务，工作由电脑执行。**当前只有 Android 手机版本，电脑运行包支持 Windows x64。**

这是程序发布仓库，不公开项目源码。软件采用 PolyForm Noncommercial 1.0.0，详见 LICENSE。不是 OpenAI 官方产品。

## 下载

前往 [Releases](https://github.com/zhuanche1-boop/codex_suixing_public/releases) 下载同一发行版本的：

- `Codex-Suixing-1.4.9.apk`：Android App。
- `Codex-Suixing-1.4.9-Windows-x64.zip`：电脑连接程序。
- `SHA256SUMS.txt`：文件校验值。

GitHub 自动生成的 Source code 压缩包只包含这个公开仓库中的说明和许可，不是 App 源码或安装包。

## 功能

- 同步电脑项目、最近对话和未归属项目的会话；新建、继续和重命名对话。
- 手机上传文件，浏览电脑文件及本地图片；图片主动保存才落盘。
- 按设备配对、扫码连接。即使多台电脑使用同一账号，手机仍按各电脑独立保存配对和草稿；当前一次连接一台电脑。这不改变账号云端聊天的同步规则。
- 中间进展持续同步；任务完成和待确认时按系统设置提醒。
- 待确认时显示“需要远程桌面”卡片；本软件不代点桌面审批，也不内置远程桌面。
- 额度圆环在前台自动更新，点击可查看详情；退到后台不新增额度查询。模型与思考强度设置依赖已适配的桌面版本。
- 会话列表显示电脑提供的未读标记，复用已有列表刷新。

## 安装与使用

**第一次使用请先阅读 [完整使用说明](INSTALL.md)**：包括 Tailscale 安装与组网、电脑初始化、手机扫码配对、日常操作、后台提醒与省电、升级和故障排查。

1. 在 Windows 电脑和 Android 手机上安装 Tailscale，登录并加入同一个私有网络。它让两端在不同 Wi-Fi 或移动数据下也能互访；Tailscale 账号与 ChatGPT 账号互相独立。
2. 在电脑完整解压 Windows 包，让本机桌面 Codex 按说明运行 `Setup.cmd` 初始化，再运行 `Start.cmd`。
3. 手机安装同版本 APK，扫描 `Show-Pairing.cmd` 显示的二维码；连接后按说明做一次验证。

手机无需登录 ChatGPT。同一可信局域网也可按完整说明使用电脑局域网地址。电脑必须保持唤醒、联网，并运行桌面 Codex 和连接程序；每台电脑分别初始化，不能互相复制配对数据。

完整版说明随公开仓库更新；已下载旧安装包的用户也请先查看上述说明。

## 限制

桌面接口可能随官方更新改变；即时模型设置目前仅适配桌面构建 `26.1103.4239.0`。电脑当前页面自动跟随、原生输入框草稿同步、跨端阅读位置、原生附件卡片、权限审批、停止任务及部分项目编辑功能尚未接入。手机正文最多保留 60 条于内存，完整记录在电脑；后台提醒受系统省电策略影响。

电脑程序以字节码分发，不直接包含业务源文件，但不能保证无法逆向分析。第三方运行时的代码和许可独立保留。

## 版本记录

[所有历史版本](https://github.com/zhuanche1-boop/codex_suixing_public/blob/main/VERSIONS.md) · [每版新增与修复](https://github.com/zhuanche1-boop/codex_suixing_public/blob/main/CHANGELOG.md)
