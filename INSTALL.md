# Codex 随行 1.0.0 初始 CLI 版使用说明

这是早期独立 Codex CLI 任务架构，原 APK 内部版本为 1.0.0，不用于同步后来桌面 Codex 的已有项目会话。该架构已被后续版本替代。本次完成历史行为测试与字节码重封装，未重新验证当前 Codex CLI 接口；仅建议研究或回溯使用。

## 1. 准备

Windows x64 电脑须已安装并登录官方 Codex CLI，且提供此历史版依赖的 app-server 接口；Android 手机安装本版 APK。电脑运行时附带 Node 22.23.4 x64，保持 runtime 目录完整，不自行替换运行时。

<a id="tailscale"></a>
## 2. 用 Tailscale 连接电脑与手机

Tailscale 把你的设备连接到一个私有网络，手机在外面使用移动数据时也能访问家里的电脑。它相当于建立“虚拟局域网”，不要求两端处于同一个 Wi-Fi。**它只解决网络连通，不能替代下面的电脑连接程序。**参见 [Tailscale 设备连接说明](https://tailscale.com/docs/how-to/connect-to-devices)。

### 2.1 在 Windows 上安装

1. 从 [Tailscale 官方下载页](https://tailscale.com/download) 下载 Windows 安装程序并安装。当前 Tailscale Windows 客户端要求 Windows 10 或更新系统；桌面 Codex 本身还需满足其系统要求。
2. 在任务栏右下角找到 Tailscale 图标，必要时展开隐藏图标。右键选择 **Log in / 登录**，在浏览器中完成登录。
3. 确认 Tailscale 已连接，记住使用的登录账号和私有网络。个人使用建议手机也使用这个账号加入同一个网络。

界面随版本变化时，以 [Tailscale Windows 官方安装说明](https://tailscale.com/docs/install/windows) 为准。

### 2.2 在 Android 上安装

1. 从 [Tailscale 官方 Android 安装说明](https://tailscale.com/docs/install/android) 中的 Google Play 或官方下载入口安装。无法使用 Google Play 时，使用官方页面提供的下载渠道。
2. 打开 Tailscale，选择 **Get Started / 开始**，同意 Android 的 VPN 连接请求。
3. 使用与电脑相同的 Tailscale 账号登录，并确认两台设备处于**同一个私有网络（tailnet）**。组织账号有多个网络时尤其要检查。
4. 打开连接开关，确认显示已连接；在设备列表或 [Tailscale 管理控制台](https://login.tailscale.com/admin/machines) 中确认电脑和手机都已加入。

Tailscale 的登录账号与 ChatGPT 账号是两回事；手机的 Tailscale 登录并不等于给 Codex 随行登录 ChatGPT。

**Android 通常只能同时运行一个 VPN。**其他 VPN 或使用 VPN 通道的网络工具可能使 Tailscale 断开；遇到冲突先停止另一个 VPN，再连接 Tailscale。详见 [Tailscale 与其他 VPN 共用说明](https://tailscale.com/docs/reference/faq/other-vpns)。

### 2.3 找到电脑的 Tailscale IPv4

在 Tailscale 的设备列表或管理控制台中，选择**要运行 Codex 的那台电脑**，复制它的 IPv4 地址。不要复制手机地址、IPv6、Wi-Fi 地址或示例地址。

也可以在电脑的 PowerShell 中运行以下只读命令；Tailscale 安装到其他位置时需调整路径：

```powershell
& "$env:ProgramFiles\Tailscale\tailscale.exe" ip -4
& "$env:ProgramFiles\Tailscale\tailscale.exe" status
```

记下电脑 IPv4，下一节初始化要使用它。若组织开启设备审批或访问规则，需要由网络管理员允许手机访问该电脑的 **TCP 8765**，自定义端口则使用实际端口。

本教程只需要两台设备直接加入 Tailscale，不需要搭建子网路由器、选择出口节点或配置公网端口转发。不要把连接端口公开到互联网。

### 2.4 只在同一局域网使用

若手机与电脑已经在同一可信局域网，且网络没有隔离设备，也可不使用 Tailscale：初始化时把电脑局域网 IPv4 作为 `--host`，防火墙只允许该网络中的可信手机访问。离开这个局域网后，此地址就不能用于远程连接。

建议从一开始使用 Tailscale。程序监听初始化时指定的地址；后续切换 Tailscale / 局域网地址，需要在电脑端保留原数据重新配置地址、重启连接程序并更新手机配对，仅修改手机地址不能改变电脑监听地址。



## 3. 初始化与运行

1. 完整解压本版 Windows ZIP 到独立目录，准备一个确实存在、允许操作的项目文件夹。
2. 在解压目录运行下列命令，两个路径/地址替换为实际值。程序会查找已安装的 codex.exe；未找到时先完成官方 CLI 的安装和登录。

```powershell
.\Setup.cmd --project 'D:\你的测试项目' --host '电脑Tailscale的IPv4'
```

3. 本次重封装将初始化逻辑嵌入字节码，并把监听地址限定为明确指定的电脑 IPv4；其余历史业务模块保持原始功能。
4. 双击 Start.cmd，保持电脑唤醒、联网。此版启动会连接 CLI，不是后续版本的桌面插件架构。
5. 若防火墙拦截，只允许 runtime/node.exe、TCP 8765、电脑本地 Tailscale IP 和可信手机远程 Tailscale IP；不关闭整个防火墙，不映射公网端口。

## 4. 手机配对与任务

把电脑生成的完整 pairing.json 私下传给自己的手机，在 App 设置中导入或粘贴。此版没有二维码配对，不需要扫描二维码。核对电脑名称与地址再连接。

选择允许操作的项目，创建任务会话并发送内容；该任务由电脑上的 CLI 执行，可在此原型界面中处理当时提供的确认、输入请求和停止操作。它不等同于 1.1.0 之后的桌面原会话同步能力。

先在独立测试设备和非重要项目上验证。历史接口不匹配时应停止使用，不要把更新版业务代码换进本包却仍标为 1.0.0。此版没有后来加入的后台完成通知、文件浏览、图片预览或额度查询。

## 5. 保管与排错

- pairing.json、data、证书与令牌不能公开；不同电脑分别初始化。
- 连接超时先检查两端 Tailscale、电脑唤醒和连接窗口、防火墙范围与地址；手机其他 VPN 可能与 Tailscale 冲突。
- 启动报 CLI 接口错误时记录脱敏错误；当前 CLI 未必兼容历史协议，不把它当作手机网络问题。
- 这是独立架构，不把其 data 目录直接覆盖到正在使用的新版部署；不在主力手机上卸载新版来试装旧版。
- 需要停止时关闭本包运行窗口；不需要提醒时不为本版额外开放手机后台省电豁免。

本包采用 PolyForm Noncommercial 1.0.0（见 LICENSE），不是 OpenAI 官方产品。源码仅私有留存，公开电脑包采用字节码分发。
