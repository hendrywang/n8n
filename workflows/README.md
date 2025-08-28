# n8n 工作流集合

这个目录包含了各种 n8n 工作流项目，按照项目名称组织在不同的子文件夹中。

## 📁 项目结构

```
workflows/
├── README.md                    # 本文件
├── vidcraft-ai/                # VidCraft AI 项目
│   ├── vidcraft-gemini-workflow.json    # n8n 工作流文件
│   ├── vidcraft-system-prompt.txt       # 系统提示词
│   ├── test-requests.json               # 测试请求示例
│   └── VidCraft-AI-Setup-Guide.md      # 设置指南
└── [future-projects]/          # 未来的项目...
```

## 🎯 现有项目

### 1. VidCraft AI (`vidcraft-ai/`)

**功能描述**: 使用 Gemini 1.5 Pro 生成短视频脚本和制作方案的 AI 工作流

**主要特性**:
- 🤖 集成 Google Gemini 1.5 Pro
- 📝 生成完整视频项目方案
- 🎬 包含脚本、分镜、字幕等
- 📱 针对 TikTok 和 YouTube Shorts 优化
- ✅ 完整的 JSON 格式验证

**使用场景**: 
- 短视频内容创作
- 励志鸡汤类视频生成
- 社交媒体内容策划

**文件说明**:
- `vidcraft-gemini-workflow.json` - 导入到 n8n 的工作流文件
- `vidcraft-system-prompt.txt` - 完整的 AI 提示词模板
- `test-requests.json` - 测试请求示例和代码
- `VidCraft-AI-Setup-Guide.md` - 详细的安装和使用指南

## 🚀 快速开始

1. **选择项目**: 进入对应的项目文件夹
2. **阅读指南**: 查看项目的 Setup Guide
3. **导入工作流**: 将 `.json` 文件导入到 n8n
4. **配置参数**: 按照指南配置必要的参数和凭证
5. **开始使用**: 运行测试验证功能

## 📋 项目清单

- [x] **VidCraft AI** - AI 短视频脚本生成 (已完成)
- [ ] **数据处理流** - 数据清洗和转换工作流 (计划中)
- [ ] **社交媒体自动化** - 多平台发布工作流 (计划中)
- [ ] **邮件营销自动化** - 邮件序列工作流 (计划中)
- [ ] **电商订单处理** - 订单处理自动化 (计划中)

## 🛠️ 开发规范

### 新项目创建规范

1. **文件夹命名**: 使用小写字母和连字符，例如 `my-awesome-workflow`
2. **必需文件**:
   - `{project-name}.json` - n8n 工作流文件
   - `README.md` 或 `{Project-Name}-Setup-Guide.md` - 项目说明文档
   - `test-*.json` - 测试用例和示例（如果适用）
3. **可选文件**:
   - `system-prompt.txt` - AI 提示词（AI 相关项目）
   - `config.json` - 配置文件
   - `examples/` - 示例文件夹

### 文档规范

每个项目的说明文档应包含：
- 📋 项目概述和功能描述
- 🛠️ 前置要求和依赖
- 🚀 安装和配置步骤
- 📝 使用方法和 API 说明
- 🧪 测试用例和示例
- 🔧 故障排除指南
- 📈 优化和扩展建议

## 📞 支持和贡献

- 💡 **新项目建议**: 在项目 Issue 中提出
- 🐛 **Bug 反馈**: 请详细描述问题和复现步骤
- 🔧 **功能改进**: 欢迎提交 Pull Request

## 📊 项目状态

| 项目名称 | 状态 | 版本 | 最后更新 | 维护状态 |
|----------|------|------|----------|----------|
| VidCraft AI | ✅ 完成 | v1.0 | 2025-01-28 | 🟢 活跃维护 |

---

**注意**: 所有工作流都基于 n8n 开源版本开发，不依赖企业版功能。