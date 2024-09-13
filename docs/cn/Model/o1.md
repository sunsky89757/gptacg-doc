# o1-preview 和 o1-mini

>o1大型语言模型系列经过强化学习训练，以执行复杂推理。o1模型在回答之前会进行思考，在回应用户之前生成一条较长的内部思维链。

```python
from openai import OpenAI


client = OpenAI(
    # This is the default and can be omitted
    base_url="https://api.juheai.top/v1",
    api_key="sk-xxx",
)

response = client.chat.completions.create(
    model="o1-mini",
    messages=[
        {
            "role": "user", 
            "content": "Write a bash script that takes a matrix represented as a string with format '[1,2],[3,4],[5,6]' and prints the transpose in the same format."
        }
    ]
)

print(response.choices[0].message.content)
```

?>如果您需要获取各个技术栈的调用示例代码，请[查阅此处>>](https://juheai.apifox.cn/)