# 图像生成

>描述你想要的画面，大模型就会给你输出满足要求的图片。

```python
import http.client
import json

conn = http.client.HTTPSConnection("api.juheai.top")
payload = json.dumps({
   "model": "dall-e-3",
   "prompt": "画一只小白兔",
   "n": 1,
   "size": "1024x1024"
})
headers = {
   'Authorization': 'Bearer sk-xxx',
   'Content-Type': 'application/json'
}
conn.request("POST", "/v1/images/generations", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

?>如果您需要获取各个技术栈的调用示例代码，请[查阅此处>>](https://juheai.apifox.cn/)