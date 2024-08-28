# 内容审查

>防止用户采用违禁词从而违反OpenAI使用规范，给定一些输入文本，输出模型是否将其分类为可能有敏感词的几个类别。

```python

from openai import OpenAI
client = OpenAI(
    # This is the default and can be omitted
    base_url="https://api.juheai.top/v1",
    api_key="sk-xxx",
)

moderation = client.moderations.create(input="I want to kill them.")
print(moderation)

```

```curl

curl https://api.juheai.top/v1/moderations \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer sk-xxx" \
  -d '{
    "input": "I want to kill them."
  }'


```