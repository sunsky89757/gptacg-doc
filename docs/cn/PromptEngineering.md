# 提示词工程

>本指南分享了在大型语言模型中获取更好结果的策略和战术。这里描述的方法有时可以结合使用以取得更好的效果。我们鼓励大家进行实验，找出最适合自己的方法。

## 六种获得更好结果的策略

### 1. 写清晰的指令

这些模型无法读懂你的想法。如果输出内容太长，请要求简洁的回复。如果输出内容过于简单，请要求专家级的写作。如果是你不喜欢格式，演示一下你希望看到的格式。模型猜测的内容越少，你就越有可能得到你想要的东西。

策略:

- 在提问中包含详细信息，以获得更相关的答案
- 要求模型扮演某个角色
- 使用分隔符清晰的区分输入的指定部分
- 指定完成任务所需的步骤
- 提供示例
- 指定输出的期望长度

### 2. 提供参考文本

语言模型可以自信地编造虚假答案，尤其是在被问及深奥话题或要求提供出处时。就像一本笔记可以帮助学生在考试中取得更好成绩一样，向这些模型提供参考文本可以帮助它们减少编造答案。

策略：

- 指示模型使用参考文本进行回答
- 指示模型在回答时引用参考文本

### 3. 将复杂的任务分解为更简单的子任务

正如在软件工程中将一个复杂系统分解为一组模块化组件是一个很好的实践方法，对于提交给语言模型的任务也是如此。复杂的任务往往比简单的任务有更高的错误率。此外，复杂的任务通常可以重新定义为更简单任务的工作流，其中早期任务的输出用于构建后续任务的输入。

策略:

- 使用意图分类来识别与用户查询最相关的指令
- 对于需要非常长对话的对话应用程序,总结或过滤先前的对话
- 分段总结长文档,并递归地构建完整摘要

### 4. 给模型时间"思考"

如果有人让你算一下17x28等于多少，你可能不能马上得出答案，但如果给你时间，你仍然可以算出来。类似地，与花时间推理出答案相比，模型在试图立即回答时更容易出现推理错误。在给出答案之前，要求提供"解题思路"可以帮助模型更可靠地推理出正确答案。

策略:

- 指示模型在匆忙得出结论之前,自己先推导出解题思路
- 使用内心独白或一系列问题来隐藏模型的推理过程
- 询问模型在之前的尝试中是否遗漏了什么

### 5. 结合外部工具

通过将其他工具的输出输入模型，以弥补模型的缺陷。例如，文本检索系统（有时称为RAG或检索增强生成）可以告诉模型相关文档。像OpenAI的代码解释器这样的代码执行引擎可以帮助模型进行数学运算和运行代码。如果一项任务可以通过工具更可靠或更高效地完成，而不是通过语言模型完成，那么将其分配给工具，以结合两者的优势。

策略：

- 使用基于嵌入的搜索来实施高效的知识检索
- 使用代码执行来执行更准确的计算或调用外部API
- 给予模型访问特定功能的权限

### 6. 系统性地测试变更

如果能够量化性能，就能更轻松地改进性能。有时，对提示的修改可能在少数个别例子中表现更好，但在更广泛的例子集中却会整体表现变差。所以，为了确保变更能整体提升性能，可能需要定义一个全面的测试套件（即“评估”）。

策略：

- 通过对比参考标准答案来评估模型输出

?>每个以上列出的策略都可以通过具体的战术来实现。这些战术旨在提供一些尝试的想法。它们绝不全面详尽，您可以自由尝试这里未提及的创意。

## 六种策略的具体示范

### 1. 写清晰的指令

**在提问中包含详细信息，以获得更相关的答案**

为了确保得到精准的回复，请提供所有重要的细节或上下文信息。否则，模型可能会误解您的意思。

