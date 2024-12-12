# Screenshot-to-Code API 文档

本文档描述了Screenshot-to-Code项目的后端API。

## 基础信息

- 基础URL: `http://localhost:7001` (默认)
- 所有API响应格式均为JSON，除非特别说明
- WebSocket连接URL: `ws://localhost:7001`

## REST API端点

### 1. 状态检查

检查后端服务是否正常运行。

```
GET /
```

**响应**:
- 返回HTML页面，显示后端运行状态

### 2. 截图服务

将网页URL转换为截图。

```
POST /api/screenshot
```

**请求体**:
```json
{
    "url": "要截图的网页URL",
    "apiKey": "screenshotone.com的API密钥"
}
```

**响应**:
```json
{
    "url": "base64格式的图片数据URL"
}
```

### 3. 评估相关API

#### 3.1 获取评估数据

获取所有评估数据。

```
GET /evals
```

**响应**:
```json
[
    {
        "input": "输入图片的base64数据",
        "outputs": ["生成的HTML代码1", "生成的HTML代码2", ...]
    }
]
```

#### 3.2 运行评估

对指定模型和技术栈运行评估。

```
POST /run_evals
```

**请求体**:
```json
{
    "models": ["模型名称列表"],
    "stack": "技术栈名称"
}
```

#### 3.3 获取支持的模型和技术栈

```
GET /models
```

**响应**:
```json
{
    "models": ["支持的模型列表"],
    "stacks": ["支持的技术栈列表"]
}
```

## WebSocket API

### 1. 代码生成

通过WebSocket实时生成代码。

```
WebSocket /generate-code
```

**连接参数**:
```json
{
    "generatedCodeConfig": "技术栈(html_tailwind/react_tailwind等)",
    "inputMode": "输入模式(image/video)",
    "codeGenerationModel": "AI模型",
    "openAiApiKey": "OpenAI API密钥",
    "anthropicApiKey": "Anthropic API密钥(可选)",
    "openAiBaseURL": "OpenAI API基础URL(可选)",
    "isImageGenerationEnabled": "是否启用图片生成(布尔值)"
}
```

**WebSocket消息类型**:

1. 状态更新:
```json
{
    "type": "status",
    "value": "状态信息",
    "variantIndex": 0
}
```

2. 代码块:
```json
{
    "type": "chunk",
    "value": "代码片段",
    "variantIndex": 0
}
```

3. 完整代码:
```json
{
    "type": "setCode",
    "value": "完整代码",
    "variantIndex": 0
}
```

4. 错误信息:
```json
{
    "type": "error",
    "value": "错误信息",
    "variantIndex": 0
}
```

## 支持的技术栈

- HTML + Tailwind
- HTML + CSS
- React + Tailwind
- Vue + Tailwind
- Bootstrap
- Ionic + Tailwind
- SVG

## 支持的AI模型

- Claude Sonnet 3.5 (推荐)
- GPT-4o (推荐)
- DALL-E 3 或 Flux Schnell (用于图片生成)

## 错误处理

所有API错误响应都会包含错误信息。WebSocket连接的错误会通过error类型的消息发送。

常见错误码:
- APP_ERROR_WEB_SOCKET_CODE: WebSocket应用错误
- USER_CLOSE_WEB_SOCKET_CODE: 用户关闭连接

## 使用示例

### 1. 基本截图到代码转换

1. 建立WebSocket连接:
```javascript
const ws = new WebSocket('ws://localhost:7001/generate-code');

ws.onopen = () => {
    ws.send(JSON.stringify({
        generatedCodeConfig: "html_tailwind",
        inputMode: "image",
        codeGenerationModel: "gpt-4o-2024-05-13",
        openAiApiKey: "your-api-key",
        isImageGenerationEnabled: true
    }));
};

ws.onmessage = (event) => {
    const response = JSON.parse(event.data);
    switch(response.type) {
        case "chunk":
            console.log("收到代码片段:", response.value);
            break;
        case "status":
            console.log("状态更新:", response.value);
            break;
        case "setCode":
            console.log("完整代码:", response.value);
            break;
        case "error":
            console.error("错误:", response.value);
            break;
    }
};
```

### 2. 网页截图

```javascript
async function takeScreenshot(url, apiKey) {
    const response = await fetch('http://localhost:7001/api/screenshot', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            url: url,
            apiKey: apiKey
        })
    });
    
    const data = await response.json();
    return data.url; // 返回base64格式的图片数据
}
```

## 环境配置

系统支持以下环境变量配置:

### API密钥
- `OPENAI_API_KEY`: OpenAI API密钥(必需)
- `ANTHROPIC_API_KEY`: Anthropic API密钥(可选)
- `REPLICATE_API_KEY`: Replicate API密钥(可选,用于Flux图片生成)
- `OPENAI_BASE_URL`: OpenAI API基础URL(可选,用于自定义API端点)

### 调试选项
- `MOCK`: 设置为true时使用模拟响应(用于调试)
- `IS_DEBUG_ENABLED`: 启用调试模式
- `DEBUG_DIR`: 调试文件输出目录
- `IS_PROD`: 生产环境标志

### 其他配置
- `NUM_VARIANTS`: 生成代码的变体数量(默认为2)