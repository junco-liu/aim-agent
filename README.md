<h1 align="center">AIM Agent</h1>

<p align="center">
  面向 VEX AIM 机器人的具身智能体框架<br>
  语音 • 视觉 • 记忆 • 工具调用 • 自主决策
</p>

<!-- <p align="center">
  <a href="./README.md">English</a>
  &nbsp;|&nbsp;
  <strong>简体中文</strong>
</p> -->

<p align="center">
  <a href="https://github.com/junco-liu/aim-agent">
    <img src="https://img.shields.io/github/stars/junco-liu/aim-agent?style=flat-square&color=dbab09&labelColor=161b22&logo=github&logoColor=white" alt="stars"/>
  </a>

  <a href="https://github.com/junco-liu/aim-agent/network/members">
    <img src="https://img.shields.io/github/forks/junco-liu/aim-agent?style=flat-square&color=58a6ff&labelColor=161b22&logo=github&logoColor=white" alt="forks"/>
  </a>

  <a href="https://github.com/junco-liu/aim-agent/releases/latest">
    <img src="https://img.shields.io/github/v/release/junco-liu/aim-agent?style=flat-square&color=482bc9&labelColor=161b22&logo=github&logoColor=white&label=latest" alt="release"/>
  </a>

  <a href="https://www.python.org/">
    <img src="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat-square&labelColor=161b22&logo=python&logoColor=white" alt="python"/>
  </a>

  <a href="https://gitee.com/junco-liu/aim-agent">
    <img src="https://img.shields.io/badge/Gitee-Mirror-C71D23?style=flat-square&labelColor=161b22&logo=gitee&logoColor=white" alt="Gitee"/>
  </a>
</p>

---

## 什么是 AIM Agent？

