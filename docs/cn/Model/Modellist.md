# 模型列表

## 模型及价格

| 模型                               | 费用/1MT   | 支持FC | 发布日期 |
| ---------------------------------- | ---------- | ------ | -------- |
| gpt-3.5-turbo                      | ¥6         | √      | 24年01月 |
| gpt-3.5-turbo-0125                 | ¥4         | √      | 24年01月 |
| gpt-3.5-turbo-instruct             | ¥12        | ×      | 23年09月 |
| gpt-4                              | ¥60        | √      | 23年03月 |
| gpt-4-1106-preview                 | ¥20        | √      | 23年11月 |
| gpt-4-0125-preview                 | ¥20        | √      | 24年01月 |
| gpt-4-turbo-preview                | ¥20        | √      | 24年01月 |
| gpt-4-turbo                        | ¥20        | √      | 24年04月 |
| gpt-4-turbo-2024-04-09             | ¥20        | √      | 24年04月 |
| tts-1                              | ¥30        | ×      | 23年11月 |
| tts-1-hd                           | ¥60        | ×      | 23年11月 |
| whisper-1                          | ¥60        | ×      | 23年06月 |
| claude-3-opus-20240229             | ¥30        | ×      | 24年02月 |
| claude-3-haiku-20240307            | ¥0.5       | ×      | 24年03月 |
| gpt-4-all                          | ¥120       | ×      | 逆向plus |
| gpt-4-gizmo-*                      | ¥60        | ×      | 逆向plus |
| dall-e-3                           | ¥0.3/张    | ×      | 23年09月 |
| text-embedding-ada-002             | ¥2         | ×      | 22年12月 |
| text-embedding-3-large             | ¥2.6       | ×      | 24年01月 |
| text-embedding-3-small             | ¥0.4       | ×      | 24年01月 |
| deepseek-chat                      | ¥4         | √      | 24年06月 |
| deepseek-coder                     | ¥4         | √      | 24年06月 |
| gpt-4o-2024-05-13                  | ¥20        | √      | 24年05月 |
| gpt-4o                             | ¥20        | √      | 24年05月 |
| claude-3-5-sonnet-20240620         | ¥6         | ×      | 24年06月 |
| midjourney-fast                    | ¥0.3/次    | ×      | 23年12月 |
| gpt-4o-mini                        | ¥1.2       | √      | 24年07月 |
| gpt-4o-2024-08-06                  | ¥10        | √      | 24年08月 |
| chatgpt-4o-latest                  | ¥20        | √      | 24年08月 |
| llama-3.1-8b                       | ¥6         | ×      | 24年08月 |
| llama-3.1-70b                      | ¥20        | ×      | 24年08月 |
| llama-3.1-405b                     | ¥30        | ×      | 24年08月 |
| flux-pro                           | ¥0.3/次    | ×      | 24年08月 |
| chatgpt-4o-latest                  | ¥20        | √      | 24年08月 |
| text-moderation-latest             | ¥1.2       | ×      | 24年08月 |
| o1-preview                         | ¥30        | ×      | 24年09月 |
| o1-preview-2024-09-12              | ¥30        | ×      | 24年09月 |
| o1-mini                            | ¥6         | ×      | 24年09月 |
| o1-mini-2024-09-12                 | ¥6         | ×      | 24年09月 |
| o1-preview-all                     | ¥0.3/次    | ×      | 24年09月 |
| o1-mini-all                        | ¥0.15/次   | ×      | 24年09月 |
| gpt-4o-realtime-preview            | ¥200(语音) | ×      | 24年10月 |
| gpt-4o-realtime-preview-2024-10-01 | ¥200(语音) | ×      | 24年10月 |
| claude-3-5-sonnet-20241022         | ¥12        | ×      | 24年10月 |

?>**1MT：**输入一百万tokens，以上计价以人民币2元1刀计算得出，若买小额，在此价格基础上*1.75。

## 获取模型

<!-- tabs:start -->

#### **curl**

```curl
curl -L -X GET 'https://api.juheai.top/v1/models' \
-H 'Accept: application/json' \
-H 'Authorization: Bearer sk-xxx'
```

#### **python**

```python

import requests

url = "https://api.juheai.top/v1/models"

payload = {}
headers = {
    'Accept': 'application/json',
    'Authorization': 'Bearer sk-xxx'
}

response = requests.request("GET", url, headers=headers, data=payload)

# 将响应内容转换为字典
response_dict = response.json()

# 提取模型 ID
model_ids = [model.get("id") for model in response_dict.get("data", [])]

# 将模型 ID 写入到文件
with open("model_ids.txt", "w") as file:
    for model_id in model_ids:
        file.write(model_id + "\n")

print("模型 ID 已保存到 model_ids.txt 文件中。")

```

<!-- tabs:end -->

## 余额查询

```python
import requests

def get_total_usage(api_key):
    headers = {
        "Authorization": f"Bearer {api_key}",
        "Content-Type": "application/json"
    }
    
    # 获取订阅信息
    response_subscription = requests.get("https://api.juheai.top/v1/dashboard/billing/subscription", headers=headers)
    if response_subscription.status_code != 200:
        return f"获取订阅数据出错: {response_subscription.text}"
    
    try:
        subscription_data = response_subscription.json()
        total_limit = subscription_data.get("hard_limit_usd")
    except ValueError:
        return "解析订阅数据时出错"

    # 获取已用额度
    response_usage = requests.get("https://api.juheai.top/v1/dashboard/billing/usage", headers=headers)
    if response_usage.status_code != 200:
        return f"获取使用数据时出错：{response_usage.text}"
    
    try:
        billing_data = response_usage.json()
        total_usage_usd = billing_data.get("total_usage", 0) / 100  # 使用默认值0以防止缺失
    except ValueError:
        return "解析使用数据时出错"

    print(f"\n总额度： ${total_limit:.2f}  \n已用额度： ${total_usage_usd:.2f}  \n剩余额度：${total_limit - total_usage_usd:.2f}  \n")

if __name__ == '__main__':
    api_key = "sk-xxx"
    get_total_usage(api_key)
```

你将会收到如下回复(举例)：

```
总额度： $292.31  
已用额度： $202.30  
剩余额度：$90.01

```

?>如果您需要获取各个技术栈的调用示例代码，请[查阅此处>>](https://juheai.apifox.cn/)