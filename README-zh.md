# DeepSeek-R1
<!-- markdownlint-disable first-line-h1 -->
<!-- markdownlint-disable html -->
<!-- markdownlint-disable no-duplicate-header -->

<div align="center">
  <img src="https://github.com/deepseek-ai/DeepSeek-V2/blob/main/figures/logo.svg?raw=true" width="60%" alt="DeepSeek-R1" />
</div>
<hr>
<div align="center" style="line-height: 1;">
  <a href="https://www.deepseek.com/" target="_blank"><img alt="Homepage"
    src="https://github.com/deepseek-ai/DeepSeek-V2/blob/main/figures/badge.svg?raw=true"/></a>
  <a href="https://chat.deepseek.com/" target="_blank"><img alt="Chat"
    src="https://img.shields.io/badge/🤖%20Chat-DeepSeek%20R1-536af5?color=536af5&logoColor=white"/></a>
  <a href="https://huggingface.co/deepseek-ai" target="_blank"><img alt="Hugging Face"
    src="https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-DeepSeek%20AI-ffc107?color=ffc107&logoColor=white"/></a>
  <br>
  <a href="https://discord.gg/Tc7c45Zzu5" target="_blank"><img alt="Discord"
    src="https://img.shields.io/badge/Discord-DeepSeek%20AI-7289da?logo=discord&logoColor=white&color=7289da"/></a>
  <a href="https://github.com/deepseek-ai/DeepSeek-V2/blob/main/figures/qr.jpeg?raw=true" target="_blank"><img alt="WeChat"
    src="https://img.shields.io/badge/WeChat-DeepSeek%20AI-brightgreen?logo=wechat&logoColor=white"/></a>
  <a href="https://twitter.com/deepseek_ai" target="_blank"><img alt="Twitter Follow"
    src="https://img.shields.io/badge/Twitter-deepseek_ai-white?logo=x&logoColor=white"/></a>
  <br>
  <a href="https://github.com/deepseek-ai/DeepSeek-R1/blob/main/LICENSE"><img alt="License"
    src="https://img.shields.io/badge/License-MIT-f5de53?&color=f5de53"/></a>
  <br>
  <a href="https://github.com/deepseek-ai/DeepSeek-R1/blob/main/DeepSeek_R1.pdf"><b>Paper Link</b>👁️</a>
</div>

## 1. 介绍

在此要介绍我们的第一代推理模型，DeepSeek-R1-Zero和DeepSeek-R1。
DeepSeek-R1-Zero，是基于大规模强化学习（RL）训练的模型，没有将监督微调（SFT）作为初始步骤，其在推理任务上展现了出色的性能。
通过强化学习，DeepSeek-R1-Zero自然地涌现出众多强大且有趣的推理行为。
然而，DeepSeek-R1-Zero面临着诸如无限重复、可读性差和语言混合等挑战。为了解决这些问题并进一步提升推理性能，
我们推出了DeepSeek-R1，它在强化学习前结合了冷启动数据。
DeepSeek-R1在数学、代码和推理任务上取得了与OpenAI-o1相当的性能。
我们已经开源了DeepSeek-R1-Zero、DeepSeek-R1，以及基于Llama和Qwen从DeepSeek-R1蒸馏得到的六个密集模型。DeepSeek-R1-Distill-Qwen-32B在各种基准测试中超越了OpenAI-o1-mini，为密集模型达到了新的最先进结果。

