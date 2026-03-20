---
title: openclip自动切片工具教程与使用心得
tags:
  - openclip
  - 自动切片工具
  - 视频处理
  - 视频剪辑
  - 视频标题
  - 视频封面
  - 视频分析
  - 视频智能分析
  - 视频智能分析工具
cover: /img/微信图片_20250504124006.jpg
banner: /img/微信图片_20250504124006.jpg
date: 2026-03-20 17:23:02
---

# openclip自动切片工具教程与使用心得
## 项目介绍：
一个轻量化自动化视频处理流水线，用于识别和提取长视频（特别是口播和直播回放）中最精彩的片段。使用 AI 驱动的分析来发现亮点，生成剪辑，并添加标题和封面。
[openclip](https://github.com/linzzzzzz/openclip)
此项目目前只有70个star,泯然众人的小项目,但上手起来还是很好用的,推荐一手.
## 安装
就算你是python小白也完全不需要担心，在这里我祭出焚决：直接git clone项目后用trae打开,让trae来帮你自动化安装依赖,这集神了.
（并且trae会自动识别项目的skill,如果你想的话可以在设置中把他添加到全局技能中，这样就能随时随地调用了。）
不过建议改成从国内的镜像源进行下载,比如清华镜像或阿里云镜像.不然太慢了,等的花儿都谢了也下不完
### 清华镜像
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

### 阿里云镜像
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/

搞不懂的也可以直接丢给trae，这集神了.
## 配置
设置 API 密钥（用于 AI 功能）
### 使用 Qwen：

export QWEN_API_KEY=your_api_key_here
### 使用 OpenRouter：

export OPENROUTER_API_KEY=your_api_key_here
目前项目只支持这俩
有一说一阿里的UI是真难用啊（
## 启动！
### 运行流水线
#### 选项 A：使用 Streamlit 网页界面
启动 Streamlit 应用：

uv run python -m streamlit run streamlit_app.py
也可以用 python -m streamlit run streamlit_app.py 指令
应用启动后，打开浏览器访问显示的 URL（通常是 http://localhost:8501）。

### 使用流程：

在侧边栏选择输入类型（视频 URL 或本地文件）
配置处理选项（LLM 提供商等）
点击「Process Video」按钮开始处理
查看实时进度和最终结果
在结果区域预览生成的剪辑和封面
优势： 无需记住命令行参数，提供可视化操作界面，适合所有用户。


### 🔄 并发处理与后台任务
#### 选项 B：使用 AI Agent 技能
如果你使用 Claude Code、TRAE、Cursor 或任何其他支持 skills 的 Agent，可以直接用自然语言处理视频，无需手动输入命令：

"帮我从这个视频里提取精彩片段：https://www.bilibili.com/video/BV1234567890"
"处理一下 ~/Downloads/livestream.mp4，用英语作为输出语言"
Agent 会自动完成环境配置、下载、转录、分析、剪辑和标题添加等全部流程。
### 虽然项目提供了命令行工具,但是我感觉还是利用skill更方便,比较命令行参数太几把难背了
只需要给trae提供视频的url,或者视频的本地路径让他来做所有事就好啦.
## 小贴士：
uv:python环境的包管理工具，类似于npm,旨在取代传统的 pip、virtualenv、pip-tools 等工具的组合。