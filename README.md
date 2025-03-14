<p align="center">
  <img width="160" src="./images/miniprogram.png">
</p>

<h1 align="center">学习卡盒</h1>

## 📝 项目介绍

学习卡盒是一个类似于 anki 的卡片式学习小程序，每个用户可以创建多个卡盒，每个卡盒中可以放很多张卡片，每张卡片分为正反两面：

- 正面可以用来记录 **“问题 \ 概念 \ 中英文”**
- 反面可以用来记录 **“答案 \ 概念解析 \ 中英文的翻译”**

<p align="center">
  <img width="400" src="./images/cards.png">
</p>

### ✨ 核心功能

#### 📁 目录管理

- **多目录支持**：每个用户拥有默认目录，可创建多个目录分类管理卡盒

#### 📦 卡盒管理

- **AI 生成卡盒**：通过描述需求让 AI 自动卡片，支持预览和自定义上下文
- **创建空白卡盒**：手动创建并添加卡片
- **导出/导入卡盒**：以固定格式导出卡盒内容为文本，或从文本导入卡片
- **卡盒封面颜色**：自定义卡盒外观颜色
- **卡盒排序**：调整卡盒在目录中的显示顺序
- **移动目录**：将卡盒移动到其他目录
- **正反面交换**：一键交换卡盒中所有卡片的正反面内容和笔记

#### 📝 卡片管理

- **AI 生成卡片**：通过 AI 生成卡片并添加到指定卡盒
- **批量删除**：支持多选删除卡片
- **卡片排序**：调整卡片在卡盒中的顺序
- **卡片关联**：建立卡片之间的关联关系，支持查看和跳转
- **卡片笔记**：为卡片添加额外笔记，支持 AI 生成笔记
- **朗读功能**：支持中英文朗读卡片内容
- **翻面模式**：在卡盒中快速翻面查看内容，适合背单词场景
- **样式设置**：自定义卡片排版（居左/居中）、文字大小、序号显示等

#### 🔍 搜索功能

- **全局搜索**：通过关键字搜索所有目录中的卡片内容
- **快速定位**：点击搜索结果直接跳转到对应卡盒和卡片位置

#### 👤 用户相关功能

- **学习统计**：记录学习时间并生成热力图，直观展示学习进度
- **AI 额度管理**：查看 AI 功能的剩余使用额度

#### 📚 学习相关功能

- **回忆模式**：展示卡片正面，用户自行判断是否记住反面内容
- **单选模式**：AI 生成混淆选项，用户选择正确答案，错误时提供解析
- **复述模式**：支持文字或语音输入回答，AI 评分判断正误
- **学习计划**：基于艾宾浩斯记忆曲线，科学安排每日学习和复习内容
- **练一练模式**：无需制定计划，随时选择学习模式进行练习

#### 🏪 卡盒集市

- **卡盒列表**：系统提供各类现成卡盒（英语短文、单词、考试知识点等）
- **分类浏览**：按类别查看和导入卡盒

## 🛠️ 技术栈

- **前端框架**：[Vue 3](https://v3.vuejs.org/) + [TypeScript](https://www.typescriptlang.org/)
- **跨端框架**：[uni-app](https://uniapp.dcloud.io/)
- **项目模版**：[Unibest](https://www.unibest.tech/)
- **CSS 框架**：[UnoCSS](https://github.com/unocss/unocss)
- **UI 组件**：[wot-design-uni](https://github.com/Moonofweisheng/wot-desig-uni)
- **后端服务**：微信云开发（数据库、云函数）

## 🚀 快速开始

### 安装依赖

```bash
pnpm i
```

### 开发模式

```bash
pnpm dev:mp-weixin
```

然后打开微信开发者工具，导入本地文件夹，选择本项目的 `dist/dev/mp-weixin` 文件夹

### 构建发布

```bash
pnpm build:mp-weixin
```

打包后的文件在 `dist/build/mp-weixin`，通过微信开发者工具导入并上传

## ☁️ 云开发配置

在使用本项目前，需要先配置微信云开发环境：

1. 在微信开发者工具中开通云开发，创建云环境
2. 在 `env` 目录下创建或修改 `.env.local`，添加以下配置：

```bash
# 云开发环境 ID
VITE_CLOUD_ENV_ID='xxx'

# 版本号
VITE_APP_VERSION='1.0.0'

# 微信同声传译插件 ID，用于朗读卡片内容
VITE_WECHAT_SI_ID = 'xxx'
```

3. 在云开发控制台中创建以下数据集合（数据库）：

   - `users` - 用户信息
   - `config` - 系统配置
   - `market` - 卡盒集市数据
   - `market-classification` - 卡盒集市分类
   - `monthly-study` - 月度学习统计

4. 在 `config` 集合中添加以下初始配置数据：

```json
{
  "id": "xxx", // 由系统生成
  "limit": { "default": "30", "max": "200", "pro": "100" }, // AI 功能限制
  "model": "microsoft/phi-4", // AI 功能模型名称，可以在 openrouter 中查看
  "reviewVersion": "xxxx" // 限制 AI 功能的版本号，如果系统版本和该版本一致，则无法使用 AI 功能
}
```

5. 在 `market-classification` 集合中添加分类数据，数据结构如下：

```json
{
  "_id": "xxx", // 由系统生成
  "title": "365 天英语口语" // 分类名称
}
```

6. 在 `market` 集合中添加卡盒数据，数据结构如下：

```json
{
  "_id": "xxx", // 由系统生成
  "cards": [
    {
      "backContent": "卡片背面内容",
      "frontContent": "卡片正面内容",
      "index": 0
    }
  ],
  "classification": "365 天英语口语", // 分类名称，对应market-classification 中的 title
  "createTime": "Tue Jan 07 2025 14:42:10 GMT+0800 (中国标准时间)",
  "description": "卡盒描述",
  "labels": ["日常口语"], // 标签
  "title": "卡盒标题"
}
```

> 注意：请确保云函数的权限配置正确，以便应用能够正常访问云资源。

5. 在云开发控制台中，为 `openrouter` 云函数添加以下环境变量：

   - `KEY` - OpenRouter 平台的 API Key，用于访问 AI 模型服务
     > 提示：你可以在 [OpenRouter](https://openrouter.ai/) 平台注册账号并获取 API Key

同时建议将 `openrouter` 云函数的超时时间设置为 60s，以确保 AI 功能能够正常运行。

## 📄 开源协议

[Apache License, Version 2.0](https://opensource.org/license/apache-2-0)
