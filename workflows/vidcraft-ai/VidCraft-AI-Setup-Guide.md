# VidCraft AI - Gemini 流式处理工作流设置指南

## 📋 概述

这个工作流使用 Google Gemini 1.5 Pro 模型来生成高质量的短视频脚本和制作方案，专门针对 TikTok 和 YouTube Shorts 平台优化。

## 🛠️ 前置要求

### 1. n8n 环境
- n8n 版本：1.0+ (推荐最新版)
- 部署方式：自托管或 n8n.cloud
- 内存要求：至少 512MB

### 2. Gemini API 密钥
- 访问 [Google AI Studio](https://makersuite.google.com/app/apikey)
- 创建新的 API 密钥
- 复制并保存密钥（格式如：`AIzaSyD...`）

## 🚀 安装步骤

### 步骤 1：导入工作流

1. 登录 n8n 界面
2. 点击 **"Import workflow"**
3. 选择 `vidcraft-gemini-workflow.json` 文件
4. 确认导入

### 步骤 2：配置 Gemini API 凭证

1. 进入 **Settings** → **Credentials**
2. 点击 **"Add credential"**
3. 选择 **"HTTP Query Auth"**
4. 配置如下：
   ```
   Name: Gemini API Key
   Query Parameter: key
   Value: 你的Gemini API密钥
   ```
5. 保存凭证

### 步骤 3：更新工作流节点

1. 打开导入的工作流
2. 点击 **"调用Gemini API"** 节点
3. 在 **Authentication** 中选择刚创建的 **"Gemini API Key"**
4. 保存节点

### 步骤 4：激活工作流

1. 点击工作流右上角的 **激活开关**
2. 确认状态显示为 **"Active"**
3. 复制生成的 Webhook URL

## 📝 使用方法

### API 端点信息

```
POST https://your-n8n-instance.com/webhook/vidcraft-ai
Content-Type: application/json
```

### 请求格式

```json
{
  "theme": "你的视频主题",
  "style": "视频风格（可选）",
  "platform": "目标平台（可选）"
}
```

### 参数说明

| 参数 | 类型 | 必填 | 默认值 | 说明 |
|------|------|------|--------|------|
| `theme` | string | ✅ | - | 视频主题或核心想法 |
| `style` | string | ❌ | "温馨治愈" | 视频风格定义 |
| `platform` | string | ❌ | "TikTok" | 目标平台 (TikTok/YouTube Shorts) |

### 风格选项

- **温馨治愈** - 柔和、暖心的情感表达
- **电影感慢镜头** - 电影级的视觉叙事
- **快节奏卡点混剪** - 动感、有冲击力的剪辑
- **温馨治愈Vlog风** - 日常、亲近的表达方式
- **舒缓温暖** - 平静、抚慰人心的氛围

## 🧪 测试工作流

### 使用 curl 测试

```bash
curl -X POST 'https://your-n8n-instance.com/webhook/vidcraft-ai' \
  -H 'Content-Type: application/json' \
  -d '{
    \"theme\": \"关于坚持和不放弃的励志视频\",
    \"style\": \"温馨治愈\",
    \"platform\": \"TikTok\"
  }'
```

### 使用 JavaScript 测试

```javascript
const response = await fetch('https://your-n8n-instance.com/webhook/vidcraft-ai', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    theme: '关于坚持和不放弃的励志视频',
    style: '温馨治愈',
    platform: 'TikTok'
  })
});

const result = await response.json();
console.log(result);
```

## 📊 响应格式

成功响应包含完整的视频项目 JSON：

```json
{
  \"videoProject\": {
    \"userInputSummary\": \"...\",
    \"strategy\": {
      \"targetAudience\": \"...\",
      \"primaryPlatform\": \"TikTok\",
      \"viralityHook\": \"...\"
    },
    \"metadata\": {
      \"title\": \"...\",
      \"description\": \"...\",
      \"tags\": [\"...\"],
      \"generatedAt\": \"2025-01-28T12:00:00.000Z\",
      \"processedBy\": \"Gemini-1.5-Pro\"
    },
    \"creativeElements\": {
      \"script\": \"完整的旁白脚本...\",
      \"storyboard\": [
        {
          \"scene\": 1,
          \"visuals\": \"画面描述...\",
          \"voiceover\": \"旁白内容...\",
          \"duration\": 5
        }
      ],
      \"subtitles\": [...],
      \"assetSuggestions\": {...}
    },
    \"callToAction\": {...}
  }
}
```

## 🔧 故障排除

### 常见问题

1. **401 Unauthorized**
   - 检查 Gemini API 密钥是否正确
   - 确认 API 密钥有效且未过期

2. **429 Too Many Requests**
   - Gemini 免费版有 60 QPM 限制
   - 等待后重试或升级到付费版

3. **Timeout 错误**
   - 增加 HTTP 请求的超时时间
   - 检查网络连接

4. **JSON 解析错误**
   - Gemini 返回格式可能不符合预期
   - 检查 Code 节点的错误处理逻辑

### 调试步骤

1. **查看执行历史**
   - 进入工作流 → Executions
   - 检查每个节点的输入输出

2. **检查节点配置**
   - 验证 API URL 正确
   - 确认请求体格式符合 Gemini API 要求

3. **测试 API 连接**
   - 使用 Postman 或 curl 直接测试 Gemini API

## 📈 优化建议

### 性能优化

1. **缓存机制**
   - 添加 Redis 节点缓存相似请求
   - 避免重复生成相同内容

2. **批量处理**
   - 实现批量主题处理
   - 提高生成效率

3. **错误重试**
   - 添加自动重试机制
   - 处理临时 API 错误

### 功能扩展

1. **多模型支持**
   - 集成 OpenAI GPT-4
   - 支持用户选择不同 AI 模型

2. **内容审核**
   - 添加内容安全检查
   - 过滤不当内容

3. **统计分析**
   - 记录生成数据
   - 分析热门主题

## 🔒 安全注意事项

1. **API 密钥保护**
   - 不要将密钥硬编码到工作流中
   - 使用 n8n 凭证管理系统

2. **访问控制**
   - 考虑添加身份验证
   - 限制 Webhook 访问

3. **内容过滤**
   - 实现敏感内容检测
   - 遵守平台内容政策

## 📞 支持联系

如有问题，请：
1. 检查本指南的故障排除部分
2. 查看 n8n 社区论坛
3. 参考 [Gemini API 文档](https://ai.google.dev/docs)

---

## 🎯 快速开始检查清单

- [ ] 已安装 n8n (v1.0+)
- [ ] 已获取 Gemini API 密钥
- [ ] 已导入工作流文件
- [ ] 已配置 API 凭证
- [ ] 已激活工作流
- [ ] 已测试 Webhook 端点
- [ ] 响应格式符合预期

完成所有项目后，你的 VidCraft AI 工作流就可以开始使用了！🎉