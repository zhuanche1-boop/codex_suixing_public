# Codex 随行 1.4.2

历史版本补录，归档日期：2026-11-10。保留原 APK 内部版本 1.4.2 / code 9；文件统一使用 Codex-Suixing 名称。

## 本版变化

- 手机主动打开 Codex 或 ChatGPT 会话时，让电脑打开对应会话；后台刷新不切换电脑页面。
- 快速切换会话时顺序处理导航并跳过过期请求。
- 修复其他项目未加载会话的模型设置被误报为响应不匹配；执行记录补充条数和输出截断提示。

## 归档与兼容说明


- Windows 按本版已留存电脑模块重新封装为字节码，使用固定 Node 22.23.4 x64；初始化工具采用当前发行方案。
- 完成历史 Node 行为测试与字节码回归，不等同于重新通过所有当前桌面版本及手机真机验证。
- 历史版本供回溯；日常使用优先选择最新版本。Android 降级可能被系统拒绝，不要为试旧版卸载主力 App 丢失配对和草稿。
- 安装方法见本版附带的使用说明；源码只保存在私有仓库。

## 版本记录

[所有历史版本](https://github.com/zhuanche1-boop/codex_suixing_public/blob/main/VERSIONS.md) · [每版新增与修复](https://github.com/zhuanche1-boop/codex_suixing_public/blob/main/CHANGELOG.md)
