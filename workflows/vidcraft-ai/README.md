# VidCraft AI - 短视频脚本生成工作流

基于 Google Gemini 1.5 Pro 的 AI 短视频内容生成系统，专门为 TikTok 和 YouTube Shorts 优化。

## 📋 项目概述

VidCraft AI 是一个完整的短视频内容生成解决方案，能够将简单的主题想法转化为包含脚本、分镜、音效建议等在内的完整视频制作方案。特别适合创作励志、治愈系、人生感悟类的"心灵鸡汤"短视频内容。

## 🎯 主要功能

- **智能脚本生成**: 将主题转化为富有感染力的旁白脚本
- **完整分镜设计**: 提供详细的视觉描述和时间安排
- **平台优化**: 针对不同平台特性优化内容策略
- **素材建议**: 提供音乐、音效、视觉素材的具体建议
- **字幕时间轴**: 自动生成字幕文件格式
- **流式响应**: 支持实时反馈和进度显示

## 📁 项目文件

```
vidcraft-ai/
├── README.md                           # 项目说明 (本文件)
├── vidcraft-gemini-workflow.json      # n8n 工作流定义文件
├── vidcraft-system-prompt.txt         # VidCraft AI 系统提示词
├── test-requests.json                  # 测试用例和调用示例
└── VidCraft-AI-Setup-Guide.md        # 详细安装配置指南
```

## 🚀 快速开始

### 1. 前置要求

- n8n 实例 (v1.0+)
- Google Gemini API 密钥
- 基本的 n8n 使用经验

### 2. 安装步骤

1. **获取 Gemini API 密钥**
   ```bash
   # 访问 Google AI Studio
   https://makersuite.google.com/app/apikey
   ```

2. **导入工作流**
   - 在 n8n 中点击 "Import workflow"
   - 选择 `vidcraft-gemini-workflow.json` 文件

3. **配置 API 凭证**
   - 创建 HTTP Query Auth 凭证
   - 设置查询参数名称为 `key`
   - 填入您的 Gemini API 密钥

4. **激活工作流**
   - 激活工作流并获取 Webhook URL

### 3. 使用示例

**API 调用**:
```bash
curl -X POST 'https://your-n8n.com/webhook/vidcraft-ai' \
  -H 'Content-Type: application/json' \
  -d '{
    "theme": "关于坚持和不放弃的励志视频",
    "style": "温馨治愈",
    "platform": "TikTok"
  }'
```

**JavaScript 调用**:
```javascript
const response = await fetch('https://your-n8n.com/webhook/vidcraft-ai', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    theme: '关于坚持和不放弃的励志视频',
    style: '温馨治愈',
    platform: 'TikTok'
  })
});

const result = await response.json();
```

## 📊 输入参数

| 参数 | 类型 | 必填 | 默认值 | 说明 |
|------|------|------|--------|------|
| `theme` | string | ✅ | - | 视频主题或核心想法 |
| `style` | string | ❌ | "温馨治愈" | 视频风格 |
| `platform` | string | ❌ | "TikTok" | 目标平台 |

### 风格选项

- **温馨治愈** - 柔和、暖心的情感表达
- **电影感慢镜头** - 电影级的视觉叙事
- **快节奏卡点混剪** - 动感、有冲击力
- **温馨治愈Vlog风** - 日常、亲近的表达
- **舒缓温暖** - 平静、抚慰人心

## 📤 输出格式

```json
{
  "videoProject": {
    "userInputSummary": "用户需求总结",
    "strategy": {
      "targetAudience": "目标受众分析",
      "primaryPlatform": "主要平台",
      "platformReasoning": "平台选择理由",
      "viralityHook": "吸引眼球的开场"
    },
    "metadata": {
      "title": "视频标题",
      "description": "视频描述",
      "tags": ["标签1", "标签2"],
      "generatedAt": "生成时间",
      "processedBy": "处理模型"
    },
    "creativeElements": {
      "script": "完整旁白脚本",
      "storyboard": [
        {
          "scene": 1,
          "visuals": "画面描述",
          "voiceover": "旁白内容",
          "onScreenText": "屏幕文字",
          "duration": 5,
          "sfx": "音效建议"
        }
      ],
      "subtitles": [
        {
          "id": 1,
          "startTime": "00:00:00,500",
          "endTime": "00:00:03,000",
          "text": "字幕内容"
        }
      ],
      "assetSuggestions": {
        "visuals": "视觉素材建议",
        "backgroundMusic": "背景音乐建议",
        "voiceoverStyle": "配音风格建议"
      }
    },
    "callToAction": {
      "text": "行动号召文字",
      "placement": "展示位置"
    }
  }
}
```

## 🎨 应用场景

### 1. 励志内容创作
- 个人成长主题
- 职场励志
- 学习动机

### 2. 情感治愈视频
- 心灵鸡汤
- 情绪疗愈
- 生活感悟

### 3. 人生哲理分享
- 价值观表达
- 人生智慧
- 经验分享

### 4. 社交媒体营销
- 品牌价值传达
- 用户情感连接
- 内容营销

## 🔧 技术架构

```
用户请求 → Webhook → 参数处理 → Gemini API → 响应解析 → JSON 验证 → 返回结果
```

### 核心组件

1. **Webhook 触发器** - 接收 HTTP 请求
2. **参数构建器** - 组装 AI 提示词
3. **Gemini API 调用** - 执行 AI 生成
4. **响应处理器** - 解析和验证输出
5. **条件分支** - 错误处理和路由
6. **响应节点** - 返回 JSON 结果

## 📈 性能指标

- **响应时间**: 通常 10-30 秒
- **成功率**: > 95% (依赖于 Gemini API 稳定性)
- **并发支持**: 取决于 n8n 实例配置
- **API 限制**: Gemini 免费版 60 QPM

## 🔍 故障排除

### 常见问题

1. **401 认证错误**
   - 检查 Gemini API 密钥是否正确
   - 确认密钥未过期

2. **429 频率限制**
   - 等待后重试
   - 考虑升级 Gemini API 套餐

3. **JSON 解析失败**
   - 检查 AI 输出格式
   - 调整提示词参数

### 调试方法

1. 查看 n8n 执行历史
2. 检查每个节点的输入输出
3. 验证 API 调用参数
4. 测试 Gemini API 连通性

## 🚧 版本历史

- **v1.0** (2025-01-28)
  - 初始版本发布
  - 支持 Gemini 1.5 Pro
  - 完整 JSON 输出格式
  - 多风格支持

## 🔮 未来规划

- [ ] 支持多种 AI 模型 (OpenAI, Claude)
- [ ] 添加图片生成功能
- [ ] 实现内容审核机制
- [ ] 支持批量生成
- [ ] 添加内容缓存优化
- [ ] 集成音频生成 API

## 📞 支持

- 详细安装指南: `VidCraft-AI-Setup-Guide.md`
- 测试示例: `test-requests.json`
- 系统提示词: `vidcraft-system-prompt.txt`

## 📜 许可证

本项目遵循 n8n 项目的开源许可证条款，仅限个人和内部商业使用。

---

**注意**: 使用本工作流需要遵守 Google Gemini API 的使用条款和内容政策。