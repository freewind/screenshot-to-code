# Troubleshooting

# 故障排除

## Getting an OpenAI API key

## 获取OpenAI API密钥

1. Go to https://platform.openai.com/api-keys
2. Create an account if you don't have one
3. Add a payment method if you haven't already
4. Create a new API key
5. Copy the key and use it in the app

1. 访问 https://platform.openai.com/api-keys
2. 如果没有账号，创建一个账号
3. 如果还没有添加支付方式，添加一个支付方式
4. 创建一个新的API密钥
5. 复制密钥并在应用中使用

## Common errors

## 常见错误

### Error: "You exceeded your current quota"

### 错误："你超出了当前配额"

This means you don't have any credits left in your OpenAI account. You need to:

这意味着你的OpenAI账户中没有剩余额度。你需要：

1. Go to https://platform.openai.com/account/billing/overview
2. Add funds to your account
3. Try again

1. 访问 https://platform.openai.com/account/billing/overview
2. 向账户添加资金
3. 重试

### Error: "The model: gpt-4-vision-preview does not exist"

### 错误："模型：gpt-4-vision-preview不存在"

This means your OpenAI account doesn't have access to GPT-4V. You need to:

这意味着你的OpenAI账户无法访问GPT-4V。你需要：

1. Go to https://platform.openai.com/account/billing/overview
2. Add a valid payment method
3. Wait for a few minutes
4. Try again

1. 访问 https://platform.openai.com/account/billing/overview
2. 添加有效的支付方式
3. 等待几分钟
4. 重试

If that doesn't work:

如果还是不行：

1. Create a new API key
2. Try with the new key

1. 创建一个新的API密钥
2. 使用新密钥重试

### Error: "Cannot connect to backend"

### 错误："无法连接到后端"

This means the frontend can't connect to the backend server. Check that:

这意味着前端无法连接到后端服务器。检查：

1. The backend is running (you should see "Uvicorn running..." in the terminal)
2. The backend URL in the frontend's .env file matches the backend's port
3. You don't have any firewall rules blocking the connection

1. 后端正在运行(你应该在终端中看到"Uvicorn running...")
2. 前端.env文件中的后端URL与后端的端口匹配
3. 没有防火墙规则阻止连接

### Error: "Module not found" when running the backend

### 运行后端时出现"找不到模块"错误

This means Python can't find some required packages. Try:

这意味着Python找不到一些必需的包。尝试：

1. Make sure you're in the poetry shell: `poetry shell`
2. Reinstall dependencies: `poetry install`
3. Try running again

1. 确保你在poetry shell中：`poetry shell`
2. 重新安装依赖：`poetry install`
3. 重新运行
