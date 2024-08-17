# 延迟优化

?>本篇引用OpenAI官方文档。

本指南涵盖了一组核心原则，您可以应用这些原则来提高与大型语言模型（LLM）相关的各种用例的延迟表现。这些技术源自与广泛客户和开发人员协作的生产应用，因此无论您在构建什么——从细化工作流程到端到端的聊天机器人，它们都应该适用！

虽然有许多单独的技术，我们将它们归纳为**七个原则**，这些原则旨在代表改善延迟的高层次方法分类。

最后，我们将通过一个[示例](#example)来演示如何应用它们。

## 七个原则

1. [更快地处理 token](#1-更快地处理-token)
2. [生成更少的 token](#2-生成更少的-token)
3. [使用更少的输入 token](#3-使用更少的输入-token)
4. [减少请求次数](#4-减少请求次数)
5. [并行化处理](#5-并行化处理)
6. [减少用户等待时间](#6-减少用户等待时间)
7. [不要默认使用 LLM](#7-不要默认使用-llm)

### 1. 更快地处理 token

**推理速度**可能是解决延迟时首先想到的事情（但正如您将会看到的，这远不是唯一的）。这指的是 LLM 处理 token 的实际**速率**，通常以 TPM（每分钟 token 数）或 TPS（每秒 token 数）来衡量。

影响推理速度的主要因素是**模型大小**——较小的模型通常运行速度更快（也更便宜），而且在正确使用的情况下甚至可以胜过较大的模型。要在保持高质量表现的情况下使用较小的模型，您可以探讨：

- 使用较长的、更详细的[提示](#)。
- 添加（更多）[少量示例](#)。
- [微调](#) / distillation。

### 2. 生成更少的 token

生成 token 几乎总是使用 LLM 时最高延迟的步骤：作为一般经验法则，**减少 50% 的输出 token 可能会减少约 50% 的延迟**。减少输出大小的方法将取决于输出类型：

- 如果您在生成**自然语言**，只需**请求模型更简洁**（如“少于20个词”或“非常简短”）可能会有所帮助。您还可以使用少量示例和/或微调来教模型生成更简短的响应。
- 如果您在生成**结构化输出**，尽量**最小化您的输出语法**：缩短函数名，省略命名参数，合并参数等。
- 最后，虽然不常见，您也可以使用 `max_tokens` 或 `stop_tokens` 来提前结束您的生成。

请始终记住：减少一个输出 token 就是（毫）秒之获！

### 3. 使用更少的输入 token

减少输入 token 虽然确实会降低延迟，但这通常不是一个重要因素——**减少50%的提示可能只会带来1-5%的延迟改善**。除非您正在处理真正大规模的上下文（文档、图像），否则您可能希望将精力花在其他方面。

然而，如果您确实在处理大规模上下文（或者您决心榨取每一点性能且已耗尽所有其他选项），您可以使用以下技术减少输入 token：

- **微调模型**，以替代对冗长说明和示例的需求。
- **过滤上下文输入**，如修剪 RAG 结果、清理 HTML 等。
- **最大化共享的提示前缀**，通过将动态部分（例如 RAG 结果、历史记录等）放在提示的后面。这让您的请求更易于进行[KV 缓存](#)，并意味着每次请求处理的输入 token 更少。([为什么这样做？](#))

### 4. 减少请求次数

每次请求都会产生一些往返延迟——这会加起来。

如果您有需要 LLM 执行的连续步骤，而不是为每个步骤都发送一个请求，请考虑**将它们放在一个提示中，并在一个响应中获取它们所有**。您将避免额外的往返延迟，并可能减少处理多个响应的复杂性。

一种实现的方法是将您的步骤集合在一个枚举列表中，并请求模型以 JSON 形式返回结果。这样您可以轻松解析并引用每个结果！

### 5. 并行化处理

并行化在使用 LLM 执行多个步骤时非常有用。

如果步骤**不是严格顺序的**，您可以**将它们分成并行调用**。两件衬衫干燥所需的时间和一件一样长。

如果步骤**是严格顺序的**，您也可能仍然能够**利用推测性执行**。这在一个结论比其他结论更可能的分类步骤中特别有效（例如审核）。

1. 同时开始步骤1和步骤2（如输入审核和故事生成）
2. 验证步骤1的结果
3. 如果结果不是预期的，则取消步骤2（并在必要时重试）

如果您对步骤1的预测正确，那么您就相当于以零附加延迟来运行它！

### 6. 减少用户等待时间

**等待**和**观看进度发生**之间有很大差别——确保您的用户体验后者。以下是一些技术：

- **流式传输**：最有效的方法，因为它将**等待**时间缩短到一秒或以下。（如果在 ChatGPT 中直到每个响应完成后才看到任何输出，体验会相当不同。）
- **分块**：如果您的输出需要进一步处理才能显示给用户（审核、翻译），请考虑**分块处理**而不是一次性处理。通过流式传输到您的后端，然后将处理后的块发送到您的前端。
- **显示您的步骤**：如果您采取多个步骤或使用工具，将其展示给用户。您展示的实际进展越多越好。
- **加载状态**：旋转器和进度条效果显著。

请注意，虽然**显示您的步骤和拥有加载状态**主要产生心理效果，但**流式传输和分块**在考虑应用+用户系统后确实减少整体延迟：用户将更快完成阅读响应。

### 7. 不要默认使用 LLM

LLM 功能非常强大且多才多艺，因此有时在更适合更快的传统方法的情况下也会被使用。识别这些情况可能会显著降低您的延迟。考虑以下例子：

- **硬编码**：如果您的**输出**受到严格限制，您可能不需要 LLM 来生成它。动作确认、拒绝消息和标准输入请求都是合适的候选项，它们可以进行硬编码。（您甚至可以使用古老的方法，为每个变化提供多个版本。）
- **预计算**：如果您的**输入**受限（如类别选择），您可以预先生成多个响应，并确保您永远不会两次向用户展示相同的响应。
- **利用 UI**：有时，通过传统的定制 UI 组件而不是 LLM 生成的文本来传达汇总的指标、报告或搜索结果效果更好。
- **传统优化技术**：LLM 应用程序仍然是应用程序；二分查找、缓存、哈希映射和运行时复杂性在 LLM 世界中仍然有用。

## 示例

现在让我们来看一个示例应用程序，识别潜在的延迟优化，并提出一些解决方案！

我们将分析一个灵感来源于真实生产应用程序的虚构客户服务机器人的架构和提示。[架构和提示](#architecture-and-prompts)部分设置舞台，[分析和优化](#analysis-and-optimizations)部分将逐步讲解延迟优化过程。

## 架构和提示

以下是一个假想的**客户服务机器人**的**初始架构**。这就是我们要进行更改的地方。

![](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-0.png)

从高层次看，图表流程描述了以下过程：

1. 用户发送一条消息，作为正在进行的对话的一部分。
2. 最后一条消息被转换为自足的**查询**。
3. 我们确定是否需要进行**额外（检索）的信息**来响应该查询。
4. 进行**检索**，产生搜索结果。
5. 助手对用户查询和搜索结果进行**推理**，并**生成响应**。
6. 将响应回发给用户。

以下是图表每个部分使用的提示。虽然它们仍然是虚构和简化的，但它们以您在生产应用中找到的相同结构和措辞编写。

注意：您在看到 "<strong>[user input here]</strong>"这样的占位符时，代表动态部分，该部分会在运行时被实际数据替代。

### [查询情境化提示（点击查看）](#)

**描述：** 将用户查询重写为一个自足的搜索查询。

```plaintext
给定之前的对话，重写最后的用户查询，以便包含所有必要的上下文。

# Example
历史记录：[{user: "What is your return policy?"},{assistant: "..."}]
用户查询："How long does it cover?"
响应："How long does the return policy cover?"

# Conversation
[最后3条对话]

# 用户查询
[最后的用户查询]
```

### [检索检查提示（点击查看）](#)

**描述：** 确定一个查询是否需要进行检索以响应。

```plaintext
给定一个用户查询，确定是否需要进行实时查找以作出响应。

# Examples
用户查询："How can I return this item after 30 days?"
响应："true"

用户查询："Thank you!"
响应："false"
```

### [助手提示（点击查看）](#)

**描述：** 填写 JSON 字段，以通过定义的步骤集进行推理，生成给定用户对话和相关检索信息的最终响应。

```plaintext
您是一个有帮助的客户服务机器人。

使用结果 JSON 来推理每个用户查询——使用检索上下文。

# Example

用户："My computer screen is cracked! I want it fixed now!!!"

助手响应：
{
"message_is_conversation_continuation": "True",
"number_of_messages_in_conversation_so_far": "1",
"user_sentiment": "Aggravated",
"query_type": "Hardware Issue",
"response_tone": "Validating and solution-oriented",
"response_requirements": "Propose options for repair or replacement.",
"user_requesting_to_talk_to_human": "False",
"enough_information_in_context": "True"
"response": "..."
}
```

### 分析和优化

现在让我们分析提供的示例应用程序，并讨论如何优化其延迟！

#### 第1部分：查看检索提示

查看架构，首先映入眼帘的是**连续的 GPT-4 调用**——这些提示潜在着效率低下，通常可以面继由单个调用或并行调用来替代。

![](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-2.png)

在这种情况下，由于需要查询的上下文化查询，因此让我们将它们**合并到一个提示中**以[减少请求次数](#)。

![](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-3.png)

事实上，添加上下文和确定是否需要检索是非常直接且定义良好的任务，因此我们很可能使用**更小的、经过微调的模型**。切换到 GPT-3.5 将让我们[更快地处理 token](#)。

![](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-4.png)

#### 第2部分：分析助手提示

现在让我们将注意力转向助手提示。似乎有很多不同的步骤在填充 JSON 字段——这可能意味着有机会进行[并行化](#)。

![](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-5.png)

但是，假设我们已经运行了一些测试，发现将 JSON 中的推理步骤分开会产生更糟糕的响应，因此我们需要探索不同的解决方案。

**我们可以使用经过微调的 GPT-3.5 而不是 GPT-4 吗？** 可能可以——但是，总的来说，从助手中获得的开放式响应最好留给 GPT-4，因为它可以更好地处理更广泛的案例。也就是说，在观察推理步骤本身时，它们可能并不都需要 GPT-4 级别的推理来生成。这些有限的、定义良好的范围使它们成为**微调中的良好候选者**。

```json
{
  "message_is_conversation_continuation": "True", // <-
  "number_of_messages_in_conversation_so_far": "1", // <-
  "user_sentiment": "Aggravated", // <-
  "query_type": "Hardware Issue", // <-
  "response_tone": "Validating and solution-oriented", // <-
  "response_requirements": "Propose options for repair or replacement.", // <-
  "user_requesting_to_talk_to_human": "False", // <-
  "enough_information_in_context": "True" // <-
  "response": "..." // X -- benefits from GPT-4
}
```

这打开了进行权衡的可能性。我们是保持这个作为**完全由 GPT-4 生成的单个请求**，还是**将其分成两个顺序请求**并用 GPT-3.5 处理除最终响应之外的所有内容？我们面临着原则的冲突：第一个选项让我们[减少请求次数](#)，但第二个可能让我们[更快地处理 token](#)。

与许多优化权衡一样，答案将取决于细节。例如：

- JSON 中`response`字段相对于其他字段的 token 比例。
- 处理大部分字段更快所带来的平均延迟减小。
- 由于进行两个请求而不是一个的平均延迟增加。

结论将因情况而异，做出决定的最佳方法是通过生产示例进行测试。在这种情况下，让我们假装测试显示期望将提示拆分为两个以[更快地处理 token](#)。

![](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-6.png)

**注意：** 我们将在第二个提示中将`response`和`enough_information_in_context`组合在一起，以避免将检索上下文传递给两个新提示。

事实上，现在推理提示不依赖于检索的上下文，我们可以进行[并行化](#)并在与检索提示同时进行时触发它。

![](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-6b.png)

#### 第3部分：优化结构化输出

让我们再看一下推理提示。

![](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-7b.png)

仔细看看推理 JSON，您可能会注意到字段名称本身相当长。

```json
{
  "message_is_conversation_continuation": "True", // <-
  "number_of_messages_in_conversation_so_far": "1", // <-
  "user_sentiment": "Aggravated", // <-
  "query_type": "Hardware Issue", // <-
  "response_tone": "Validating and solution-oriented", // <-
  "response_requirements": "Propose options for repair or replacement.", // <-
  "user_requesting_to_talk_to_human": "False", // <-
}
```

通过缩短它们并将说明移到注释中，我们可以[生成更少的 token](#)。

```json
{
  "cont": "True", // whether last message is a continuation
  "n_msg": "1", // number of messages in the continued conversation
  "tone_in": "Aggravated", // sentiment of user query
  "type": "Hardware Issue", // type of the user query
  "tone_out": "Validating and solution-oriented", // desired tone for response
  "reqs": "Propose options for repair or replacement.", // response requirements
  "human": "False", // whether user is expressing want to talk to human
}
```

![](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-8b.png)

这个小改动删除了 19 个输出 token。在使用 GPT-3.5 的情况下，这可能只会带来几毫秒的改善，而在使用 GPT-4 的情况下，这可能会减去近一秒的延迟。

![](https://cdn.openai.com/API/docs/images/token-counts-latency-customer-service-large.png)

您可能想象，但是，这对于更大的模型输出来说具有非常显著的影响。

我们可以走得更远，使用单个字符作为 JSON 字段，或者将所有内容放入一个数组中，但这可能会开始影响我们的响应质量。知道答案的最佳方法，还是通过测试。

#### 示例回顾

让我们回顾一下我们为客户服务机器人示例所做的优化：

![](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-11b.png)

1. **合并**查询情境化和检索检查步骤以[减少请求次数](#)。
2. 对于新提示，**切换到更小的、经过微调的 GPT-3.5**以[更快地处理 token](#)。
3. 将助手提示分为两个，**对推理步骤切换到更小的、经过微调的 GPT-3.5**，以[更快地处理 token](#)。
4. **[并行化](#)**检索检查和推理步骤。
5. **缩短推理字段名称**并将注释移到提示中，以[生成更少的 token](#)。

## 结论

您现在应该熟悉可以用来改善 LLM 应用程序延迟的核心原则集。在探索这些技术时，请始终记得测量延迟来源，并测试每种解决方案的影响。现在去让您的应用程序**飞起来吧**！