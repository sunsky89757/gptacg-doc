# 向量嵌入

>OpenAI 的文本嵌入衡量文本字符串的相关性。嵌入通常用于：
>- 搜索（根据查询字符串的相关性对结果进行排名）
>- 聚类（根据相似度将文本字符串分组）
>- 推荐（推荐与相关文本字符串）

```python
import requests
import json

url = "https://api.juheai.top/v1/embeddings"

payload = json.dumps({
   "model": "text-embedding-ada-002",
   "input": "你好，世界！"
})
headers = {
   'Authorization': 'Bearer sk-xxx',
   'User-Agent': 'Apifox/1.0.0 (https://apifox.com)',
   'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```