| 不推荐                   | 推荐                                                                                                                   |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------- |
| 如何在 Excel 中添加数字  | 如何在 Excel 中汇总一行美元金额？我想自动对整张工作表中的所有行进行汇总，并将所有总数放在名为“Total”的列的右侧。       |
| 总统是谁                 | 2021年墨西哥总统是谁，选举多久举行一次？                                                                               |
| 编写代码计算斐波那契数列 | 编写一个TypeScript函数高效计算斐波那契数列。详细注释代码，解释每个部分的作用以及为何这样编写。                         |
| 总结会议记录             | 用一个段落总结会议记录。然后写一个包括发言人及其要点的markdown列表。最后，列出发言人建议的下一步或行动项目（如果有）。 |

**要求模型扮演某个角色**

在请求体中，"role": "system" 部分的content可以定义角色信息。如下所示

```python
"messages": [
      {
         "role": "system",
         "content": "You are a helpful assistant.（此处的内容可以修改为自定义角色的描述）"  
      },
      {
         "role": "user",
         "content": "你好（此处为你提问的问题）"
      }
   ]
```

>**system：**<br>当我请你帮忙写东西时，你会回复一份文档，每段至少包含一个笑话或俏皮话。<br>
>**user：**<br>请向我的钢螺栓供应商写一封感谢信，感谢他们在这么短的时间内按时送货。这让我们顺利完成了一个重要订单的交付。

**使用分隔符清晰的区分输入的指定部分**

分隔符如三重引号、XML标签、章节标题等可以帮助划分需要区别对待的文本部分。

>**user：**<br>请将三引号中的文本总结为一首俳句。<br>"""文本在此处插入"""

>```
>system：
>你将得到一对关于同一话题的文章（用XML标签分隔）。首先总结每篇文章的论点。然后指出哪篇文章的论点更好，并解释原因。
>user：
><article>在此处插入第一篇文章</article>
><article>在此处插入第二篇文章</article>
>```

>**system：**<br>你将收到一份论文摘要和一个建议的标题。论文标题应该清晰地反映论文主题，并且具有吸引力。如果标题不符合这些标准，请提供5个备用标题。<br>
>**user：**<br>摘要：xxx<br>标题：xxx

对于这种简单的任务，使用分隔符可能并不会影响输出质量。然而，任务越复杂，区分任务细节就越重要。请明确表达你的要求，不要让模型费力去猜测你的意图。

**指定完成任务所需的步骤**

某些任务最好分解为一系列步骤。明确列出这些步骤可以让模型更容易遵循。

>**system：**
>
>请按照以下步骤处理用户输入。
>
>- 步骤1 - 用户会在三引号中提供文字。将这段文字总结成一句话，前缀为“Summary: ”。
>- 步骤2 - 将步骤1中的总结翻译成西班牙语，前缀为“Translation: ”
>
>**user：**
>
>"""插入的文本"""

**提供示例**

提供适用于所有情况的一般指示通常比通过示例演示任务的各种形式更有效，但在某些情况下，提供示例可能会更容易。例如，如果您希望模型模仿某种特定的回应用户查询的风格，而这种风格难以清晰描述。这种方法被称为“少样本”提示。

>**system：**<br>以举例中一致的风格作答。例如：教我关于耐心的知识。你的回答：耐心是磨盘，越久越香。<br>
>**user：**<br>教我关于耐心的知识。<br>

**指定输出的期望长度**

可以要求模型生成具有特定长度的输出。这种长度可以用单词、句子、段落或要点的数量来表示。不过，请注意，让模型生成特定数量的单词时，精确度可能不高。相对而言，模型在生成特定数量的段落或要点时会更加准确。

>**user：**<br>总结由三引号分隔的文本，字数约为50字。<br>"""插入的文本"""

>**user：**<br>用两段话总结由三引号分隔的文本。<br>"""插入的文本"""

>**user：**<br>用三点总结以下用三引号括起来的文本。<br>"""插入的文本"""

### 2. 提供参考文本

**指示模型使用参考文本进行回答**

