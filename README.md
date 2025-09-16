线条小狗冒险日记 (Line Puppy's Adventure Diary)
一个将你 fleeting 的情绪，物化为一份可以被珍藏和回顾的、独一-无二的数字艺术品(旅行明信片) 的AIGC应用。

 <!-- 替换为您的Hugging Face Space链接 -->

<!-- 建议您在这里替换为一张应用截图或精美的Banner图 -->

核心创意 ✨
在快节奏的数字时代，许多AIGC内容如过眼云烟，“阅后即焚”。“线条小狗冒险日记” 旨在解决这一问题。它不是一个简单的图片生成工具，而是一个沉浸式的情感转化与收藏平台。

项目的核心创意是：将用户当下抽象、易逝的情绪（如“今天很开心”、“加班到头秃”），通过AIGC转化为一张具象的、富有故事性的、且独一无二的“线条小狗旅行明信片”，让情感变成可以被看见、被分享、被珍藏的有形故事。

主要功能 🚀
AI旅行明信片生成：输入你此刻的心情，AI将为你创作一张包含专属图像和旅行日志的明信片。

互动式情绪地图：在精心设计的地图上选择一个最能代表你心情的“目的地”，开启一场心灵之旅。

动态旅行故事：利用 Google Gemini API 将你的简短输入扩展成一段富有感染力的第一人称旅行见闻。

风格化AI图像：通过自训练的LoRA模型确保“线条小狗”风格的统一性，并结合ControlNet控制小狗姿态，使其与场景和情绪精准匹配。

“惊喜包裹”体验：生成的结果会以一个待拆封的“包裹”形式呈现，增加了开箱的仪式感和期待感。

个人旅行图鉴：所有生成的明信片都会被自动收藏到你的专属“旅行图鉴”中，可以随时回顾每一次的心情之旅。

用户流程 🗺️
graph TD
    A[🏠 打开应用] --> B{📍 在地图上选择情绪目的地};
    B --> C[📝 写下旅行寄语/心情];
    C --> D[🚀 点击出发];
    D --> E[🎁 等待包裹送达...];
    E --> F[🎉 点击拆开惊喜包裹];
    F --> G[💌 查看并收获专属明信片];
    G --> H[🖼️ 明信片自动存入旅行图鉴];
    G --> B;

技术架构 🛠️
这是一个前后端分离、服务解耦的现代化Web应用，旨在实现低成本、高可用的长期部署。

<!-- 建议您在这里替换为一张架构图 -->

前端 (Frontend)

技术栈: HTML, CSS, Vanilla JavaScript (构建为单页应用 SPA)

部署: Cloudflare Pages - 提供全球CDN加速和持续集成。

逻辑后端 (Logic Backend)

技术栈: FastAPI (Python 框架)

职责: 处理API请求、调用LLM服务、与数据库交互。

部署: Hugging Face Spaces (CPU实例) - 实现Serverless和按需启动。

AI计算后端 (AI Backend)

技术栈: Stable Diffusion WebUI + 自定义LoRA模型 + ControlNet

职责: 接收Prompt和参数，生成核心图像。

部署: 独立的云GPU平台 (如 AutoDL, Vast.ai 等)，通过 Cloudflare Tunnel 暴露安全的API接口。

文本生成 (Text Generation)

服务: Google Gemini API

职责: 生成所有创意文本，包括地点名称、旅行日志和地图坐标。

数据库与存储 (Database & Storage)

服务: Supabase

职责: 使用 PostgreSQL 数据库存储明信片的文本数据，使用 Storage 服务永久存储生成的图片文件。

如何本地部署 👨‍💻
1. 准备环境
本地已安装并成功运行的 Stable Diffusion WebUI，并已加载：

基础Checkpoint模型 (例如 AnythingV5)

您自己训练的 xiantiaogou_style.safetensors LoRA模型。

对应的 control_v11p_sd15_canny ControlNet模型。

Python 3.9+

Node.js 和 npm/pnpm

2. 启动AI计算后端
在 stable-diffusion-webui 目录下，编辑 webui-user.sh (或 .bat) 文件。

设置启动参数以开启API和公网访问（推荐使用Cloudflare Tunnel）：

export COMMANDLINE_ARGS="--listen --api --skip-torch-cuda-test --server-name 0.0.0.0"

启动服务: ./webui.sh

通过Cloudflare Tunnel等工具将 http://127.0.0.1:7860 暴露到公网，获得一个类似 https://your-tunnel.trycloudflare.com 的URL。

3. 启动逻辑后端
克隆本仓库: git clone https://github.com/your-username/line-puppy-adventure.git

进入后端目录: cd line-puppy-adventure/backend

创建并激活虚拟环境:

python -m venv venv
source venv/bin/activate

安装依赖: pip install -r requirements.txt

设置环境变量: 创建一个 .env 文件，并填入以下内容：

STABLE_DIFFUSION_API_URL="[https://your-tunnel.trycloudflare.com/sdapi/v1/txt2img](https://your-tunnel.trycloudflare.com/sdapi/v1/txt2img)" # 替换为你的SD API地址
GEMINI_API_KEY="your_google_gemini_api_key"
SUPABASE_URL="your_supabase_project_url"
SUPABASE_KEY="your_supabase_anon_key"

启动FastAPI服务: uvicorn main:app --reload

4. 启动前端
前端代码位于 frontend 目录，可以直接在浏览器中打开 index.html 进行测试，或使用 live-server 等工具启动。

注意: 确保前端JS代码中的API请求地址指向你本地运行的FastAPI后端 (例如 http://127.0.0.1:8000)。

最大的挑战与最满意的设计 ❤️
最大的挑战:

前端UI健壮性: 由于明信片内容（图片尺寸、文字长度）由AI动态生成，使用纯CSS构建一个能稳定适应各种动态内容的布局，避免元素溢出或重叠，是一个巨大的挑战。

交互流程打磨: 如何将一个简单的“输入->输出”流程，设计成一个充满“冒险”和“惊喜”感的体验，花费了大量时间进行推演和迭代。

最满意的设计:

“惊喜包裹”交互。这个设计将用户在等待生成结果时的枯燥感，巧妙地转化为了“等待礼物”的期待感。用户亲手“拆开”包裹的动作，极大地增强了最终获得明信片时的仪式感和满足感，是整个产品从冰冷工具变得温暖、充满人情味的点睛之笔。

致谢 🙏
感谢 Stable Diffusion 社区和所有模型创作者。

感谢 Gradio 和 FastAPI 提供了强大的开源工具。

感谢 Hugging Face, Cloudflare, 和 Supabase 提供了强大的Serverless平台和后端服务。

由 [Your Name] 创建 <!-- 替换为你的名字 -->
