# 语音转文字stt

>大模型试图将声音转化成精准的文字（或者翻译后的文字）。

**转录**
```python
import requests

url = "https://api.juheai.top/v1/audio/transcriptions"
headers = {
    "Authorization": "Bearer sk-xxx"
}
data = {
    "model": "whisper-1"
}
files = {
    "file": open("speech.mp3", "rb")
}

response = requests.post(url, headers=headers, data=data, files=files)
transcription = response.json()

print(transcription.get("text", "No transcription found"))

```
**翻译为英语**

```python
from openai import OpenAI
client = OpenAI(
    # This is the default and can be omitted
    base_url="https://api.juheai.top/v1",
    api_key="sk-xxx",
)

audio_file= open("speech.mp3", "rb")
translation = client.audio.translations.create(
  model="whisper-1", 
  file=audio_file
)
print(translation.text)
```

?>如果您需要获取各个技术栈的调用示例代码，请[查阅此处>>](https://juheai.apifox.cn/)