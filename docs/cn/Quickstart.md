# 快速接入

>聚合API按照OpenAI API那样，提供了一个简单的接口，能够使用最先进的 AI 模型进行自然语言处理、图像生成、语义搜索和语音识别。按照本指南学习如何生成对自然语言提示的人类化响应、创建用于语义搜索的向量嵌入，以及从文本描述生成图像。

**首先，你可以这样使用聚合API：**

<!-- tabs:start -->

#### **curl**
```curl
curl "https://api.juheai.top/v1/chat/completions" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer sk-xxx" \
    -d '{
        "model": "gpt-4o-2024-05-13",
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
你将会收到如下回复
```curl
{"id":"chatcmpl-9wk81HBBspfBfOcKnaTtsuELgfXen","model":"gpt-4o-2024-05-13","object":"chat.completion","created":1723787416,"choices":[{"index":0,"message":{"role":"assistant","content":"你好！有什么我可以帮助你的吗？"},"finish_reason":"stop"}],"usage":{"prompt_tokens":18,"completion_tokens":9,"total_tokens":27}}
```
#### **python**

```python
import requests
import json

url = "https://api.juheai.top/v1/chat/completions"

payload = json.dumps({
   "model": "gpt-4o-2024-05-13",
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

你将会收到如下回复：

```python
{
  "id": "chatcmpl-9wkE9z3XjWjBGMtfuCzt4cXu3D48J",
  "object": "chat.completion",
  "created": 1723787749,
  "model": "gpt-4o-2024-05-13",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "你好！有什么我可以帮你的吗？",
        "refusal": null
      },
      "logprobs": null,
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 18,
    "completion_tokens": 9,
    "total_tokens": 27
  },
  "system_fingerprint": "fp_3aa7262c27"
}
```
<!-- tabs:end -->

**你还可以使用OpenAI提供的官方库：**

安装openai库
```
pip install openai
```

```python
from openai import OpenAI
client = OpenAI(
    # This is the default and can be omitted
    base_url="https://api.juheai.top/v1",
    api_key="sk-xxx",
)

completion = client.chat.completions.create(
  model="gpt-4o",
  messages=[
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Hello!"}
  ]
)

print(completion.choices[0].message)

```

