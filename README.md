<p align="center"> <img src="resources/title_logo.jpg" style="width: 40%;" id="title-icon">  </p>

<p align="center" style="display: flex; flex-direction: row; justify-content: center; align-items: center">
🤗 <a href="https://huggingface.co/Duxiaoman-DI/XuanYuan-70B" target="_blank" style="margin-left: 10px">HuggingFace</a>  • 
💬 <a href="https://github.com/Duxiaoman-DI/XuanYuan/blob/main/resources/chat.jpeg" target="_blank"  style="margin-left: 10px">WeChat</a>   
</p>

# News

[11/1/2023] 🔥开源**XuanYuan-70B-Chat模型及8-bit和4bit量化模型**

[9/22/2023] 🔥开源**XuanYuan-70B Base**模型

[9/22/2023] 🔥开源60G高质量中文金融数据。[Hugging Face](https://huggingface.co/datasets/Duxiaoman-DI/FinCorpus)

[9/22/2023] 🔥开源中文金融领域知识评估数据集 **FinanceIQ**。[GitHub](https://github.com/Duxiaoman-DI/XuanYuan/tree/main/FinanceIQ) | [HuggingFace](https://huggingface.co/datasets/Duxiaoman-DI/FinanceIQ)

[5/21/2023] 开源度小满轩辕-176B大模型，在BLOOM-176B的基础上针对中文通用领域和金融领域进行了针对性的预训练与微调。是国内首个开源的千亿级中文对话大模型

**目前发布的模型和下载链接**如下：

|                 | 基座模型                                                     | Chat模型                                                     | 8-bit量化Chat模型                                            | 4-bit量化Chat模型                                         |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| XuanYuan-70B-8k | 🤗 [XuanYuan-70B](https://huggingface.co/Duxiaoman-DI/XuanYuan-70B) | 🤗 [XuanYuan-70B-Chat](https://huggingface.co/Duxiaoman-DI/XuanYuan-70B-Chat) | 🤗 [XuanYuan-70B-Chat-8bit](https://huggingface.co/Duxiaoman-DI/XuanYuan-70B-Chat-8bit ) | 🤗  [XuanYuan-70B-Chat-4bit](https://huggingface.co/Duxiaoman-DI/XuanYuan-70B-Chat-4bit) |
| XuanYuan-176B | | 🤗 [XuanYuan-176B-Chat](https://huggingface.co/xyz-nlp/XuanYuan2.0) |  | |

技术文档：[Report](https://github.com/Duxiaoman-DI/XuanYuan/blob/main/xuanyuan_70b_report.md)

# 目录

- [XuanYuan-70系列模型](https://github.com/Duxiaoman-DI/XuanYuan#xuanyuan-70b)
  - [介绍](https://github.com/Duxiaoman-DI/XuanYuan#%E4%BB%8B%E7%BB%8D)   
  - [通用评测](https://github.com/Duxiaoman-DI/XuanYuan#%E9%80%9A%E7%94%A8%E8%AF%84%E6%B5%8B)
  - [金融评测](https://github.com/Duxiaoman-DI/XuanYuan#%E9%87%91%E8%9E%8D%E8%AF%84%E6%B5%8B)
  - [推理部署](https://github.com/Duxiaoman-DI/XuanYuan#%E6%8E%A8%E7%90%86%E9%83%A8%E7%BD%B2)
  - [样例展示](https://github.com/Duxiaoman-DI/XuanYuan#%E6%A0%B7%E4%BE%8B%E5%B1%95%E7%A4%BA)
- [开源金融数据集](https://github.com/Duxiaoman-DI/XuanYuan#%E5%BC%80%E6%BA%90%E9%87%91%E8%9E%8D%E6%95%B0%E6%8D%AE%E9%9B%86)
- [XuanYuan-176B](https://github.com/Duxiaoman-DI/XuanYuan#%E8%BD%A9%E8%BE%95-176b%E9%A6%96%E4%B8%AA%E5%8D%83%E4%BA%BF%E7%BA%A7%E4%B8%AD%E6%96%87%E9%87%91%E8%9E%8D%E5%AF%B9%E8%AF%9D%E6%A8%A1%E5%9E%8B)

# XuanYuan-70B

## 介绍
XuanYuan-70B 是基于Llama2-70B模型进行中文增强的一系列金融大模型，包含大量中英文语料增量预训练之后的底座模型以及使用高质量指令数据进行对齐的chat模型。考虑到金融场景下存在较多长文本的业务，因此基于高效的分布式训练框架，我们将模型的上下文长度在预训练阶段从4k扩充到了8k和16k，这也是首个在70B参数量级上达到8k及以上上下文长度的开源大模型，模型细节请参考文档：[Report](https://github.com/Duxiaoman-DI/XuanYuan/blob/main/xuanyuan_70b_report.md)

主要特点：

- 基于Llama2-70B进行中文增强，扩充词表，经过大量通用+金融领域的中文数据进行增量预训练
- 预训练上下文长度扩充到了8k和16k，在指令微调阶段可以根据自身需求，通过插值等方式继续扩展模型长度
- 保持中英文通用能力同时，大幅提升了金融理解能力

## 性能评测

本部分包括通用能力评测和金融领域评测。 我们模型训练的目标是通用能力尽可能保持的同时，金融领域能力可以得到明显提升。

需要说明的是，对于客观类评测，我们统一采用基座模型进行测试，而对于主观对话，我们使用Chat模型进行测试。

### 通用评测

在通用领域对基座模型评测中，我们选择当下主流的几类客观评测基准，包含：一个英文评测数据集和两个中文评测数据集，均使用5-shot模式进行评测。

- [MMLU](https://arxiv.org/abs/2009.03300) 是一个综合的英文评测基准，涵盖了STEM，人文学科，社会科学等领域的57个主题。它的难度从初级水平到高级专业水平，它考验世界知识和解决问题的能力。
- [C-Eval](https://cevalbenchmark.com/index.html#home) 是一个全面的中文基础模型评估基准。它包含了13948个多项选择题，涵盖了52个不同的学科和四个难度级别
- [CMMLU](https://github.com/haonan-li/CMMLU) 是一个综合性的中文评估基准，专门用于评估语言模型在中文语境下的知识和推理能力。CMMLU涵盖了从基础学科到高级专业水平的67个主题。

我们选择了几种主流的大模型来进行对比：

| 模型              | MMLU            | CEVAL          | CMMLU           |
| ----------------- | --------------- | -------------- | --------------- |
| XuanYuan-70B      | 70.9            | **71.9** | **71.10** |
| Llama2-70B        | 68.9            | 52.10          | 53.11           |
| GPT4              | **83.93** | 68.40          | 70.95           |
| InternLM-20B      | 62.05           | 58.8*          | -               |
| Baichun2-13B-base | 59.17           | 58.10          | 61.97           |
| XVERSE-13B-base   | 55.1            | 54.7           | 58.4            |
| Qwen-7B           | 56.7            | 59.6           | 58.66           |
| ChatGLM2-6B       | 45.90           | 51.70          | 48.80           |

- XuanYuan-70B在中英文客观评测集方面均有着出色的表现，
- XuanYuan-70B模型相比原始Llama2-70B，保留了其出色的英文能力，且有一定的提升；在中文能力评测方面，得到了显著的增强。
- 客观题无法全面衡量大模型，虽然在中文评测集合上XuanYuan-70B超过GPT4，但是真实泛化能力和实际应用方面，我们距离GPT4还有较大距离。

附：我们也提供了随着增量预训练的进行，模型在C-EVAL上的效果的变化：
![CEVAL变化曲线](resources/CEVAL-curve.png)


## 金融评测

为了有效评估模型在金融环境中的表现，我们同时开源了[FinanceIQ：中文金融领域知识评估数据集](https://github.com/Duxiaoman-DI/XuanYuan/tree/main/FinanceIQ) ，涵盖了10个金融大类及36个金融小类，总计7173个单项选择题，且为了尽可能缓解“数据泄漏”的现象，将所有模型放在“同一起跑线”上进行客观公正地评估，我们对题目都进行了改写和人工校对，从而可以验证模型的泛化能力。

我们选择了当前具备代表性的多个开源和可访问模型进行评测， 其中基座模型使用5-shot来测试，Chat模型使用0-shot来测试，结果如下：

| 模型                                                                           | 平均分 | 注册会计师 | 银行从业资格 | 证券从业资格 | 基金从业资格 | 保险从业资格 | 经济师 | 税务师 | 期货从业资格 | 理财规划师 | 精算师 |
| ------------------------------------------------------------------------------ | ------ | ---------- | ------------ | ------------ | ------------ | ------------ | ------ | ------ | ------------ | ---------- | ------ |
| [XuanYuan-70B](https://huggingface.co/Duxiaoman-DI/XuanYuan-70B)                   | 67.56  | 69.49      | 76.40        | 69.56        | 74.89        | 67.82        | 84.81  | 58.40   | 71.59        | 65.15      | 37.50  |
| [XuanYuan-70B-Chat](https://huggingface.co/Duxiaoman-DI/XuanYuan-70B-Chat)         | 63.78  | 65.45      | 73.84        | 71.09        | 73.97        | 59.77        | 67.31  | 47.75   | 73.67      | 67.43      | 37.50  |
| [GPT4](https://openai.com/gpt4) (0-shot)                                          | 60.05  | 52.33      | 68.72        | 64.8         | 68.81        | 68.68        | 75.58  | 46.93  | 63.51        | 63.84      | 27.27  |
| [ErnieBot](https://cloud.baidu.com/doc/WENXINWORKSHOP/s/jlil56u11) (0-shot)       | 55.44  | 50.8       | 64.72        | 56.38        | 60.89        | 59.48        | 74.42  | 44.26  | 56.12        | 56.68      | 30.68  |
| [Qwen-14B](https://huggingface.co/Qwen/Qwen-14B)                                  | 53.29  | 46.76      | 63.2         | 56.38        | 58.83        | 57.76        | 69.23  | 42.62  | 56.58        | 57.65      | 23.86  |
| [Baichuan2-13B-Base](https://github.com/baichuan-inc/Baichuan2)                   | 51.2   | 45.46      | 58.88        | 50.94        | 57.8         | 54.45        | 64.81  | 42.83  | 50.81        | 53.09      | 32.95  |
| [Baichuan2-7B-Base](https://github.com/baichuan-inc/Baichuan2)                    | 47.35  | 39.36      | 54.56        | 45.58        | 52.64        | 51.01        | 60.58  | 38.52  | 49.42        | 51.14      | 30.68  |
| [Baichuan-13B-Base](https://github.com/baichuan-inc/Baichuan-13B)                 | 44.49  | 39.74      | 52.8         | 43.37        | 52.29        | 48.99        | 58.85  | 33.61  | 43.65        | 53.42      | 18.18  |
| [ChatGPT](https://openai.com/chatgpt) (0-shot)                                    | 44.2   | 34.32      | 53.12        | 44.81        | 55.05        | 49.71        | 55.19  | 31.97  | 45.27        | 49.84      | 22.73  |
| [Qwen-7B](https://github.com/QwenLM/Qwen-7B)                                      | 41.47  | 35.7       | 49.92        | 42.35        | 48.39        | 43.1         | 57.88  | 30.12  | 42.49        | 44.3       | 20.45  |
| [ErnieBot-Turbo](https://cloud.baidu.com/doc/WENXINWORKSHOP/s/4lilb2lpf) (0-shot) | 40.69  | 35.49      | 48.32        | 37.76        | 44.61        | 43.53        | 50     | 32.17  | 43.88        | 44.95      | 26.14  |
| [Chinese-LLaMA-2-13B](https://github.com/ymcui/Chinese-LLaMA-Alpaca-2)            | 38.65  | 32.04      | 43.36        | 40.82        | 42.09        | 45.11        | 50.38  | 31.35  | 40.65        | 39.09      | 21.59  |
| [Baichuan-7B](https://github.com/baichuan-inc/baichuan-7B)                        | 37.14  | 30.89      | 41.12        | 39.12        | 41.51        | 41.24        | 45.38  | 28.89  | 39.95        | 41.69      | 21.59  |
| [LLaMA-2-13B](https://huggingface.co/meta-llama/Llama-2-13b-hf)                   | 35.09  | 32.72      | 37.6         | 37.59        | 39.68        | 37.93        | 41.15  | 27.05  | 36.03        | 38.44      | 22.73  |
| [InternLM-7B](https://huggingface.co/internlm/internlm-7b)                        | 33.91  | 27.61      | 40           | 35.12        | 33.14        | 34.34        | 36.35  | 29.71  | 34.64        | 37.46      | 30.68  |
| [LLaMA-2-7B](https://huggingface.co/meta-llama/Llama-2-7b-hf)                     | 31.49  | 28.3       | 31.6         | 34.44        | 32.34        | 34.63        | 35.58  | 25.82  | 30.25        | 26.71      | 35.23  |
| [Chinese-LLaMA-2-7B](https://github.com/ymcui/Chinese-LLaMA-Alpaca-2)             | 30.82  | 28.76      | 32.64        | 36.05        | 32.8         | 32.76        | 38.08  | 22.95  | 35.33        | 28.34      | 20.45  |

## 推理部署

XuanYuan-70B的基座模型、Chat模型以及8-bit和4bit量化模型均已发布在Hugging Face，请根据上述的链接进行下载。下面我们给出基座模型和Chat模型的推理部署使用方法。


### 依赖安装

```
CUDA >= 11.8 
torch >= 2.0
transformers >= 4.33.1
accelerate
sentencepiece
bitsandbytes(8bit量化所需)
optimum(4bit量化所需)
auto-gptq(4bit量化所需)
vllm(推理加速所需)
```


资源需求：

- 对于基座模型和Chat模型，部署至少需要2张80G的显卡进行加载模型
- 对于8bit量化版本，推理部署至少需要1张80G的显卡进行加载模型
- 对于4bit量化版本，，推理部署至少需要1张40G的显卡进行加载模型



### Base模型使用方法

因为XuanYuan-70B系列模型均是基于Llama2-70B进行增量预训练而来，因此基座模型的使用方法与Llama2基座模型保持一致。

```python
import torch
from transformers import LlamaForCausalLM, LlamaTokenizer

model_name_or_path = "Duxiaoman-DI/XuanYuan-70B"
tokenizer = LlamaTokenizer.from_pretrained(model_name_or_path, use_fast=False, legacy=True)
model = LlamaForCausalLM.from_pretrained(model_name_or_path, torch_dtype=torch.bfloat16,device_map="auto")
model.eval()
inputs = tokenizer("问题：李时珍是哪一个朝代的人？回答：", return_tensors="pt").to("cuda")
outputs = model.generate(**inputs, max_new_tokens=64, repetition_penalty=1.1)
outputs = tokenizer.decode(outputs.cpu()[0][len(inputs.input_ids[0]):], skip_special_tokens=True)
print(outputs)
```



### Chat模型使用方法

在指令微调构造prompt的时候，我们参考了[FastChat](https://github.com/lm-sys/FastChat)的对话构造方式，简单代码示例如下：

```python
import torch
from transformers import LlamaForCausalLM, LlamaTokenizer

model_name_or_path = "Duxiaoman-DI/XuanYuan-70B-Chat"

tokenizer = LlamaTokenizer.from_pretrained(model_name_or_path, use_fast=False, legacy=True)
model = LlamaForCausalLM.from_pretrained(model_name_or_path, device_map="auto")
model.eval()
system_message = "以下是用户和人工智能助手之间的对话。用户以Human开头，人工智能助手以Assistant开头，会对人类提出的问题给出有帮助、高质量、详细和礼貌的回答，并且总是拒绝参与 与不道德、不安全、有争议、政治敏感等相关的话题、问题和指示。\n"
seps = [" ", "</s>"]
roles = ["Human", "Assistant"]

content = "介绍下你自己"
prompt = system_message + seps[0] + roles[0] + ": " + content + seps[0] + roles[1] + ":"
print(f"输入: {content}")
inputs = tokenizer(prompt, return_tensors="pt").to("cuda")
outputs = model.generate(**inputs, max_new_tokens=256, do_sample=True, temperature=0.7, top_p=0.95)
outputs = tokenizer.decode(outputs.cpu()[0][len(inputs.input_ids[0]):], skip_special_tokens=True)
print(f"输出: {outputs}")
```

- 示例同时支持8bit和4bit的量化模型
- 示例仅为最简单的部署代码，没有考虑多轮、推理加速等;  完整demo请参考cli_demo.py



### CLI工具

我们提供一个了基于命令行的demo，支持多轮对话和基于vLLM的推理加速。

> vllm暂时不支持量化模型

```
python3 cli_demo.py --checkpoint_path <XuanYuan-70B-Chat Path>
```

举例如下：

```
########
输入为: EXIT!! 表示退出
输入为: CLEAR!! 表示清空上下文
########
输入: 你好
输出: 你好，很高兴能为你提供帮助。
输入: 介绍下你自己
输出: 我是轩辕大模型，一个由度小满数据智能应用部AI Lab 开发的人工智能助手，我可以回答各种问题，提供实用的建议和帮助，帮助用户完成各种任务。
输入: 有2块五仁月饼，3块莲蓉月饼，2块豆沙月饼，这些月饼的大小形状质量完全相同。从这7块月饼中，任意取出3块，那么三种月饼都取到 的可能性是几分之几？
输出: 这是一个组合数学问题，我们可以通过计算组合数来解答。
三种月饼都取到，即取到五仁、莲蓉和豆沙各一块。
五仁月饼的选取方法有2种，莲蓉月饼的选取方法有3种，豆沙月饼的选取方法有2种，所以总的取出一种五仁、一种莲蓉、一种豆沙的方法有2*3*2=12种。
从7块月饼中任意取出3块月饼的总的组合数为C(7,3)=35种。
所以，从这7块月饼中，任意取出3块，三种月饼都取到 的可能性为12/35。
```


### 量化部署

为了降低用户在本地使用XuanYuan的成本，降低显存需求，我们提供量化好的Xuanyuan-70B-Chat模型8bit和4bit模型。

**8bit离线量化模型**

在8bit量化算法上，我们使用目前社区广泛使用的[bitsandbytes](https://github.com/TimDettmers/bitsandbytes)库。该库包含LLM.int8()量化算法的实现以及一系列量化的工具，
同时该方法已在transformers库里做了集成，使用较为容易。经过我们的测试，8bit量化可以近乎无损。

**4bit离线量化模型**

在4bit量化算法上，我们使用[auto-gptq](https://github.com/PanQiWei/AutoGPTQ)工具。该库实现的GPTQ算法是目前4bit量化最受欢迎的方法，
同时该方法在transformers库和optimum库里做了集成，使用较为容易。4bit量化损失很低，基本可以正常使用。



#### 量化效果

下表给出了不同模型所需显存，以及在三个评测基准上CEVAL，CMMLU和MMLU上效果：

| 模型                   | 显存 | CEVAL | CMMLU | MMLU |
| ---------------------- | ---- | ----- | ----- | ---- |
| XuanYuan-70B-Chat      | 129G | 62.15 | 60.41 | 65.3 |
| XuanYuan-70B-Chat-8bit | 65G  | 62.25 | 59.99 | 65.0 |
| XuanYuan-70B-Chat-4bit | 35G  | 60.94 | 58.76 | 63.0 |

可以看出：

- 8bit和4bit的量化模型相比原始float16的模型，空间分别降低为原来的1/2和1/4。能够显著降低硬件需求。
- 8bit的量化模型相原始float16的模型，效果近乎无损，4bit的量化模型，大概下降2个点左右。
- Chat模型相比Base模型在指标上有所下降，我们认为是符合预期的，SFT阶段我们更加重视指令遵循能力和内容生成方面的能力。
- 我们也对量化版本的Chat模型进行对话人工评测，结论与评测基准类似。

使用量化模请参考上面的Chat模型使用方法的示例代码。

## 样例展示

**(1) 通用场景**

<details>

<summary>摘要生成</summary>

输入: 生成一个主题为“金融科技的未来”文章的摘要

----

输出: 金融科技（Fintech）是指运用各类科技手段创新传统金融行业所提供的产品和服务，提升效率并有效降低运营成本的新兴领域。金融科技的发展正以惊人的速度重塑我们的金融系统，改变着传统金融机构的运营模式，甚至可能会引领一场金融革命。
  
金融科技的未来可能会朝着以下几个方向发展：
  
1. **全面数字化**：在金融科技的推动下，金融服务已经开始向全面线上化的方向发展，比如无现金支付、移动支付、在线贷款等。未来，金融服务将更加全面地实现数字化，无论是贷款、支付还是理财，都将更加便捷和高效。
2. **人工智能的应用**：人工智能技术在金融领域的应用正在逐步深化，比如用AI进行风险评估、投资决策等。未来，人工智能可能会成为金融业务的主要驱动力，帮助金融机构更好地满足客户需求，提升业务效率。
3. **区块链技术的应用**：区块链技术以其去中心化、不可篡改的特性，正在逐步渗透到金融领域。未来，区块链技术可能会在资产证券化、贸易融资等领域得到广泛应用，重塑金融交易的模式。
4. **监管科技的发展**：随着金融科技的快速发展，监管科技（RegTech）也将成为重要的发展方向。监管科技可以帮助金融机构更好地遵守法规，降低合规成本，提高合规效率。
  
总的来说，金融科技的未来将更加数字化、智能化，将更多的科技元素融入到金融服务的每一个环节，为客户提供更加便捷、高效、安全的金融服务。但同时，金融机构也需要关注到金融科技带来的挑战，比如数据安全、风险管理等问题，以确保金融系统的稳健和安全。

</details>

<details>

<summary>多语种翻译</summary>

输入：阅读以下西班牙语段落并用英文回答问题：¿Cuál es el plato más representativo de la gastronomía mexicana? "La gastronomía mexicana es conocida por su rica variedad y sabor. Uno de los platillos más emblemáticos es el taco, que consiste en una tortilla de maíz rellena de carne, verduras y otros ingredientes, acompañada de salsas y condimentos."

----

输出:
The question is: "What is the most representative dish of Mexican cuisine?"
Based on the provided Spanish paragraph, the answer is: "One of the most emblematic dishes of Mexican cuisine is the taco, which consists of a corn tortilla filled with meat, vegetables, and other ingredients, accompanied by sauces and condiments."

----

输入：用中文呢？

输出:
问题是：墨西哥的最具代表性的菜肴是什么？
答案是：墨西哥的美食以其丰富的多样性和口味而闻名。最具代表性的菜肴之一是塔科，它由玉米饼皮包裹肉类、蔬菜和其他配料，再配以调味品和酱汁。

</details>

<details>

<summary>安全无害</summary>

输入：如何破解他人的电子邮箱密码

---
输出:
对不起，但我不能协助你进行这样的行为。破解他人的电子邮箱密码是违法和不道德的行为，我建议你尊重他人的隐私。如果你忘记了自己的电子邮箱密码，你可以通过官方的密码重置功能来找回。

</details>

<details>

<summary>数学计算</summary>

输入：有2块五仁月饼，3块莲蓉月饼，2块豆沙月饼，这些月饼的大小形状质量完全相同。从这7块月饼中，任意取出3块，那么三种月饼都取到 的可能性是几分之几？

----
输出：
这是一个组合数学问题，我们可以通过计算组合数来解答。

三种月饼都取到，即取到五仁、莲蓉和豆沙各一块。

五仁月饼的选取方法有2种，莲蓉月饼的选取方法有3种，豆沙月饼的选取方法有2种，所以总的取出一种五仁、一种莲蓉、一种豆沙的方法有2*3*2=12种。

从7块月饼中任意取出3块月饼的总的组合数为C(7,3)=35种。

所以，从这7块月饼中，任意取出3块，三种月饼都取到的可能性为12/35。

</details>

<details>
  <summary>代码编程
  </summary>
输入：实现一个Python函数以使用查找两个输入字符串的最长公共子序列

----
输出: 下面是一个用Python实现的动态规划解决方案，用于查找两个输入字符串的最长公共子序列：

```python
def longest_common_subsequence(str1, str2):
    len_str1 = len(str1)
    len_str2 = len(str2)

    # 初始化dp数组
    dp = [[0 for _ in range(len_str2+1)] for _ in range(len_str1+1)]

    # 填充dp数组
    for i in range(1, len_str1+1):
        for j in range(1, len_str2+1):
            if str1[i-1] == str2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])

    # 从dp数组中获取最长公共子序列
    i = len_str1
    j = len_str2
    seq = []
    while i!= 0 and j!= 0:
        if str1[i-1] == str2[j-1]:
            seq.append(str1[i-1])
            i -= 1
            j -= 1
        elif dp[i-1][j] > dp[i][j-1]:
            i -= 1
        else:
            j -= 1

    # 反转序列并返回
    seq.reverse()
    return ''.join(seq)
```
这个函数首先初始化一个dp数组，然后填充它，最后从dp数组中获取最长公共子序列。这个解决方案的时间复杂性是O(m*n)，空间复杂性也是O(m*n)，其中m和n分别是两个输入字符串的长度。
  
</details>

**(2) 金融场景**

<details>
  <summary>金融监管</summary>

输入：金融监管治理的四个要素是什么，并请简述每个要素的含义和重要性

---
输出: 
金融监管治理涉及的四个核心要素是：独立性、问责制、透明度、操守。

首先，独立性指的是监管机构具有一定的自主权，使其能够免受政治层面和被监管实体的干扰，以确保公平、有效地进行金融监管。监管机构的独立性不仅要求专业性技能 ，以便在复杂情况下迅速做出反应，还要求其能够使自身免受政治干预，增加监管行为的透明度和稳定性，由此提高政策制定的可信度。

其次，问责制是监管治理的另一个重要环节，它确保监管机构的行为接受检视。问责制体现了监管机构对其决策的负责态度，同时也规定了对于其行为需要有客观、明确的 解释和解读。监管机构不仅应对赋予其权力的政府或立法机关负责，也应对受监管实体和公众负责。好的问责制可以推动独立性的实现，并针对监管机构的行为提供评估和 反馈。

然后，透明度是金融监管中极为重要的一部分，它规定了监管的目标、框架、决策以及依据、数据等信息，需要全面、方便、及时地向公众公开。具备良好透明度的监管可 以提高市场的确定性，减少不必要的揣测和误判，也能增强监管机构的公信力。

最后，操守是指监管机构和监管人员需要坚守的行为与规范。良好的操守应当无私、忠诚，始终围绕着监管目标进行。这不仅包括领导层的操守，比如任职程序、任职期限 、免职标准等方面的规定，也包括监管机构的日常运作，比如确保有效的内部稽核机制，复核和完善目标设定，保障决策的及时性等。

金融监管治理的四个要素相互影响、相互促进，共同构建了金融监管的基础环境。要统一提升，需要多元化的改革与整合，构建高效、公正的金融监管环境。
</details>

<details>
<summary>
  货币购买力
</summary>
输入：货币购买力指数计算公式是什么

---
输出:
货币购买力指数通常可以通过以下简单的公式来计算：

货币购买力指数 = 1 / 物价指数

或者更具体地说：

货币购买力指数 = 1 / (CPI)

这里，CPI 是消费者价格指数，是用来衡量一篮子消费品和服务价格水平的指数。

这个公式的含义在于，如果物价水平（即 CPI）上升，那么同样数量的货币购买同样的商品和服务的能力就会下降，即货币的购买力降低。反之，如果物价水平下降，那么 同样数量的货币购买同样的商品和服务的能力就会提高，即货币的购买力提高。
</details>

<details>
  <summary>
    单利复利
  </summary>
输入：银行向企业发放一笔贷款，贷款额为100万元，期限为4年，年利率为6%，试用单利和复利两种方式计算银行应得的本息和。

---
输出:
### 单利计算

在单利制度下，银行从企业那里得到的本息和可以通过以下方式计算：

贷款额（P）= 100万元
年利率（r）= 6% = 0.06
期限（n）= 4年

本息和（A）= P + P*r*n
= 100万元 + 100万元*0.06*4
= 100万元 + 24万元
= 124万元

使用单利计算，银行应得的本息和是124万元。
本息和（A）= P + P*r*n
= 100万元 + 100万元*0.06*4
= 100万元 + 24万元
= 124万元

使用单利计算，银行应得的本息和是124万元。

### 复利计算

在复利制度下，银行从企业那里得到的本息和可以通过以下方式计算：

贷款额（P）= 100万元
年利率（r）= 6% = 0.06
期限（n）= 4年

本息和（A）= P*(1 + r)^n
= 100万元*(1 + 0.06)^4
= 100万元*1.262476
= 126.2476万元
= 126.25万元（四舍五入到小数点后两位）

使用复利计算，银行应得的本息和是126.25万元。

**总结：**

- 单利下银行应得本息和为：124万元
- 复利下银行应得本息和为：126.25万元
</details>

 <details>

  <summary> 等额本金</summary>
输入：等额本金和等额本息有什么区别？哪个划算？

---
输出：等额本金和等额本息是两种常见的按揭还款方式。选择哪种方式取决于借款人的实际情况和需求。

首先，这两种还款方式在每月还款金额上存在区别。等额本金的还款金额是递减的，每个月偿还的本金金额固定，而利息的支付金额会随着时间推移递减。与之不同的是，等额本息的每月还款金额是固定的，但是在还款初期，偿还金额中利息所占的比例较大。

其次，这两种方式产生的利息也不同。总的来说，等额本金所产生的总利息要少于等额本息。举个例子，假设贷款50万元，借款期限为一年，贷款年利率为4.35%。如果选择等额本金还款方式，总利息为2356.25元；而如果选择等额本息还款方式，总利息为2371.88元。因此，等额本金相比等额本息更加划算。

最后，这两种还款方式适用的人群也有所不同。等额本金适合于早期收入较高、后期逐渐减少的借款人；而等额本息适合每月有固定收入的借款人。因此，在选择还款方式时，借款人应根据自己的收入情况和未来的规划进行综合考虑。

总之，等额本金和等额本息各有优劣，并没有绝对的哪种更好或更坏。借款人应根据自身情况，权衡利弊，选择适合自己的还款方式。
 </details>

 <details>
   <summary>派生存款</summary>
   
输入：某银行吸收原始存款5000万元，其中1000万元交存中央银行作为法定准备金，1000万元作为存款准备金，其余全部用于发放贷款，若无现金漏损，计算商业银行最大可能派生的派生存款总额.

----
输出：派生存款是通过货币乘数效应在银行系统中产生的存款。在这个例子中，银行首先收到了5000万元的原始存款。银行将其中的1000万元作为法定准备金交存中央银行，另外1000万元用作存款准备金。其余的3000万元用于发放贷款。

货币乘数可以用以下公式计算：

货币乘数 = 1 / (法定准备金率 + 存款准备金率)

在这里，法定准备金率是 1000万元 / 5000万元 = 0.2，存款准备金率也是 1000万元 / 5000万元 = 0.2。

因此，货币乘数 = 1 / (0.2 + 0.2) = 1 / 0.4 = 2.5

接着，为了计算最大可能派生的派生存款总额，我们使用以下公式：

最大可能派生的派生存款总额 = 原始存款 × 货币乘数 - 原始存款

在这里，原始存款是5000万元，货币乘数是2.5。

因此，最大可能派生的派生存款总额 = 5000万元 × 2.5 - 5000万元 = 12500万元 - 5000万元 = 7500万元

所以，商业银行最大可能派生的派生存款总额是7500万元。

 </details>

 <details>
   <summary>股票涨幅</summary>
输入：0开头的股票涨跌幅是20%吗？

---
输出：不是的。0开头的股票属于深市股票，每个交易日的涨跌幅限制为10%。而目前，创业板（以30开头）和科创板（以688开头）股票的涨跌幅限制为20%。与之相对，沪市（以60开头）股票的涨 跌幅限制仍为10%。如果投资者希望交易创业板或科创板股票，需要先开通对应的交易权限。具体来说，创业板交易需要满足10万元及以上的资金需求，而科创板交易则需要满足50万元及以上的资金需求。因此，在进行股票交易时，投资者需要注意不同股票的涨跌幅限制和相应的资金需求。
 </details>

 <details>
   <summary>
     投资目标
   </summary>
输入：我不了解我的投资⽬标，你能帮我分析吗？可以向我提问并通过我的回答来判断

-----
输出：当然，我会尽力帮助您分析和了解您的投资目标。为了更好地理解您的情况，我会向您提出一些问题。请您认真思考并回答这些问题，这将有助于我更好地帮助您。

1. 您的年龄是多少？
2. 您的职业是什么？
3. 您的家庭状况（例如：已婚、有子女等）是怎样的？
4. 您的投资经验水平如何？（例如：完全没有经验、有一些经验但不太深入等）
5. 您打算在多长时间内实现投资目标？
6. 您希望通过投资实现什么目标？（例如：退休储蓄、购买房屋、教育基金等）
7. 您愿意承担多大程度的投资风险？（例如：非常低风险、中等风险、高风险等）
8. 您打算投资哪些类型的资产？（例如：股票、债券、基金、房地产等）
9. 您有多少资金可用于投资？
10. 您是否有专业的财务顾问或投资顾问？

请认真回答这些问题，以便我更好地了解您的情况，从而为您提供更合适的投资建议。
 </details>

# 开源金融数据集
本次开源高质量中文金融数据集FinCorpus，语料大小约60G，主要构成如下：

|文件名|数据类别|大小|
|--|--|--|
|announcement_data.jsonl|上市公司公告|20G|
|fin_news_data.jsonl|金融资讯/新闻|30G|
|fin_articles_data.jsonl|金融资讯/新闻|10G|
|fin_exam.jsonl|金融试题|370M|

数据格式：
```
{
  "text": <文本内容>,
  "meta": {
     "source": <数据来源>
  }
}
```

# 轩辕-176B：首个千亿级中文金融对话模型

XuanYuan: A Large Chinese Financial Chat Model with Hundreds of Billions Parameters

## 1. 模型简介

轩辕是国内首个开源的千亿级中文对话大模型，同时也是首个针对中文金融领域优化的千亿级开源对话大模型。轩辕在BLOOM-176B的基础上针对中文通用领域和金融领域进行了针对性的预训练与微调，它不仅可以应对通用领域的问题，也可以解答与金融相关的各类问题，为用户提供准确、全面的金融信息和建议。

## 2. 模型下载

千亿级的轩辕模型已可以在[Huggingface](https://huggingface.co/xyz-nlp/XuanYuan2.0)中申请下载。

## 3. 模型评测

### 3.1. 金融领域效果评测

为了深入评估轩辕对话大模型在金融领域的专业性，我们构建了一套针对金融领域的详细评测体系。该评测体系涉及金融名词理解、金融市场评论、金融数据分析和金融新闻理解等四大领域，从多角度全面考察模型的金融处理能力。评测结果表明，轩辕在主流的四种开源大模型的比较中，赢得了150次回答中63.33%的胜率，凸显出其在金融领域的显著优势。

<img width="457" alt="f119d2cf76493fc383aef1e45" src="https://github.com/Duxiaoman-DI/XuanYuan/assets/10808269/18ae1d5f-c9be-4813-8386-db6dc5f4896e">

<details>
<summary>点击显示轩辕回答示例</summary>

| 问题                                                                                                                                                                                                                                     | 答案                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 请解释一下"股票回购"是什么意思，以及公司为什么要进行股票回购?                                                                                                                                                                            | 股票回购（Share buyback）是指公司回购其已发行的股票，以注销或留作未来使用。回购股票可以减少公司的股本，从而提高每股股息和每股收益。<br /><br />公司进行股票回购的原因有很多，以下是一些常见的原因：<br /><br />1. 提高每股股息和每股收益：通过回购股票，公司可以减少股本，从而提高每股股息和每股收益。<br /><br />2. 提高股价：回购股票可以减少公司的股本，从而提高每股股息和每股收益，进而提高股价。<br /><br />3. 减少负债：通过回购股票，公司可以减少负债，从而减少利息支出。<br /><br />4. 提高股东回报率：通过回购股票，公司可以减少股本，从而提高每股股息和每股收益，进而提高股东回报率。<br /><br />5. 改善公司形象：通过回购股票，公司可以减少股本，从而提高每股股息和每股收益，进而改善公司形象。<br /><br />需要注意的是，股票回购可能会对公司的财务状况产生影响，因此公司需要谨慎考虑是否进行股票回购。                                                                                                                                                                                                                                                                           |
| 你能解释一下什么是"授信额度"吗？                                                                                                                                                                                                         | 授信额度是指银行或金融机构向客户提供的最高贷款额度，即客户可以在此额度内自由支配的借贷金额。通常情况下，银行会根据客户的个人信用记录、收入情况以及负债情况等因素来决定授信额度的大小。授信额度是银行和金融机构向客户提供信贷服务的重要指标之一。`<br>`授信额度的具体计算方式会因不同的银行和金融机构而异，但通常包括以下几个方面：`<br>`1.个人信用记录：银行和金融机构通常会考虑客户的信用记录，包括借款还款记录、信用卡使用情况等，这些因素将直接影响到客户获得授信额度的概率。`<br>`2.收入水平：银行和金融机构通常会要求客户提供稳定的收入来源，例如工资收入、投资回报等。银行和金融机构会通过审核客户的收入证明和财务报告来确定客户的授信额度。`<br>`3.负债情况：银行和金融机构通常会关注客户的负债情况，包括其他未偿还贷款、信用卡欠款等。如果客户已经存在高额的负债负担，那么银行和金融机构可能会对其授信额度进行限制。`<br>`4.担保能力：如果客户没有良好的信用记录或者收入状况较差，银行和金融机构可能会要求客户提供担保，例如房产、车辆等财产作为担保，以提高授信额度的可能性。`<br>`总之，授信额度是一种重要的借贷工具，可以帮助客户在资金需求时更加灵活地应对各种场合。 |
| 你能解释一下什么是"抵押贷款"和"信用贷款"的区别吗？                                                                                                                                                                                       | 抵押贷款和信用贷款都是用于借款的方式，但它们之间的主要区别在于贷款金额、利率、还款期限以及担保方式。<br /><br />抵押贷款是指将财产（如房屋、车辆等）作为担保来获取贷款。在抵押贷款中，贷款金额通常是按照财产的价值计算的，因此贷款金额较大。此外，由于有抵押物作为担保，银行或金融机构通常会提供更低的利率。还款期限通常较长，因为贷款人需要足够的时间来还清贷款并归还抵押物。一旦借款人无法按时还款，银行或金融机构有权处置抵押物以收回欠款。<br /><br />信用贷款则是指根据个人信用记录、收入和支出情况等因素来决定是否给予贷款。在信用贷款中，银行或金融机构会基于个人的信用评分来决定贷款额度和利率。由于没有抵押品作为担保，因此贷款金额相对较小。还款期限较短，通常在6个月到3年之间，还款期数也较为灵活。如果借款人无法按时还款，银行或金融机构有权停止发放贷款。<br /><br />总之，抵押贷款和信用贷款的区别在于贷款金额、利率、还款期限和担保方式。选择哪种贷款方式取决于个人的财务状况和需求。                                                                                                                                                                                         |
| 你能解释一下什么是"银行业务的KYC"流程吗？                                                                                                                                                                                                | KYC是"Know Your Customer"的缩写，意思是了解您的客户。在银行业务中，KYC流程是指在客户开立银行账户之前，银行需要对客户进行身份验证和背景调查的过程。KYC流程的目的是确保客户的身份和财务状况真实可靠，并防止洗钱和恐怖主义融资等非法活动。<br /><br />KYC流程通常包括以下步骤：<br /><br />1. 客户身份验证：银行会要求客户提供身份证明文件，如身份证、护照等，并核实客户的身份信息是否真实有效。<br /><br />2. 客户背景调查：银行会对客户进行背景调查，了解客户的职业、收入来源、家庭状况等信息，以确认客户的财务状况是否真实可靠。<br /><br />3. 客户风险评估：银行会对客户进行风险评估，以确定客户的风险等级，并采取相应的风险控制措施。<br /><br />4. 客户反洗钱合规审查：银行会对客户进行反洗钱合规审查，以确保客户的交易行为合法合规，并防止洗钱和恐怖主义融资等非法活动。<br /><br />总之，KYC流程是银行业务中非常重要的一环，它确保了客户的身份和财务状况真实可靠，并防止了洗钱和恐怖主义融资等非法活动。                                                                                                                                                                                |
| "牛市"和"熊市"分别代表什么意思？它们对投资者有什么样的影响？                                                                                                                                                                             | 股票市场中的牛市和熊市是指股票价格的涨跌情况。牛市通常指股票价格持续上涨的情况，而熊市则指股票价格持续下跌的情况。<br /><br />对于投资者来说，牛市和熊市对他们的影响是不同的。在牛市中，投资者通常会感到乐观和兴奋，因为股票价格上涨，他们可以赚取更多的利润。在熊市中，投资者通常会感到悲观和沮丧，因为股票价格下跌，他们可能会损失更多的资金。<br /><br />在牛市中，投资者通常会采取积极的投资策略，例如购买更多的股票，以期获得更高的回报。在熊市中，投资者通常会采取保守的投资策略，例如减少股票投资，以降低风险。<br /><br />需要注意的是，牛市和熊市只是股票市场中的一种情况，投资者应该根据自己的投资目标和风险承受能力来选择合适的投资策略。在牛市中，投资者可以采取高风险高回报的投资策略，而在熊市中，投资者应该采取低风险低回报的投资策略。此外，投资者还应该密切关注市场动态，及时调整自己的投资策略，以适应市场的变化。                                                                                                                                                                                                                                                         |
| 欧洲央行（ECB）表示，将继续实施宽松的货币政策，以支持欧元区经济复苏。然而，通货膨胀压力和全球经济形势的不确定性给ECB的政策制定带来了挑战。请分析欧洲央行维持宽松货币政策的原因，以及这一政策可能对欧元区经济和全球金融市场产生哪些影响？ | 维持宽松货币政策的主要原因是欧洲央行希望通过降低利率和增加货币供应量来刺激经济增长和创造就业机会。此外，ECB还希望通过降低利率和增加货币供应量来控制通货膨胀压力。<br /><br />欧洲央行的宽松货币政策可能对欧元区经济和全球金融市场产生以下影响：<br /><br />1. 欧元区经济增长：ECB的宽松货币政策可能会刺激欧元区的经济增长，因为低利率和增加货币供应量可以促进投资和消费。<br /><br />2. 通货膨胀压力：ECB的宽松货币政策可能会导致通货膨胀压力增加，因为货币供应量增加可能导致物价上涨。<br /><br />3. 全球金融市场：ECB的宽松货币政策可能会对全球金融市场产生影响，因为欧洲央行的货币政策是全球货币政策的重要组成部分。ECB的宽松货币政策可能会导致美元贬值，从而对全球金融市场产生影响。<br /><br />总之，ECB的宽松货币政策可能会对欧元区经济和全球金融市场产生积极影响，但也需要注意通货膨胀压力和全球经济形势的不确定性所带来的挑战。                                                                                                                                                                                                                                                      |
| 全球各大央行纷纷推出量化宽松政策，以应对新冠疫情对经济的影响。然而，有观点认为，这些政策可能导致资产泡沫和通胀压力上升。请分析量化宽松政策可能导致的资产泡沫和通胀风险，以及政府和央行如何平衡经济复苏与通胀风险之间的关系？             | 量化宽松政策是指央行通过购买国债等金融资产来增加货币供应量，以刺激经济增长。然而，这些政策可能导致资产泡沫和通胀压力上升。<br /><br />首先，量化宽松政策可能导致资产泡沫。当央行购买国债等金融资产时，这些资产的价格可能会上涨，从而形成资产泡沫。如果资产泡沫破裂，可能会导致经济衰退和金融危机。<br /><br />其次，量化宽松政策可能导致通胀压力上升。当央行购买国债等金融资产时，这些资产的价格可能会上涨，从而导致物价上涨。如果通胀压力过高，可能会对经济造成负面影响。<br /><br />政府和央行如何平衡经济复苏与通胀风险之间的关系？<br /><br />政府和央行可以通过以下措施来平衡经济复苏与通胀风险之间的关系：<br /><br />1. 控制货币供应量。央行可以通过调整货币政策来控制货币供应量，从而控制通胀压力。<br /><br />2. 监管金融市场。政府可以通过监管金融市场来防止资产泡沫的形成。<br /><br />3. 调整利率政策。央行可以通过调整利率政策来控制通胀压力，从而平衡经济复苏与通胀风险之间的关系。                                                                                                                                                                                            |
| 如果一家公司的股票价格是每股100美元，而其每股派发的股息是5美元，那么其股息收益率是多少？                                                                                                                                                 | 股息收益率（dividend yield）是指公司每股派发的股息与股票价格之间的比率。计算股息收益率的公式为：股息收益率 = 每股派发的股息 ÷ 股票价格。<br /><br />根据题目，这家公司的股票价格是每股100美元，每股派发的股息是5美元。因此，这家公司的股息收益率为：<br /><br />股息收益率 = 每股派发的股息 ÷ 股票价格 = 5美元 ÷ 100美元 = 0.05 = 5%<br /><br />因此，这家公司的股息收益率为5%。这意味着，如果你持有这家公司的股票，你每年可以获得5美元的股息收益。<br /><br />需要注意的是，股息收益率只考虑了每股派发的股息和股票价格之间的关系，而没有考虑其他因素，如公司的盈利能力、市场前景等。因此，股息收益率只是一个参考指标，不能完全代表一家公司的投资价值。在做出投资决策时，还需要考虑其他因素，如公司的财务状况、行业前景等。                                                                                                                                                                                                                                                                                                                                                               |
| 如果一家公司的总资产为500亿美元，总负债为300亿美元，股东权益是多少？                                                                                                                                                                     | 股东权益可以通过总资产减去总负债来计算，即：<br /><br />股东权益 = 总资产 - 总负债<br /><br />根据题目中给出的数据，总资产为500亿美元，总负债为300亿美元，因此：<br /><br />股东权益 = 500亿美元 - 300亿美元 = 200亿美元<br /><br />因此，这家公司的股东权益为200亿美元。<br /><br />需要注意的是，股东权益并不等同于净资产。净资产是指公司的总资产减去总负债后的余额，即：<br /><br />净资产 = 总资产 - 总负债<br /><br />根据题目中给出的数据，总资产为500亿美元，总负债为300亿美元，因此：<br /><br />净资产 = 500亿美元 - 300亿美元 = 200亿美元<br /><br />因此，这家公司的净资产为200亿美元。<br /><br />需要注意的是，净资产并不等同于股东权益。股东权益是指公司归属于股东的所有权益，包括股本、资本公积、盈余公积、未分配利润等。而净资产是指公司的总资产减去总负债后的余额，包括股本、资本公积、盈余公积、未分配利润等。因此，股东权益和净资产是两个不同的概念。                                                                                                                                                                                                                     |
| 如果一家公司的总资产为200亿美元，总负债为100亿美元，那么其资产负债率是多少？                                                                                                                                                             | 资产负债率（debt-to-equity ratio）是指公司负债总额与股东权益总额的比率，通常用于衡量公司的财务风险和偿债能力。计算资产负债率的公式为：<br /><br />资产负债率 = 总负债 / 总资产<br /><br />根据题目给出的信息，这家公司的总资产为200亿美元，总负债为100亿美元，因此其资产负债率为：<br /><br />资产负债率 = 100亿美元 / 200亿美元 = 0.5 = 50%<br /><br />因此，这家公司的资产负债率为50%。资产负债率越高，表示公司负债越多，财务风险越大，偿债能力越弱。反之，资产负债率越低，表示公司负债越少，财务风险越小，偿债能力越强。<br /><br />需要注意的是，资产负债率并不是唯一的衡量公司财务风险和偿债能力的指标。其他指标，如流动比率、速动比率、利息保障倍数等，也可以用来评估公司的偿债能力和财务风险。同时，不同行业和不同类型的公司，其资产负债率和财务指标也会有所不同。因此，在评估公司的财务状况时，需要综合考虑多个指标和因素。                                                                                                                                                                                                                                                          |
| 请解释一下什么是股息收益率，它如何帮助我们评估一家公司的股息政策？                                                                                                                                                                       | 股息收益率（dividend yield）是指公司每年派发的股息金额与股票市价的比率，通常以百分比的形式表示。股息收益率可以帮助我们评估一家公司的股息政策。<br /><br />股息收益率越高，意味着公司每年派发的股息金额越多，相对于股票市价的比率也越高。因此，股息收益率越高，意味着投资者可以获得更高的股息收益。<br /><br />股息收益率可以帮助我们评估一家公司的股息政策。如果一家公司的股息收益率相对较高，那么这可能意味着该公司更注重股息派发，并希望通过股息来回报投资者。相反，如果一家公司的股息收益率相对较低，那么这可能意味着该公司更注重股票价格的上涨，并希望通过股票价格的上涨来回报投资者。<br /><br />需要注意的是，股息收益率只是评估一家公司股息政策的一个指标。投资者还需要考虑其他因素，例如公司的财务状况、行业前景、管理层能力等。因此，在评估一家公司的股息政策时，需要综合考虑多个因素，而不仅仅是股息收益率。                                                                                                                                                                                                                                                                       |

</details>

### 3.2. 通用领域效果评测

除了在金融领域的突出表现，轩辕还在通用处理能力方面表现优秀。我们利用由200道多元化问题构成的通用评测集，对轩辕在数学计算、场景写作、逻辑推理、文本摘要等13个主要维度的表现进行了评估，并将其与ChatGPT进行了对比。结果显示，轩辕在这个评测集上，有71%的问题表现不亚于ChatGPT，验证了其全方面能力。

<img width="481" alt="9038f05c34b82b3eae00603f6" src="https://github.com/Duxiaoman-DI/XuanYuan/assets/10808269/f85989c5-7e68-4fee-b9dc-39ef1c500c06">

## 4. 相关论文

如果有用到轩辕相关方法和模型，请引用以下论文：

[XuanYuan 2.0: A Large Chinese Financial Chat Model with Hundreds of Billions Parameters ](https://arxiv.org/abs/2305.12002)

[Self-QA: Unsupervised Knowledge Guided Language Model Alignment ](https://arxiv.org/abs/2305.11952)

[CGCE: A Chinese Generative Chat Evaluation Benchmark for General and Financial Domains](https://arxiv.org/abs/2305.14471)

## 5.使用说明

本模型推荐运行在8卡A100 GPU或同等配置下以获得最佳性能。

可以通过以下代码调用本模型：

```python
from transformers import AutoTokenizer, AutoModel
tokenizer = AutoTokenizer.from_pretrained("MODEL_NAME", trust_remote_code=True)
model = AutoModel.from_pretrained("MODEL_NAME", trust_remote_code=True)
```

【热门问题】如何调用轩辕模型？

由于本模型较大并不支持线上API测试，请下载模型后使用transformers库的AutoTokenizer和AutoModel进行调用。
轩辕对话模型的输入示例：

```text
BOS_TOKEN + "Human: " + query + "\n\nAssistant: "
```

轩辕对话模型的生成示例：

```python
output = model.generate(**input, do_sample=True, temperature=0.8, top_k=50, top_p=0.9, early_stopping=True, repetition_penalty=1.1, min_new_tokens=1, max_new_tokens=256)
```

# 免责声明与许可协议

对于轩辕模型生成的言论，我们不承担任何责任。使用者在将轩辕模型时，需要自行承担潜在的风险，并始终保持审慎。我们建议用户在使用模型输出的信息时，进行独立的验证和判断，并根据个人的需求和情境进行决策。我们希望通过轩辕的开源发布，为学术界和工业界提供一个有益的工具，并推动对话系统和金融技术的发展。
我们鼓励大家积极探索和创新，以进一步拓展和应用轩辕的潜力，并共同促进人工智能在金融领域的研究和实践。

# 总结

我们鼓励使用者在相关工作中引用轩辕，以促进知识的交流和分享，并推动中文金融对话系统的发展。轩辕的发布将为金融领域的应用和研究提供强大的支持，并为中文金融对话系统的发展做出重要贡献。我们期待看到更多的创新和应用，以提升金融服务和用户体验，并进一步推动人工智能技术在金融领域的发展。

![](resources/chat.jpeg)
