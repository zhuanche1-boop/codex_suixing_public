# Codex 随行 1.0.0

历史版本补录，归档日期：2026-11-10。保留原 APK 内部版本 1.0.0 / code 1；文件统一使用 Codex-Suixing 名称。

## 本版变化

- 初始版本：通过电脑 Codex CLI 建立独立任务会话，手机收发消息并查看执行状态。
- 提供 HTTPS 配对、项目选择、任务确认与停止能力；这是早期 CLI 架构，与后续桌面原会话同步方案不同。

## 归档与兼容说明

- 此版是 CLI 架构历史原型，不应与 1.1.0 及之后的电脑配置混用。
- 本次只验证历史行为测试和字节码运行；未重新验证当前 Codex CLI 的接口兼容性。
- Windows 按本版已留存电脑模块重新封装为字节码，使用固定 Node 22.23.4 x64；初始化工具采用当前发行方案。
- 完成历史 Node 行为测试与字节码回归，不等同于重新通过所有当前桌面版本及手机真机验证。
- 历史版本供回溯；日常使用优先选择最新版本。Android 降级可能被系统拒绝，不要为试旧版卸载主力 App 丢失配对和草稿。
- 安装方法见本版附带的使用说明；源码只保存在私有仓库。

## 版本记录

[所有历史版本](https://github.com/zhuanche1-boop/codex_suixing_public/blob/main/VERSIONS.md) · [每版新增与修复](https://github.com/zhuanche1-boop/codex_suixing_public/blob/main/CHANGELOG.md)
