# screenshot-to-code

A simple tool to convert screenshots, mockups and Figma designs into clean, functional code using AI. **Now supporting Claude Sonnet 3.5 and GPT-4o!**

# 截图转代码

一个使用AI将截图、设计稿和Figma设计转换为整洁、可用代码的简单工具。**现已支持Claude Sonnet 3.5和GPT-4o!**

https://github.com/abi/screenshot-to-code/assets/23818/6cebadae-2fe3-4986-ac6a-8fb9db030045

Supported stacks:

支持的技术栈：

- HTML + Tailwind
- HTML + CSS
- React + Tailwind
- Vue + Tailwind
- Bootstrap
- Ionic + Tailwind
- SVG

Supported AI models:

支持的AI模型：

- Claude Sonnet 3.5 - Best model!
- GPT-4o - also recommended!
- DALL-E 3 or Flux Schnell (using Replicate) for image generation

See the [Examples](#-examples) section below for more demos.

查看下方的[示例](#-examples)部分获取更多演示。

We also just added experimental support for taking a video/screen recording of a website in action and turning that into a functional prototype.

我们还刚刚添加了实验性功能，支持将网站运行时的视频/屏幕录制转换为可用的原型。

![google in app quick 3](https://github.com/abi/screenshot-to-code/assets/23818/8758ffa4-9483-4b9b-bb66-abd6d1594c33)

[Learn more about video here](https://github.com/abi/screenshot-to-code/wiki/Screen-Recording-to-Code).

[点击此处了解更多关于视频功能的信息](https://github.com/abi/screenshot-to-code/wiki/Screen-Recording-to-Code)。

[Follow me on Twitter for updates](https://twitter.com/_abi_).

[在Twitter上关注我获取更新](https://twitter.com/_abi_)。

## 🌍  Hosted Version

## 🌍  托管版本

[Try it live on the hosted version (paid)](https://screenshottocode.com). If you're a large or medium enterprise (50+ employees), [book a meeting to explore custom enterprise plans](https://cal.com/abi-raja-wy2pfh/30min).

[在托管版本上试用(付费)](https://screenshottocode.com)。如果你是大型或中型企业(50+员工)，[预约会议探讨定制企业方案](https://cal.com/abi-raja-wy2pfh/30min)。

## 🛠 Getting Started

## 🛠 开始使用

The app has a React/Vite frontend and a FastAPI backend.

该应用使用React/Vite构建前端，FastAPI构建后端。

Keys needed:

需要的密钥：

- [OpenAI API key with access to GPT-4](https://github.com/abi/screenshot-to-code/blob/main/Troubleshooting.md) or Anthropic key (optional)
- Both are recommended so you can compare results from both Claude and GPT4o

- [可访问GPT-4的OpenAI API密钥](https://github.com/abi/screenshot-to-code/blob/main/Troubleshooting.md)或Anthropic密钥(可选)
- 推荐同时使用两者，这样你可以比较Claude和GPT4o的结果

If you'd like to run the app with Ollama open source models (not recommended due to poor quality results), [follow this comment](https://github.com/abi/screenshot-to-code/issues/354#issuecomment-2435479853).

如果你想使用Ollama开源模型运行应用(由于结果质量较差，不推荐)，[请参考这个评论](https://github.com/abi/screenshot-to-code/issues/354#issuecomment-2435479853)。

Run the backend (I use Poetry for package management - `pip install poetry` if you don't have it):

运行后端(我使用Poetry进行包管理 - 如果你没有安装，请执行`pip install poetry`):

```bash
cd backend
echo "OPENAI_API_KEY=sk-your-key" > .env
echo "ANTHROPIC_API_KEY=your-key" > .env
poetry install
poetry shell
poetry run uvicorn main:app --reload --port 7001
```
You can also set up the keys using the settings dialog on the front-end (click the gear icon after loading the frontend).

你也可以在前端使用设置对话框设置密钥(加载前端后点击齿轮图标)。

Run the frontend:

运行前端：

```bash
cd frontend
yarn
yarn dev
```

Open http://localhost:5173 to use the app.

打开 http://localhost:5173 使用应用。

If you prefer to run the backend on a different port, update VITE_WS_BACKEND_URL in `frontend/.env.local`

如果你想在不同端口运行后端，请在`frontend/.env.local`中更新VITE_WS_BACKEND_URL

For debugging purposes, if you don't want to waste GPT4-Vision credits, you can run the backend in mock mode (which streams a pre-recorded response):

出于调试目的，如果你不想浪费GPT4-Vision额度，你可以在模拟模式下运行后端(会流式传输预录制的响应)：

```bash
MOCK=true poetry run uvicorn main:app --reload --port 7001
```

## Docker

If you have Docker installed on your system, in the root directory, run:

如果你的系统上安装了Docker，在根目录运行：

```bash
echo "OPENAI_API_KEY=sk-your-key" > .env
docker-compose up -d --build
```

The app will be up and running at http://localhost:5173. Note that you can't develop the application with this setup as the file changes won't trigger a rebuild.

应用将在 http://localhost:5173 运行。注意使用这种设置你无法开发应用，因为文件更改不会触发重新构建。

## 🙋‍♂️ FAQs

## 🙋‍♂️ 常见问题

- **I'm running into an error when setting up the backend. How can I fix it?** [Try this](https://github.com/abi/screenshot-to-code/issues/3#issuecomment-1814777959). If that still doesn't work, open an issue.
- **How do I get an OpenAI API key?** See https://github.com/abi/screenshot-to-code/blob/main/Troubleshooting.md
- **How can I configure an OpenAI proxy?** - If you're not able to access the OpenAI API directly (due to e.g. country restrictions), you can try a VPN or you can configure the OpenAI base URL to use a proxy: Set OPENAI_BASE_URL in the `backend/.env` or directly in the UI in the settings dialog. Make sure the URL has "v1" in the path so it should look like this: `https://xxx.xxxxx.xxx/v1`
- **How can I update the backend host that my front-end connects to?** - Configure VITE_HTTP_BACKEND_URL and VITE_WS_BACKEND_URL in front/.env.local For example, set VITE_HTTP_BACKEND_URL=http://124.10.20.1:7001
- **Seeing UTF-8 errors when running the backend?** - On windows, open the .env file with notepad++, then go to Encoding and select UTF-8.
- **How can I provide feedback?** For feedback, feature requests and bug reports, open an issue or ping me on [Twitter](https://twitter.com/_abi_).

- **在设置后端时遇到错误，如何修复？** [试试这个](https://github.com/abi/screenshot-to-code/issues/3#issuecomment-1814777959)。如果仍然不行，请提交issue。
- **如何获取OpenAI API密钥？** 参见 https://github.com/abi/screenshot-to-code/blob/main/Troubleshooting.md
- **如何配置OpenAI代理？** - 如果你无法直接访问OpenAI API(例如由于国家限制)，你可以尝试使用VPN或配置OpenAI基础URL使用代理：在`backend/.env`中设置OPENAI_BASE_URL，或直接在UI设置对话框中设置。确保URL路径中包含"v1"，应该看起来像这样：`https://xxx.xxxxx.xxx/v1`
- **如何更新前端连接的后端主机？** - 在front/.env.local中配置VITE_HTTP_BACKEND_URL和VITE_WS_BACKEND_URL，例如，设置VITE_HTTP_BACKEND_URL=http://124.10.20.1:7001
- **运行后端时看到UTF-8错误？** - 在Windows上，使用notepad++打开.env文件，然后转到Encoding选择UTF-8。
- **如何提供反馈？** 对于反馈、功能请求和错误报告，请提交issue或在[Twitter](https://twitter.com/_abi_)上联系我。

## 📚 Examples

## 📚 示例

**NYTimes**

| Original                                                                                                                                                        | Replica                                                                                                                                                         |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <img width="1238" alt="Screenshot 2023-11-20 at 12 54 03 PM" src="https://github.com/abi/screenshot-to-code/assets/23818/3b644dfa-9ca6-4148-84a7-3405b6671922"> | <img width="1414" alt="Screenshot 2023-11-20 at 12 59 56 PM" src="https://github.com/abi/screenshot-to-code/assets/23818/26201c9f-1a28-4f35-a3b1-1f04e2b8ce2a"> |

**Instagram page (with not Taylor Swift pics)**

**Instagram页面(不是Taylor Swift的图片)**

https://github.com/abi/screenshot-to-code/assets/23818/503eb86a-356e-4dfc-926a-dabdb1ac7ba1

**Hacker News** but it gets the colors wrong at first so we nudge it

**Hacker News** 但它一开始颜色不对，所以我们稍微调整了一下

https://github.com/abi/screenshot-to-code/assets/23818/3fec0f77-44e8-4fb3-a769-ac7410315e5d
