# 聚合AI，让全球顶级AI大模型人人可用

`纯官转API` `超高并发` `无需魔法` `可用性≥99%` `多种模型`

## 概述

!>**声明：**本站提供的服务仅限学习、研究、测试等用途，请不要用于任何危害国家安全的用途，本站不承担用户导致的法律责任，并保留追究法律责任的权利。

[聚合AI](https://www.gptacg.com)是一个大模型集成平台，包含OpenAI、Anthropic、Gemini及中国主流大模型。您通过[购买聚合AI](https://www.juheaistore.top)，即可方便快速实现多家大模型的统一调用，如gpt-4o、claude-3-opus、gemini-pro-1.5等，[已支持模型清单>>](cn/ModelList.md)，与官网同步支持最新模型。

如果您是非允许使用国家的用户，在官方网站购买要考虑如何绕过官方IP审查、封号等复杂问题，这并不是每个用户所擅长的，会消耗大量的精力和时间，试错成本极高。

选择聚合AI平台即可免去在多家AI公司注册、认证和绑卡购买的过程，让您完全回归需求本质，专注于研究借助AI处理实际问题。

![聚合AI工作原理图](imag/juheaiyuanli.webp "聚合AI工作原理图")

选择聚合AI服务，可以满足您以下需求：

- **解决了地域限制问题**
  
  OpenAI等国外大模型是禁止部分亚洲国家使用的，聚合AI将这部分国家用户的请求，先做合法化处理，再与官方对接传递，而用户什么都不需要做即可像非限制国家那样自用使用任意大模型。

- **解决了频率限制问题**
  
  官方API对于用户有分级调用频率的限制，中转API解决了此类问题，并且支持超高并发，完全支持用户高频率日常使用，也支持企业用于生产作业。

- **解决了费用成本问题**
  
  官方API是按充值美金计算的，根据目前的汇率7：1左右，想要使用100美金的API服务，就要支付高达700元人民币，而聚合AI却最低可致200元兑换100美金，成本节约3倍之多。

?> **纯真性原则** 聚合AI所有API模型均采用官方纯净转发，无附加灌注提示词，非逆向获取。除支持基础参数外，我们还同样支持函数调用function call、结构化输出Structured Outputs等高级参数。

?> **稳定性原则** 我们致力于为您提供最稳定的API服务，我们通过[uptime心跳检测>>](https://uptime.gptacg.com/status/juheai)24小时不间断监控模型可用性。历史数据显示，过去半年聚合API的平均可用性超过99%，远超过市面平均水平。

?> **隐私性原则** 聚合AI采用开源中转程序[New-api](https://github.com/Calcium-Ion/new-api)实现转发，全部代码来源于开源社区，我们承诺不对程序添加任何二次开发代码，仅通过程序日志功能收集用户请求基本参数以方便计费，不保留任何content内容，高度重视用户的数据隐私。

## 如何使用

我们为您提供了两种使用方式，理论上都是通过API实现对接，但表现形式差异较大，您可以根据您的需要选择任意方式使用：

<!-- tabs:start -->

#### **Chat程序**

**该方式更适合入门新手。** 您可以通过访问我们的站点 https://www.gptacg.com ，选择NextChat、Dooy-AI、LibreChat任意一种AI程序开始使用，仅需简单设置即可像使用ChatGPT Plus那样开启AI对话之旅！使用方法请查阅[应用程序篇](cn/UseApp.md)。

![Chat程序](imag/Chat程序.webp)

?>程序统一使用方法为在设置中配置API-Key和Base_Url接口：https://api.juheai.top ,个别程序需要书写为：https://api.juheai.top/v1 或者 https://api.juheai.top/v1/chat/completions 。

#### **API调用**

**该方式更适合程序开发。** 聚合AI的API对接格式与OpenAI对接格式完全一致，您可以查阅[官方API文档](https://platform.openai.com/docs/api-reference/introduction)，或通过以下方式快速接入：

<!-- tabs:start -->

#### **curl请求**

```

curl https://api.juheai.top/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer sk-xxx" \
  -d '{
    "model": "gpt-4o",
    "messages": [
      {
        "role": "system",
        "content": "You are a helpful assistant."
      },
      {
        "role": "user",
        "content": "你好"
      }
    ]
  }'

```

您将收到如下返回：

```

{
  "id": "chatcmpl-9vNXutfC8NJxijJ5JNKey7Edfs1Jv",
  "object": "chat.completion",
  "created": 1723462234,
  "model": "gpt-4o-2024-05-13",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "你好！有什么我可以帮忙的吗？"
      },
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 18,
    "completion_tokens": 9,
    "total_tokens": 27
  },
  "system_fingerprint": "fp_abc28019ad"
}


```

#### **python请求**

```python

import requests
import json

url = "https://api.juheai.top/v1/chat/completions"

payload = json.dumps({
   "model": "gpt-4o",
   "messages": [
      {
         "role": "system",
         "content": "You are a helpful assistant."
      },
      {
         "role": "user",
         "content": "你好"
      }
   ],
   "stream": False
})
headers = {
   'Accept': 'application/json',
   'Authorization': 'Bearer sk-xxx',
   'User-Agent': 'Apifox/1.0.0 (https://apifox.com)',
   'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)

```
您将收到如下返回：

```python

{
  "id": "chatcmpl-9vNS7xiWDXMfZ6UZ6zsFQUbmOOvgQ",
  "object": "chat.completion",
  "created": 1723461875,
  "model": "gpt-4o-2024-05-13",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "你好！有什么我可以帮忙的吗？"
      },
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 18,
    "completion_tokens": 9,
    "total_tokens": 27
  },
  "system_fingerprint": "fp_abc28019ad"
}

```

<!-- tabs:end -->

<!-- tabs:end -->

## 关键概念

**Base_Url接口**

Base_Url指的是基础URL，也称之为接口或基础端点，用于构建API调用地址。用户在进行API请求时，通常需要与具体的端点路径结合，以构成完整的请求URL。例如，Base_Url为 https://api.openai.com ，具体端点路径为 /v1/chat/completions 时，完整请求URL为 https://api.openai.com/v1/chat/completions 。聚合AI的Base_Url接口统一为 https://api.juheai.top 。Base_Url与API Key在API调用时缺一不可。

**API Key令牌**

API Key令牌是一种用于验证和授权访问API的字符序列。每个API Key都是唯一的，与持有用户绑定。输入正确API Key的客户端可以享受大模型的API服务，它相当于是您打开房门的钥匙。Base_Url与API Key在API调用时缺一不可。

**Tokens**

Tokens是AI中对文本进行细化处理后，对文本使用量的基本计量单元，有点类似于字符量，但存在差异，具体换算关系可以粗略的等同于1000 tokens = 750 个单词 = 500 个汉字。[OpenAI官方计算工具（需魔法访问）](https://platform.openai.com/tokenizer)

**Stream流式输出**

流式输出指的是数据在不断生成和接收过程中立即被处理和输出，而不是等待生成和处理完所有数据后才进行输出。这对Chat场景非常有效，用户在发送问题后能够在更短的时间内就收到AI的回复，然后像打字机一样陆续完成回答，相较于非流式输出，用户等待时间更短，体验更好。

**Embedding向量模型**

向量模型能够将语言、图像、声音等多样化的信息，转化为一种通用的、数学化的表达形式，为AI开启一扇通往对世界智能理解与创造的大门。向量模型擅长将抽象的概念和具体的事物转化为一系列数值，这些数值在多维空间中按照特定的模式排列，形成了向量。在AI理解世界的过程中，向量模型扮演着一个至关重要的角色，甚至可以说它是AI大模型用以构建和理解复杂数据的基础，也是对不同形态数据的一种标准化的“浓缩”。

**FC(Fuction_Call)函数调用**

大模型自身能力更聚焦于推理分析，函数调用Fuction_Call作为能力的补充，允许你将模型（如 gpt-4o）连接到外部工具和系统，这对于搭建多功能的AI智能体（如数学计算、上网搜索、查询天气、查询数据库等）非常有用。

**RAG**

检索增强生成 (RAG) 是一种使用来自私有或专有数据源的信息来辅助文本生成的技术。它将检索模型（设计用于搜索大型数据集或知识库）和生成模型（例如大型语言模型 (LLM)，此类模型会使用检索到的信息生成可供阅读的文本回复）结合在一起。简单点理解就是你如果有一份文件需要大模型解读，RAG将先把文件拆解，并组织相关内容，大模型参考自身训练数据和RAG提交的这些新内容推理并生成回答，这比仅使用大模型自身训练数据生成的答案更加精准。

**LLM**

LLM（Large Language Model）指的是训练在大规模文本数据上的语言模型，如GPT-4o。LLM具有强大的语言理解和生成能力，可以执行各种自然语言处理任务，如文本生成、翻译、问答等。

**直连/中转API**

直连API：不经过任何第三方服务器，请求端直接连接官方API服务，比如OpenAI直连API，对应的直连接口必须为 https://api.openai.com ，如果不是，那100%是中转API。

中转API：经过第三方服务器转发即为中转API，接口为第三方中转服务商提供的第三方接口，如聚合AI的接口为： https://api.juheai.top 。

直连API和中转API没有好与不好之分，选择能满足自身需求，两者均可。下面为直连API和中转API的主要区别：

| 对比项  | 直连API          | 中转API          |
|--------|------------------|------------------|
| 地域要求  | 必须为支持国家IP | 无限制           |
| 价格    | 汇率价           | 一般会低于汇率价  |
| API稳定性  | 绝对稳定         | 可能会有波动      |
| API质量    | 100%            | 视服务商而定，最高100%原品质   |
| API速度    | 较快            | 视服务商而定，优化后可比直连更快   |
| 风险 | 非支持地区100%封号 | 0封号风险            |
| 并发量  | 一般小额并发很低 | 轮询账号，超高并发 |

**速率限制**

速率限制有五种测量方式：每分钟请求数（RPM）、每天请求数（RPD）、每分钟令牌数（TPM）、每天令牌数（TPD）和每分钟图像数（IPM）。根据首先发生的情况，速度限制可以在任何选项中触发。例如，你可能会向ChatCompletions端点发送20个请求，但只有100个令牌，如果你的RPM是20，那么这将达到你的限制，即使你在这20个请求中没有发送15万个令牌（如果你的TPM限制是15万）。

## 并发性能

?> **注释：** 以下为聚合AI模型经测试的并发量参考值，表中未列出模型并发量与同级模型共享，如gpt-4-1106-preview的并发与gpt-4-turbo-prevew并发共享。

| 模型名称           | real_rpm | tpm         |
|-----------------------------|----------|-------------|
| gpt-4o-mini                 | 820000.0 | 82000000.0  |
| gpt-4o                      | 461700.0 | 76950000.0  |
| gpt-4-turbo                 | 50880.0  | 8480000.0   |
| gpt-4                       | 43920.0  | 7320000.0   |
| gpt-4-turbo-preview         | 50880.0  | 8480000.0   |
| text-embedding-ada-002      | 136500.0 | 22750000.0  |
| text-embedding-3-small      | 136500.0 | 22750000.0  |
| text-embedding-3-large      | 136500.0 | 22750000.0  |
| gpt-3.5-turbo                | 127800.0 | 21180000.0  |
| gpt-3.5-turbo-instruct       | 77760.0  | 12960000.0  |
| dall-e-3                    | 318.0    | 0.0         |
| tts-1                       | 162.0    | 0.0         |
| whisper-1                   | 162.0    | 0.0         |

