# 购买使用

以下是正文内容,我在这里随便加点内容

## 二级标题

正文内容，我在这里又加了内容

### 三级标题

正文内容，这里又有了

## 二级标题

正文内容

### 三级标题

正文内容

这是什么内容

| 姓名       | 年龄 | 工作         |
| :--------- | :--- | :----------- |
| 小可爱     | 18   | 吃可爱多     |
| 小小勇敢   | 20   | 爬棵勇敢树   |
| 小小小机智 | 22   | 看一本机智书 |

# 你好

我在这里编辑内容

| 第一列       | 第二列 | 第三列 | 第四列 | 第五列 |
| ------------ | ------ | ------ | ------ | ------ |
| 这是主要内容 | 1      | 2      | 3      | 4      |
| 收到         | 端点   | 但是   | 温恩   | 方法   |

![123](https://res.u-tools.cn/website5/static/assets/plugin/plugin-1.png)


这是缩放后的效果

    <html>
      <head>
      </head>
    </html>

<!-- tabs:start -->

#### **免费版**

Hello!

您可以在这里使用免费的NextChat

访问链接：https://chat.gptacg.com

#### **通用API**

Bonjour!

#### **速刷API**

Ciao!

<!-- tabs:end -->


```python

from pathlib import Path
from openai import OpenAI

# 初始化 OpenAI 客户端
client = OpenAI(
    base_url="https://api.juheai.top/v1",
    api_key="sk-QwPdMcvX2WCshRgQC98d221180Cc4dBa987b37A145Eb9a05",
)

# 定义语音合成输入文本
input_text = "Hello world! This is a streaming test."

# 创建语音合成请求
response = client.audio.speech.create(
    model="tts-1",
    voice="alloy",
    input=input_text,
)

# 输出文件路径
output_path = Path(__file__).parent / "output.mp3"

# 尝试使用 content 属性读取所有二进制数据并写入文件
try:
    with open(output_path, "wb") as f:
        f.write(response.content)
    print(f"语音合成完成，已保存到 {output_path}")
except AttributeError:
    print("属性 'content' 不存在，尝试使用 'read' 方法。")


```