如果我们能为模型提供与当前查询相关的可信信息，那么我们可以指导模型利用这些信息来生成答案。鉴于所有模型都有有限的上下文窗口，我们需要一种方法来动态查找与所提问题相关的信息。可以使用Embbeding嵌入来实现高效的知识检索。

>**system：**
>
>使用由三引号分隔提供的文章来回答问题。如果在文章中找不到答案，请写 “我找不到答案。”
>
>**user：**<br><插入文章，每篇文章都用三个引号分隔>
>问题：<插入问题>


**指示模型在回答时引用参考文本**

如果输入已经补充了相关知识，可以直接请求模型在答案中添加引文，并引用提供的文档段落。需要注意的是，输出中的引文可以通过在提供的文档中进行字符串匹配来进行程序化验证。

>**system：**
>
>你将获得一个由三重引号分隔的文件和一个问题。您的任务是仅使用提供的文件来回答问题，并引用用于回答问题的文档段落。如果文档不包含回答此问题所需的信息，则只需写：“信息不足。” 如果提供了问题的答案，则必须用引用注释。使用以下格式引用相关段落（{"引用": …}）。
>
>**user：**<br>"""请在此处插入文档"""
>
>问题：<插入问题>

### 3. 将复杂的任务分解为更简单的子任务

**使用意图分类来识别与用户查询最相关的指令**

对于需要处理不同情况的多个独立指令集的任务，一种有效的方法是首先对查询类型进行分类，并根据分类来确定所需的指令。这可以通过定义固定类别，并为每个类别预设处理指令来实现。这一过程还可以递归进行，将一个复杂的任务分解为多个阶段。采用这种方法的优点在于，每个查询只需要包含完成当前阶段所需的指令，这比用一个查询完成整个任务更能降低错误率。此外，这种方法还可以降低成本，因为较大的提示信息运行费用更高（详情参见定价信息）。

举例来说，对于一个客户服务应用程序，可以将查询分类如下：

>**system**
>
>您将收到客户服务查询。请将每个查询分类为一级类别和二级类别。请以json格式提供您的输出，其中包含以下键：一级类别和二级类别。
>
>一级类别 - 账单问题、技术支持、账户管理或一般咨询。
>
>二级类别 - 账单问题：
>- 退订或升级
>- 添加付款方式
>- 收费解释
>- 费用争议
>
>二级类别 - 技术支持：
>- 故障排除
>- 设备兼容性
>- 软件更新
>
>二级类别 - 账户管理：
>- 重置密码
>- 更新个人信息
>- 关闭账户
>- 账户安全
>
>二级类别 - 一般咨询：
>- 产品信息
>- 价格
>- 反馈
>- 与人工客服对话
>
>**user**
>
>我需要让我的网络再次工作。

基于客户查询的分类，可以向模型提供一组更具体的指令，以便其处理下一步。例如，假设客户需要帮助解决 "故障排除"。

>**system**
>
>您将收到需要在技术支持背景下进行故障排除的客户服务查询。帮助用户如下:
>
>- 请他们检查路由器的所有电缆是否已连接。注意电缆随着时间推移可能会松动。
>- 如果所有电缆都已连接但问题依然存在，请询问他们使用的是哪种路由器型号。
>- 现在教他们如何重启设备：
>  -- 如果型号是MTD-327J，建议他们按住红色按钮5秒钟，然后等待5分钟再测试连接。
>  -- 如果型号是MTD-327S，建议他们拔掉并重新插入电源，然后等待5分钟再测试连接。
>- 如果重启设备并等待5分钟后问题仍存在，通过输出{"请求IT支持"}将他们连接到IT支持。
>- 如果用户开始提出与此主题无关的问题，请确认他们是否希望结束当前的故障排除聊天，并根据以下方案分类他们的请求：
>
><在此插入上述的主要/次要分类方案>
>
>**user**
>我需要让我的网络重新连接。

