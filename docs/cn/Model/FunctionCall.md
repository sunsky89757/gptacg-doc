# 函数调用

>大模型自身能力更聚焦于推理分析，函数调用Fuction_Call作为能力的补充，允许你将模型（如 gpt-4o）连接到外部工具和系统，这对于搭建多功能的AI智能体（如数学计算、上网搜索、查询天气、查询数据库等）非常有用。

```python
import requests
import json

url = "https://api.juheai.top/v1/chat/completions"

payload = json.dumps({
    "model": "gpt-4o",
    "temperature": 0,
    # "stream": True,
    "messages": [
        {
            "role": "user",
            "content": "查一下纽约今天的天气?"
        }
    ],
    "tools": [
        {
            "type": "function",
            "function": {
                "name": "get_current_weather",
                "description": "Get the current weather in a given location",
                "parameters": {
                    "type": "object",
                    "properties": {
                        "location": {
                            "type": "string",
                            "description": "The city and state, e.g. San Francisco, CA"
                        },
                        "unit": {
                            "type": "string",
                            "enum": [
                                "celsius",
                                "fahrenheit"
                            ]
                        }
                    },
                    "required": [
                        "location"
                    ]
                }
            }
        }
    ],
    "tool_choice": "auto"
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