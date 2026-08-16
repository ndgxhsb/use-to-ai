# AI 帮答隔离器

面向 SillyTavern 1.18.x 的独立 AI 帮答扩展。

目标：解决长对话后原生 AI 帮答被角色/旁白文风污染的问题。

## 核心机制

- 不调用原生 Impersonate。
- 使用独立 Connection Profile 请求。
- 默认关闭当前 Preset / Instruct 注入。
- 强隔离模式默认开启：先把最近剧情转换为中性事实，再结合“只来自用户历史消息”的文风样本生成下一条用户输入。
- 结果只写入 `#send_textarea`，不自动发送，不直接修改 `chat[]`。
- 会过滤 `dream_plot`、`dream_after_format`、`image###`、常见状态栏等内容。

## 安装

在 SillyTavern 中打开 Extensions → Install Extension，然后粘贴本仓库地址。

> 注意：如果仓库是私有仓库，SillyTavern 通过普通 GitHub URL 安装时通常无法直接读取。建议把此插件仓库设为 public，或先下载 ZIP 本地安装。

## 第一次使用

1. 确保 Connection Manager 中至少存在一个可用 Profile。
2. 重启 SillyTavern。
3. 输入框发送按钮附近会出现魔杖按钮和齿轮按钮。
4. 点齿轮选择 AI 帮答使用的 Connection Profile。
5. 保持“强隔离模式”开启。
6. 点魔杖生成；结果只会写入输入框，由你检查后手动发送。

## v0.1.0 测试重点

- 长对话后是否仍然模仿 AI/角色文风。
- 是否错误输出 `<dream_plot>`、状态栏或 `image###`。
- 是否替其他角色继续说话。
- 是否错误触发生图或记忆写入。
