# 应用程序

随着近两年AI的发展，开源社区[Github](https://github.com/)涌现出了许多优秀的开源AI程序项目，用户可以基于自身需要选择合适的开源AI程序进行使用，经实践发现，支持OpenAI Compatible（OpenAI兼容）的程序均可使用本站API，很庆幸大部分AI程序都在这样做。统一接入方式：Base_Url接口 + API Key，其中接口视程序情况而定，存在以下三种情况，其中绝大部分是第一种情况：
```
https://api.juheai.top
https://api.juheai.top/v1
https://api.juheai.top/v1/chat/completions
```
下面我们将列出一部分优秀AI应用程序的配置方法，以帮助用户节约时间快速使用程序：

## LibreChat

>**介绍：**外国人的项目，仿GPT PLUS界面UI的ChatUI程序，迄今为止最为强大的ChatUI，程序最牛逼的地方在于支持丰富的AI功能，对话、RAG分析文件、插件、语音、多端同步样样都行。
><br> **项目地址：** https://github.com/danny-avila/LibreChat</br>

**配置：**一般登录程序后仅需要填写API Key即可，访问入口： https://lc.gptacg.com 。如需自行部署，可以参考文章[《Librechat快速部署指南》](https://www.gptacg.com/librechat-easy-deploy-guide/)。

![设置LibreChat](../imag/configapi.webp)

![设置LibreChat2](../imag/configapi2.webp)

## NextChat

>**介绍：**这是一个中国大佬的项目，因为做的太丝滑团队导致被收购了，目前新的团队也出了商业版本，不过失去了大佬的创作，商业版风格直接变了味，还是开源版比较舒服。
><br> **项目地址：** https://github.com/ChatGPTNextWeb/ChatGPT-Next-Web</br>

**配置：**需要在设置中勾选自定义接口，并填写接口地址：https://api.juheai.top 和 API KEY，访问入口： https://vvip.gptacg.com 。如需自行部署，可参考文章[《通过NextChat(ChatGPT-Next-Web)低成本给自己或客户部署GPT程序》](https://www.gptacg.com/deploy-a-low-cost-gpt-program/)

![NextChat设置](../imag/nextchatconfig.webp)

## Dooy-AI

>**介绍：**github原名叫chatgpt-web-midjourney-proxy，作者是Dooy，项目名字又长识别度又低，索性咱们以作者名字冠名更朗朗上口，这个项目除了支持chat外，还支持midjourney绘图、suno音乐、luma视频创作的可视化操作，可玩性极高。
><br> **项目地址：** https://github.com/Dooy/chatgpt-web-midjourney-proxy</br>

**配置：**需要在设置中填写接口地址：https://api.juheai.top 和 API Key，访问入口：https://dooy.gptacg.com 。如需自行部署，可参考文章[《拥有私人GPT：chatgpt-web-midjourney-proxy完整部署指南》](https://www.gptacg.com/chatgpt-web-midjourney-proxy-complete-deployment-guide/)

![Dooy-AI设置](../imag/dooy-aiconfig.webp)

## LobeChat

>**介绍：**现代化设计的开源 ChatGPT/LLMs 聊天应用与开发框架，支持语音合成、多模态、可扩展的（function call）插件系统，一键免费拥有你自己的 ChatGPT/Gemini/Claude/Ollama 应用。
><br> **项目地址：** https://github.com/lobehub/lobe-chat</br>

**配置：**需要在设置中填写接口地址：https://api.juheai.top/v1 和API Key，访问入口：https://lobe.gptacg.com 。

![LobeChat设置](../imag/lobechatconfig.webp)

## Chatbox

>**介绍：**Chatbox AI 是一款 AI 客户端应用和智能助手，支持众多先进的 AI 模型和 API，可在 Windows、MacOS、Android、iOS、Linux 和网页版上使用。
><br> **项目地址：** https://github.com/Bin-Huang/chatbox</br>

**配置：**需要在设置中选择OPENAI API，填写API域名： https://api.juheai.top 和API Key，下载并安装客户端进行本地使用。

![chatBox设置](../imag/chatboxconfig.webp)

## 沉浸式翻译

>**介绍：**全网口碑炸裂的双语对照网页翻译插件。你可以完全免费地使用它来实时翻译外语网页，PDF翻译，EPUB电子书翻译，视频双语字幕翻译等。还可以自由选择调用OpenAI (ChatGPT)、DeepL、Gemini等人工智能引擎来翻译上述内容。在手机上也可以随时随地用哦，真正帮助你打破信息壁垒。
><br> **项目地址：** https://github.com/immersive-translate/immersive-translate</br>

**配置：**安装沉浸式翻译浏览器插件后，在设置中选择OpenAI，并按照图示填写API Key和自定义API接口地址：https://api.juheai.top/v1/chat/completion ,即可开始使用。

![沉浸式翻译设置1](../imag/chenjinshiconfig1.webp)

![沉浸式翻译设置1](../imag/chenjinshiconfig2.webp)

## chatGPTBox

>**介绍：**将ChatGPT深度集成到浏览器中, 你所需要的一切均在于此。起初以为这只是一个单纯的浏览器页面翻译插件，直到用起来才发现它不止于此，我觉得它的页面总结和对话的能力更为出色，当然还有更多功能等你发掘。
><br> **项目地址：** https://github.com/josStorer/chatGPTBox</br>

**配置：**安装ChatGPTBox插件后，在高级 - API地址菜单中填写自定义OpenAI API地址：https://api.juheai.top ，然后进入常规菜单，在API模式中输入API Key和对应的模型即可使用。

![chatgptbox设置1](../imag/chatgptboxconfig1.webp)

![chatgptbox设置1](../imag/chatgptboxconfig2.webp)

## chatgpt-on-wechat

>**介绍：**基于大模型搭建的聊天机器人，同时支持 微信公众号、企业微信应用、飞书、钉钉 等接入，可选择GPT3.5/GPT-4o/GPT4.0/ Claude/文心一言/讯飞星火/通义千问/ Gemini/GLM-4/Claude/Kimi/LinkAI，能处理文本、语音和图片，访问操作系统和互联网，支持基于自有知识库进行定制企业智能客服。
><br> **项目地址：** https://github.com/zhayujie/chatgpt-on-wechat</br>

**配置方式一：**如果你是docker-compose方式部署，在docker/docker-compose.yml文件中添加如下环境变量：

```
<!-- 其它参数项 -->
environment:
      OPEN_AI_API_KEY: 'sk-xxx'
      OPEN_AI_API_BASE: 'https://api.juheai.top/v1'
<!-- 其它参数项 -->
```

**配置方式二：**如果直接Python部署，则在config.json文件中添加

```
<!-- 其它参数项 -->
"open_ai_api_key": "sk-xxx",
"open_ai_api_base": "https://api.openai.com/v1",
<!-- 其它参数项 -->

```

## 酒馆SillyTavern

![酒馆截图](../imag/sillytarben.webp)

>**介绍：**看图明意，这是一个可以依托于大模型进行角色扮演的程序，没玩过，感兴趣可以研究研究，聚合AI是完全支持API接入的。
><br> **项目地址：** https://github.com/SillyTavern/SillyTavern</br>

**配置方式：**设置中输入自定义端点：https://api.juheai.top/v1 ，和自定义API密钥。

![酒馆设置](../imag/sillytarvenconfig.webp)

## openai-translator

>**介绍：**既是浏览器插件也是跨平台桌面端应用，基于 ChatGPT API 的划词翻译浏览器插件和跨平台桌面端应用。
><br> **项目地址：** https://github.com/openai-translator/openai-translator</br>

**配置方式：**设置中输入API URL：https://api.juheai.top 和API密钥。

![OpenAI-Translator设置](../imag/openaitranslatorconfig.webp)

## continue

>**介绍：**continue是领先的开源 AI 代码助手。你可以连接任何模型和任何上下文，在 VS Code 和 JetBrains 里面构建自定义的自动补全和聊天体验。
><br> **项目地址：** https://github.com/continuedev/continue</br>

**配置方式：**安装IDE的continu插件，并在config.json文件中输入如下内容（原自带内容删除）：

```
{
  "models": [
    {
      "title": "JuheAI",
      "provider": "openai",
      "model": "gpt-4o",
      "apiBase": "https://api.juheai.top/v1",
      "apiType": "openai",
      "apiKey": "sk-xxx"
    }
  ]
}
```

## fastgpt

>**介绍：**基于 LLM 大语言模型的知识库问答系统，提供开箱即用的数据处理、模型调用等能力。同时可以通过 Flow 可视化进行工作流编排，从而实现复杂的问答场景！
><br> **项目地址：** https://github.com/labring/FastGPT</br>

**配置方式：**

## dify

## bisheng

## gpt_academic

## AnythingLLM

## OpenWebUI

## 问天