AIM Agent 是一个面向 [VEX AIM 编程机器人](https://api.vex.com/aim/index.html)的智能体应用。它使机器人能够感知环境、进行推理并做出自主决策——将 VEX AIM 从可编程机器人转变为能够进行自然交互的智能体。

通过将 VEX AIM WebSocket 库与大语言模型相结合，AIM Agent 打通了 AI 推理与物理机器人控制之间的桥梁。

## 核心能力

- [x] **语音交互** - 通过自然语言语音指令与机器人对话，支持实时语音识别与语音合成 
- [ ] **视觉感知** - 利用机器人摄像头进行物体检测、颜色识别和 AprilTag 检测 
- [x] **记忆** - 在多轮交互中维护对话上下文和环境状态，自动保留最近十轮对话 
- [x] **工具调用** - 大语言模型可自主调用机器人控制函数（运动、传感器、屏幕、声音、LED） 
- [x] **自主决策** - 智能体感知环境、推理情况并自主决定行动，无需人工干预 
- [ ] **传感器访问** - 读取机器人惯性传感器、视觉系统和触摸屏数据 
- [x] **屏幕与声音** - 绘制图形、显示文字、展示表情、播放声音和音符 
- [x] **LED 控制** - 设置机器人 LED 颜色，用于指示状态或表达情绪 
- [x] **对话附图** - 发送消息时自动附带机器人当前摄像头画面，让 AI "看见"环境 

## 前置条件

- 一台 VEX AIM 编程机器人，VEXos 版本 1.0.1 或更高
- 阿里云百炼 API Key（DashScope）

## 开始之前

### 为 VEX AIM 设置联网配置

VEX AIM 机器人支持两种 Wi-Fi 连接模式：

#### 热点模式（仅在此模式下为AIM配网）

在热点（Access Point, AP）模式下，机器人创建自己的 Wi-Fi 网络，电脑可直接连接，无需路由器。

1. 在机器人屏幕上，进入 **设置 → 无线电 → 热点**
2. 启用热点模式（图标变绿表示已启用）
3. 点击热点图标查看连接信息：
   - **MAC 地址**
   - **Wi-Fi 网络 SSID**
   - **Wi-Fi 网络密码**
   - **IP 地址**（默认：`192.168.4.1`）
4. 在电脑上，使用显示的密码连接到机器人的 Wi-Fi SSID

> **注意：** 连接到机器人的 Wi-Fi 将断开当前正在使用的其他 Wi-Fi 网络。

详细操作请参阅 [Wi-Fi 初始设置指南](https://api.vex.com/aim/home/websocket/wifi_setup/connection_initial.html)。

#### 联网模式

在联网模式下，机器人加入已有的 Wi-Fi 网络。当需要同时访问互联网和机器人时，此模式更为适用。

配置详情请参阅 [配置 VEX AIM Wi-Fi 联网模式](https://api.vex.com/aim/home/websocket/wifi_setup/connection_sta.html)。

### 获取阿里云百炼 API Key

AIM Agent 通过阿里云百炼平台调用大语言模型。请按以下步骤获取 API Key：

1. 访问 [阿里云百炼控制台](https://bailian.console.aliyun.com/cn-beijing?tab=api#/api)
2. 使用阿里云账号注册或登录（支持手机号或支付宝）
3. 完成个人实名认证（免费额度必需）
4. 进入 **API Key 管理**，点击 **创建 API Key**
5. 复制并妥善保存你的 API Key

> **提示：** 新用户完成实名认证后可获得免费 Token 额度。

你也可以在 [DashScope 控制台](https://dashscope.aliyun.com/) 管理 API Key。

## 使用示例

- 走一个正方形
- 演奏小星星
- 看到球了吗，过去拿球

## 使用手册

### 界面概览

AIM Agent 采用侧边栏导航布局，包含四个主要页面：

| 页面 | 图标 | 说明 |
|---|---|---|
| **对话** | ![](/images/icons/speech_bubbles_chat_conversation_messages.svg) | 与 AI 机器人进行对话交互 |
| **帮助** | ![](/images/icons/help.svg) | 查看帮助文档（即本页面） |
| **设置** | ![](/images/icons/management_settings.svg) | 配置机器人连接和 API Key |
| **关于** | ![](/images/icons/info.svg) | 查看应用版本和模型信息 |

### 对话功能

#### 文字对话

在底部输入框中输入消息，按 **Enter** 发送，**Shift+Enter** 换行。AI 会根据对话内容自主决定是否调用机器人控制功能。

#### 语音输入

- 点击输入框左侧的语音按钮
- 再次点击或按键结束录音，语音将自动转为文字并发送
- 录音期间按钮会变色提示当前状态

#### 视频流与对话附图

- 点击工具栏的相机按钮，一键开启视频流 + 对话附图功能
- 开启后右侧将显示机器人摄像头实时画面，同时每次对话会自动附带当前画面
- 再次点击按钮可关闭视频流并收起摄像头面板
- 摄像头面板下方会显示分辨率、帧率和延迟信息

#### 对话管理

- **复制**：每条消息旁有复制按钮，可快速复制消息内容
- **删除**：用户消息旁有删除按钮，删除时会同时移除对应的 AI 回复
- **重新生成**：AI 消息旁有重新生成按钮，可重新获取 AI 回复
- **清空对话**：点击工具栏的 🗑 按钮可清空所有对话记录

### 设置页面

#### 连接区域

- **机器人 IP**：输入 VEX AIM 机器人的 IP 地址（默认 `192.168.4.1`）
- **连接/断开**：点击按钮连接或断开机器人

#### 模型区域

- **API Key**：输入阿里云百炼 API Key，点击保存按钮保存
- **TTS 音色**：选择语音合成的音色，可选：
  - Cherry — 甜美女声（默认）
  - Serena — 温柔女声
  - Ethan — 沉稳男声
  - Chelsie — 活泼女声
  - Jada — 知性女声

### 主题切换

点击顶部标题栏的主题切换按钮，可在浅色/深色主题之间切换。所有页面、图标、滚动条等均会适配当前主题。

### 帮助页面

帮助页面自动从远程仓库加载最新文档。如果加载失败，可右键点击页面选择"刷新"重新加载。

### 关于页面

查看当前版本号、使用的模型信息、相关链接和版权声明。

### 使用的模型

| 功能 | 模型 | 说明 |
|---|---|---|
| 对话推理 | qwen3.6-plus | 大语言模型，负责理解指令与工具调用 |
| 语音合成 | qwen3-tts-flash-realtime | 实时流式 TTS，输出 pcm 格式 |
| 语音识别 | paraformer-realtime-v2 | 实时流式 ASR，支持中文语音输入 |

## 参考链接

- [VEX AIM API 参考](https://api.vex.com/aim/index.html) — VEXcode AIM 官方 API 文档
- [VEX AIM WebSocket 库](https://github.com/VEX-Robotics/AIM_Websocket_Library) — VEX AIM Python WebSocket 客户端
- [Wi-Fi 设置指南](https://api.vex.com/aim/home/websocket/wifi_setup/connection_initial.html) — 如何连接 VEX AIM 机器人
- [阿里云百炼](https://bailian.console.aliyun.com/) — LLM API 服务（DashScope）
- [DashScope API 文档](https://bailian.console.aliyun.com/cn-beijing?tab=api#/api) — API 参考与密钥管理