请注意，该模型已被指示在对话状态变化时发出特定的字符串。这使我们能够将系统转变为一个状态机，其中不同的状态决定要插入的指令。通过跟踪状态、该状态下相关的指令以及可选的状态转换，我们可以为用户体验设定防护措施，而这在不太结构化的方法中是难以实现的。

**对于需要非常长对话的对话应用程序,总结或过滤先前的对话**

由于模型具有固定的上下文长度，用户和助手之间的对话（整个对话包含在上下文窗口中）无法无限期持续。

对此问题有多种解决方法，其中一种是总结对话中的先前轮次。当输入的大小达到预定的阈值长度时，可以触发一个查询，总结部分对话内容，并将之前对话的摘要作为系统消息的一部分。或者，可以在整个对话过程中在后台异步总结先前的对话。

另一种解决方案是动态选择对话中与当前查询最相关的部分。

**分段总结长文档,并递归地构建完整摘要**

由于模型的上下文长度是固定的，因此它们无法在一次查询中总结出长度超出上下文长度减去生成摘要长度的文本。

要总结像书这样非常长的文档，可以通过多次查询来依次总结文档的各个部分。然后，将这些部分的摘要连接起来，再次进行总结，如此反复，直到对整本书的内容完成总结。如果在理解后续内容时需要参考前面的信息，可以在总结新的内容时，将之前的内容摘要一起包含进来。OpenAI 之前的研究表明，使用GPT-3的变体进行这样的总结过程是有效的。

### 4. 给模型时间"思考"

**指示模型在匆忙得出结论之前,自己先推导出解题思路**

有时，当我们明确要求模型先进行基于基本原理的推理，再得出结论时，会获得更好的效果。比如说，我们希望模型评估学生解答数学题的正确性。最直接的方法就是询问模型学生的解答是否正确。

>**system**
>
>判断学生的解决方案是否正确。
>
>**user**
>
>问题陈述：我正在建设一个太阳能发电设施，需要帮助计算财务状况。
>- 土地成本为每平方英尺100美元
>- 我能以每平方英尺250美元的价格购买太阳能电池板
>- 我谈判了一份维护合同，每年将花费固定的10万美元，外加每平方英尺10美元
>第一年运营的总成本是平方英尺数的函数。
>
>学生的解决方案：设x为安装的面积（平方英尺）。
>1. 土地成本：100x
>2. 太阳能电池板成本：250x
>3. 维护成本：100,000 + 10x
>总成本：100x + 250x + 100,000 + 10x = 360x + 100,000
>
>**assistant**
>
>学生的解决方案是正确的。

但是学生的解决方案实际上是不正确的！我们可以通过提示模型首先生成自己的解决方案来让模型成功地注意到这一点。

>**system**
>
>首先解决你自己的问题。然后将你的解决方案与学生的解决方案进行比较，评估学生的解决方案是否正确。在自己解决问题之前，不要决定学生的解决方案是否正确。
>
>**user**
>
>问题陈述：我正在建设一个太阳能发电设施，需要帮助计算财务状况。
>- 土地成本为每平方英尺100美元
>- 我能以每平方英尺250美元的价格购买太阳能电池板
>- 我谈判了一份维护合同，每年将花费固定的10万美元，外加每平方英尺10美元
>第一年运营的总成本是多少？请用平方英尺数表示。
>
>学生的解决方案：设x为安装的面积（平方英尺）。
>1. 土地成本：100x
>2. 太阳能电池板成本：250x
>3. 维护成本：100,000 + 100x
>总成本：100x + 250x + 100,000 + 100x = 450x + 100,000
>
>**assistant**
>
>设x为安装的面积（平方英尺）。
>1. 土地成本：100x
>2. 太阳能电池板成本：250x
>3. 维护成本：100,000 + 10x
>总成本：100x + 250x + 100,000 + 10x = 360x + 100,000
>
>学生的解答是不正确的。他们在维护成本计算上犯了错误，用了100x而不是10x。第一年的正确总成本是360x + 100,000。

