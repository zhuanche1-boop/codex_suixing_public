# Codex 随行 1.4.5

历史版本补录，归档日期：2026-11-10。保留原 APK 内部版本 1.4.5 / code 12；文件统一使用 Codex-Suixing 名称。

## 本版变化

- 新增离线扫码配对：电脑生成二维码，手机扫描后核对电脑名称与地址。
- 扫码页面按需使用相机，离开后释放；二维码保存在受保护的本地目录，重新显示不会重置配对身份。

## 归档与兼容说明

- 配对二维码含遥控凭证，不应公开；扫码不替代 Tailscale 等网络连通条件。
- Windows 按本版已留存电脑模块重新封装为字节码，使用固定 Node 22.23.4 x64；初始化工具采用当前发行方案。
- 完成历史 Node 行为测试与字节码回归，不等同于重新通过所有当前桌面版本及手机真机验证。
- 历史版本供回溯；日常使用优先选择最新版本。Android 降级可能被系统拒绝，不要为试旧版卸载主力 App 丢失配对和草稿。
- 安装方法见本版附带的使用说明；源码只保存在私有仓库。

## 版本记录

[所有历史版本](https://github.com/zhuanche1-boop/codex_suixing_public/blob/main/VERSIONS.md) · [每版新增与修复](https://github.com/zhuanche1-boop/codex_suixing_public/blob/main/CHANGELOG.md)