**注意：在本地运行DeepSeek-R1系列模型之前，我们建议您先阅读[使用建议](#usage-recommendations)部分。**

<p align="center">
  <img width="80%" src="figures/benchmark.jpg">
</p>

## 2. 模型概述

---
**后训练**：基于基础模型的大规模强化学习

- 我们直接对基础模型应用强化学习（RL）而没有依赖监督微调（SFT）作为初始步骤。这种方法允许模型探索思维链（CoT）来解决复杂问题，从而推动了DeepSeek-R1-Zero的开发。DeepSeek-R1-Zero展示了自我验证、反思和生成长CoT等能力，标志着研究社区的一个重要里程碑。值得注意的是，它是第一个开源研究，验证了LLM的推理能力可以通过RL激励，而无需SFT。这一突破为该领域的未来发展铺平了道路。

- 我们介绍了我们的管道来开发DeepSeek-R1。该管道包括两个旨在发现改进的推理模式和与人类偏好对齐的RL阶段，以及两个SFT阶段，作为模型推理和非推理能力的种子。我们相信该管道将通过创建更好的模型使行业受益。

---

**蒸馏**：小模型也可以很强大

- 我们证明了大型模型的推理模式可以被蒸馏到小型模型中，与在小模型上通过RL发现的推理模式相比，性能更好。开源的DeepSeek-R1及其API将使研究社区在未来蒸馏出更好的小型模型。

- 我们使用DeepSeek-R1生成的推理数据，对研究社区广泛使用的密集模型进行了微调。评估结果表明，蒸馏后的小型密集模型在基准测试中表现出色。我们开源了基于Qwen2.5和Llama3系列的1.5B、7B、8B、14B、32B和70B的蒸馏模型。

## 3. 模型下载

### DeepSeek-R1 模型

<div align="center">

| **Model** | **#Total Params** | **#Activated Params** | **Context Length** | **Download** |
| :------------: | :------------: | :------------: | :------------: | :------------: |
| DeepSeek-R1-Zero | 671B | 37B | 128K   | [🤗 HuggingFace](https://huggingface.co/deepseek-ai/DeepSeek-R1-Zero)   |
| DeepSeek-R1   | 671B | 37B |  128K   | [🤗 HuggingFace](https://huggingface.co/deepseek-ai/DeepSeek-R1)   |

</div>

DeepSeek-R1-Zero & DeepSeek-R1 是基于DeepSeek-V3-Base训练的。
有关模型架构的更多详细信息，请参阅[DeepSeek-V3](https://github.com/deepseek-ai/DeepSeek-V3)仓库。

### DeepSeek-R1-Distill 蒸馏模型

<div align="center">

| **Model** | **Base Model** | **Download** |
| :------------: | :------------: | :------------: |
| DeepSeek-R1-Distill-Qwen-1.5B  | [Qwen2.5-Math-1.5B](https://huggingface.co/Qwen/Qwen2.5-Math-1.5B) | [🤗 HuggingFace](https://huggingface.co/deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B)   |
| DeepSeek-R1-Distill-Qwen-7B  | [Qwen2.5-Math-7B](https://huggingface.co/Qwen/Qwen2.5-Math-7B) | [🤗 HuggingFace](https://huggingface.co/deepseek-ai/DeepSeek-R1-Distill-Qwen-7B)   |
| DeepSeek-R1-Distill-Llama-8B  | [Llama-3.1-8B](https://huggingface.co/meta-llama/Llama-3.1-8B) | [🤗 HuggingFace](https://huggingface.co/deepseek-ai/DeepSeek-R1-Distill-Llama-8B)   |
| DeepSeek-R1-Distill-Qwen-14B   | [Qwen2.5-14B](https://huggingface.co/Qwen/Qwen2.5-14B) | [🤗 HuggingFace](https://huggingface.co/deepseek-ai/DeepSeek-R1-Distill-Qwen-14B)   |
|DeepSeek-R1-Distill-Qwen-32B  | [Qwen2.5-32B](https://huggingface.co/Qwen/Qwen2.5-32B) | [🤗 HuggingFace](https://huggingface.co/deepseek-ai/DeepSeek-R1-Distill-Qwen-32B)   |
| DeepSeek-R1-Distill-Llama-70B  | [Llama-3.3-70B-Instruct](https://huggingface.co/meta-llama/Llama-3.3-70B-Instruct) | [🤗 HuggingFace](https://huggingface.co/deepseek-ai/DeepSeek-R1-Distill-Llama-70B)   |

</div>

DeepSeek-R1-Distill 模型是基于开源模型使用DeepSeek-R1生成的样本进行微调的。
我们稍微改变了它们的配置和分词器。请使用我们的设置来运行这些模型。

## 4. 评估结果

### DeepSeek-R1 评估

对于我们所有的模型，最大生成长度设置为32,768个token。对于需要采样的基准测试，我们使用温度为0.6，top-p值为0.95，每个查询生成64个响应来估计pass@1。

<div align="center">


| Category | Benchmark (Metric) | Claude-3.5-Sonnet-1022 | GPT-4o 0513 | DeepSeek V3 | OpenAI o1-mini | OpenAI o1-1217 | DeepSeek R1 |
|----------|-------------------|----------------------|------------|--------------|----------------|------------|--------------|
| | Architecture | - | - | MoE | - | - | MoE |
| | # Activated Params | - | - | 37B | - | - | 37B |
| | # Total Params | - | - | 671B | - | - | 671B |
| English | MMLU (Pass@1) | 88.3 | 87.2 | 88.5 | 85.2 | **91.8** | 90.8 |
| | MMLU-Redux (EM) | 88.9 | 88.0 | 89.1 | 86.7 | - | **92.9** |
| | MMLU-Pro (EM) | 78.0 | 72.6 | 75.9 | 80.3 | - | **84.0** |
| | DROP (3-shot F1) | 88.3 | 83.7 | 91.6 | 83.9 | 90.2 | **92.2** |
| | IF-Eval (Prompt Strict) | **86.5** | 84.3 | 86.1 | 84.8 | - | 83.3 |
| | GPQA-Diamond (Pass@1) | 65.0 | 49.9 | 59.1 | 60.0 | **75.7** | 71.5 |
| | SimpleQA (Correct) | 28.4 | 38.2 | 24.9 | 7.0 | **47.0** | 30.1 |
| | FRAMES (Acc.) | 72.5 | 80.5 | 73.3 | 76.9 | - | **82.5** |
| | AlpacaEval2.0 (LC-winrate) | 52.0 | 51.1 | 70.0 | 57.8 | - | **87.6** |
| | ArenaHard (GPT-4-1106) | 85.2 | 80.4 | 85.5 | 92.0 | - | **92.3** |
| Code | LiveCodeBench (Pass@1-COT) | 33.8 | 34.2 | - | 53.8 | 63.4 | **65.9** |
| | Codeforces (Percentile) | 20.3 | 23.6 | 58.7 | 93.4 | **96.6** | 96.3 |
| | Codeforces (Rating) | 717 | 759 | 1134 | 1820 | **2061** | 2029 |
| | SWE Verified (Resolved) | **50.8** | 38.8 | 42.0 | 41.6 | 48.9 | 49.2 |
| | Aider-Polyglot (Acc.) | 45.3 | 16.0 | 49.6 | 32.9 | **61.7** | 53.3 |
| Math | AIME 2024 (Pass@1) | 16.0 | 9.3 | 39.2 | 63.6 | 79.2 | **79.8** |
| | MATH-500 (Pass@1) | 78.3 | 74.6 | 90.2 | 90.0 | 96.4 | **97.3** |
| | CNMO 2024 (Pass@1) | 13.1 | 10.8 | 43.2 | 67.6 | - | **78.8** |
| Chinese | CLUEWSC (EM) | 85.4 | 87.9 | 90.9 | 89.9 | - | **92.8** |
| | C-Eval (EM) | 76.7 | 76.0 | 86.5 | 68.9 | - | **91.8** |
| | C-SimpleQA (Correct) | 55.4 | 58.7 | **68.0** | 40.3 | - | 63.7 |

</div>


### 蒸馏模型评估


<div align="center">

| Model                                    | AIME 2024 pass@1 | AIME 2024 cons@64 | MATH-500 pass@1 | GPQA Diamond pass@1 | LiveCodeBench pass@1 | CodeForces rating |
|------------------------------------------|------------------|-------------------|-----------------|----------------------|----------------------|-------------------|
| GPT-4o-0513                          | 9.3              | 13.4              | 74.6            | 49.9                 | 32.9                 | 759               |
| Claude-3.5-Sonnet-1022             | 16.0             | 26.7                 | 78.3            | 65.0                 | 38.9                 | 717               |
| o1-mini                              | 63.6             | 80.0              | 90.0            | 60.0                 | 53.8                 | **1820**          |
| QwQ-32B-Preview                              | 44.0             | 60.0                 | 90.6            | 54.5               | 41.9                 | 1316              |
| DeepSeek-R1-Distill-Qwen-1.5B       | 28.9             | 52.7              | 83.9            | 33.8                 | 16.9                 | 954               |
| DeepSeek-R1-Distill-Qwen-7B          | 55.5             | 83.3              | 92.8            | 49.1                 | 37.6                 | 1189              |
| DeepSeek-R1-Distill-Qwen-14B         | 69.7             | 80.0              | 93.9            | 59.1                 | 53.1                 | 1481              |
| DeepSeek-R1-Distill-Qwen-32B        | **72.6**         | 83.3              | 94.3            | 62.1                 | 57.2                 | 1691              |
| DeepSeek-R1-Distill-Llama-8B         | 50.4             | 80.0              | 89.1            | 49.0                 | 39.6                 | 1205              |
| DeepSeek-R1-Distill-Llama-70B        | 70.0             | **86.7**          | **94.5**        | **65.2**             | **57.5**             | 1633              |

</div>


## 5. 聊天网站 & API平台

您可以在DeepSeek的官方网站上与DeepSeek-R1聊天：[chat.deepseek.com](https://chat.deepseek.com)，并切换到“DeepThink”按钮。

我们还在DeepSeek平台提供了OpenAI兼容的API：[platform.deepseek.com](https://platform.deepseek.com/)

## 6. 如何本地运行

### DeepSeek-R1 系列模型

请访问[DeepSeek-V3](https://github.com/deepseek-ai/DeepSeek-V3)仓库，了解更多关于本地运行DeepSeek-R1的信息。

**注意：Hugging Face的Transformers尚未直接支持。**

### DeepSeek-R1-Distill 蒸馏系列模型

DeepSeek-R1-Distill 模型可以像Qwen或Llama模型一样使用。

例如，您可以使用[vLLM](https://github.com/vllm-project/vllm)轻松启动一个服务：

```shell
vllm serve deepseek-ai/DeepSeek-R1-Distill-Qwen-32B --tensor-parallel-size 2 --max-model-len 32768 --enforce-eager
```

您也可以使用[SGLang](https://github.com/sgl-project/sglang)轻松启动一个服务：

```bash
python3 -m sglang.launch_server --model deepseek-ai/DeepSeek-R1-Distill-Qwen-32B --trust-remote-code --tp 2
```

### 使用建议

**我们建议遵循以下配置，在利用DeepSeek-R1系列模型进行基准测试时，以实现预期的性能：**

1. 将温度设置在0.5-0.7之间（0.6是推荐值），以防止无限重复或不连贯的输出。
2. **避免添加系统提示；所有指令应包含在用户提示中。**
3. 对于数学问题，建议在提示中包含一个指令，例如：“请逐步推理，并将最终答案放在\boxed{}中。”
4. 在评估模型性能时，建议进行多次测试并平均结果。

此外，我们观察到DeepSeek-R1系列模型在回答某些查询时，往往会跳过思考模式（即输出“\<think\>\n\n\</think\>”），这可能会对模型的性能产生不利影响。
**为了确保模型进行彻底推理，我们建议在每个输出的开头强制模型以“\<think\>\n”开始其响应。**

### 官方提示

在官方DeepSeek网页/应用中，我们不使用系统提示，而是设计了两个特定的提示，用于文件上传和网络搜索，以提供更好的用户体验。此外，网页/应用中的温度为0.6。

对于文件上传，请按照模板创建提示，其中{file_name}、{file_content}和{question}是参数。

```
file_template = \
"""[file name]: {file_name}
[file content begin]
{file_content}
[file content end]
{question}"""
```

对于Web搜索，{search_results}、{cur_date}和{question}是参数。

对于中文查询，我们使用以下提示：
```
search_answer_zh_template = \
'''# 以下内容是基于用户发送的消息的搜索结果:
{search_results}
在我给你的搜索结果中，每个结果都是[webpage X begin]...[webpage X end]格式的，X代表每篇文章的数字索引。请在适当的情况下在句子末尾引用上下文。请按照引用编号[citation:X]的格式在答案中对应部分引用上下文。如果一句话源自多个上下文，请列出所有相关的引用编号，例如[citation:3][citation:5]，切记不要将引用集中在最后返回引用编号，而是在答案对应部分列出。
在回答时，请注意以下几点：
- 今天是{cur_date}。
- 并非搜索结果的所有内容都与用户的问题密切相关，你需要结合问题，对搜索结果进行甄别、筛选。
- 对于列举类的问题（如列举所有航班信息），尽量将答案控制在10个要点以内，并告诉用户可以查看搜索来源、获得完整信息。优先提供信息完整、最相关的列举项；如非必要，不要主动告诉用户搜索结果未提供的内容。
- 对于创作类的问题（如写论文），请务必在正文的段落中引用对应的参考编号，例如[citation:3][citation:5]，不能只在文章末尾引用。你需要解读并概括用户的题目要求，选择合适的格式，充分利用搜索结果并抽取重要信息，生成符合用户要求、极具思想深度、富有创造力与专业性的答案。你的创作篇幅需要尽可能延长，对于每一个要点的论述要推测用户的意图，给出尽可能多角度的回答要点，且务必信息量大、论述详尽。
- 如果回答很长，请尽量结构化、分段落总结。如果需要分点作答，尽量控制在5个点以内，并合并相关的内容。
- 对于客观类的问答，如果问题的答案非常简短，可以适当补充一到两句相关信息，以丰富内容。
- 你需要根据用户要求和回答内容选择合适、美观的回答格式，确保可读性强。
- 你的回答应该综合多个相关网页来回答，不能重复引用一个网页。
- 除非用户要求，否则你回答的语言需要和用户提问的语言保持一致。

# 用户消息为：
{question}'''
```


对于英文查询，我们使用以下提示：
```
search_answer_en_template = \
'''# The following contents are the search results related to the user's message:
{search_results}
In the search results I provide to you, each result is formatted as [webpage X begin]...[webpage X end], where X represents the numerical index of each article. Please cite the context at the end of the relevant sentence when appropriate. Use the citation format [citation:X] in the corresponding part of your answer. If a sentence is derived from multiple contexts, list all relevant citation numbers, such as [citation:3][citation:5]. Be sure not to cluster all citations at the end; instead, include them in the corresponding parts of the answer.
When responding, please keep the following points in mind:
- Today is {cur_date}.
- Not all content in the search results is closely related to the user's question. You need to evaluate and filter the search results based on the question.
- For listing-type questions (e.g., listing all flight information), try to limit the answer to 10 key points and inform the user that they can refer to the search sources for complete information. Prioritize providing the most complete and relevant items in the list. Avoid mentioning content not provided in the search results unless necessary.
- For creative tasks (e.g., writing an essay), ensure that references are cited within the body of the text, such as [citation:3][citation:5], rather than only at the end of the text. You need to interpret and summarize the user's requirements, choose an appropriate format, fully utilize the search results, extract key information, and generate an answer that is insightful, creative, and professional. Extend the length of your response as much as possible, addressing each point in detail and from multiple perspectives, ensuring the content is rich and thorough.
- If the response is lengthy, structure it well and summarize it in paragraphs. If a point-by-point format is needed, try to limit it to 5 points and merge related content.
- For objective Q&A, if the answer is very brief, you may add one or two related sentences to enrich the content.
- Choose an appropriate and visually appealing format for your response based on the user's requirements and the content of the answer, ensuring strong readability.
- Your answer should synthesize information from multiple relevant webpages and avoid repeatedly citing the same webpage.
- Unless the user requests otherwise, your response should be in the same language as the user's question.

# The user's message is:
{question}'''
```

## 7. 许可证

本代码仓库和模型权重均采用[MIT许可证](https://github.com/deepseek-ai/DeepSeek-R1/blob/main/LICENSE)。
DeepSeek-R1系列支持商业使用，允许任何修改和衍生作品，包括但不限于蒸馏以训练其他LLMs。请注意：
- DeepSeek-R1-Distill-Qwen-1.5B, DeepSeek-R1-Distill-Qwen-7B, DeepSeek-R1-Distill-Qwen-14B and DeepSeek-R1-Distill-Qwen-32B are derived from [Qwen-2.5 series](https://github.com/QwenLM/Qwen2.5), which are originally licensed under [Apache 2.0 License](https://huggingface.co/Qwen/Qwen2.5-1.5B/blob/main/LICENSE), and now finetuned with 800k samples curated with DeepSeek-R1.
- DeepSeek-R1-Distill-Llama-8B is derived from Llama3.1-8B-Base and is originally licensed under [Llama3.1 license](https://huggingface.co/meta-llama/Llama-3.1-8B/blob/main/LICENSE).
- DeepSeek-R1-Distill-Llama-70B is derived from Llama3.3-70B-Instruct and is originally licensed under [Llama3.3 license](https://huggingface.co/meta-llama/Llama-3.3-70B-Instruct/blob/main/LICENSE).

## 8. 引用

```bibtex
@misc{deepseekai2025deepseekr1incentivizingreasoningcapability,
      title={DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning}, 
      author={DeepSeek-AI},
      year={2025},
      eprint={2501.12948},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2501.12948}, 
}
```

## 9. Contact
If you have any questions, please raise an issue or contact us at [service@deepseek.com](mailto:service@deepseek.com).
