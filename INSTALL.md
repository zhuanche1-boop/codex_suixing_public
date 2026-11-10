# Codex 随行 1.4.7 历史版使用说明

本次归档使用原 Android 1.4.7 安装包，电脑业务模块来自本版可验证历史源码。文件名统一为 Codex-Suixing；内部包名与签名保持不变。

这是历史版本，功能以对应 Release 的“本版变化”和实际界面为准。未重新对所有当前手机与桌面版本完成真机验收，日常使用优先选择最新版本。不要将新版本全部功能视为旧版本已有能力。

## 1. 准备条件

- Android 8.0 或更新手机、Windows x64 电脑。
- 电脑已安装并登录桌面 Codex，具有 codex-app-tools 桌面连接能力，至少有一个本地已有对话。
- 电脑保持唤醒，桌面 Codex 与连接程序持续运行。手机无需登录 ChatGPT。
- 从本版 Release 下载 APK、Windows-x64.zip、使用说明和 SHA256SUMS.txt；不要下载 GitHub 自动生成的 Source code 包作为安装包。

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



## 3. 初始化电脑

1. 将 Windows ZIP 完整解压到固定目录，例如 D:\Codex-Suixing-1.4.7。保持 runtime、vendor（若有）和所有配套文件完整；无需另外安装 Node.js。
2. 让这台电脑的桌面 Codex 在一个已有对话中读取本机真实会话 ID 和电脑 Tailscale IPv4，在解压目录运行以下命令。两处中文值必须替换，不要猜测或使用其他电脑的值。

```powershell
.\Setup.cmd --thread-id '本机真实Codex会话ID' --host '电脑Tailscale的IPv4'
```

3. 看到生成 pairing.json 和连接地址后，双击 Start.cmd。电脑运行窗口可最小化，但不能关闭；不要重复启动同一端口。
4. 若 Windows 防火墙拦截，只允许本程序 runtime/node.exe 的 TCP 8765（或实际端口），本地地址限定为电脑 Tailscale IP，远程地址限定为可信手机 Tailscale IP。不关闭整个防火墙，不开放公网端口。
5. 本次重封装采用当前已验证的初始化工具：保留原设备令牌/证书，监听明确指定的 IPv4；并未替换旧版会话、消息等业务模块。固定使用随包 Node 22.23.4 x64，不单独替换运行时。

## 4. 手机安装与配对

1. 打开 APK 安装到手机，按系统提示允许本次安装来源。已有新版 App 时不要为了降级而卸载，卸载可能丢失配对和草稿；建议历史版本只在独立测试设备上使用。
2. 两端 Tailscale 在线，电脑连接程序已启动。
3. 在 App 设置中导入本机的完整 pairing.json，或粘贴其完整内容；核对电脑名称、地址后连接。
4. 支持扫码配对，也可导入 pairing.json。 如果使用扫码功能，在电脑双击 Show-Pairing.cmd 打开二维码；浏览器未打开时可运行 Show-Pairing.cmd --no-open，再打开 data/pairing-qr.html。没有扫码功能的旧版不提供这个入口。
5. pairing.json、data 和二维码包含私人遥控凭证，不要上传仓库、群聊或在线二维码网站。

## 5. 使用与连接检查

连接成功后打开项目与已有会话，输入文字并发送，由电脑执行。各版支持的菜单和文件能力以实际界面为准。遇到发送结果不确定，先在电脑确认是否已收到，再决定重发。

首次可在允许测试的会话发送“请只回复连接测试成功，不修改文件或运行命令”。这会新增一轮真实对话并可能消耗少量额度。异地使用前，切换手机到移动数据并保持 Tailscale 连接，确认会话仍可刷新。

若该版有“消息提醒”设置，允许系统通知并测试一次。先使用系统默认省电策略；只有锁屏后收不到提醒时，再针对 Codex 随行和 Tailscale 调整后台权限。关闭声音只影响提醒方式；关闭消息提醒或“暂停接收”才停止后台接收，恢复需在设置重新开启。1.1.0 尚无后台完成提醒。

## 6. 多电脑、备份与升级

每台电脑分别初始化。不同电脑不得互相复制 data 或 pairing.json；有多电脑列表的版本可在设置中切换，其余版本需重新导入目标电脑信息。

同一电脑升级时，新包解压到独立目录，在可以暂时断开时停止旧连接程序。备份并复制本机完整 data 和 pairing.json，保留证书、令牌、desktop-sends.json 等记录后，从新目录启动。更新按程序路径设置的防火墙规则。原文件及安装包保留备份；不同时启动两份服务。

## 7. 排错

| 现象 | 检查 |
| --- | --- |
| 连不上 / 超时 | 两端是否同一 Tailscale 网络、电脑是否唤醒、程序是否已启动、地址是否为电脑 IP、端口与防火墙是否正确、手机是否有其他 VPN 冲突 |
| 缺少会话 ID | 在本机已有桌面 Codex 对话中执行初始化，使用真实 ID |
| 缺少桌面插件 | 该桌面环境需提供 codex-app-tools，只有网页版或命令行工具不够；旧接口也可能已不兼容当前桌面版本 |
| 身份验证失败 | 核对对应电脑，恢复原 data 身份或确认设备身份后重新导入；不要跳过证书校验 |
| 只在 Wi-Fi 可用 | 配对是否误用局域网地址，移动数据下 Tailscale 是否仍在线 |
| 没有某个新版按钮 | 旧版未必具有新功能，查看对应版本变化记录，不把最新说明当成旧版功能清单 |

软件采用 PolyForm Noncommercial 1.0.0，详见随包 LICENSE；第三方组件许可独立保留。不是 OpenAI 官方产品，业务源码只存于私有仓库。字节码分发不保证无法逆向分析。