**使用内心独白或一系列问题来隐藏模型的推理过程**

前述策略表明，在回答具体问题之前，有时模型详细推理问题是很重要的。对于某些应用程序，模型用来得出最终答案的推理过程不适合与用户分享。例如，在辅导应用中，我们可能希望鼓励学生自己解决问题，但模型对学生解决方案的推理过程可能会向学生透露答案。

内心独白是一种可以用来缓解这种情况的策略。内心独白的想法是指示模型将输出中那些应隐藏的部分放入一种易于解析的结构化格式中。然后在将输出呈现给用户之前，对输出进行解析，并只显示输出的一部分。

>**system**
>
>按照以下步骤回答用户的查询：
>
>1. 首先，自己解决问题。不要依赖学生的解决方案，因为它可能是错误的。将此步骤中的所有工作用三重引号（"""）括起来。
>2. 将你的解决方案与学生的解决方案进行比较，并评估学生的解决方案是否正确。将此步骤中的所有工作用三重引号（"""）括起来。
>3. 如果学生犯了错误，找出在不直接给出答案的情况下可以给学生的提示。将此步骤中的所有工作用三重引号（"""）括起来。
>4. 如果学生犯了错误，向学生提出上一步中的提示（不用三重引号括起来）。不要使用“第四步 - ...”，而是写“提示：”。
>
>**user**
>
>问题陈述：<插入问题陈述>
>
>学生解决方案：<插入学生解决方案>

或者，这可以通过一系列查询来实现，其中的所有查询结果（除了最后一个）都对最终用户隐藏。

首先，我们可以让模型独立解决问题。由于这个初始查询不需要提供学生的解决方案，因此可以忽略。这样做的一个额外好处是，模型的解决方案不会受到学生尝试解决方案的影响。

>**user**
>
><插入问题陈述>

接下来，我们可以让模型使用所有可用的信息来评估学生解答的正确性。

>**system**
>
>将你的解决方案与学生的解决方案进行比较，并评估学生的解决方案是否正确。
>
>**user**
>
>问题描述："""<插入问题描述>"""
>
>你的解决方案："""<插入模型生成的解决方案>"""
>
>学生的解决方案："""<插入学生的解决方案>"""

最后，我们可以让模型使用其自己的分析，以一个乐于助人的导师的身份构建回复。

>**system**
>
>你是一名数学导师。如果学生出错，请提供一个不直接揭示答案的提示。如果学生没有出错，只需给他们一个鼓励的评论。
>
>**user**
>
>问题陈述："""<插入问题陈述>"""
>
>您的解答："""<插入模型生成的解答>"""
>
>学生的解答："""<插入学生的解答>"""
>
>分析："""<插入从前一步生成的模型分析>"""

**询问模型在之前的尝试中是否遗漏了什么**

假设我们使用一个模型来列出与特定问题相关的来源摘录。每列出一个摘录后，模型需要决定是继续列出下一个摘录还是停止。如果来源文件很大，模型通常会过早停止，导致漏掉一些相关摘录。在这种情况下，通过向模型提出后续查询，找出之前漏掉的摘录，通常可以获得更好的效果。

> **system**
>
> 我将向你提供一份用三重引号分隔的文件。你的任务是选择与以下问题相关的摘录：“人工智能历史上有哪些重大的范式转变。”
>
> 确保选取的摘录包含所有解释所需的上下文——换句话说，不要遗漏提取相关内容。提供的输出应采用如下的JSON格式：
>
> ```json
> [{"excerpt": "..."},
> ...
> {"excerpt": "..."}]
> ```
> **user**
>
> """<插入文档内容>"""
> **assistant**
>
> ```json
> [{"excerpt": "模型在这里撰写摘录"},
> ...
> {"excerpt": "模型在这里撰写另一段摘录"}]
> ```
> **用户**
>
> 还有更多相关的摘录吗？请注意不要重复摘录。此外，确保选取的摘录包含所有解释所需的上下文——换句话说，不要遗漏提取相关内容。

### 5. 结合外部工具

**使用基于嵌入的搜索来实施高效的知识检索**

模型可以利用外部信息源作为输入的一部分，从而生成更有见识和最新的回答。例如，如果用户问一个关于特定电影的问题，我们可以在模型的输入中添加电影的高质量信息（如演员、导演等）。通过使用嵌入技术，我们能够高效地进行知识检索，使相关信息在运行时动态添加到模型输入中。

文本嵌入是一个向量，它可以衡量文本字符串之间的关联性。相似或相关的字符串会比不相关的字符串更接近。借助快速的向量搜索算法，嵌入技术可以实现高效的知识检索。具体来说，可以将文本语料库切分成若干小块，对每一块进行嵌入并独立存储。然后，对给定的查询进行嵌入，并执行向量搜索，找到与查询最相关的嵌入文本块（即在嵌入空间中最接近的）。

**使用代码执行来执行更准确的计算或调用外部API**

语言模型本身无法准确执行算术运算或长时间计算。在需要这种功能的时候，可以指示模型编写代码并运行，以代替模型自行计算。具体来说，可以要求模型将需要运行的代码放入指定的格式中，比如用三重反引号括起来。生成输出后，可以提取并运行这些代码。最后，如有必要，可以将代码执行引擎（如Python解释器）的输出结果作为模型下一个查询的输入。

>**system**
>
>你可以通过将 Python 代码放在三个反引号之间来编写和执行，例如 ` ```代码写在这里``` `。使用此方法进行计算。
>
>**user**
>
>求以下多项式的所有实数根：`3*x**5 - 5*x**4 - 3*x**3 - 7*x - 10`。

另一个代码执行的好例子是调用外部API。如果一个模型被正确引导使用某个API，它可以编写利用该API的代码。您可以通过提供文档或代码示例来教会模型如何使用该API。

>**system**
>
>您可以通过将 Python 代码放在三重反引号中来编写和执行代码。另外请注意，您可以使用以下模块来帮助用户向朋友发送消息：
>
>```python
>import message
>message.write(to="John", message="嘿，下班后见个面怎么样？")
>```

!>**警告：**运行模型生成的代码本质上不安全，在任何尝试这样操作的应用中都应该采取预防措施。尤其是，需要一个沙盒环境来执行代码，从而限制不受信任代码可能带来的危害。

**给予模型访问特定功能的权限**

Chat Completions API允许在请求中传递函数描述列表，这使得模型能够根据提供的模式生成函数参数。生成的函数参数以JSON格式由API返回，并可用于执行函数调用。函数调用的结果可以在后续请求中反馈给模型，从而实现闭环。这是使用OpenAI模型调用外部函数的推荐方法。

### 6. 系统性地测试变更

有时候，我们难以判断一个变化——例如，新指令或新设计——是否使系统变得更好或更糟。查看一些示例可能会暗示哪种更好，但由于样本量小，很难区分是真正的改进还是随机运气。可能这种变化在某些输入情况下提高了性能，但在其他输入情况下却降低了性能。

评估程序（或“评测”）对于优化系统设计非常有用。好的评测应该具备以下特点：

1. 代表现实世界的使用场景（或至少是多样化的）
2. 包含大量测试案例以提高统计效力（见下表的指南）
3. 易于自动化或重复

| 检测差异 | 必要样本量（95% 置信度） |
| :-------: | :----------------------: |
|    30%    |          大约 10          |
|    10%    |         大约 100          |
|    3%     |         大约 1,000        |
|    1%     |         大约 10,000       |

输出评测可以由计算机、人类或两者结合完成。计算机可以通过客观标准（例如，单一正确答案的问题）以及一些主观或模糊标准来自动化评测，其中模型输出由其他模型查询进行评估。OpenAI Evals 是一个开源软件框架，提供了创建自动化评测工具。

当存在多种可能输出且其质量被认为同样高的情况下（例如，对于需要长答案的问题），基于模型的评测可能会很有用。能够通过模型评测的边界与需要人为评估的边界是模糊的，并且随着模型变得更强大而不断变化。我们鼓励进行实验，以了解基于模型的评测在您的应用场景中的效果。

**通过对比参考标准答案来评估模型输出**

假设已知问题的正确答案应该参考一组已知的事实集。那么我们可以使用模型查询来计算答案中包含了多少必需的事实。例如，使用以下系统消息：

>**system**
>
>您将获得问题的答案。检查答案中是否直接包含以下信息：
>- 尼尔·阿姆斯特朗是第一个登上月球的人。
>- 尼尔·阿姆斯特朗第一次登上月球的日期是1969年7月21日。
>
>对于这些要点中的每一点，请执行以下步骤：
>
>1. 重述这个要点。
>2. 提供答案中最接近这一要点的引用。
>3. 考虑一下，如果一个不熟悉该主题的人阅读这个引用，能否直接推断出这个要点。先解释为什么，然后再做出决定。
>4. 如果第3步的答案是肯定的，则写“是”，否则写“否”。
>
>最后，统计一下“是”的答案有多少个。将此统计结果以`{"count": <插入统计数>}`的形式提供。

以下是一个满足两个要点的示例输入：

>**system**
>
><插入上述系统消息>
>
>**user**
>
>尼尔·阿姆斯特朗因成为第一个踏上月球的人而闻名。这一历史性事件发生在1969年7月21日，阿波罗11号任务期间。

以下是一个仅满足一个要点的示例输入：

>**system**
>
><插入上述系统消息>
>
>**user**
>
>尼尔·阿姆斯特朗在人类历史上首次登上月球时创造了历史。

以下是一个不满足任何要点的示例输入：

>**system**
>
><插入上述系统消息>
>
>**user**
>
>在69年的夏天，一次伟大的航行，
阿波罗11号，像传说中的勇者之手。
阿姆斯特朗迈出了一步，历史展开，
"一小步"，他说，为一个新世界。

这种基于模型的评估有多种可能的变体。请考虑以下跟踪候选答案与黄金标准答案之间重叠类型的变体，同时还跟踪候选答案是否与黄金标准答案的任何部分相矛盾。

>**system**
>
>使用以下步骤回复用户输入。完全重述每一步后再继续。即“第1步：逐步推理...”
>
>1. 逐步推理提交的答案与专家答案中的信息是不相干、相同、子集、超集，还是重叠（即有交集但不是子集/超集）。
>2. 逐步推理提交的答案是否与专家答案的任何方面相矛盾。
>3. 输出一个结构类似于{"type_of_overlap": "disjoint" or "equal" or "subset" or "superset" or "overlapping", "contradiction": true or false}的JSON对象。

以下是不合格答案的一个示例输入，但答案并未与专家答案相矛盾：

>**system**
>
><插入上述系统消息>
>
>**user**
>
>问题: 尼尔·阿姆斯特朗最出名的事件是什么？该事件发生的日期是？假设时间是UTC时间。
>
>提交答案: 难道他不是登上月球了吗？
>
>专家答案: 尼尔·阿姆斯特朗因成为第一个登上月球的人而闻名。这一历史性事件发生在1969年7月21日。

以下是与专家答案直接矛盾的一个示例输入：

>**system**
>
><插入上述系统消息>
>
>**user**
>
>问题: 尼尔·阿姆斯特朗最出名的事件是什么？该事件发生的日期是？假设时间是UTC时间。
>
>提交答案: 1969年7月21日，尼尔·阿姆斯特朗成为继巴兹·奥尔德林之后第二个登上月球的人。
>
>专家答案: 尼尔·阿姆斯特朗因成为第一个登上月球的人而闻名。这一历史性事件发生在1969年7月21日。