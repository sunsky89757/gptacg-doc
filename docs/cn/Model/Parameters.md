# 参数

此处列出请求体支持的一些参数，如有需要可以添加。更详细的参数介绍参考[OpenAI官方文档](https://platform.openai.com/docs/api-reference)

## 请求体

```
frequency_penalty
```
number or null

默认值 0

在-2.0到2.0之间的数字。正值根据文本中已有频率惩罚新标记，从而减少模型逐字重复同一行的可能性。

```
logit_bias
```
boolean or null

默认值 false

修改指定标记在生成内容中出现的可能性。接受一个 JSON 对象，该对象将标记（通过词汇表中的标记 ID 指定）映射到-100 到 100 的相关偏差值。从数学上讲，偏差是添加到模型生成的 logits 中然后再进行采样。具体效果因模型而异，但 -1 到 1 之间的数值会减少或增加选择的可能性；像 -100 或 100 这样的数值应该会导致相关标记被禁止或独占选择。

```
logprobs
```
boolean or null

默认值 false

是否返回输出标记的对数概率。如为真，则在消息内容中返回每个输出标记的对数概率。

```
top_logprobs
```
integer or null

一个介于0到20之间的整数，指定在每个标记位置返回最可能的标记数量，每个都带有相关的对数概率。如果使用此参数，则必须将logprobs设置为true。

```
max_tokens
```
integer or null

聊天完成中可以生成的最大令牌数。输入令牌和生成令牌的总长度受模型上下文长度限制。

```
n
```
integer or null

默认值 1

对于每条输入消息要生成多少聊天完成选项。请注意，您的费用将基于所有选项中生成的标记数量收取。保持 n 为 1 以尽量减少成本。

```
presence_penalty
```
number or null

默认值 0

介于-2.0到2.0之间的数字。正值会根据新词在文本中出现的情况进行惩罚，从而增加模型谈论新话题的可能性。

```
response_format
```
object

一个指定模型输出格式的对象。与GPT-4o、GPT-4o mini、GPT-4 Turbo以及所有gpt-3.5-turbo-1106以后的GPT-3.5 Turbo型号兼容。设置为 { "type": "json_schema", "json_schema": {...} } 可启用结构化输出，确保模型将符合您提供的JSON schema。设置为 { "type": "json_object" } 可启用JSON模式，确保模型生成的消息是有效的JSON。

**重要提示：**在使用JSON模式时，您还必须通过系统或用户消息指示模型生成JSON。如果没有这样做，模型可能会不断产生空白字符直到达到token限制，从而导致请求长时间运行且看似“卡住”。另外注意，如果finish_reason="length"，表示生成超过了max_tokens或者对话超过了最大上下文长度，那么消息内容可能会部分被截断。

```
stop
```
string / array / null

默认值 null

最多4个序列，API将停止生成更多的标记。

```
stream
```
boolean or null

默认值 false

如果设置，将发送部分消息增量，就像在ChatGPT中一样。令牌将在变得可用时作为仅数据的服务器发送事件发送，流将以data: [DONE] 消息终止。

```
temperature
```
number or null

默认值 1

我们建议的采样温度在 0 和 2 之间。较高的值（如 0.8）会使输出更随机，而较低的值（如 0.2）则使其更集中和确定。  

通常，我们建议修改此参数或 top_p，但不同时修改两者。

```
top_p
```
number or null

默认值 1

另一种替代采样温度的方法称为核采样，其中模型只考虑具有top_p概率质量的标记。因此，0.1意味着仅考虑包含前10%概率质量的标记。

我们通常建议更改此参数或温度，但不要同时更改。

```
tool_choice
```
string or object

控制模型调用的工具（如果有）。none 表示模型不会调用任何工具，而是生成一条消息。auto 表示模型可以选择生成一条消息或调用一个或多个工具。required 表示模型必须调用一个或多个工具。通过 {"type": "function", "function": {"name": "my_function"}} 指定特定的工具会强制模型调用该工具。
当没有工具时，默认值为 none。当有工具时，默认值为 auto。

## 返回格式

```
id
```
string

聊天完成的唯一标识符。

```
choices
```
array

聊天完成选项列表。如果 n 大于 1，可以有多个。

```
created
```
integer

创建聊天完成的 Unix 时间戳（以秒为单位）。

```
model
```
string

用于聊天完成的模型。

```
service_tier
```
string or null

用于处理请求的服务等级。只有在请求中指定了service_tier参数时，才会包含此字段。

```
system_fingerprint
```
string

此指纹代表模型运行的后端配置。

可与种子请求参数结合使用，以了解可能影响确定性的后端更改何时发生。

```
object
```
string

对象类型，总是 chat.completion。

```
usage
```
object

完成请求的使用统计。