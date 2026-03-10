# JSON 自动解析功能使用说明

## 功能概述

我已经为你的 Team 管理系统添加了 JSON 自动解析功能，让你可以快速从 ChatGPT API 获取 Token 并自动填充到导入表单中。

## 功能位置

在管理后台的 "导入 Team" 模态框中，"单个导入" 标签页下，你会看到一个绿色的 "🚀 快速解析 JSON" 区域。

## 使用步骤

### 1. 获取 JSON 数据
1. 确保已登录 ChatGPT (https://chatgpt.com)
2. 点击 "打开 API 页面" 按钮，或直接访问：`https://chatgpt.com/api/auth/session`
3. 复制返回的完整 JSON 数据

### 2. 解析并填充
1. 将复制的 JSON 数据粘贴到文本框中
2. 点击 "解析并填充" 按钮
3. 系统会自动提取以下信息并填充到对应字段：
   - 用户邮箱 (`user.email`)
   - Access Token (`accessToken`)
   - Session Token (`sessionToken`)

### 3. 完成导入
1. 检查自动填充的字段是否正确
2. 如需要，手动填写其他可选字段（Refresh Token、Client ID、Account ID）
3. 点击 "导入" 按钮完成 Team 导入

## 功能特点

- **自动识别**：智能解析 JSON 格式，提取关键字段
- **实时反馈**：显示解析结果和成功填充的字段
- **错误处理**：JSON 格式错误时会显示具体错误信息
- **一键清空**：提供清空所有字段的快捷按钮
- **导入格式生成**：自动生成标准的导入格式字符串

## 示例 JSON 格式

```json
{
  "user": {
    "email": "your@email.com",
    "name": "Your Name"
  },
  "accessToken": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIs...",
  "sessionToken": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIs...",
  "expires": "2024-12-31T23:59:59.000Z"
}
```

## 长期存储建议

- **推荐保存 Session Token**：它的有效期更长，可以用于自动刷新 Access Token
- **Access Token 作为备用**：虽然有效期较短，但可以立即使用
- **组合使用最佳**：同时保存 AT 和 ST，系统会优先使用 ST 进行刷新

## 故障排除

### JSON 解析失败
- 检查 JSON 格式是否完整和正确
- 确保没有多余的字符或截断
- 尝试重新获取 JSON 数据

### 字段未自动填充
- 检查 JSON 中是否包含 `user.email`、`accessToken`、`sessionToken` 字段
- 确保字段值不为空

### 导入失败
- 确保至少填写了 Access Token 或 Session Token
- 检查 Token 格式是否正确（通常以 `eyJ` 开头）
- 如果使用 Refresh Token，确保同时填写了 Client ID

## 技术实现

- 前端 JavaScript 解析 JSON 数据
- 自动填充表单字段
- 集成到现有的导入流程中
- 保持与原有功能的兼容性

这个功能大大简化了 Token 获取和导入的过程，让你可以快速批量管理 ChatGPT Team 账号。