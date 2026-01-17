AI 圈一直在寻找强大的 Claude 或 GPT 替代方案。最近，**NVIDIA（英伟达）**悄然推出重磅福利：通过 **NIM 平台**免费提供 **GLM-4.7** 和 **MiniMax M2.1** 的 API 接入。

这两个模型在编程和工程领域表现强悍。如果你苦于没有外网环境使用 Claude Code，这套"英伟达全家桶"绝对是目前的最佳替代方案。

![image.png](attachment:f17dfbf6-60ca-47e6-95f5-aa376b071602:image.png)

---

## 🚀 为什么值得尝试这两个模型？

这两个模型在开发者圈子里口碑极佳：

- **GLM-4.7**：近期编程领域的黑马。实测表明，它的代码生成逻辑和纠错能力已稳居**第一梯队**，某些场景下甚至不输 Claude 3.5。
- **MiniMax M2.1**：擅长**多语言工程能力**，处理复杂指令和长上下文表现稳健，被认为是可以正面对抗闭源大模型的国产之光。

最关键的是：**注册即用，免费且暂无明显限额。**

---

## 🛠️ 三步搭建顶级 AI 工作站

### 第一步：获取 NVIDIA 免费 API Key

1. 访问 [[NVIDIA NIM 官网](https://build.nvidia.com/)](https://build.nvidia.com/)并注册账户。
2. 登录后进入设置中心，生成 **API Keys**。
3. **注意：**过期时间建议勾选"永不过期"，妥善保存这个 Key。

![image.png](attachment:80bc3dbb-2793-42f4-9396-1bb3f4c02e50:image.png)

### 第二步：配置 [Cherry Studio](https://cherry-ai.com/) 客户端

为获得最佳使用体验，推荐搭配 **Cherry Studio**（支持智能对话、自主 Agent 和统一模型管理）。

![image.png](attachment:4a00dec9-e2b7-4a80-8740-9490ea7e74fe:image.png)

1. 下载并安装 [Cherry Studio](https://cherry-ai.com/)。
2. 点击左下角「设置」（齿轮图标），选择左侧菜单的「模型服务」。
3. 在右侧服务商列表中找到**「英伟达（NVIDIA）」**。
4. 填入刚才获取的 **API Key**。

![image.png](attachment:e36e02e3-89b2-47ef-a44e-08a417762cf1:image.png)

### 第三步：添加并启用模型

1. 在 Cherry Studio 设置页面底部点击「管理」按钮。
2. 在搜索框中分别搜索并添加以下模型 ID：
    - `z-ai/glm4.7`
    - `minimaxai/minimax-m2.1`
3. 确认添加后，即可在对话窗口切换使用这两个模型。

![image.png](attachment:6dcd90b7-4340-47fd-a4c8-ea5b170f6428:image.png)

![image.png](attachment:16b3636b-58af-4a24-9557-1f2cdc9ce640:image.png)

---

## 🧪 实战测试：生成全栈 Web 应用

为了测试真实能力，我使用了一个复杂的 Prompt，让模型设计并编写一个名为《活着么》（类似"死了么" App）的 Web 应用。

### 提示词需求（部分）：

> 你是一名资深全栈工程师。请设计《活着么》状态确认应用。
> 
> - **功能**：邮箱登录、每日签到（存活确认）、状态留言（很好/还行/累）、24小时未签到自动邮件通知亲友。
> - **技术栈**：前端 Vue/React，后端 Node.js，数据库 SQLite。
> - **审美**：极简、温暖、高级感、动态背景。

### 运行结果反馈：

不管是 GLM-4.7 还是 MiniMax M2.1，给出的代码结构都非常清晰：

- **工程化思维极强**：自动生成了清晰的项目目录结构。
- **代码完整度高**：从后端的心跳检测逻辑到前端的 Canvas 状态趋势图，注释详尽且可以直接运行。
- **UI 审美在线**：CSS 自动生成了呼吸灯动效和柔光渐变背景，完全符合“高级感”的要求。