# 文本生成

>给定一组包含对话的消息，模型将返回一个回应。

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
   'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

?>如果您需要获取各个技术栈的调用示例代码，请[查阅此处>>](https://juheai.apifox.cn/)