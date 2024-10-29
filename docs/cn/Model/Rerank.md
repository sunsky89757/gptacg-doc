# 重排模型

>采用查询和文档作为输入，结合向量检索匹配结果，给向量相似度输出分值。

```python
import requests

url = "https://api.juheai.top/v1/rerank"

payload = {
    "model": "bge-reranker-v2-m3",
    "query": "Apple",
    "documents": ["苹果", "香蕉", "水果", "蔬菜"],
    "top_n": 4,
    "return_documents": True,
    "max_chunks_per_doc": 123,
    "overlap_tokens": 79
}
headers = {
    "Authorization": "Bearer sk-xxx",
    "Content-Type": "application/json"
}

response = requests.request("POST", url, json=payload, headers=headers)

print(response.text)
```

?>如果您需要获取各个技术栈的调用示例代码，请[查阅此处>>](https://juheai.apifox.cn/)