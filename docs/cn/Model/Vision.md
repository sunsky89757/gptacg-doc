# 识图

>GPT-4o、GPT-4o mini 和 GPT-4 Turbo 拥有视觉能力，这意味着这些模型可以处理图像并回答有关它们的问题，喂给模型图片和问题，它将返回识图结果。

```python
import requests
import json

url = "https://api.juheai.top/v1/chat/completions"

payload = json.dumps({
   "model": "gpt-4o-2024-08-06",
   "stream": False,
   "messages": [
      {
         "role": "user",
         "content": [
            {
               "type": "text",
               "text": "这张图片有什么"
            },
            {
               "type": "image_url",
               "image_url": {
                  "url": "https://github.com/dianping/cat/raw/master/cat-home/src/main/webapp/images/logo/cat_logo03.png"
               }
            }
         ]
      }
   ],
   "max_tokens": 400
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