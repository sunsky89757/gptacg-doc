# 模型及计价

## 模型清单

| 模型                               | 费用/1MT   | 输出/输出 | 发布日期 | 备注                            |
| ---------------------------------- | ---------- | --------- | -------- | ------------------------------- |
| gpt-3.5-turbo                      | ¥6         | 3         | 24年01月 |                                 |
| gpt-3.5-turbo-0125                 | ¥4         | 3         | 24年01月 |                                 |
| gpt-3.5-turbo-instruct             | ¥12        | 1.33      | 23年09月 |                                 |
| gpt-4                              | ¥60        | 2         | 23年03月 |                                 |
| gpt-4-1106-preview                 | ¥20        | 3         | 23年11月 |                                 |
| gpt-4-0125-preview                 | ¥20        | 3         | 24年01月 |                                 |
| gpt-4-turbo-preview                | ¥20        | 3         | 24年01月 |                                 |
| gpt-4-turbo                        | ¥20        | 3         | 24年04月 |                                 |
| gpt-4-turbo-2024-04-09             | ¥20        | 3         | 24年04月 |                                 |
| tts-1                              | ¥30        | 1         | 23年11月 | 语音输出                        |
| tts-1-hd                           | ¥60        | 1         | 23年11月 | 语音输出                        |
| whisper-1                          | ¥60        | 1         | 23年06月 | 语音输入                        |
| gpt-4-all                          | ¥120       | 3         | 23年09月 | 逆向plus                        |
| gpt-4-gizmo-*                      | ¥60        | 3         | 23年09月 | 逆向plus                        |
| dall-e-3                           | ¥0.3/张    | -         | 23年09月 | 绘图模型                        |
| text-embedding-ada-002             | ¥2         | 1         | 22年12月 | 向量模型                        |
| text-embedding-3-large             | ¥2.6       | 1         | 24年01月 | 向量模型                        |
| text-embedding-3-small             | ¥0.4       | 1         | 24年01月 | 向量模型                        |
| gpt-4o-2024-05-13                  | ¥20        | 3         | 24年05月 |                                 |
| gpt-4o                             | ¥20        | 3         | 24年05月 | 常用推荐                        |
| claude-3-5-sonnet-20240620         | ¥60        | 5         | 24年06月 | 常用推荐，<mark>高价模型</mark> |
| midjourney-fast                    | ¥0.3/次    | -         | 23年12月 | 绘图模型                        |
| gpt-4o-mini                        | ¥1.2       | 4         | 24年07月 |                                 |
| gpt-4o-2024-08-06                  | ¥10        | 4         | 24年08月 |                                 |
| llama-3.1-8b                       | ¥6         | 1         | 24年08月 | 开源模型                        |
| llama-3.1-70b                      | ¥20        | 1         | 24年08月 | 开源模型                        |
| llama-3.1-405b                     | ¥30        | 1         | 24年08月 | 开源模型                        |
| flux-pro                           | ¥0.3/次    | -         | 24年08月 |                                 |
| chatgpt-4o-latest                  | ¥20        | 3         | 24年08月 |                                 |
| text-moderation-latest             | ¥1.2       | 1         | 24年08月 |                                 |
| o1-preview                         | ¥180       | 4         | 24年09月 | 最强模型，<mark>高价模型</mark> |
| o1-preview-2024-09-12              | ¥180       | 4         | 24年09月 | 最强模型，<mark>高价模型</mark> |
| o1-mini                            | ¥36        | 4         | 24年09月 | <mark>高价模型</mark>           |
| o1-mini-2024-09-12                 | ¥36        | 4         | 24年09月 | <mark>高价模型</mark>           |
| o1-preview-all                     | ¥0.4/次    | -         | 24年09月 | 逆向plus（下架）                |
| o1-mini-all                        | ¥0.2/次    | -         | 24年09月 | 逆向plus（下架）                |
| gpt-4o-realtime-preview            | ¥200(语音) | 4         | 24年10月 | 实时语音模型                    |
| gpt-4o-realtime-preview-2024-10-01 | ¥200(语音) | 4         | 24年10月 | 实时语音模型                    |
| claude-3-5-sonnet-20241022         | ¥60        | 5         | 24年10月 | 最强模型，<mark>高价模型</mark> |
| deepseek-chat                      | ¥2         | 2         | 24年10月 |                                 |
| DeepSeek-V2.5                      | ¥2.66      | 2         | 24年10月 | 开源模型                        |
| gemini-1.5-pro                     | ¥24        | 4         | 24年10月 |                                 |
| gemini-1.5-pro-002                 | ¥24        | 4         | 24年10月 |                                 |
| gemini-1.5-pro-latest              | ¥24        | 4         | 24年10月 |                                 |
| gemini-1.5-flash                   | ¥12        | 4         | 24年10月 |                                 |
| gemini-1.5-flash-002               | ¥12        | 4         | 24年10月 |                                 |
| gemini-1.5-flash-latest            | ¥12        | 4         | 24年10月 |                                 |
| moonshot-v1-128k                   | ¥90        | 1         | 24年10月 |                                 |
| moonshot-v1-32k                    | ¥36        | 1         | 24年10月 |                                 |
| moonshot-v1-8k                     | ¥18        | 1         | 24年10月 |                                 |
| qwen-max                           | ¥240       | 1         | 24年10月 | 最强模型                        |
| qwen-max-longcontext               | ¥240       | 1         | 24年10月 |                                 |
| qwen-plus                          | ¥20        | 1         | 24年10月 |                                 |
| qwen-turbo                         | ¥12        | 1         | 24年10月 |                                 |
| Qwen2.5-72B-Instruct-128K          | ¥8.26      | 1         | 24年10月 | 开源模型                        |
| Qwen2.5-72B-Instruct               | ¥8.26      | 1         | 24年10月 | 开源模型                        |
| Qwen2.5-Math-72B-Instruct          | ¥8.26      | 1         | 24年10月 | 开源模型                        |
| Qwen2.5-32B-Instruct               | ¥2.52      | 1         | 24年10月 | 开源模型                        |
| Qwen2.5-14B-Instruct               | ¥1.4       | 1         | 24年10月 | 开源模型                        |
| Qwen2.5-7B-Instruct                | ¥1.4       | 1         | 24年10月 | 开源模型                        |
| Qwen2.5-Coder-7B-Instruct          | ¥1.4       | 1         | 24年10月 | 开源模型                        |
| bge-m3                             | ¥0.14      | 1         | 24年10月 | 开源向量模型                    |
| bge-reranker-v2-m3                 | ¥0.14      | 1         | 24年10月 | 开源重排模型                    |
| gemini-1.5-flash-8b                | ¥3         | 4         | 24年10月 |                                 |
| glm-4-plus                         | ¥40        | 1         | 24年11月 |                                 |
| glm-4-0520                         | ¥80        | 1         | 24年11月 |                                 |
| glm-4-long                         | ¥0.8       | 1         | 24年11月 |                                 |
| glm-4-airx                         | ¥8         | 1         | 24年11月 |                                 |
| glm-4-flash                        | ¥0.14      | 1         | 24年11月 |                                 |
| glm-4v-plus                        | ¥80        | 1         | 24年11月 |                                 |
| glm-4v                             | ¥40        | 1         | 24年11月 |                                 |
| claude-3-5-haiku-20241022          | ¥20        | 5         | 24年11月 | <mark>高价模型</mark>           |
| Doubao-pro-128k                    | ¥16        | 1         | 24年11月 |                                 |
| Doubao-pro-32k                     | ¥2.4       | 1         | 24年11月 |                                 |
| Doubao-pro-4k                      | ¥2.4       | 1         | 24年11月 |                                 |
| Doubao-lite-128k                   | ¥2.4       | 1         | 24年11月 |                                 |
| Doubao-lite-32k                    | ¥1.2       | 1         | 24年11月 |                                 |
| Doubao-lite-4k                     | ¥1.2       | 1         | 24年11月 |                                 |
| grok-beta                          | ¥10        | 3         | 24年11月 |                                 |
| claude-3-5-sonnet-20240620-rev     | ¥12        | 5         | 24年11月 | 性价比高的逆向模型              |
| gemini-exp-1114                    | ¥12        | 4         | 24年11月 |                                 |
| grok-vision-beta                   | ¥20        | 4         | 24年11月 |                                 |
| gpt-4o-2024-11-20                  | ¥20        | 4         | 24年11月 | 创作力较gpt-4o有所提升          |
| gemini-exp-1121                    | ¥12        | 4         | 24年11月 |                                 |
| o1-preview-rev                     | ¥30        | 4         | 24年11月 | 性价比高的逆向/az模型           |
| o1-mini-rev                        | ¥6         | 4         | 24年11月 | 性价比高的逆向/az模型           |
| o1-all                             | ¥0.4/次    | -         | 24年12月 | 逆向官方plus，满血o1            |
| o1-pro-all                         | ¥0.6/次    | -         | 24年12月 | 逆向官方pro，满血pro版o1        |
| nova-micro-v1                      | ¥0.56      | 4         | 24年12月 | AWS新模型，小杯                 |
| nova-lite-v1                       | ¥0.96      | 4         | 24年12月 | AWS新模型，中杯，多模态         |
| nova-pro-v1                        | ¥12.8      | 4         | 24年12月 | AWS新模型，大杯，多模态         |
| gemini-exp-1206                    | ¥12        | 4         | 24年12月 |                                 |
| llama-3.3-70b                      | ¥20        | 3         | 24年12月 | 开源模型                        |


?>**1MT：**输入一百万tokens，以上计价以人民币2元1刀计算得出，若买10美金小额，在此价格基础上*1.75，输出按官方比例执行。输出/输入即输出费用与输入费用比率，如输入费用¥10，输出/输入=4，输出费用则为¥40。

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