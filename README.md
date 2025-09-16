💌 线条小狗明信片工厂 (Line Puppy Postcard Factory)
欢迎来到线条小狗明信片工厂！这是一个有趣的应用，它利用 Stable Diffusion 和专门训练的“线条小狗”LoRA 模型，将您输入的祝福语或故事，变成一张张风格独特、充满温馨情感的线条小狗主题明信片。

（在这里替换成您的应用截图或GIF动图）

✨ 项目特色
AI 艺术生成：基于强大的 Stable Diffusion 模型，将文本创意转化为可见的艺术作品。

独特的艺术风格：集成特定的线条小狗 LoRA 模型，确保每一张图片都拥有可爱、治愈的“线条小狗”风格。

个性化定制：用户可以输入任意文字，AI 会根据文本内容智能生成对应的场景和图像。

简洁的用户界面：提供一个直观、易于操作的前端界面，让用户可以轻松创作和下载自己的明信片。

解耦的后端服务：通过 API 与 Stable Diffusion WebUI 进行通信，架构清晰，易于扩展和维护。

🛠️ 技术栈
后端：Python, Flask

AI 模型：Stable Diffusion

模型微调：线条小狗 LoRA (Line Puppy Style)

API 服务：Stable Diffusion WebUI API

前端：HTML, CSS, JavaScript

🚀 开始使用
想要在您自己的电脑上运行这个项目吗？请按照以下步骤操作。

1. 先决条件
在开始之前，请确保您的系统已经安装并配置好以下环境：

Python 3.8+

Git

AUTOMATIC1111/stable-diffusion-webui：这是我们AI绘图的核心服务。请确保它能正常运行，并且您已经下载了基础的 Stable Diffusion 大模型 (e.g., v1-5-pruned-emaonly.safetensors)。

2. 安装步骤
第一步：克隆本项目

git clone [https://github.com/your-username/line-puppy-postcard-factory.git](https://github.com/your-username/line-puppy-postcard-factory.git)
cd line-puppy-postcard-factory

(请将 your-username/line-puppy-postcard-factory 替换为您自己的仓库地址)

第二步：配置 Stable Diffusion WebUI

下载 LoRA 模型：

从 Civitai 或其他来源下载线条小狗 LoRA 模型文件。

将下载好的 .safetensors 文件放入您的 stable-diffusion-webui/models/Lora 文件夹中。

启动 WebUI 并开启 API：

为了让我们的应用能够和 WebUI 通信，您必须在启动时添加 --api 参数。

对于 Windows 用户: 编辑 webui-user.bat 文件，在 COMMANDLINE_ARGS= 后面添加 --api。

set COMMANDLINE_ARGS=--api

对于 aports/Linux 用户: 编辑 webui-user.sh 文件，在 COMMANDLINE_ARGS= 后面添加 --api。

export COMMANDLINE_ARGS="--api"

修改完毕后，正常启动 Stable Diffusion WebUI。如果一切顺利，它将在 http://127.0.0.1:7860/ 上运行。

第三步：安装后端依赖并运行

创建并激活虚拟环境 (推荐):

python -m venv venv
# Windows
venv\Scripts\activate
# aports/Linux
source venv/bin/activate

安装 Python 依赖包:

pip install -r requirements.txt

运行 Flask 应用:

flask run

您的后端服务现在应该已经在 http://127.0.0.1:5000/ 上运行了。

3. 如何使用
确保您的 Stable Diffusion WebUI (API模式) 和 Flask 后端服务都在运行。

打开浏览器，访问 http://127.0.0.1:5000/。

在输入框中写下您的祝福、一个小故事或者任何您想画的场景。

点击“生成明信片”按钮。

稍等片刻，一张独一无二的线条小狗明信片就会出现在您的眼前！

🤝 如何贡献
我们非常欢迎社区的贡献！如果您有任何好的想法或者发现了Bug，请：

Fork 本仓库。

创建一个新的分支 (git checkout -b feature/AmazingFeature)。

提交您的修改 (git commit -m 'Add some AmazingFeature')。

将您的分支推送到远程仓库 (git push origin feature/AmazingFeature)。

提交一个 Pull Request。

📄 许可证
本项目采用 MIT 许可证 - 详情请见 LICENSE 文件。

🙏 致谢
感谢 AUTOMATIC1111 创造了如此强大的 Stable Diffusion WebUI。

感谢“线条小狗 LoRA 模型”的作者，为我们带来了这么可爱的艺术风格。

现在就开始创作属于您自己的温馨明信片吧！
