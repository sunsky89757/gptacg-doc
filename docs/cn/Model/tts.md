# 文字转语音tts

>大模型试图将你的文字转化为真实的声音。

```curl
curl https://api.juheai.top/v1/audio/speech \
  -H "Authorization: Bearer sk-xxx" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "tts-1",
    "input": "让全球顶级AI人人可用 - 聚合AI",
    "voice": "alloy"
  }' \
  --output speech.mp3
```

```python
import http.client
import json

conn = http.client.HTTPSConnection("api.juheai.top")
payload = json.dumps({
   "model": "tts-1",
   "input": "Hello World, how are you?",
   "voice": "alloy"
})
headers = {
   'Authorization': 'Bearer sk-xxx',
   'User-Agent': 'Apifox/1.0.0 (https://apifox.com)',
   'Content-Type': 'application/json'
}
conn.request("POST", "https://api.juheai.top/v1/audio/speech", payload, headers)
res = conn.getresponse()
data = res.read()

# Save the binary data to a file
with open('output_audio.mp3', 'wb') as audio_file:
    audio_file.write(data)

print("Audio saved successfully as output_audio.mp3")
```

?>如果您需要获取各个技术栈的调用示例代码，请[查阅此处>>](https://juheai.apifox.cn/)