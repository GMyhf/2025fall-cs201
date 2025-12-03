# 人工智能概览

*Updated 2025-12-03 19:51 GMT+8*  
*Compiled by Hongfei Yan (2025 Summer)*    

https://github.com/GMyhf/2025fall-cs201/blob/main/AI_literacy.md



人工智能（AI）是研究和开发能够执行通常需要人类智能的任务的技术和方法的学科，包括语音识别、图像理解、自然语言处理、机器人等[1] [2]。早在1950年，艾伦·图灵提出了检验机器智能的“模仿游戏”（即**图灵测试**），检验机器是否能让人分不清其与人类对话的区别。1956年达特茅斯会议（**Dartmouth AI Workshop**）召开，被认为是人工智能领域的创始时刻，约翰·麦卡锡等人首次正式提出“人工智能”这一术语[1]。此后，AI发展经历了多次高潮与低谷，到21世纪依赖于强大的计算资源、海量数据和新算法的**深度学习**技术实现突破，推动AI进入广泛应用阶段。



# 1. AI三大流派

人工智能的发展思想分为三个主要流派：

- **符号主义（Symbolic AI）**：核心观点是通过符号表示和逻辑推理来实现智能。典型方法包括专家系统、搜索算法、逻辑推理（如一阶逻辑）、规划系统等。代表人物有艾伦·纽厄尔、赫伯特·西蒙、约翰·麦卡锡等。符号主义强调可解释性强，适用于有明确规则的任务（如数学推理、棋类游戏）。其代表成果包括20世纪80年代的专家系统（如DEC公司的XCON系统，显著提高了配置效率）以及IBM的棋类程序**深蓝（Deep Blue）**，1997年击败国际象棋冠军卡斯帕罗夫。但符号主义的缺点是学习能力弱，难以处理模糊信息，需要大量手工编码规则。

- **连接主义（Connectionism）**：核心观点是通过模拟人脑神经元网络结构来实现智能，依赖数据驱动学习。主要方法是各种人工神经网络（ANN）和深度学习（如卷积神经网络CNN、循环神经网络RNN、Transformer等）。代表人物包括Geoffrey Hinton、Yann LeCun、Ilya Sutskever、David Rumelhart等。约翰·霍普菲尔德（John Hopfield）与Geoffrey Hinton于2024年获得诺贝尔物理学奖，以表彰他们在神经网络领域的奠基性贡献。连接主义流派引领了近年来AI的主要突破（“强数据、弱规则”）。其代表成果包括最早的单层感知机（Perceptron，1958年）以及1986年Rumelhart等人提出的**误差反向传播算法**（Backpropagation），使多层神经网络得以高效训练。现代连接主义系统在图像识别、语音识别、自然语言处理、自动驾驶等领域均取得了巨大成功，例如Google的AlphaGo和各种视觉模型、OpenAI的GPT系列语言模型等[3]。
- **行为主义（Behaviorism）**：在AI领域常指“机器人行动派”或强化学习思想。其核心思想是智能体通过与环境交互并根据反馈（奖惩）自主学习，无需事先假设内部知识结构。代表人物有罗德尼·布鲁克斯（Rodney Brooks）、李开复等。行为主义AI强调“行动优先”，对现代机器人学和强化学习影响深远。典型应用是基于强化学习的系统，如**AlphaGo/AlphaZero**（通过自我博弈学习围棋策略）和自动驾驶等。行为主义流派下的智能体可视为通过试错和环境反馈来优化决策。



# 2. AI的“三要素”：算法、算力、数据

人工智能的发展依赖于三大要素：**算法**（Algorithm）、**算力**（Compute）和**数据**（Data）。

- **算法（灵魂）**：不同任务类型对应不同算法范式。常见分类包括监督学习（使用标注数据训练模型进行分类或回归）、无监督学习（从无标签数据中挖掘结构，如聚类）、强化学习（使用奖惩机制优化策略）。例如，逻辑回归用于分类（监督学习），KMeans用于聚类（无监督学习）。机器学习和深度学习的算法不断演进，引入了多层神经网络、注意力机制等创新架构。
- **算力（引擎）**：深度学习模型往往需要巨大的计算资源。GPU/TPU等高性能硬件使得训练大规模神经网络成为可能。以PyTorch为例，我们可以简单检测当前硬件环境中GPU或Apple MPS的可用性。
- **数据（燃料）**：训练模型需要大量高质量的数据。监督学习尤其依赖标注数据。例如，李飞飞等人在2006年发起的ImageNet计划收集了数千万张图像，并依托众包标注创造了包含1400万张标注图片的大型数据集，大大推动了计算机视觉算法的发展。与此同时，无标签数据也通过自动记录等方式提供了海量信息，可用于无监督学习。总之，算法、算力与数据三者共同构成AI系统的基础。



# 3. 前沿应用案例

- **智能博弈：AlphaGo/AlphaZero**：DeepMind的AlphaGo结合了深度卷积神经网络（CNN）、强化学习和蒙特卡洛树搜索（MCTS），成为首个战胜围棋人类冠军的AI系统。2016年AlphaGo以4:1击败李世石，2017年以3:0战胜柯洁。其强化学习版本AlphaGo Zero无需人类棋谱，从随机对弈中自学，经过数周训练便超越了原版AlphaGo。进一步的AlphaZero甚至能从零开始自学多种棋类（围棋、国际象棋、日本将棋等），展现出超强的策略学习能力。它证明了放弃人类经验、有条件的自我对弈（self-play）学习在某些领域能带来更优解。
- **自然语言处理：Transformer与GPT**：Transformer模型由Google研究者在2017年提出（著名论文*Attention Is All You Need*），其核心是**自注意力机制**，允许模型并行处理序列并捕捉远距离依赖[4]。Transformer架构广泛应用于大规模自然语言处理和其它领域，催生了众多预训练模型如GPT系列和BERT[4]。GPT（Generative Pre-trained Transformer）是OpenAI推出的一类语言模型，采用巨大的Transformer解码器结构进行无监督预训练后再微调。GPT-3于2020年问世，拥有约1750亿参数[2]，能够生成连贯流畅的文本，支持零样本学习（zero-shot）和少样本学习（few-shot），在翻译、对话、写作等任务中表现优异。**GPT-4**（2023年发布）在GPT-3.5基础上进一步扩展规模和能力，是一个支持文本和图像输入的**多模态大模型**[5] [3]。GPT-4在包括模拟律师资格考试（bar exam）在内的多项专业测试中表现出类人水平（成绩在前10%）[3]。与前代模型相比，GPT-4更加可靠、富有创造力，能够处理更复杂、更长的指令[5]。GPT系列模型被广泛应用于对话机器人、内容生成、编程辅助、教育辅导等场景。

**示例：使用预训练模型进行问答**。以Hugging Face Transformer为例，下述 `first_qa.py`代码载入本地中文预训练模型进行问答推理：



> | 模型                                     | 适用语言 | 用途     |
> | ---------------------------------------- | -------- | -------- |
> | `distilbert-base-cased-distilled-squad`  | 英文     | 英文问答 |
> | `uer/roberta-base-chinese-extractive-qa` | 中文     | 中文问答 |
>
> Q: 如何用**浏览器手动下载** `uer/roberta-base-chinese-extractive-qa` 模型，做到完全 **离线部署** 的步骤：
>
> 1. 打开模型页面
>
> 浏览器访问：https://huggingface.co/uer/roberta-base-chinese-extractive-qa
>
> 2. 进入 “Files and versions” 页面，手动下载以下几个关键文件：
>
> | 文件名                    | 说明                           |
>| ------------------------- | ------------------------------ |
> | `config.json`             | 模型结构配置                   |
> | `pytorch_model.bin`       | 模型权重（很大，400MB 左右）   |
> | `tokenizer_config.json`   | tokenizer 配置                 |
> | `vocab.txt`               | 中文词表（必需）               |
> | `special_tokens_map.json` | 特殊符号定义（可选但推荐）     |
> | `tokenizer.json`          | tokenizer 的二进制形式（可选） |
> 
> 你可以在网页中依次点击这些文件，然后点击右上角 “Download”。
>
> 
>
> 或者这里下载：
>
> https://disk.pku.edu.cn/link/AA5F507BA7BC504334ACA7FCBECFE64995
>Name: model-roberta-chinese-qa.zip
> Expires: Never
> Pickup Code: zXih



我的clab云虚拟机beijing.zhengmao.ltd，`AI_literacy`文件夹

```
[rocky@jensen AI_literacy]$ tree
.
├── first_qa.py
└── models
    └── roberta-chinese-qa
        ├── config.json
        ├── pytorch_model.bin
        ├── special_tokens_map.json
        ├── tokenizer_config.json
        └── vocab.txt

```



**创建独立的虚拟环境 & 安装 深度学习框架 PyTorch**

> 为每个项目创建独立的虚拟环境，避免依赖冲突。
>
> ```
> cd ~/AI_literacy  # 替换为你的项目路径
> python3 -m venv .venv
> source .venv/bin/activate
> ```
>
> > 退出虚拟环境命令：`deactivate`
>
> 
>
> 安装 深度学习框架 PyTorch  
> pip install -U transformers  
> pip install torch



`first_qa.py`

```python
from transformers import pipeline

qa = pipeline(
    "question-answering",
    #model="./models/distilbert-base-cased-distilled-squad",
    model="./models/roberta-chinese-qa",
    tokenizer="./models/roberta-chinese-qa",
    framework="pt"  # 显式要求使用 PyTorch
)

result = qa(
    question="谁是人工智能之父？",
    context="艾伦·图灵是人工智能之父，被誉为计算机科学的奠基人。"
)

print(result)       # 看完整结果
print(result["answer"])  # 输出应为：艾伦·图灵
```

上述代码中，指定了本地下载的中文问答模型目录，通过pipeline接口直接进行抽取式问答推理。在真实应用中，可替换为更强大的模型（如GPT-4）并结合语言提示（Prompt）实现更复杂的自然语言任务。

运行结果展示

```
(.venv) [rocky@jensen AI_literacy]$ python first_qa.py 
Device set to use cpu
{'score': 0.31832563877105713, 'start': 0, 'end': 5, 'answer': '艾伦·图灵'}
艾伦·图灵
```



> 用一个本地的中文问答模型，在一段文本里提取问题的答案。
>
> 1. 引入 Hugging Face 的 `pipeline`
>
> ```python
>from transformers import pipeline
> ```
> 
> 这是 Hugging Face `transformers` 提供的简洁 API，用于快速构建 NLP 任务管道，例如文本分类、问答、翻译等。
>
> 
>
> 2. 构造问答任务的 pipeline（使用本地模型）
>
> ```python
>qa = pipeline(
>  "question-answering",
>  #model="./distilbert-base-cased-distilled-squad",
>     model="./roberta-chinese-qa",      # 使用本地中文模型目录
>     framework="pt"                     # 强制使用 PyTorch
>    )
>    ```
> 
> 参数说明：
>
> | 参数                           | 含义                                                         |
>| ------------------------------ | ------------------------------------------------------------ |
> | `"question-answering"`         | 指定任务类型是抽取式问答（extractive QA）                    |
> | `model="./roberta-chinese-qa"` | 指向本地下载的模型文件夹，里面包含 `pytorch_model.bin`、`config.json` 等 |
> | `framework="pt"`               | 显式要求使用 PyTorch，而不是 TensorFlow，防止意外加载 TF 模型引发错误 |
> 
> `tokenizer` 会自动从模型目录中加载，无需单独指定。
>
> ------
>
> 3. 运行问答推理
>
> ```python
>result = qa(
>  question="谁是人工智能之父？",
>  context="艾伦·图灵是人工智能之父，被誉为计算机科学的奠基人。"
>    )
>    ```
> 
> 说明：
>
> - 输入的 `question` 是用户要问的问题；
>- `context` 是包含答案的上下文文本（模型会在里面查找答案）；
> - 返回的是一个包含 **预测答案位置、内容、置信度** 的字典结构。
> 
> 
>
> 🛠 常见补充建议：
>
> - **更复杂 context**：你可以给它更多段落，它会找最有可能的答案；
>
> - **中文精度提高**：你可以尝试 `hfl/chinese-roberta-wwm-ext-large` 之类的模型；
>
> 



# 4. 深度学习与神经网络

深度学习是连接主义流派的核心方法之一，其核心思想是利用**多层神经网络**自动从数据中学习层次化的特征表示。本节将系统介绍神经网络的关键训练机制——**反向传播算法**，并结合5个由浅入深的PyTorch实战示例，帮助读者掌握从基础建模到复杂图像分类任务的完整流程。



**神经网络与反向传播**

**反向传播（Backpropagation）** 是训练神经网络的基石算法。它通过两个阶段协同工作： 

1. **前向传播**：输入数据逐层经过加权求和与非线性激活函数（如 ReLU、Softmax），最终输出预测结果； 
2. **反向传播**：基于损失函数（如交叉熵、均方误差）计算预测值与真实标签之间的误差，并利用**链式法则**高效地计算损失对每一层参数的梯度。

随后，优化器（如 SGD、Adam）依据这些梯度更新网络权重，目标是最小化整体损失。这一机制使得训练包含数十甚至上百层的深度网络成为可能，直接推动了深度学习的爆发式发展。

**反向传播算法流程**

1. **前向传播**：输入 → 逐层计算 → 输出预测值 $\hat{y}$ 
2. **损失计算**：$L = \text{Loss}(\hat{y}, y)$ 
3. **梯度反传**：从输出层向输入层，逐层计算 $\frac{\partial L}{\partial w}$ 和 $\frac{\partial L}{\partial b}$ 
4. **参数更新**：例如使用梯度下降：
   $$ w \leftarrow w - \eta \cdot \frac{\partial L}{\partial w} $$
   其中 $\eta$ 为学习率。 
5. **迭代训练**：遍历训练集多个 epoch，直至损失收敛或达到预设轮次。

> ⚠️ **注意**：深层网络易遭遇**梯度消失**（vanishing gradients）或**梯度爆炸**（exploding gradients）问题，尤其在使用 Sigmoid 或 Tanh 激活函数时。现代实践中常采用 **ReLU 激活函数**、**批归一化（BatchNorm）** 和**残差连接（ResNet）** 等技术加以缓解。



**交互可视化：理解神经网络**

Google 提供了一个优秀的交互式神经网络训练工具，帮助直观理解模型如何分离非线性可分数据：

https://developers.google.com/machine-learning/crash-course/neural-networks/interactive-exercises?hl=zh-cn

**任务目标**：配置一个神经网络，使其能够将下图中的橙点与蓝点分开，并在训练数据和测试数据上实现低于 0.2 的损失。

**操作指南：**

1. 调整网络结构：
   - 点击 **HIDDEN LAYERS** 左侧的 **+ / –** 添加/删除隐藏层；
   - 点击某隐藏层上方的 **+ / –** 调整该层神经元数量。
2. 修改超参数：
   - 从 **Learning rate** 下拉菜单选择合适的学习率（建议尝试 0.01 ~ 0.1）；
   - 从 **Activation** 下拉菜单选择激活函数（推荐 **ReLU**）。
3. 点击 ▶️ 开始训练，观察损失曲线与决策边界演化。
4. 若未达标，点击 **Reset** 并尝试新配置。

**成功示例截图如下**（损失均低于 0.2）：

<img src="https://raw.githubusercontent.com/GMyhf/img/main/img/6e8ec7f85c470b44edc373985d94337c.png" alt="6e8ec7f85c470b44edc373985d94337c" style="zoom: 50%;" />



**PyTorch 实战：5 个神经网络应用示例**

以下示例涵盖从手动实现到现代架构的完整演进路径。后四个示例使用PyTorch编写， 教程在 https://www.runoob.com/pytorch/pytorch-tutorial.html 或参看附录 A。

| 编号 | 示例名称                     | 内容概述                                          | 技术要点                                   |
| ---- | ---------------------------- | ------------------------------------------------- | ------------------------------------------ |
| 1    | `0_xor_bp_neural_net_manual` | 手动实现反向传播，解决 XOR 非线性分类问题         | 张量运算、梯度手动计算、无框架依赖         |
| 2    | `1_iris_neural_network`      | 使用全连接网络对鸢尾花数据集进行三分类            | 数据加载、`nn.Module`、交叉熵损失          |
| 3    | `2_mnist_resnet18`           | 微调 ResNet18 对 MNIST 手写数字分类               | 迁移学习、图像预处理、`torchvision.models` |
| 4    | `3_cifar10_resnet18`         | 在 CIFAR-10 上训练 ResNet18                       | 数据增强、学习率调度、GPU 加速             |
| 5    | `4_tiny_imagenet_resnet50`   | 使用 ResNet50 处理更复杂的 Tiny ImageNet 分类任务 | 大规模数据处理、模型微调、性能评估         |

> 所有代码均可在配套仓库（https://github.com/GMyhf/2025spring-cs201/tree/main/LLM）中找到，建议按顺序实践，逐步掌握从“理解原理”到“工程部署”的完整技能链。



## 4.1 在异或问题（XOR）中手动实现反向传播

异或问题是经典的非线性可分问题，用来演示神经网络的学习能力。一个简单的神经网络可手动实现反向传播来解决异或。以下先给出简洁的伪代码，再给出可以运行的Python代码示例展示了反向传播更新权重的方式：

```python
# 假设网络结构：输入层2个节点，隐藏层2个节点，输出层1个节点
# 初始化权重
W1 = random([...])  # 输入到隐藏层
W2 = random([...])  # 隐藏层到输出层
learning_rate = 0.1

for epoch in range(epochs):
    # 前向计算
    hidden = sigmoid(X @ W1)       # X为输入[四组XOR输入]
    output = sigmoid(hidden @ W2)  # 预测
    # 计算误差
    error = (y - output)           # y为真实标签
    # 反向传播（链式法则）
    dW2 = hidden.T @ (error * output * (1 - output))
    dW1 = X.T @ ((error * output * (1 - output)) @ W2.T * hidden * (1 - hidden))
    # 更新权重
    W2 += learning_rate * dW2
    W1 += learning_rate * dW1

```



Backpropagation in Neural Network

https://www.geeksforgeeks.org/machine-learning/backpropagation-in-neural-network/



反向传播（Back Propagation），又称为“误差的反向传播”，是一种用于训练神经网络的方法。其目标是通过调整网络中的权重（weights）和偏置（biases），来减小模型预测输出与实际输出之间的差异。

它通过迭代方式更新权重和偏置，以最小化损失函数（cost function）。在每一个训练周期（epoch）中，模型会根据误差梯度（error gradient）更新参数，常用的优化算法包括梯度下降（Gradient Descent）或随机梯度下降（SGD）。该算法使用微积分中的<mark>链式法则</mark>来计算梯度，从而能够有效地穿越复杂的神经网络结构，优化损失函数。

> Back Propagation is also known as "Backward Propagation of Errors" is a method used to train neural network . Its goal is to reduce the difference between the model’s predicted output and the actual output by adjusting the weights and biases in the network.
>
> It works iteratively to adjust weights and bias to minimize the cost function. In each epoch the model adapts these parameters by reducing loss by following the error gradient. It often uses optimization algorithms like **gradient descent** or **stochastic gradient descent**. The algorithm computes the gradient using the chain rule from calculus allowing it to effectively navigate complex layers in the neural network to minimize the cost function.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20250701163824448467/Backpropagation-in-Neural-Network-1.webp" alt="Backpropagation-in-Neural-Network-1" style="zoom:67%;" />

<center>A simple illustration of how the backpropagation works by adjustments of weights</center>

<center>通过权重调整，简单展示反向传播的工作方式</center>



**反向传播的重要性：**

- **高效的权重更新**：利用链式法则计算损失函数对每个权重的梯度，从而高效地更新参数。
- **良好的扩展性**：适用于多层结构和复杂架构，是深度学习可行的核心算法。
- **自动学习能力**：训练过程自动进行，模型会不断调整自身来优化性能。

> **Back Propagation** plays a critical role in how neural networks improve over time. Here's why:
>
> 1. **Efficient Weight Update**: It computes the gradient of the loss function with respect to each weight using the chain rule making it possible to update weights efficiently.
> 2. **Scalability**: The Back Propagation algorithm scales well to networks with multiple layers and complex architectures making deep learning feasible.
> 3. **Automated Learning**: With Back Propagation the learning process becomes automated and the model can adjust itself to optimize its performance.



### 4.1.1 反向传播算法的工作流程

反向传播算法包括两个主要步骤：**前向传播（Forward Pass）** 和 **反向传播（Backward Pass）**

#### 1. 前向传播

输入数据从输入层开始，经过带权重的连接传递到隐藏层。例如，一个有两个隐藏层 h1 和 h2 的网络中，h1 的输出作为 h2 的输入。在应用激活函数前，还会加上偏置项。

每一层都会计算输入的加权和（记作 `a`），再通过如 ReLU 等激活函数得到输出 `o`。最终，输出层通常会使用 softmax 激活函数将结果转换为分类概率。

> ### Working of Back Propagation Algorithm
>
> The Back Propagation algorithm involves two main steps: the **Forward Pass** and the **Backward Pass**.
>
> ### 1. Forward Pass Work
>
> In **forward pass** the input data is fed into the input layer. These inputs combined with their respective weights are passed to hidden layers. For example in a network with two hidden layers (h1 and h2) the output from h1 serves as the input to h2. Before applying an activation function, a bias is added to the weighted inputs.
>
> Each hidden layer computes the weighted sum (`a`) of the inputs then applies an activation function like [**ReLU (Rectified Linear Unit)**](https://www.geeksforgeeks.org/deep-learning/relu-activation-function-in-deep-learning/) to obtain the output (`o`). The output is passed to the next layer where an activation function such as [**softmax**](https://www.geeksforgeeks.org/deep-learning/the-role-of-softmax-in-neural-networks-detailed-explanation-and-applications/) converts the weighted outputs into probabilities for classification.

<img src="https://raw.githubusercontent.com/GMyhf/img/main/img/Backpropagation-in-Neural-Network-2.webp" alt="Backpropagation-in-Neural-Network-2" style="zoom:67%;" />

<center>The forward pass using weights and biases</center>

> h1,h2，表示隐藏层的两个神经元



#### 2. Backward Pass反向传播

反向传播阶段会将预测输出与实际输出的误差向后传递，并调整每一层的权重和偏置。常见的误差计算方法是**均方误差（MSE）**：

$MSE = (\text{Predicted Output} − \text{Actual Output})^2$

在误差计算之后，通过链式法则计算梯度，这些梯度用于指导权重和偏置的更新方向和幅度。反向传播过程是逐层执行的，<mark>激活函数的导数在梯度计算中起着关键作用</mark>。



**反向传播的示例：机器学习中的案例**

假设我们使用 sigmoid 激活函数，目标输出为 0.5，学习率为 1。

> #### 2. Backward Pass
>
> In the backward pass the error (the difference between the predicted and actual output) is propagated back through the network to adjust the weights and biases. One common method for error calculation is the [**Mean Squared Error (MSE)**](https://www.geeksforgeeks.org/maths/mean-squared-error/) given by:
>
> $MSE = (\text{Predicted Output} − \text{Actual Output})^2$
>
> Once the error is calculated the network adjusts weights using **gradients** which are computed with the chain rule. These gradients indicate how much each weight and bias should be adjusted to minimize the error in the next iteration. The backward pass continues layer by layer ensuring that the network learns and improves its performance. The activation function through its derivative plays a crucial role in computing these gradients during Back Propagation.
>
> 
>
> **Example of Back Propagation in Machine Learning**
>
> Let’s walk through an example of Back Propagation in machine learning. Assume the neurons use the sigmoid activation function for the forward and backward pass. The target output is 0.5 and the learning rate is 1.

<img src="https://raw.githubusercontent.com/GMyhf/img/main/img/Backpropagation-in-Neural-Network-3.webp" alt="Backpropagation-in-Neural-Network-3" style="zoom:67%;" />

<center>Example (1) of backpropagation sum</center>



### 4.1.2 前向传播

#### 1. 初始计算

The weighted sum at each node is calculated using:

> $a_j=\sum(w_{i,j}∗x_i)$

Where,

- $a_j$ is the weighted sum of all the inputs and weights at each node
- $w_{i,j}$ represents the weights between the $i^{th}$ input and the $j^{th}$ neuron
- $x_i$ represents the value of the $i^{th}$ input

`O (output):`After applying the activation function to `a`, we get the output of the neuron:

> $o_j = \text{activation function}(a_j)$

#### 2. Sigmoid函数

The sigmoid function returns a value between 0 and 1, introducing non-linearity into the model.

> $y_j = \frac{1}{1+e^{−a_j}}$ 

<img src="https://raw.githubusercontent.com/GMyhf/img/main/img/Backpropagation-in-Neural-Network-4.webp" alt="Backpropagation-in-Neural-Network-4" style="zoom:67%;" />

<center>To find the outputs of y3, y4 and y5</center>



#### 3. 输出计算

h1 节点：
$$
a_1 = (w_{1,1} \times x_1) + (w_{2,1} \times x_2)
$$

$$
a_1 = (0.2 \times 0.35) + (0.2 \times 0.7) = 0.21
$$

计算完 $a_1$ 后，我们可以继续计算 $y_3$ 的值：

$$
y_j = F(a_j) = \frac{1}{1 + e^{-a_1}}
$$

$$
y_3 = F(0.21) = \frac{1}{1 + e^{-0.21}} = 0.56
$$



h2 节点：
$$
a_2 = (w_{1,2} \times x_1) + (w_{2,2} \times x_2) = (0.3 \times 0.35) + (0.3 \times 0.7) = 0.315
$$

$$
y_4 = F(0.315) = \frac{1}{1 + e^{-0.315}} = 0.578
$$



输出节点 O3：
$$
a_3 = (w_{1,3} \times y_3) + (w_{2,3} \times y_4) = (0.3 \times 0.56) + (0.9 \times 0.58) = 0.702
$$

$$
y_5 = F(0.702) = \frac{1}{1 + e^{-0.702}} = 0.67
$$



> At h1 node
>
> Once we calculated the a1 value, we can now proceed to find the y3 value:
>
> Similarly find the values of y4 at h2 and y5 at O3



<img src="https://raw.githubusercontent.com/GMyhf/img/main/img/Backpropagation-in-Neural-Network-5.webp" alt="Backpropagation-in-Neural-Network-5" style="zoom:67%;" />

<center>Values of y3, y4 and y5</center>



#### 4. 误差计算

Our actual output is 0.5 but we obtained 0.67**.** To calculate the error we can use the below formula:

> $Error_j=y_{target}−y_5$ 

=> 0.5−0.67=−0.17

Using this error value we will be backpropagating.



### 4.1.3 反向传播

#### 1. Calculating Gradients计算梯度

The change in each weight is calculated as:

> $Δw_{ij}=η×δ_j×O_j$

Where:

- $δ_j$ is the error term for each unit,
- $η$ is the learning rate.

#### 2. Output Unit Error输出层误差

For O3:

> $δ_5=y_5(1−y_5)(y_{target}−y_5)$

=0.67(1−0.67)(−0.17)=−0.0376

#### 3. Hidden Unit Error隐藏层误差

For h1:

> $δ_3=y_3(1−y_3)(w_{1,3}×δ_5)$

=0.56(1−0.56)(0.3×−0.0376)=−0.0027



For h2:

> $δ_4=y_4(1−y_4)(w_{2,3}×δ_5)$

=0.59(1−0.59)(0.9×−0.0376)=−0.0819



#### 4. Weight Updates权重更新

For the weights from hidden to output layer:

> $Δw_{2,3}=1×(−0.0376)×0.59=−0.022184$

New weight:

> $w_{2,3}(new)=−0.022184+0.9=0.877816$

For weights from input to hidden layer:

> $Δw_{1,1}=1×(−0.0027)×0.35=0.000945$

New weight:

> $w_{1,1}(new)=0.000945+0.2=0.200945$

Similarly other weights are updated:

- $w_{1,2}(new)=0.273225$
- $w_{1,3}(new)=0.086615$
- $w_{2,1}(new)=0.269445$
- $w_{2,2}(new)=0.18534$

The updated weights are illustrated below

<img src="https://raw.githubusercontent.com/GMyhf/img/main/img/Backpropagation-in-Neural-Network-5-20251127160556998.webp" alt="Backpropagation-in-Neural-Network-5" style="zoom:67%;" />

<center>Through backward pass the weights are updated</center>

> 上图权重没有更新，例如：$w_{2,2}$应该更新为0.18534



After updating the weights the forward pass is repeated yielding:

- y3=0.57
- y4=0.56
- y5=0.61

仍未达到目标值 0.5，因此继续进行反向传播，直到收敛。

> Since y5=0.61 is still not the target output the process of calculating the error and backpropagating continues until the desired output is reached.



This process demonstrates how Back Propagation iteratively updates weights by minimizing errors until the network accurately predicts the output.

> $Error=y_{target}−y_5$

=0.5−0.61=−0.11=0.5−0.61=−0.11

This process is said to be continued until the actual output is gained by the neural network.



### 4.1.4 用于 XOR 问题的反向传播实现

**Q: XOR 问题是什么？**

> XOR（异或）是一个经典的逻辑问题，它的输入输出如下：
>
> | 输入 A | 输入 B | 输出 |
> | ------ | ------ | ---- |
> | 0      | 0      | 0    |
> | 0      | 1      | 1    |
> | 1      | 0      | 1    |
> | 1      | 1      | 0    |
>
> 这个问题**不能用一条直线分开**（不是线性可分的），所以单层感知机无法解决，必须用**至少一个隐藏层的神经网络**。



> “**单层感知机**”（Single-Layer Perceptron）是神经网络最原始、最简单的形式，由 Frank Rosenblatt 在 1957 年提出。理解它，有助于明白为什么像 **XOR 这样的问题无法被它解决**，从而引出多层神经网络和反向传播的必要性。
>
> 单层感知机结构：
>
> - **输入层**：接收特征（比如 $x_1, x_2$）
> - **输出层**：**直接输出结果**（没有隐藏层！）
> - 每个输入有一个对应的权重 $w_1, w_2$，还有一个偏置 $b$
>
> **数学表达：**
> $$
> z = w_1 x_1 + w_2 x_2 + b
> \nonumber
> $$
>
> $$
> \text{output} = \begin{cases} 1 & \text{if } z \geq 0 \\ 0 & \text{if } z < 0 \end{cases}
> \nonumber
> $$
>
> > 注意：**没有激活函数（或只有阶跃函数）**，**没有隐藏层**，所以叫“单层”。
> >
> > 阶跃函数是“硬判决”，适合理论分析；但因为不可导，不能用于现代神经网络的训练。
>
> ------
>
> **单层感知机能做什么**？
>
> 它只能解决 **线性可分**（linearly separable）的问题。
>
> **例子：AND 门**
>
> | x₁   | x₂   | y    |
> | ---- | ---- | ---- |
> | 0    | 0    | 0    |
> | 0    | 1    | 0    |
> | 1    | 0    | 0    |
> | 1    | 1    | 1    |
>
> 可以用一条直线分开 0 和 1 → **线性可分** → **单层感知机可以学会**
>
> 比如：
> 取 (w_1 = 1, w_2 = 1, b = -1.5)
> 则：
>
> - (0+0-1.5 = -1.5 < 0 → 0)
> - (1+1-1.5 = 0.5 ≥ 0 → 1)
>
> 完美！
>
> ------
>
> **单层感知机不能做什么？**
>
> **XOR 问题（异或）：**
>
> | x₁   | x₂   | y    |
> | ---- | ---- | ---- |
> | 0    | 0    | 0    |
> | 0    | 1    | 1    |
> | 1    | 0    | 1    |
> | 1    | 1    | 0    |
>
> 在二维平面上画出来：
>
> ```
> (0,1) ● (y=1)        (1,1) ○ (y=0)
> 
> (0,0) ○ (y=0)        (1,0) ● (y=1)
> ```
>
> 你会发现：**无法用一条直线把 ● 和 ○ 完全分开**！
>
> → 这就是 **非线性可分问题**。
>
> **结论**： 
>
> > **单层感知机无法解决 XOR 问题**，因为它缺乏非线性表达能力。
>
> ------
>
> ** 那怎么办？——引入隐藏层！**
>
> 1969 年，Minsky 和 Papert 在《Perceptrons》一书中指出了这个局限，导致神经网络研究一度停滞。
>
> 直到后来人们发现：
>
> > **只要加一个隐藏层，并使用非线性激活函数（如 sigmoid、ReLU），神经网络就能逼近任意函数**（万能近似定理）。
>
> 于是，**多层感知机**（MLP） + **反向传播** 成为解决方案。
>
> ------
>
> **🔄 对比总结**
>
> | 特性                | 单层感知机         | 多层感知机（带反向传播） |
> | ------------------- | ------------------ | ------------------------ |
> | 隐藏层              | ❌ 没有             | ✅ 有（至少1层）          |
> | 激活函数            | 阶跃函数（不可导） | Sigmoid / ReLU（可导）   |
> | 能否解决 AND/OR/NOT | ✅ 可以             | ✅ 可以                   |
> | 能否解决 XOR        | ❌ 不行             | ✅ 可以                   |
> | 是否支持反向传播    | ❌ 不支持（不可导） | ✅ 支持                   |
> | 学习能力            | 仅线性分类         | 非线性建模               |
>
> ------
>
> 小知识
>
> - “感知机”（Perceptron）通常特指**单层、使用阶跃激活、用感知机学习规则更新权重**的模型。
> - 而我们今天说的“神经网络”，一般指**多层、可微激活、用梯度下降+反向传播训练**的模型，也叫 **多层感知机**（MLP），尽管名字里有“感知机”，但已经完全不同了。
>
> 



以下代码演示了如何在神经网络中使用反向传播来解决 XOR 问题。该神经网络包含：

> This code demonstrates how Back Propagation is used in a neural network to solve the XOR problem. The neural network consists of:
>

#### 1. 定义神经网络结构

输入层：2个节点，隐藏层：4个神经元，输出层：1个神经元，激活函数：Sigmoid

> We define a neural network as Input layer with 2 inputs, Hidden layer with 4 neurons, Output layer with 1 output neuron and use **Sigmoid** function as activation function.

- **self.input_size = input_size**: stores the size of the input layer
- **self.hidden_size = hidden_size:** stores the size of the hidden layer
- **self.weights_input_hidden = np.random.randn(self.input_size, self.hidden_size)**: initializes weights for input to hidden layer
- **self.weights_hidden_output = np.random.randn(self.hidden_size, self.output_size)**: initializes weights for hidden to output layer
- **self.bias_hidden = np.zeros((1, self.hidden_size)):** initializes bias for hidden layer
- **self.bias_output = np.zeros((1, self.output_size)):** initializes bias for output layer



```python3
import numpy as np


class NeuralNetwork:
    def __init__(self, input_size, hidden_size, output_size):
        self.input_size = input_size
        self.hidden_size = hidden_size
        self.output_size = output_size

        self.weights_input_hidden = np.random.randn(
            self.input_size, self.hidden_size)
        self.weights_hidden_output = np.random.randn(
            self.hidden_size, self.output_size)

        self.bias_hidden = np.zeros((1, self.hidden_size))
        self.bias_output = np.zeros((1, self.output_size))

    def sigmoid(self, x):
        return 1 / (1 + np.exp(-x))

    def sigmoid_derivative(self, x):
        return x * (1 - x)
```



#### 2. 定义前向传播

In Forward pass inputs are passed through the network activating the hidden and output layers using the sigmoid function.

- **self.hidden_activation = np.dot(X, self.weights_input_hidden) + self.bias_hidden**: calculates activation for hidden layer
- **self.hidden_output= self.sigmoid(self.hidden_activation)**: applies activation function to hidden layer
- **self.output_activation= np.dot(self.hidden_output, self.weights_hidden_output) + self.bias_output:** calculates activation for output layer
- **self.predicted_output = self.sigmoid(self.output_activation):** applies activation function to output layer





```python3
def feedforward(self, X):
    self.hidden_activation = np.dot(
        X, self.weights_input_hidden) + self.bias_hidden
    self.hidden_output = self.sigmoid(self.hidden_activation)

    self.output_activation = np.dot(
        self.hidden_output, self.weights_hidden_output) + self.bias_output
    self.predicted_output = self.sigmoid(self.output_activation)

    return self.predicted_output
```



#### 3. 定义反向传播

In Backward pass or Back Propagation the errors between the predicted and actual outputs are computed. The gradients are calculated using the derivative of the sigmoid function and weights and biases are updated accordingly.

- **output_error = y - self.predicted_output:** calculates the error at the output layer
- **output_delta = output_error * self.sigmoid_derivative(self.predicted_output):** calculates the delta for the output layer
- **hidden_error = np.dot(output_delta, self.weights_hidden_output.T):** calculates the error at the hidden layer
- **hidden_delta = hidden_error \* self.sigmoid_derivative(self.hidden_output):** calculates the delta for the hidden layer
- **self.weights_hidden_output += np.dot(self.hidden_output.T, output_delta) * learning_rate:** updates weights between hidden and output layers
- **self.weights_input_hidden += np.dot(X.T, hidden_delta) * learning_rate:** updates weights between input and hidden layers



```python3
def backward(self, X, y, learning_rate):
    output_error = y - self.predicted_output
    output_delta = output_error * \
        self.sigmoid_derivative(self.predicted_output)

    hidden_error = np.dot(output_delta, self.weights_hidden_output.T)
    hidden_delta = hidden_error * self.sigmoid_derivative(self.hidden_output)

    self.weights_hidden_output += np.dot(self.hidden_output.T,
                                         output_delta) * learning_rate
    self.bias_output += np.sum(output_delta, axis=0,
                               keepdims=True) * learning_rate
    self.weights_input_hidden += np.dot(X.T, hidden_delta) * learning_rate
    self.bias_hidden += np.sum(hidden_delta, axis=0,
                               keepdims=True) * learning_rate
```



#### 4. 训练网络

The network is trained over 10,000 epochs using the Back Propagation algorithm with a learning rate of 0.1 progressively reducing the error.

- **output = self.feedforward(X):** computes the output for the current inputs
- **self.backward(X, y, learning_rate):** updates weights and biases using Back Propagation
- **loss = np.mean(np.square(y - output)):** calculates the mean squared error (MSE) loss



```python3
def train(self, X, y, epochs, learning_rate):
    for epoch in range(epochs):
        output = self.feedforward(X)
        self.backward(X, y, learning_rate)
        if epoch % 4000 == 0:
            loss = np.mean(np.square(y - output))
            print(f"Epoch {epoch}, Loss:{loss}")
```

#### 5. 测试神经网络

- **X = np.array([[0, 0], [0, 1], [1, 0], [1, 1]]):** defines the input data
- **y = np.array([[0], [1], [1], [0]]):** defines the target values
- **nn = NeuralNetwork(input_size=2, hidden_size=4, output_size=1):** initializes the neural network
- **nn.train(X, y, epochs=10000, learning_rate=0.1):** trains the network
- **output = nn.feedforward(X):** gets the final predictions after training





```python3
X = np.array([[0, 0], [0, 1], [1, 0], [1, 1]])
y = np.array([[0], [1], [1], [0]])

nn = NeuralNetwork(input_size=2, hidden_size=4, output_size=1)
nn.train(X, y, epochs=10000, learning_rate=0.1)

output = nn.feedforward(X)
print("Predictions after training:")
print(output)
```

**Output:**

![Screenshot-2025-03-07-130223](https://raw.githubusercontent.com/GMyhf/img/main/img/Screenshot-2025-03-07-130223.png)

<center>Trained Model</center>



训练初期损失为 0.2713，逐步下降到 0.0066（第8000轮）。最终模型可以很好地逼近 XOR 函数的输出，即：

- 对于输入 [0,0] 和 [1,1]，输出接近 0

- 对于输入 [0,1] 和 [1,0]，输出接近 1

  

> - The output shows the training progress of a neural network over 10,000 epochs. Initially the loss was high (0.2713) but it gradually decreased as the network learned reaching a low value of 0.0066 by epoch 8000.
> - The final predictions are close to the expected XOR outputs: approximately 0 for [0, 0] and [1, 1] and approximately 1 for [0, 1] and [1, 0] indicating that the network successfully learned to approximate the XOR function.



### 4.1.5 反向传播的优点

**易于实现**：适合初学者，无需太多神经网络背景

**结构简单，灵活应用**：从简单前馈到复杂卷积/循环网络都可使用

**高效**：直接根据误差更新权重，学习速度快

**良好的泛化能力**：有助于模型在新数据上表现更好

**可扩展性好**：适用于大型数据集和深层模型

> **Advantages of Back Propagation for Neural Network Training**
>
> The key benefits of using the Back Propagation algorithm are:
>
> 1. **Ease of Implementation:** Back Propagation is beginner-friendly requiring no prior neural network knowledge and simplifies programming by adjusting weights with error derivatives.
> 2. **Simplicity and Flexibility:** Its straightforward design suits a range of tasks from basic feedforward to complex convolutional or recurrent networks.
> 3. **Efficiency**: Back Propagation accelerates learning by directly updating weights based on error especially in deep networks.
> 4. **Generalization:** It helps models generalize well to new data improving prediction accuracy on unseen examples.
> 5. **Scalability:** The algorithm scales efficiently with larger datasets and more complex networks making it ideal for large-scale tasks.



### 4.1.6 反向传播面临的挑战

**梯度消失**：在深层网络中梯度可能过小，导致学习困难（特别是在使用 sigmoid/tanh 时）

**梯度爆炸**：梯度可能变得过大，使训练不稳定

**过拟合**：模型结构过于复杂时，可能记住训练集而非学习一般性规律

> **Challenges with Back Propagation**
>
> While Back Propagation is useful it does face some challenges:
>
> 1. **Vanishing Gradient Problem**: In deep networks the gradients can become very small during Back Propagation making it difficult for the network to learn. This is common when using activation functions like sigmoid or tanh.
> 2. **Exploding Gradients**: The gradients can also become excessively large causing the network to diverge during training.
> 3. **Overfitting:** If the network is too complex it might memorize the training data instead of learning general patterns.



### 4.1.7 完整代码

`xor_nn.py`

```python
# 对于XOR问题（输入为[0,0], [0,1], [1,0], [1,1]），期望输出为[0,1,1,0]
# 手动实现反向传播，没有使用深度学习框架，这有助于理解底层原理
# https://www.geeksforgeeks.org/backpropagation-in-neural-network/
import numpy as np


class NeuralNetwork:
    def __init__(self, input_size, hidden_size, output_size):
        self.input_size = input_size  # 输入特征维度
        self.hidden_size = hidden_size  # 隐藏层神经元数量
        self.output_size = output_size  # 输出层神经元数量

        # 输入层到隐藏层的权重，形状为 (输入维度, 隐藏层维度)
        self.weights_input_hidden = np.random.randn(self.input_size, self.hidden_size)
        # 隐藏层到输出层的权重，形状为 (隐藏层维度, 输出层维度)
        self.weights_hidden_output = np.random.randn(self.hidden_size, self.output_size)

        # 隐藏层的偏置，形状为 (1, 隐藏层维度)
        self.bias_hidden = np.zeros((1, self.hidden_size))
        # 输出层的偏置，形状为 (1, 输出层维度)
        self.bias_output = np.zeros((1, self.output_size))

    def sigmoid(self, x):  # 激活函数，将输入压缩到(0,1)区间
        return 1 / (1 + np.exp(-x))

    def sigmoid_derivative(self, x):
        return x * (1 - x)  # Sigmoid的导数，用于反向传播中的梯度计算

    def feedforward(self, X):
        # 隐藏层计算
        self.hidden_activation = np.dot(X, self.weights_input_hidden) + self.bias_hidden  # 线性变换
        self.hidden_output = self.sigmoid(self.hidden_activation)  # 激活函数

        # 输出层计算
        self.output_activation = np.dot(self.hidden_output, self.weights_hidden_output) + self.bias_output
        self.predicted_output = self.sigmoid(self.output_activation)

        return self.predicted_output

    def backward(self, X, y, learning_rate):
        # 计算输出层误差
        output_error = y - self.predicted_output  # 误差 = 真实值 - 预测值
        # 计算输出层的delta（梯度的一部分，损失对激活输入的梯度）
        output_delta = output_error * self.sigmoid_derivative(self.predicted_output)  # Delta = 误差 × 激活函数导数
        # output_delta = (y - ŷ) * σ'(z_output)

        # 计算隐藏层误差（反向传播）
        hidden_error = np.dot(output_delta, self.weights_hidden_output.T)  # 将误差从输出层反向传播到隐藏层
        # hidden_error = output_delta @ W_hidden_output^T
        # 计算隐藏层的delta（损失对隐藏层激活输入的梯度）
        hidden_delta = hidden_error * self.sigmoid_derivative(self.hidden_output)  # Delta = 误差 × 激活函数导数
        # hidden_delta = (hidden_error) * σ'(z_hidden)

        # 更新权重和偏置（使用梯度下降法）
        # 计算并更新隐藏层到输出层的权重
        self.weights_hidden_output += np.dot(self.hidden_output.T,
                                             output_delta) * learning_rate  # 权重更新量 = 学习率 × (隐藏层输出转置 × 输出层delta)
        # W_hidden_output += learning_rate * (hidden_output^T @ output_delta)

        # 更新输出层偏置，基于所有样本的输出层delta沿列求和
        self.bias_output += np.sum(output_delta, axis=0, keepdims=True) * learning_rate  # 偏置更新量 = 学习率 × (沿列求和输出层delta)
        # b_output += learning_rate * sum(output_delta)

        # 计算并更新从输入层到隐藏层的权重的梯度
        self.weights_input_hidden += np.dot(X.T, hidden_delta) * learning_rate  # 权重更新量 = 学习率 × (输入数据转置 × 隐藏层delta)
        # W_input_hidden += learning_rate * (X^T @ hidden_delta)

        # 更新隐藏层偏置，基于所有样本的隐藏层delta沿列求和
        # axis=0：沿列求和，聚合所有样本的梯度
        # keepdims=True：保持原矩阵的行数维度，确保偏置更新的形状兼容性
        self.bias_hidden += np.sum(hidden_delta, axis=0, keepdims=True) * learning_rate  # 偏置更新量 = 学习率 × (沿列求和隐藏层delta)
        # b_hidden += learning_rate * sum(hidden_delta)

    def train(self, X, y, epochs, learning_rate):
        for epoch in range(epochs):
            output = self.feedforward(X)  # 前向传播
            self.backward(X, y, learning_rate)  # 反向传播与参数更新
            if epoch % 4000 == 0:
                loss = np.mean(np.square(y - output))  # 计算均方误差
                print(f"Epoch {epoch}, Loss:{loss}")


X = np.array([[0, 0], [0, 1], [1, 0], [1, 1]])
y = np.array([[0], [1], [1], [0]])

# 输入维度 2（二维二进制特征），隐藏层4个神经元，输出层1个神经元（二分类问题）
nn = NeuralNetwork(input_size=2, hidden_size=4, output_size=1)
# 训练总轮次, 学习率
nn.train(X, y, epochs=10000, learning_rate=0.1)

output = nn.feedforward(X)
print("Predictions after training:")
print(output)
"""
Epoch 0, Loss:0.2653166263520884
Epoch 4000, Loss:0.007000926683956338
Epoch 8000, Loss:0.001973630232951721
Predictions after training:
[[0.03613239]
 [0.96431351]
 [0.96058291]
 [0.03919372]]
"""
```



最终训练后，该网络可以准确学习XOR逻辑（训练数据：${([0,0]\to0),([0,1]\to1),([1,0]\to1),([1,1]\to0)}$），输出接近预期。该示例验证了多层网络和反向传播能解决线性模型无法处理的问题。



## 4.2 基于简单的全连接网络鸢尾花数据集分类

**任务描述**：使用全连接神经网络对经典的Iris（鸢尾花）数据集进行多分类。鸢（yuān）尾花数据集包含三个类别，每个类别有50个样本，每个样本有四个特征：花萼长度、花萼宽度、花瓣长度、花瓣宽度。目标是根据这四个特征预测花的种类，属于多分类问题。

**关键步骤**：数据预处理（标准化、训练/测试集划分）、模型构建、训练与评估。示例代码（PyTorch）：



### 准备数据

鸢尾花数据集通常是通过scikit-learn的datasets模块获取的，所以可能需要结合scikit-learn来加载数据，然后转换成PyTorch的Tensor。

数据预处理方面，需要将特征数据和标签分开。特征数据需要标准化或归一化，因为不同特征的量纲可能不同，这对神经网络的训练有帮助。标签需要转换成数值形式，比如0、1、2，然后可能还需要转换为长整型张量，因为交叉熵损失函数在PyTorch中通常要求这样的格式。



### 训练模型和验证

构建神经网络模型。考虑到鸢尾花数据集相对简单，可能不需要很深的网络。一个简单的全连接网络可能就足够了。比如，输入层4个节点，隐藏层可以选择10个节点，输出层3个节点对应三个类别。激活函数可以用ReLU，输出层用Softmax，不过更常见的做法是使用CrossEntropyLoss，它内部已经结合了Softmax，所以输出层不需要显式应用Softmax。

接下来是数据集的划分，通常分为训练集和测试集。这里需要注意的是，鸢尾花数据集样本较少，可能需要进行分层抽样，确保每个类别的样本在训练集和测试集中的比例一致。或者使用交叉验证，但由于用户可能希望一个简单的示例，可能直接采用80-20的划分。

将数据转换为PyTorch的DataLoader，方便批量训练。数据集进行训练可以分小批量处理。

训练过程中，定义损失函数和优化器。交叉熵损失函数适用于多分类问题，优化器可以选择Adam或SGD。学习率需要适当设置，比如0.01或0.001。

训练循环部分，需要迭代多个epoch，在每个epoch中进行前向传播、计算损失、反向传播和参数更新。同时，可以监控训练过程中的损失和准确率的变化。

验证阶段，使用测试集评估模型的准确率，确保模型没有过拟合，并且泛化能力良好。

可能需要注意的问题包括数据标准化应该在训练集上计算均值和标准差，然后应用到测试集，避免数据泄漏。另外，标签是否需要转换为one-hot编码？在PyTorch中，CrossEntropyLoss不需要，因为标签是类别的索引。

现在，将这些步骤整合成代码：

1. 导入必要的库：torch, sklearn.datasets中的load_iris，sklearn.model_selection的train_test_split，以及相关的PyTorch模块。
2. 加载数据，划分训练集和测试集，并进行标准化处理。使用StandardScaler对特征进行标准化，处理时注意仅拟合训练数据。
3. 转换数据为PyTorch的Tensor，并创建DataLoader。可能由于数据量小，直接使用整个数据集作为批量。
4. 定义神经网络模型的结构，使用全连接层和ReLU激活函数。
5. 初始化模型、损失函数和优化器。
6. 编写训练循环，迭代epoch，计算损失，反向传播，记录准确率。
7. 在测试集上评估模型性能。

另外，由于鸢尾花数据集样本较少，模型可能会很快过拟合，所以可能需要早停或者调整网络结构，比如减少隐藏层的大小，或者添加正则化，比如Dropout层。不过，作为示例，可能保持简单即可。

这样应该能完成一个基本的分类任务。不过可能需要调整超参数，比如学习率、epoch次数，或者网络结构，以达到更好的效果。例如，如果准确率不够高，可以尝试增加隐藏层的大小，或者增加更多的层。但鸢尾花数据集相对简单，可能简单的模型就足够。

另外，可能需要注意数据划分时的随机种子，确保结果可复现。此外，标准化处理是否正确应用，避免数据泄漏。在示例中，已经正确使用fit_transform在训练集，transform在测试集。



以下是使用PyTorch实现Fisher鸢尾花数据集分类的Python程序`iris_neural_network.py`，强调使用了神经网络进行分类。

如果缺少module，安装即可，例如：pip install torch scikit-learn torchvision matplotlib等。



**完整`iris_neural_network.py`代码**

```python
import torch, torch.nn as nn, torch.optim as optim
from torch.utils.data import TensorDataset, DataLoader
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler


# 定义模型结构
class IrisNet(nn.Module):
    def __init__(self, input_size=4, hidden_size=10, num_classes=3):
        super(IrisNet, self).__init__()
        self.net = nn.Sequential(
            nn.Linear(input_size, hidden_size),
            nn.ReLU(),
            nn.Linear(hidden_size, num_classes)
        )

    def forward(self, x):
        return self.net(x)


# 训练函数
def train(model, dataloader, criterion, optimizer, device):
    model.train()
    running_loss = 0.0
    for batch_X, batch_y in dataloader:
        batch_X, batch_y = batch_X.to(device), batch_y.to(device)

        optimizer.zero_grad()
        outputs = model(batch_X)
        loss = criterion(outputs, batch_y)
        loss.backward()
        optimizer.step()

        running_loss += loss.item() * batch_X.size(0)

    return running_loss / len(dataloader.dataset)


# 测试函数
def evaluate(model, X, y, device):
    model.eval()
    with torch.no_grad():
        X, y = X.to(device), y.to(device)
        outputs = model(X)
        _, predicted = torch.max(outputs, 1)
        accuracy = (predicted == y).float().mean().item()
    return accuracy, predicted


# 主程序
def main():
    # 设置设备
    if torch.backends.mps.is_available():
        device = torch.device("mps")
    elif torch.cuda.is_available():
        device = torch.device("cuda")
    else:
        device = torch.device("cpu")

    # 加载数据
    iris = load_iris()
    X, y = iris.data, iris.target

    X_train, X_test, y_train, y_test = train_test_split(
        X, y, test_size=0.2, random_state=42, stratify=y
    )
    """
    random_state=42
    设定随机数种子，从而确保每次运行代码时数据划分的结果都是相同的。这样做可以使实验具有可重复性，
    有利于调试和结果对比。

    stratify=y
    这个参数表示按照 y 中的标签进行分层抽样，也就是说，训练集和测试集中各类别的
    比例会与原始数据中的类别比例保持一致。这对于类别不平衡的数据集尤为重要，可以
    避免某一类别在划分时被严重低估或过采样。
    """

    # 标准化：只在训练集上计算均值和标准差，再将相同的变换应用到测试集上
    scaler = StandardScaler()
    X_train = scaler.fit_transform(X_train)
    X_test = scaler.transform(X_test)

    # 转换为 Tensor
    X_train = torch.tensor(X_train, dtype=torch.float32)
    X_test = torch.tensor(X_test, dtype=torch.float32)
    y_train = torch.tensor(y_train, dtype=torch.long)
    y_test = torch.tensor(y_test, dtype=torch.long)

    # 构造 DataLoader
    train_dataset = TensorDataset(X_train, y_train)
    train_loader = DataLoader(train_dataset, batch_size=16, shuffle=True)

    # 模型、损失函数、优化器
    model = IrisNet().to(device)
    criterion = nn.CrossEntropyLoss()
    optimizer = optim.Adam(model.parameters(), lr=0.01)

    # 训练
    num_epochs = 100
    for epoch in range(1, num_epochs + 1):
        loss = train(model, train_loader, criterion, optimizer, device)
        if epoch % 10 == 0:
            print(f"Epoch [{epoch:3d}/{num_epochs}], Loss: {loss:.4f}")

    # 评估
    test_acc, test_pred = evaluate(model, X_test, y_test, device)
    print(f"\n✅ Test Accuracy: {test_acc * 100:.2f}%")

    # 示例预测
    sample = X_test[0].unsqueeze(0)
    sample_pred = model(sample.to(device))
    pred_class = torch.argmax(sample_pred, dim=1).item()
    print(f"🔍 Sample Prediction: True = {y_test[0].item()}, Predicted = {pred_class}")


if __name__ == "__main__":
    main()

```

> 如果无法使用GPU
>
> **在运行时强制使用CPU调试**
>
> ```
> CUDA_VISIBLE_DEVICES="" python iris_neural_network.py
> ```
>
> 这样禁用CUDA，使用CPU。



> 云虚拟机运行结果：
>
> ![image-20250915152854981](https://raw.githubusercontent.com/GMyhf/img/main/img/image-20250915152854981.png)



**代码说明：**

1. **数据准备**：
   - 使用scikit-learn加载鸢尾花数据集
   - 将数据划分为训练集（80%）和测试集（20%）
   - 使用标准化处理（StandardScaler）对特征进行归一化

2. **神经网络结构**：
   - 输入层：4个神经元（对应4个特征）
   - 隐藏层：10个神经元（使用ReLU激活函数）
   - 输出层：3个神经元（对应3个类别）

3. **训练配置**：
   - 使用交叉熵损失函数（CrossEntropyLoss）
   - 使用Adam优化器（学习率0.01）
   - 训练100个epoch

4. **训练过程**：
   - 每个epoch记录损失和准确率
   - 每10个epoch打印训练进度

5. **评估与预测**：
   - 最终在测试集上评估模型准确率
   - 包含一个预测示例展示



该网络经过训练后，通常能在测试集上达到90%以上的准确率。实验结果表明，使用多层全连接网络即可较好解决该多分类任务（Iris数据集规模小，网络不需过深）。



> **注意事项：**
>
> 1. 由于数据集较小，模型可能很快达到100%训练准确率
> 2. 可以调整以下参数优化性能：
>    - 隐藏层大小（10）
>    - 学习率（0.01）
>    - epoch数量（100）
>    - 优化器（尝试SGD等）
> 3. 添加正则化（如Dropout层）可以防止过拟合
> 4. 可以使用GPU加速（将数据和模型移动到`cuda`设备）



> **可视化：监督学习 + 无监督学习（Iris 数据集）**
>
> ```python
> import numpy as np
> import matplotlib.pyplot as plt
> from sklearn.datasets import load_iris
> from sklearn.linear_model import LogisticRegression
> from sklearn.cluster import KMeans
> from sklearn.model_selection import train_test_split
> from sklearn.preprocessing import StandardScaler
> from sklearn.metrics import accuracy_score
> 
> # 1. 加载数据
> iris = load_iris()
> X = iris.data
> y = iris.target
> 
> # 2. 标准化数据
> scaler = StandardScaler()
> X_scaled = scaler.fit_transform(X)
> 
> # 3. 划分训练集和测试集（用于监督学习）
> train_x, test_x, train_y, test_y = train_test_split(X_scaled, y, test_size=0.3, random_state=42)
> 
> # 4. 监督学习：逻辑回归分类
> clf = LogisticRegression(max_iter=200)
> clf.fit(train_x, train_y)
> pred = clf.predict(test_x)
> print("Logistic Regression Accuracy:", accuracy_score(test_y, pred))
> 
> # 5. 无监督学习：KMeans 聚类（聚成3类）
> kmeans = KMeans(n_clusters=3, random_state=42)
> clusters = kmeans.fit_predict(X_scaled)
> 
> # 6. 可视化聚类（降维到二维）
> from sklearn.decomposition import PCA
> pca = PCA(n_components=2)
> X_2d = pca.fit_transform(X_scaled)
> 
> plt.figure(figsize=(10, 5))
> 
> # 聚类结果
> plt.subplot(1, 2, 1)
> plt.scatter(X_2d[:, 0], X_2d[:, 1], c=clusters, cmap='viridis', s=50)
> plt.title("KMeans Clustering (unsupervised)")
> 
> # 原始标签
> plt.subplot(1, 2, 2)
> plt.scatter(X_2d[:, 0], X_2d[:, 1], c=y, cmap='Set1', s=50)
> plt.title("Ground Truth Labels (supervised)")
> 
> plt.show()
> 
> ```
>
> > 使用 `LogisticRegression` 训练一个有监督分类器，并输出测试集准确率；
> >
> > 使用 `KMeans` 进行无监督聚类；
> >
> > 使用 PCA 将 4 维数据降维为 2 维，以便可视化聚类结果和真实标签；
> >
>
> 如图所示，通过使用PCA将特征降至二维，可视化聚类效果与真实分类的对比：
>
> 
>
> <img src="https://raw.githubusercontent.com/GMyhf/img/main/img/image-20250727143806445.png" alt="image-20250727143806445" style="zoom: 67%;" />
>
> <center>图：Iris 数据聚类（左：网络聚类结果；右：真实类别）</center>
>



## 4.3 基于 ResNet18 的MNIST手写数字识别

通过手写数字识别的实例，我们可以看到神经网络的强大，也可以更好地理解它是如何运行的。

MNIST 是计算机视觉领域最经典的基准数据集之一，包含 60,000 张训练图像和 10,000 张测试图像，均为 28×28 像素的灰度手写数字（0–9）。尽管任务看似简单，但它常被用于验证深度学习模型的基本能力。

本示例使用 **ResNet18** 架构对 MNIST 进行分类。虽然 ResNet18 原为 RGB 图像（3通道）设计，但通过适当调整输入层，我们可将其成功应用于单通道灰度图像，并在 MNIST 上轻松达到 **99%+ 的准确率**。

**关键步骤**

1. **数据加载与增强**

   - 使用 `torchvision.datasets.MNIST` 加载数据。
   - 对训练集应用轻微的数据增强（如随机旋转 ±10°），提升泛化能力。
   - 对图像进行标准化：均值和标准差均为 `0.5`（因像素值范围为 [0,1]）。

2. **模型适配**

   - 将 ResNet18 的首层卷积从 3 通道输入改为 **1 通道**：

     ```python
     net.conv1 = nn.Conv2d(1, 64, kernel_size=7, stride=2, padding=3, bias=False)
     ```

   - 修改全连接层输出维度为 **10**（对应 0–9 十个类别）。

3. **训练策略**

   - 优化器：SGD（学习率 0.01，动量 0.9，权重衰减 5e-4）
   - 学习率调度：余弦退火（`CosineAnnealingLR`）
   - 早停机制：若连续 10 个 epoch 验证损失无显著下降，则提前终止

4. **评估与可视化**

   - 报告整体准确率及每类准确率
   - 可视化部分测试样本及其预测结果



**完整`mnist_resnet18.py`代码**

```python
import torch
import torchvision
import torchvision.transforms as transforms
import torch.nn as nn
import torch.optim as optim
import torchvision.models as models
import matplotlib.pyplot as plt
import numpy as np
import time

def main():
    # 1. 数据增强 + 预处理
    transform_train = transforms.Compose([
        transforms.RandomRotation(10),  # 随机旋转
        transforms.ToTensor(),
        transforms.Normalize((0.5,), (0.5,))  # MNIST 是单通道，使用 (0.5,) 来规范化
    ])

    transform_test = transforms.Compose([
        transforms.ToTensor(),
        transforms.Normalize((0.5,), (0.5,))
    ])

    # 加载 MNIST 数据集
    trainset = torchvision.datasets.MNIST(root='./data', train=True, download=True, transform=transform_train)
    trainloader = torch.utils.data.DataLoader(trainset, batch_size=128, shuffle=True, num_workers=2, pin_memory=True)

    testset = torchvision.datasets.MNIST(root='./data', train=False, download=True, transform=transform_test)
    testloader = torch.utils.data.DataLoader(testset, batch_size=100, shuffle=False, num_workers=2, pin_memory=True)

    classes = [str(i) for i in range(10)]  # MNIST 类别是 0 到 9

    # 2. 设置设备和模型
    device = torch.device("mps" if torch.backends.mps.is_available() else "cpu")
    print("Using device:", device)

    # 加载预定义的 ResNet18 并修改输入层和输出层
    net = models.resnet18(weights=None)
    # 修改输入层的第一个卷积层，使其接受单通道（1通道灰度图像）
    net.conv1 = nn.Conv2d(1, 64, kernel_size=(7, 7), stride=(2, 2), padding=(3, 3), bias=False)
    net.fc = nn.Linear(net.fc.in_features, 10)  # MNIST 10 类
    net.to(device)

    # 定义损失函数和优化器
    criterion = nn.CrossEntropyLoss()
    optimizer = optim.SGD(net.parameters(), lr=0.01, momentum=0.9, weight_decay=5e-4)
    scheduler = optim.lr_scheduler.CosineAnnealingLR(optimizer, T_max=100)

    # 3. 训练过程
    best_loss = float('inf')
    patience = 10  # 提高耐心
    patience_counter = 0

    start_time = time.time()
    print("Starting training with early stopping...")
    for epoch in range(800):  # 可适当增大 epoch
        net.train()
        epoch_loss = 0.0
        for i, data in enumerate(trainloader, 0):
            inputs, labels = data
            inputs, labels = inputs.to(device), labels.to(device)

            optimizer.zero_grad()
            outputs = net(inputs)
            loss = criterion(outputs, labels)
            loss.backward()
            optimizer.step()

            epoch_loss += loss.item()
            if i % 100 == 99:
                print(f"[{epoch + 1}, {i + 1:5d}] loss: {loss.item():.3f}")

        avg_loss = epoch_loss / len(trainloader)
        print(f"[{epoch+1}] Avg Loss: {avg_loss:.3f}")

        if avg_loss < best_loss - 1e-4:
            best_loss = avg_loss
            patience_counter = 0
        else:
            patience_counter += 1
            print(f"No improvement. Patience: {patience_counter}/{patience}")
            if patience_counter >= patience:
                print("Early stopping triggered.")
                break

    end_time = time.time()
    execution_time_minutes = (end_time - start_time) / 60
    print(f"✅ Training completed in {execution_time_minutes:.2f} minutes.")

    # 保存模型
    torch.save(net.state_dict(), './resnet18_mnist.pth')

    # 4. 测试准确率
    correct = 0
    total = 0
    net.eval()
    with torch.no_grad():
        for data in testloader:
            images, labels = data
            images, labels = images.to(device), labels.to(device)
            outputs = net(images)
            _, predicted = torch.max(outputs.data, 1)
            total += labels.size(0)
            correct += (predicted == labels).sum().item()

    print(f"Accuracy on test images: {100 * correct / total:.2f}%")

    # 每类准确率
    class_correct = list(0. for _ in range(10))
    class_total = list(0. for _ in range(10))
    with torch.no_grad():
        for data in testloader:
            images, labels = data
            images, labels = images.to(device), labels.to(device)
            outputs = net(images)
            _, predicted = torch.max(outputs.data, 1)
            c = (predicted == labels).squeeze()
            for i in range(len(labels)):
                class_correct[labels[i]] += c[i].item()
                class_total[labels[i]] += 1

    for i in range(10):
        print(f'Accuracy of {classes[i]:5s}: {100 * class_correct[i] / class_total[i]:.2f}%')

    # --- 可视化预测 ---

    def imshow_grid(images, labels, preds=None, classes=None, rows=8, cols=8):
        images = images.cpu() / 2 + 0.5  # unnormalize
        npimg = images.numpy()
        fig, axes = plt.subplots(rows, cols, figsize=(cols * 1.5, rows * 1.5))
        for i in range(rows * cols):
            r, c = divmod(i, cols)
            ax = axes[r, c]
            img = np.transpose(npimg[i], (1, 2, 0))
            ax.imshow(img.squeeze(), cmap="gray")
            title = f'{classes[labels[i]]}'
            if preds is not None:
                title += f'\n→ {classes[preds[i]]}'
            ax.set_title(title, fontsize=8)
            ax.axis('off')
        plt.tight_layout()
        plt.show()

    # 获取一批图像用于显示
    dataiter = iter(testloader)
    images, labels = next(dataiter)
    while images.size(0) < 64:
        more_images, more_labels = next(dataiter)
        images = torch.cat([images, more_images], dim=0)
        labels = torch.cat([labels, more_labels], dim=0)
    images = images[:64]
    labels = labels[:64]

    # 预测
    net.eval()
    with torch.no_grad():
        outputs = net(images.to(device))
        _, predicted = torch.max(outputs, 1)

    # 显示图像网格
    imshow_grid(images, labels, predicted.cpu(), classes=classes, rows=8, cols=8)

if __name__ == "__main__":
    import torch.multiprocessing
    torch.multiprocessing.set_start_method('spawn', force=True)
    main()


```

典型结果：使用ResNet18能在MNIST上达到99%以上的准确率。该任务展示了深度卷积网络在图像分类中的强大能力。



**常见问题解答**

**Q: 为什么需要修改 `net.conv1`？**

> ResNet18 默认输入为 3 通道（RGB），而 MNIST 是单通道灰度图。必须将第一个卷积层的输入通道数从 3 改为 1，否则会报维度不匹配错误。其余结构（如 kernel size=7、stride=2 等）保持不变以保留原始设计意图。
>
> **`nn.Conv2d(1, 64, kernel_size=(7, 7), stride=(2, 2), padding=(3, 3), bias=False)`** 这一行就是修改原来 `ResNet18` 中第一个卷积层（`conv1`）的定义，以使其能接收单通道的灰度图像（`1` 通道）。
>
> - **`1`**: 输入图像的通道数（即 MNIST 图像的灰度通道数）。
> - **`64`**: 输出的卷积通道数（ResNet18 中通常是 64）。
> - **`kernel_size=(7, 7)`**: 卷积核的大小为 7x7。这个值与原始 ResNet18 中的设置一致。
> - **`stride=(2, 2)`**: 卷积的步长为 2，这意味着每次卷积后，图像尺寸会减少一半。
> - **`padding=(3, 3)`**: 填充为 3，保持输入图像的尺寸在卷积后不至于变化太大（确保卷积后输出的空间维度适当）。
> - **`bias=False`**: 通常在深度网络中，如果使用了批量归一化（BatchNorm）等层，卷积层可以去掉偏置项。

**Q: 能否在 CPU 上运行？**

> 可以。若无 GPU 或 MPS（Apple Silicon）支持，程序会自动回退到 CPU。如需强制使用 CPU（例如调试时），可运行：
>
> ```bash
> CUDA_VISIBLE_DEVICES="" python mnist_resnet18.py
> ```



**总结**

本项目展示了如何将为自然图像设计的现代 CNN（如 ResNet18）迁移到简单但经典的 MNIST 任务上。通过**输入层适配**、**合理训练策略**和**结果可视化**，不仅验证了模型有效性，也加深了对神经网络工作原理的理解。

> **提示**：对于 MNIST 这类简单任务，小型 CNN（如 LeNet-5）已足够高效。使用 ResNet18 更多是为了演示模型迁移与适配技巧。



### 实验结果

#### 在16GB内存的 Mac mini 运行

> 运行机器
>
> <img src="https://raw.githubusercontent.com/GMyhf/img/main/img/202507261935350.png" alt="b452b39cfb47eb8bf5b640c828b6b71b" style="zoom:50%;" />
>
> 
>
> 详细训练日志
>
> ```
> /Users/hfyan/miniconda3/bin/python /Users/hfyan/git/2025spring-cs201/LLM/mnist_resnet18.py 
> 100%|██████████| 9.91M/9.91M [02:52<00:00, 57.6kB/s]
> 100%|██████████| 28.9k/28.9k [00:00<00:00, 97.2kB/s]
> 100%|██████████| 1.65M/1.65M [00:04<00:00, 374kB/s]
> 100%|██████████| 4.54k/4.54k [00:00<00:00, 6.74kB/s]
> Using device: mps
> Starting training with early stopping...
> /Users/hfyan/miniconda3/lib/python3.10/site-packages/torch/utils/data/dataloader.py:683: UserWarning: 'pin_memory' argument is set as true but not supported on MPS now, then device pinned memory won't be used.
>   warnings.warn(warn_msg)
> [1,   100] loss: 0.136
> [1,   200] loss: 0.132
> [1,   300] loss: 0.035
> [1,   400] loss: 0.098
> [1] Avg Loss: 0.150
> [2,   100] loss: 0.137
> [2,   200] loss: 0.030
> [2,   300] loss: 0.030
> [2,   400] loss: 0.015
> [2] Avg Loss: 0.052
> [3,   100] loss: 0.018
> [3,   200] loss: 0.105
> [3,   300] loss: 0.078
> [3,   400] loss: 0.026
> [3] Avg Loss: 0.039
> [4,   100] loss: 0.032
> [4,   200] loss: 0.056
> [4,   300] loss: 0.008
> [4,   400] loss: 0.013
> [4] Avg Loss: 0.031
> [5,   100] loss: 0.003
> [5,   200] loss: 0.025
> [5,   300] loss: 0.029
> [5,   400] loss: 0.022
> [5] Avg Loss: 0.027
> [6,   100] loss: 0.041
> [6,   200] loss: 0.022
> [6,   300] loss: 0.047
> [6,   400] loss: 0.005
> [6] Avg Loss: 0.023
> 
> ...
> 
> No improvement. Patience: 6/10
> [43,   100] loss: 0.010
> [43,   200] loss: 0.000
> [43,   300] loss: 0.012
> [43,   400] loss: 0.002
> [43] Avg Loss: 0.008
> No improvement. Patience: 7/10
> [44,   100] loss: 0.001
> [44,   200] loss: 0.004
> [44,   300] loss: 0.035
> [44,   400] loss: 0.000
> [44] Avg Loss: 0.011
> No improvement. Patience: 8/10
> [45,   100] loss: 0.002
> [45,   200] loss: 0.014
> [45,   300] loss: 0.010
> [45,   400] loss: 0.014
> [45] Avg Loss: 0.010
> No improvement. Patience: 9/10
> [46,   100] loss: 0.001
> [46,   200] loss: 0.076
> [46,   300] loss: 0.001
> [46,   400] loss: 0.004
> [46] Avg Loss: 0.009
> No improvement. Patience: 10/10
> Early stopping triggered.
> ✅ Training completed in 27.72 minutes.
> Accuracy on test images: 99.57%
> Accuracy of 0    : 99.59%
> Accuracy of 1    : 99.91%
> Accuracy of 2    : 99.71%
> Accuracy of 3    : 99.80%
> Accuracy of 4    : 99.49%
> Accuracy of 5    : 99.33%
> Accuracy of 6    : 99.37%
> Accuracy of 7    : 99.22%
> Accuracy of 8    : 99.90%
> Accuracy of 9    : 99.31%
> 
> Process finished with exit code 0
> 
> ```
> 
> 
> 
> <img src="https://raw.githubusercontent.com/GMyhf/img/main/img/202507261936331.png" alt="22485e1e277b7dfea954fe0cd8a1af4f" style="zoom:50%;" />
> 
> 



#### 在16GB内存的 window 机器运行

> 在window机器，用 WSL 安装 Ubuntu，用cpu运行
>
> 环境设置，可以参考：https://github.com/GMyhf/2025fall-cs201/blob/main/LLM/Build%20LLM%20Setup_window.md
>
> ```
> $ CUDA_VISIBLE_DEVICES="" python mnist_resnet18.py
> ```
>
> Windows 10 专业版，版本号22H2，安装日期 2021/6/12
>
> 处理器 Intel(R)Xeon(R)W-2223 CPU @ 3.60GHz 3.60GHz
> 机带 RAM 16.0 GB (15.7 GB 可用)
> 系统类型 64 位操作系统, 基于 x64 的处理器
>
> ```
> 100%|████████████| 9.91M/9.91M [00:06<00:00, 1.52MB/s]
> 100%|████████████| 28.9k/28.9k [00:00<00:00, 133kB/s]
> 100%|████████████| 1.65M/1.65M [00:01<00:00, 905kB/s]
> 100%|████████████| 4.54k/4.54k [00:00<00:00, 9.23MB/s]
> Using device: cpu
> Starting training with early stopping...
> /home/yhf/.venv/lib/python3.12/site-packages/torch/utils/data/dataloader.py:666: UserWarning: 'pin_memory' argument is set as true but no accelerator is found, then device pinned memory won't be used.
>   warnings.warn(warn_msg)
> [1,   100] loss: 0.099
> [1,   200] loss: 0.072
> [1,   300] loss: 0.038
> [1,   400] loss: 0.079
> [1] Avg Loss: 0.149
> [2,   100] loss: 0.028
> [2,   200] loss: 0.010
> [2,   300] loss: 0.012
> [2,   400] loss: 0.112
> [2] Avg Loss: 0.053
> [3,   100] loss: 0.017
> [3,   200] loss: 0.032
> [3,   300] loss: 0.009
> [3,   400] loss: 0.027
> [3] Avg Loss: 0.037
> [4,   100] loss: 0.024
> [4,   200] loss: 0.087
> [4,   300] loss: 0.010
> [4,   400] loss: 0.045
> [4] Avg Loss: 0.032
> [5,   100] loss: 0.034
> [5,   200] loss: 0.009
> [5,   300] loss: 0.019
> [5,   400] loss: 0.038
> [5] Avg Loss: 0.026
> [6,   100] loss: 0.032
> [6,   200] loss: 0.046
> [6,   300] loss: 0.037
> [6,   400] loss: 0.039
> [6] Avg Loss: 0.023
> [7,   100] loss: 0.038
> 
> ...
> 
> [43] Avg Loss: 0.008
> No improvement. Patience: 5/10
> [44,   100] loss: 0.046
> [44,   200] loss: 0.002
> [44,   300] loss: 0.023
> [44,   400] loss: 0.008
> [44] Avg Loss: 0.010
> No improvement. Patience: 6/10
> [45,   100] loss: 0.021
> [45,   200] loss: 0.001
> [45,   300] loss: 0.006
> [45,   400] loss: 0.001
> [45] Avg Loss: 0.011
> No improvement. Patience: 7/10
> [46,   100] loss: 0.008
> [46,   200] loss: 0.006
> [46,   300] loss: 0.002
> [46,   400] loss: 0.049
> [46] Avg Loss: 0.010
> No improvement. Patience: 8/10
> [47,   100] loss: 0.001
> [47,   200] loss: 0.015
> [47,   300] loss: 0.001
> [47,   400] loss: 0.026
> [47] Avg Loss: 0.008
> No improvement. Patience: 9/10
> [48,   100] loss: 0.002
> [48,   200] loss: 0.002
> [48,   300] loss: 0.002
> [48,   400] loss: 0.004
> [48] Avg Loss: 0.010
> No improvement. Patience: 10/10
> Early stopping triggered.
> ✅ Training completed in 75.11 minutes.
> Accuracy on test images: 99.35%
> Accuracy of 0    : 99.59%
> Accuracy of 1    : 99.91%
> Accuracy of 2    : 99.22%
> Accuracy of 3    : 99.50%
> Accuracy of 4    : 99.59%
> Accuracy of 5    : 99.22%
> Accuracy of 6    : 99.37%
> Accuracy of 7    : 99.22%
> Accuracy of 8    : 99.38%
> Accuracy of 9    : 98.41%
> /home/yhf/NNCode/mnist_resnet18.py:142: UserWarning: FigureCanvasAgg is non-interactive, and thus cannot be shown
> plt.show()
> ```
> 
> 



#### 在32GB内存的 clab 云虚拟机运行

2025年11月26日，在clab云虚拟机跑。虚拟机只有CPU。

<img src="https://raw.githubusercontent.com/GMyhf/img/main/img/33caace9ba4252b9bcc6707b67f18746.png" alt="33caace9ba4252b9bcc6707b67f18746" style="zoom: 33%;" />



clab虚拟机需要登录网关，能访问外网，因为要下载数据

> 否则，报302错误
>
> (.venv) [rocky@jensen AI_literacy]$ python MNIST_nn.py 
> Traceback (most recent call last):
> File "/home/rocky/AI_literacy/MNIST_nn.py", line 166, in <module>
> main()
> File "/home/rocky/AI_literacy/MNIST_nn.py", line 25, in main
> trainset = torchvision.datasets.MNIST(root='./data', train=True, download=True, transform=transform_train)
> File "/home/rocky/AI_literacy/.venv/lib64/python3.9/site-packages/torchvision/datasets/mnist.py", line 100, in __init__
>
> self.download()
>
> File "/home/rocky/AI_literacy/.venv/lib64/python3.9/site-packages/torchvision/datasets/mnist.py", line 197, in download
> raise RuntimeError(s)
> RuntimeError: Error downloading train-images-idx3-ubyte.gz:
> Tried https://ossci-datasets.s3.amazonaws.com/mnist/, got:
> <urlopen error [Errno 110] Connection timed out>
> Tried http://yann.lecun.com/exdb/mnist/, got:
> HTTP Error 302: Moved Temporarily



> 
>
> ```
> (.venv) [rocky@jensen AI_literacy]$ python MNIST_nn.py 
> 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 9.91M/9.91M [06:09<00:00, 26.8kB/s]
> 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 28.9k/28.9k [00:00<00:00, 113kB/s]
> 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 1.65M/1.65M [00:01<00:00, 1.12MB/s]
> 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 4.54k/4.54k [00:00<00:00, 4.41MB/s]
> Using device: cpu
> Starting training with early stopping...
> /home/rocky/AI_literacy/.venv/lib64/python3.9/site-packages/torch/utils/data/dataloader.py:666: UserWarning: 'pin_memory' argument is set as true but no accelerator is found, then device pinned memory won't be used.
>   warnings.warn(warn_msg)
> [1,   100] loss: 0.200
> [1,   200] loss: 0.084
> [1,   300] loss: 0.060
> [1,   400] loss: 0.100
> [1] Avg Loss: 0.150
> [2,   100] loss: 0.095
> [2,   200] loss: 0.102
> [2,   300] loss: 0.010
> [2,   400] loss: 0.032
> [2] Avg Loss: 0.049
> [3,   100] loss: 0.024
> [3,   200] loss: 0.051
> [3,   300] loss: 0.064
> [3,   400] loss: 0.019
> [3] Avg Loss: 0.039
> [4,   100] loss: 0.040
> [4,   200] loss: 0.071
> [4,   300] loss: 0.068
> [4,   400] loss: 0.052
> [4] Avg Loss: 0.030
> [5,   100] loss: 0.039
> [5,   200] loss: 0.031
> [5,   300] loss: 0.005
> [5,   400] loss: 0.002
> [5] Avg Loss: 0.025
> [6,   100] loss: 0.081
> [6,   200] loss: 0.019
> [6,   300] loss: 0.040
> [6,   400] loss: 0.006
> [6] Avg Loss: 0.023
> 
> ...
> 
> [40,   200] loss: 0.001
> [40,   300] loss: 0.019
> [40,   400] loss: 0.076
> [40] Avg Loss: 0.010
> No improvement. Patience: 4/10
> [41,   100] loss: 0.001
> [41,   200] loss: 0.012
> [41,   300] loss: 0.014
> [41,   400] loss: 0.009
> [41] Avg Loss: 0.012
> No improvement. Patience: 5/10
> [42,   100] loss: 0.003
> [42,   200] loss: 0.002
> [42,   300] loss: 0.053
> [42,   400] loss: 0.001
> [42] Avg Loss: 0.010
> No improvement. Patience: 6/10
> [43,   100] loss: 0.011
> [43,   200] loss: 0.000
> [43,   300] loss: 0.006
> [43,   400] loss: 0.005
> [43] Avg Loss: 0.008
> No improvement. Patience: 7/10
> [44,   100] loss: 0.013
> [44,   200] loss: 0.030
> [44,   300] loss: 0.021
> [44,   400] loss: 0.004
> [44] Avg Loss: 0.010
> No improvement. Patience: 8/10
> [45,   100] loss: 0.003
> [45,   200] loss: 0.012
> [45,   300] loss: 0.002
> [45,   400] loss: 0.037
> [45] Avg Loss: 0.008
> No improvement. Patience: 9/10
> [46,   100] loss: 0.001
> [46,   200] loss: 0.006
> [46,   300] loss: 0.000
> [46,   400] loss: 0.020
> [46] Avg Loss: 0.010
> No improvement. Patience: 10/10
> Early stopping triggered.
> ✅ Training completed in 91.75 minutes.
> Accuracy on test images: 99.43%
> Accuracy of 0    : 99.80%
> Accuracy of 1    : 99.65%
> Accuracy of 2    : 99.03%
> Accuracy of 3    : 99.70%
> Accuracy of 4    : 99.19%
> Accuracy of 5    : 98.77%
> Accuracy of 6    : 99.37%
> Accuracy of 7    : 99.71%
> Accuracy of 8    : 99.38%
> Accuracy of 9    : 99.60%
> ```
> 
> 



## 4.4 基于 ResNet18 的 CIFAR-10 图像分类

本项目旨在复现并改进 菜鸟教程（https://www.runoob.com/pytorch/pytorch-image-classification.html）中的 CIFAR-10 分类示例。原始实现仅达到约 **76.8%** 的测试准确率，低于经典基线（如 cuda-convnet 报告的 **82%+**）。为此，我们引入 **ResNet18 架构**、**增强的数据预处理策略** 和 **学习率调度机制**，显著提升模型性能。

最终在 Mac Studio（M1 Ultra）与 Clab 云服务器上均实现了 **>83.5%** 的测试准确率，成功超越基础 CNN 基线。



### 数据集简介：CIFAR-10

CIFAR-10 是由 Alex Krizhevsky 等人构建的经典图像分类数据集，源自 80 Million Tiny Images（http://people.csail.mit.edu/torralba/tinyimages/）。

- **图像数量**：60,000 张 32×32 彩色图像 
- **类别数**：10 类（互斥） 
  - airplane, automobile, bird, cat, deer, dog, frog, horse, ship, truck
- **划分**：
  - 训练集：50,000 张（每类 5,000）
  - 测试集：10,000 张（每类 1,000，均匀采样）

> 官网：https://www.cs.toronto.edu/~kriz/cifar.html

| Class      | 示例图像                                                     |
| ---------- | ------------------------------------------------------------ |
| airplane   | ![airplane](https://www.cs.toronto.edu/~kriz/cifar-10-sample/airplane1.png) … |
| automobile | ![automobile](https://www.cs.toronto.edu/~kriz/cifar-10-sample/automobile1.png) … |
| ...        | （其余略，详见官网）                                         |

> 注意：“automobile” 指轿车/SUV，“truck” 仅指大型卡车，两者无重叠。
>
> **Baseline results**
>
> You can find some baseline replicable results on this dataset [on the project page for cuda-convnet](http://code.google.com/p/cuda-convnet/). These results were obtained with a convolutional neural network. Briefly, they are **18%** test error without data augmentation and 11% with. Additionally, [Jasper Snoek](http://www.cs.toronto.edu/~jasper/) has a [new paper](http://hips.seas.harvard.edu/content/practical-bayesian-optimization-machine-learning-algorithms) in which he used Bayesian hyperparameter optimization to find nice settings of the weight decay and other hyperparameters, which allowed him to obtain a test error rate of 15% (without data augmentation) using the architecture of the net that got 18%.

------



### 改进措施

**现代网络架构（ResNet18） + 充分的数据增强 + 学习率调度**

| 改进项         | 具体实现                                                     |
| -------------- | ------------------------------------------------------------ |
| **网络架构**   | 使用 `torchvision.models.resnet18(weights=None)`，从头训练   |
| **输入尺寸**   | 保留原始 32×32（无需 Resize，因未加载 ImageNet 预训练权重）  |
| **数据增强**   | `RandomCrop`, `HorizontalFlip`, `RandomRotation`, `ColorJitter` |
| **优化器**     | SGD + momentum=0.9 + weight_decay=5e-4                       |
| **学习率调度** | `CosineAnnealingLR`（平滑衰减）                              |
| **训练控制**   | Early stopping（patience=10）防止过拟合                      |
| **评估指标**   | 总体准确率 + 每类准确率 + 可视化预测网格                     |



完整 `image_classification-ResNet18-RandomCropFlipLR_Cosine.py`代码

```python
import torch
import torchvision
import torchvision.transforms as transforms
import torch.nn as nn
import torch.optim as optim
import torchvision.models as models
import matplotlib.pyplot as plt
import numpy as np
import time

def main():
    # === 1. 数据增强与加载 ===
    transform_train = transforms.Compose([
        transforms.RandomCrop(32, padding=4),
        transforms.RandomHorizontalFlip(),
        transforms.RandomRotation(10),  # 随机旋转
        transforms.ColorJitter(brightness=0.2, contrast=0.2, saturation=0.2, hue=0.2),  # 色彩调整
        transforms.ToTensor(),
        transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5))
    ])

    transform_test = transforms.Compose([
        transforms.ToTensor(),
        transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5))
    ])

    trainset = torchvision.datasets.CIFAR10(root='./data', train=True, download=True, transform=transform_train)
    trainloader = torch.utils.data.DataLoader(trainset, batch_size=128, shuffle=True, num_workers=2, pin_memory=True)

    testset = torchvision.datasets.CIFAR10(root='./data', train=False, download=True, transform=transform_test)
    testloader = torch.utils.data.DataLoader(testset, batch_size=100, shuffle=False, num_workers=2, pin_memory=True)

    classes = ('plane', 'car', 'bird', 'cat', 'deer',
               'dog', 'frog', 'horse', 'ship', 'truck')

    # === 2. 模型与训练配置 ===
    device = torch.device("mps" if torch.backends.mps.is_available() else "cpu")
    print("Using device:", device)

    # 加载预定义的 ResNet18 并修改输出层
    net = models.resnet18(weights=None)
    net.fc = nn.Linear(net.fc.in_features, 10)  # CIFAR10 10 类
    net.to(device)

    # 定义损失函数和优化器
    criterion = nn.CrossEntropyLoss()
    optimizer = optim.SGD(net.parameters(), lr=0.01, momentum=0.9, weight_decay=5e-4)
    scheduler = optim.lr_scheduler.CosineAnnealingLR(optimizer, T_max=100)

    # === 3. 训练循环（含 Early Stopping）===
    best_loss = float('inf')
    patience = 10 # 提高耐心
    patience_counter = 0

    start_time = time.time()
    print("Starting training with early stopping...")
    for epoch in range(800):  # 可适当增大 epoch
        net.train()
        epoch_loss = 0.0
        for i, data in enumerate(trainloader, 0):
            inputs, labels = data
            inputs, labels = inputs.to(device), labels.to(device)

            optimizer.zero_grad()
            outputs = net(inputs)
            loss = criterion(outputs, labels)
            loss.backward()
            optimizer.step()

            epoch_loss += loss.item()
            if i % 100 == 99:
                print(f"[{epoch + 1}, {i + 1:5d}] loss: {loss.item():.3f}")

        avg_loss = epoch_loss / len(trainloader)
        print(f"[{epoch+1}] Avg Loss: {avg_loss:.3f}")

        if avg_loss < best_loss - 1e-4:
            best_loss = avg_loss
            patience_counter = 0
        else:
            patience_counter += 1
            print(f"No improvement. Patience: {patience_counter}/{patience}")
            if patience_counter >= patience:
                print("Early stopping triggered.")
                break



    end_time = time.time()
    execution_time_minutes = (end_time - start_time) / 60
    print(f"✅ Training completed in {execution_time_minutes:.2f} minutes.")


    # 保存模型
    torch.save(net.state_dict(), './resnet18_cifar10_data_augument.pth')

    # === 4. 测试评估 ===
    correct = 0
    total = 0
    net.eval()
    with torch.no_grad():
        for data in testloader:
            images, labels = data
            images, labels = images.to(device), labels.to(device)
            outputs = net(images)
            _, predicted = torch.max(outputs.data, 1)
            total += labels.size(0)
            correct += (predicted == labels).sum().item()

    print(f"Accuracy on test images: {100 * correct / total:.2f}%")

    # 每类准确率
    class_correct = list(0. for _ in range(10))
    class_total = list(0. for _ in range(10))
    with torch.no_grad():
        for data in testloader:
            images, labels = data
            images, labels = images.to(device), labels.to(device)
            outputs = net(images)
            _, predicted = torch.max(outputs.data, 1)
            c = (predicted == labels).squeeze()
            for i in range(len(labels)):
                class_correct[labels[i]] += c[i].item()
                class_total[labels[i]] += 1

    for i in range(10):
        print(f'Accuracy of {classes[i]:5s}: {100 * class_correct[i] / class_total[i]:.2f}%')

    # === 5. 可视化预测结果 ===
    def imshow_grid(images, labels, preds=None, classes=None, rows=8, cols=8):
        images = images.cpu() / 2 + 0.5  # unnormalize
        npimg = images.numpy()
        fig, axes = plt.subplots(rows, cols, figsize=(cols * 1.5, rows * 1.5))
        for i in range(rows * cols):
            r, c = divmod(i, cols)
            ax = axes[r, c]
            img = np.transpose(npimg[i], (1, 2, 0))
            ax.imshow(img)
            title = f'{classes[labels[i]]}'
            if preds is not None:
                title += f'\n→ {classes[preds[i]]}'
            ax.set_title(title, fontsize=8)
            ax.axis('off')
        plt.tight_layout()
        plt.show()

    # 获取一批图像用于显示
    dataiter = iter(testloader)
    images, labels = next(dataiter)
    while images.size(0) < 64:
        more_images, more_labels = next(dataiter)
        images = torch.cat([images, more_images], dim=0)
        labels = torch.cat([labels, more_labels], dim=0)
    images = images[:64]
    labels = labels[:64]

    # 预测
    net.eval()
    with torch.no_grad():
        outputs = net(images.to(device))
        _, predicted = torch.max(outputs, 1)

    # 显示图像网格
    imshow_grid(images, labels, predicted.cpu(), classes=classes, rows=8, cols=8)

if __name__ == "__main__":
    import torch.multiprocessing
    torch.multiprocessing.set_start_method('spawn', force=True)
    main()

```



### 实验结果

#### 在 Apple M1 Ultra (Mac Studio, 64GB RAM)

- **设备**：`mps`
- **训练耗时**：79.91 分钟
- **早停轮次**：第 208 轮
- **测试准确率**：**83.57%**

| 类别    | 准确率              |
| ------- | ------------------- |
| plane   | 83.70%              |
| car     | 92.20%              |
| bird    | 78.70%              |
| **cat** | **60.40%** ← 最弱项 |
| deer    | 79.30%              |
| dog     | 77.40%              |
| frog    | 90.30%              |
| horse   | 92.50%              |
| ship    | 88.50%              |
| truck   | 92.70%              |

> 预测可视化：
> <img src="https://raw.githubusercontent.com/GMyhf/img/main/img/202507280020181.jpg" alt="预测结果" style="zoom: 50%;" />

> 运行输出结果如下：
>
> ```
> /Users/hfyan/miniconda3/bin/python /Users/hfyan/Desktop/LLMs-from-scratch-main/runoob/pytorch-image-classification/image_classification-ResNet18-RandomCropFlipLR_Cosine.py 
> Using device: mps
> Starting training with early stopping...
> [1,   100] loss: 1.752
> [1,   200] loss: 1.675
> [1,   300] loss: 1.654
> [1] Avg Loss: 1.806
> [2,   100] loss: 1.497
> [2,   200] loss: 1.459
> [2,   300] loss: 1.453
> [2] Avg Loss: 1.520
> [3,   100] loss: 1.534
> [3,   200] loss: 1.383
> [3,   300] loss: 1.167
> [3] Avg Loss: 1.372
> [4,   100] loss: 1.390
> [4,   200] loss: 1.221
> [4,   300] loss: 1.238
> [4] Avg Loss: 1.244
> [5,   100] loss: 1.089
> [5,   200] loss: 1.020
> [5,   300] loss: 1.133
> [5] Avg Loss: 1.159
> ......
> No improvement. Patience: 1/10
> [192,   100] loss: 0.187
> [192,   200] loss: 0.293
> [192,   300] loss: 0.356
> [192] Avg Loss: 0.302
> [193,   100] loss: 0.223
> [193,   200] loss: 0.348
> [193,   300] loss: 0.309
> [193] Avg Loss: 0.301
> [194,   100] loss: 0.303
> [194,   200] loss: 0.219
> [194,   300] loss: 0.280
> [194] Avg Loss: 0.304
> No improvement. Patience: 1/10
> [195,   100] loss: 0.279
> [195,   200] loss: 0.296
> [195,   300] loss: 0.313
> [195] Avg Loss: 0.296
> [196,   100] loss: 0.254
> [196,   200] loss: 0.385
> [196,   300] loss: 0.280
> [196] Avg Loss: 0.300
> No improvement. Patience: 1/10
> [197,   100] loss: 0.216
> [197,   200] loss: 0.298
> [197,   300] loss: 0.290
> [197] Avg Loss: 0.298
> No improvement. Patience: 2/10
> [198,   100] loss: 0.267
> [198,   200] loss: 0.218
> [198,   300] loss: 0.367
> [198] Avg Loss: 0.290
> [199,   100] loss: 0.270
> [199,   200] loss: 0.240
> [199,   300] loss: 0.351
> [199] Avg Loss: 0.301
> No improvement. Patience: 1/10
> [200,   100] loss: 0.251
> [200,   200] loss: 0.227
> [200,   300] loss: 0.302
> [200] Avg Loss: 0.299
> No improvement. Patience: 2/10
> [201,   100] loss: 0.348
> [201,   200] loss: 0.301
> [201,   300] loss: 0.193
> [201] Avg Loss: 0.299
> No improvement. Patience: 3/10
> [202,   100] loss: 0.313
> [202,   200] loss: 0.329
> [202,   300] loss: 0.305
> [202] Avg Loss: 0.295
> No improvement. Patience: 4/10
> [203,   100] loss: 0.266
> [203,   200] loss: 0.254
> [203,   300] loss: 0.307
> [203] Avg Loss: 0.294
> No improvement. Patience: 5/10
> [204,   100] loss: 0.372
> [204,   200] loss: 0.295
> [204,   300] loss: 0.348
> [204] Avg Loss: 0.300
> No improvement. Patience: 6/10
> [205,   100] loss: 0.392
> [205,   200] loss: 0.353
> [205,   300] loss: 0.306
> [205] Avg Loss: 0.296
> No improvement. Patience: 7/10
> [206,   100] loss: 0.262
> [206,   200] loss: 0.213
> [206,   300] loss: 0.396
> [206] Avg Loss: 0.293
> No improvement. Patience: 8/10
> [207,   100] loss: 0.293
> [207,   200] loss: 0.204
> [207,   300] loss: 0.337
> [207] Avg Loss: 0.291
> No improvement. Patience: 9/10
> [208,   100] loss: 0.413
> [208,   200] loss: 0.294
> [208,   300] loss: 0.315
> [208] Avg Loss: 0.295
> No improvement. Patience: 10/10
> Early stopping triggered.
> ✅ Training completed in 79.91 minutes.
> Accuracy on test images: 83.57%
> Accuracy of plane: 83.70%
> Accuracy of car  : 92.20%
> Accuracy of bird : 78.70%
> Accuracy of cat  : 60.40%
> Accuracy of deer : 79.30%
> Accuracy of dog  : 77.40%
> Accuracy of frog : 90.30%
> Accuracy of horse: 92.50%
> Accuracy of ship : 88.50%
> Accuracy of truck: 92.70%
> 
> Process finished with exit code 0
> ```
>
> 



#### 在 Clab 云服务器 (32 vCPU, 32GB RAM)

- **设备**：`cpu`
- **训练耗时**：636.54 分钟（约 10.6 小时）
- **早停轮次**：第 277 轮
- **测试准确率**：**83.67%**

| 类别    | 准确率                |
| ------- | --------------------- |
| plane   | 84.70%                |
| car     | 91.90%                |
| bird    | 84.00%                |
| **cat** | **65.90%**** ← 最弱项 |
| deer    | 81.10%                |
| dog     | 77.60%                |
| frog    | 89.40%                |
| horse   | 85.00%                |
| ship    | 91.70%                |
| truck   | 85.40%                |

> 预测可视化：
> <img src="https://raw.githubusercontent.com/GMyhf/img/main/img/b353056ebdc1085718fc43ab6d2a1316.png" alt="云服务器结果" style="zoom:50%;" />



> 结果如下：
>
> ```
> /home/rocky/AI_literacy/.venv/bin/python /home/rocky/AI_literacy/CIFAR-10_nn.py 
> 100%|██████████| 170M/170M [00:15<00:00, 11.1MB/s]
> /usr/lib64/python3.9/tarfile.py:2288: RuntimeWarning: The default behavior of tarfile extraction has been changed to disallow common exploits (including CVE-2007-4559). By default, absolute/parent paths are disallowed and some mode bits are cleared. See https://access.redhat.com/articles/7004769 for more details.
>   warnings.warn(
> Using device: cpu
> Starting training with early stopping...
> /home/rocky/AI_literacy/.venv/lib64/python3.9/site-packages/torch/utils/data/dataloader.py:666: UserWarning: 'pin_memory' argument is set as true but no accelerator is found, then device pinned memory won't be used.
>   warnings.warn(warn_msg)
> [1,   100] loss: 1.893
> [1,   200] loss: 1.658
> [1,   300] loss: 1.698
> [1] Avg Loss: 1.804
> [2,   100] loss: 1.399
> [2,   200] loss: 1.580
> [2,   300] loss: 1.407
> [2] Avg Loss: 1.517
> [3,   100] loss: 1.346
> [3,   200] loss: 1.492
> [3,   300] loss: 1.097
> [3] Avg Loss: 1.373
> [4,   100] loss: 1.309
> [4,   200] loss: 1.182
> [4,   300] loss: 1.187
> [4] Avg Loss: 1.244
> [5,   100] loss: 1.104
> [5,   200] loss: 1.084
> [5,   300] loss: 1.081
> [5] Avg Loss: 1.151
> ......
> [267,   100] loss: 0.278
> [267,   200] loss: 0.226
> [267,   300] loss: 0.188
> [267] Avg Loss: 0.249
> [268,   100] loss: 0.218
> [268,   200] loss: 0.220
> [268,   300] loss: 0.206
> [268] Avg Loss: 0.256
> No improvement. Patience: 1/10
> [269,   100] loss: 0.200
> [269,   200] loss: 0.175
> [269,   300] loss: 0.298
> [269] Avg Loss: 0.256
> No improvement. Patience: 2/10
> [270,   100] loss: 0.325
> [270,   200] loss: 0.265
> [270,   300] loss: 0.319
> [270] Avg Loss: 0.258
> No improvement. Patience: 3/10
> [271,   100] loss: 0.316
> [271,   200] loss: 0.139
> [271,   300] loss: 0.263
> [271] Avg Loss: 0.251
> No improvement. Patience: 4/10
> [272,   100] loss: 0.260
> [272,   200] loss: 0.184
> [272,   300] loss: 0.141
> [272] Avg Loss: 0.256
> No improvement. Patience: 5/10
> [273,   100] loss: 0.263
> [273,   200] loss: 0.327
> [273,   300] loss: 0.246
> [273] Avg Loss: 0.250
> No improvement. Patience: 6/10
> [274,   100] loss: 0.193
> [274,   200] loss: 0.221
> [274,   300] loss: 0.227
> [274] Avg Loss: 0.250
> No improvement. Patience: 7/10
> [275,   100] loss: 0.185
> [275,   200] loss: 0.354
> [275,   300] loss: 0.254
> [275] Avg Loss: 0.258
> No improvement. Patience: 8/10
> [276,   100] loss: 0.354
> [276,   200] loss: 0.326
> [276,   300] loss: 0.246
> [276] Avg Loss: 0.250
> No improvement. Patience: 9/10
> [277,   100] loss: 0.183
> [277,   200] loss: 0.383
> [277,   300] loss: 0.295
> [277] Avg Loss: 0.256
> No improvement. Patience: 10/10
> Early stopping triggered.
> ✅ Training completed in 636.54 minutes.
> Accuracy on test images: 83.67%
> Accuracy of plane: 84.70%
> Accuracy of car  : 91.90%
> Accuracy of bird : 84.00%
> Accuracy of cat  : 65.90%
> Accuracy of deer : 81.10%
> Accuracy of dog  : 77.60%
> Accuracy of frog : 89.40%
> Accuracy of horse: 85.00%
> Accuracy of ship : 91.70%
> Accuracy of truck: 85.40%
> 
> Process finished with exit code 0
> 
> ```
>
> 
>
> ![f44849630ac92c19ff8f0b2e922801ab](https://raw.githubusercontent.com/GMyhf/img/main/img/f44849630ac92c19ff8f0b2e922801ab.png)
>
> 



### 常见问题解答（FAQ）

**Q1: 为什么不用 `transforms.Resize(224)`？**

- **关键点**：是否使用预训练权重。
  - 若 `weights=None`（从头训练）→ **不需要 Resize**，可直接用 32×32 输入。
  - 若 `weights=ResNet18_Weights.DEFAULT` → 必须 Resize 到 ≥224×224，或修改首层卷积核。

> 本项目选择从头训练，故保留原始分辨率，避免信息失真。

------

**Q2: 如何解读 `_, predicted = torch.max(outputs, 1)`？**

- `outputs`：形状为 `(N, 10)` 的 logits 张量。
- `torch.max(..., dim=1)`：沿类别维度（dim=1）找最大值。
  - 返回 `(values, indices)`
  - `_` 忽略最大值，`predicted` 保留类别索引（0~9）

> 示例：若输出 `[2.1, 4.2, ..., 3.3]`，则 `predicted = 1`（对应 "automobile"）

------

**Q3: 每类准确率是如何计算的？**

通过遍历测试集，对每个样本：

1. 判断 `predicted == label`
2. 累加到对应类别的 `class_correct[label]`
3. 同时累加 `class_total[label]`

最终：`accuracy[i] = class_correct[i] / class_total[i]`

> 这能揭示模型弱点（如“猫”类准确率显著偏低）。



### 与 Baseline 对比总结

| 方法                          | 准确率     | 是否超越 82%？ |
| ----------------------------- | ---------- | -------------- |
| 原始简易 CNN                  | 76.77%     | ❌              |
| **本项目（ResNet18 + 增强）** | **83.57%** | ✅              |
| cuda-convnet（无增强）        | 82%        | —              |
| cuda-convnet（有增强）        | 89%        | ⚠️ 仍有差距     |

> 下一步可尝试：MixUp、Cutout、Label Smoothing、更大模型（如 ResNet50）、迁移学习等。

------



> 附录：ImageNet Top-5 错误率演进（参考）
>
> ![ImageNet Top-5 Error](https://raw.githubusercontent.com/GMyhf/img/main/img/image-20250726164756658.png)
>
> - **2012 AlexNet**：开启深度学习时代（16.4% < 26%）
> - **2015 ResNet**：首次超越人类（3.6% < 5.0%）
> - **Top-5 定义**：只要真实标签在模型预测的前5名中，即视为正确。



### 结论

通过合理使用 **现代网络架构（ResNet18）** + **充分的数据增强** + **学习率调度**，我们在 CIFAR-10 上轻松超越了早期 CNN 基线，验证了“更强模型 + 更好训练策略 = 更高性能”的原则。





## 4.5 基于 ResNet50 的 Tiny ImageNet 图像分类

本项目演示如何使用 **PyTorch** 和 **torchvision** 在 **Tiny ImageNet** 数据集上微调 **预训练 ResNet50 模型**，完成图像分类任务。尽管 Tiny ImageNet（约 500MB）远小于完整 ImageNet（150GB+），但仍需合理配置数据路径、批大小（batch size）和设备资源。我们在 Apple Silicon（MPS 后端）上成功完成 25 轮训练，验证准确率达 **80.14%**，耗时约 4.5 小时。



### 1. 背景知识

#### 1.1 为什么选择 Tiny ImageNet？

| 特性     | ImageNet                 | Tiny ImageNet     |
| -------- | ------------------------ | ----------------- |
| 类别数   | 1,000                    | 200               |
| 训练图像 | ~128 万张                | 10 万张（500/类） |
| 验证图像 | 5 万张                   | 1 万张（50/类）   |
| 图像尺寸 | 通常 224×224（原始更大） | 固定 64×64        |
| 磁盘占用 | ~150 GB                  | ~250 MB（压缩后） |

Tiny ImageNet 保留了 ImageNet 的语义多样性，同时大幅降低计算开销，非常适合教学、原型验证和本地调试。

#### 1.2 为什么使用 ResNet50？

ResNet50 是由 He et al. (2015) 提出的经典深度卷积网络，其核心创新是**残差连接（skip connection）**，有效缓解了深层网络中的梯度消失与退化问题。

- **结构**：50 层（含卷积、池化、全连接）
- **输入尺寸**：224×224（需对 64×64 图像进行上采样）
- **迁移学习优势**：在 ImageNet 上预训练的权重可显著加速收敛
- **输出层**：默认 1000 类 → 微调为 200 类

------

### 2. 数据准备

#### 2.1 下载与预处理

官方数据集地址： 

```bash
wget http://cs231n.stanford.edu/tiny-imagenet-200.zip
```

> 或者直接下载预处理好的数据。
>
> tiny-imagenet-200.zip, https://disk.pku.edu.cn/link/AA068C93E37D564808A74B8F282DCE0F11
> Name: tiny-imagenet-200.zip
> Expires: Never



解压后，`val/` 目录下的所有图像位于同一文件夹，不符合 `torchvision.datasets.ImageFolder` 的要求（需按类别分目录）。我们提供自动化脚本 `tinyimagenet.sh` 完成整理：

```bash
#!/bin/bash

# download and unzip dataset
#wget http://cs231n.stanford.edu/tiny-imagenet-200.zip
unzip tiny-imagenet-200.zip

current="$(pwd)/tiny-imagenet-200"

# training data
cd $current/train
for DIR in $(ls); do
   cd $DIR
   rm *.txt
   mv images/* .
   rm -r images
   cd ..
done

# validation data
cd $current/val
annotate_file="val_annotations.txt"
length=$(cat $annotate_file | wc -l)
for i in $(seq 1 $length); do
    # fetch i th line
    line=$(sed -n ${i}p $annotate_file)
    # get file name and directory name
    file=$(echo $line | cut -f1 -d" " )
    directory=$(echo $line | cut -f2 -d" ")
    mkdir -p $directory
    mv images/$file $directory
done
rm -r images
echo "done"
```

运行后目录结构如下：

```
tiny-imagenet-200/
├── train/          # 200 个子目录，每类 500 张图
├── val/            # 200 个子目录，每类 50 张图
├── test/           # 无标签（用于竞赛）
├── wnids.txt       # 类别 ID 列表
└── words.txt       # 类别名称映射
```

> 总大小约 **472 MB**。

------

### 3. 模型训练

#### 3.1 环境与硬件

- **设备**：Mac Studio (Apple M1 Ultra, 64GB 统一内存)
- **PyTorch 后端**：MPS（Metal Performance Shaders）
- **关键限制**：MPS **不支持 float64**，需显式使用 `.float()`

#### 3.2 完整代码

 `tiny_imagenet_resnet50_epoch25.py` 

```python
import os
import copy
import torch
import torch.nn as nn
import torch.optim as optim
from torchvision import datasets, models, transforms

# 训练和验证函数
def train_model(model, criterion, optimizer, scheduler, dataloaders, dataset_sizes, num_epochs=25, device='cpu'):
    best_model_wts = copy.deepcopy(model.state_dict())
    best_acc = 0.0

    for epoch in range(num_epochs):
        print('Epoch {}/{}'.format(epoch+1, num_epochs))
        print('-' * 10)

        # 每个 epoch 分为训练和验证阶段
        for phase in ['train', 'val']:
            if phase == 'train':
                model.train()  # 设置为训练模式
            else:
                model.eval()   # 设置为评估模式

            running_loss = 0.0
            running_corrects = 0

            # 遍历数据
            for inputs, labels in dataloaders[phase]:
                inputs = inputs.to(device)
                labels = labels.to(device)

                optimizer.zero_grad()  # 梯度清零

                # 前向传播
                with torch.set_grad_enabled(phase == 'train'):
                    outputs = model(inputs)
                    _, preds = torch.max(outputs, 1)
                    loss = criterion(outputs, labels)

                    # 仅在训练阶段反向传播与参数更新
                    if phase == 'train':
                        loss.backward()
                        optimizer.step()

                running_loss += loss.item() * inputs.size(0)
                running_corrects += torch.sum(preds == labels.data)

            if phase == 'train':
                scheduler.step()

            epoch_loss = running_loss / dataset_sizes[phase]

            # MPS 后端不支持 float64 运算。解决方法是使用 float32，即调用 .float()。
            #epoch_acc = running_corrects.double() / dataset_sizes[phase]
            epoch_acc = running_corrects.float() / dataset_sizes[phase]

            print('{} Loss: {:.4f} Acc: {:.4f}'.format(phase, epoch_loss, epoch_acc))

            # 保存最佳模型参数
            if phase == 'val' and epoch_acc > best_acc:
                best_acc = epoch_acc
                best_model_wts = copy.deepcopy(model.state_dict())
        print()

    print('Best val Acc: {:.4f}'.format(best_acc))
    model.load_state_dict(best_model_wts)
    return model

def main():
    # 1. 数据预处理与加载
    # 注意：此处假定ImageNet数据集按照train/val文件夹分别存放各类别图片，
    # 且每个类别作为一个子文件夹存在
    data_transforms = {
        'train': transforms.Compose([
            transforms.RandomResizedCrop(224),           # 随机裁剪为224×224
            transforms.RandomHorizontalFlip(),           # 随机水平翻转
            transforms.ToTensor(),                         # 转为Tensor
            transforms.Normalize([0.485, 0.456, 0.406],    # ImageNet均值
                                 [0.229, 0.224, 0.225])      # ImageNet标准差
        ]),
        'val': transforms.Compose([
            transforms.Resize(256),
            transforms.CenterCrop(224),                           # 中心裁剪
            transforms.ToTensor(),
            transforms.Normalize([0.485, 0.456, 0.406],
                                 [0.229, 0.224, 0.225])
        ]),
    }

    # Tiny ImageNet 数据路径
    data_dir = '/Users/hfyan/data/tiny-imagenet-200'
    image_datasets = {x: datasets.ImageFolder(os.path.join(data_dir, x),
                                                data_transforms[x])
                      for x in ['train', 'val']}

    # 设置 num_workers 为 8 以利用多进程数据加载
    dataloaders = {x: torch.utils.data.DataLoader(image_datasets[x],
                                                    batch_size=128,    # 可根据实际情况调整
                                                    shuffle=True,
                                                    num_workers=8)
                   for x in ['train', 'val']}

    dataset_sizes = {x: len(image_datasets[x]) for x in ['train', 'val']}
    class_names = image_datasets['train'].classes

    #device = torch.device("cuda:0" if torch.cuda.is_available() else "cpu")
    # 使用 MPS 作为 GPU 后端（适用于 Apple Silicon）
    if torch.backends.mps.is_available():
        device = torch.device("mps")
        print("Using MPS device for GPU acceleration")
    else:
        device = torch.device("cpu")
        print("MPS device not available, using CPU")

    #2. 构建模型（使用预训练 ResNet50）
    # 这里我们加载预训练的 ResNet50 模型，并修改最后的全连接层以适应Tiny ImageNet的类别数（200类）
    model_ft = models.resnet50(weights=models.ResNet50_Weights.DEFAULT)
    num_ftrs = model_ft.fc.in_features
    model_ft.fc = nn.Linear(num_ftrs, len(class_names))
    model_ft = model_ft.to(device)

    criterion = nn.CrossEntropyLoss()
    optimizer_ft = optim.SGD(model_ft.parameters(), lr=0.001, momentum=0.9)

    # 学习率调整策略，每7个epoch降低一次学习率
    exp_lr_scheduler = optim.lr_scheduler.StepLR(optimizer_ft, step_size=7, gamma=0.1)

    #3. 训练模型
    num_epochs = 25  # 可根据需要调整epoch数量
    model_ft = train_model(model_ft, criterion, optimizer_ft, exp_lr_scheduler,
                           dataloaders, dataset_sizes, num_epochs=num_epochs, device=device)

    #4. 保存模型，文件名建议为 tiny_imagenet_resnet50_epoch25.pth
    torch.save(model_ft.state_dict(), 'tiny_imagenet_resnet50_epoch25.pth')
    print("Model saved as tiny_imagenet_resnet50_epoch25.pth")

if __name__ == '__main__':
    main()
```

> **说明**
>
> - **数据预处理**
>   使用了 `transforms` 对数据进行了数据增强（如随机裁剪、水平翻转）以及归一化（ImageNet常用的均值和标准差）。数据文件夹需要符合 `ImageFolder` 的要求，每个类别存放在独立的子文件夹中。
> - **模型构建**
>   本示例中采用预训练的 ResNet50 模型，并修改了最后一层全连接层以输出与类别数匹配的概率分布。
> - **训练过程**
>   代码中定义了 `train_model` 函数，对模型进行训练和验证，并在验证集上选取准确率最高的模型参数。学习率调度器用于逐步降低学习率以便更好地收敛。
> - **注意事项**
>   - ImageNet 数据集较大，建议在使用时注意数据加载、内存管理和训练时长。
>   - 如需更深入的模型调优或使用分布式训练，请参考 PyTorch 官方文档和相关资料。
>
> 该示例代码为入门级示例，实际项目中可能需要更多的优化和配置。
>
> 
>
> **主入口保护**：所有涉及多进程或多线程的代码都封装在 `if __name__ == '__main__':` 下，避免 macOS 下的启动问题。



**2025/2/24 11:30开始运行，16:00结束**

>  File "/Users/hfyan/data/tiny_imagenet_resnet50_epoch25.py", line 47, in train_model
>
>  epoch_acc = running_corrects.double() / dataset_sizes[phase]
>
>  TypeError: Cannot convert a MPS Tensor to float64 dtype as the MPS framework doesn't support float64. Please use float32 instead.
>
>  (base) hfyan@HongfeideMac-Studio data % python tiny_imagenet_resnet50_epoch25.py 

```
(base) hfyan@HongfeideMac-Studio data % python tiny_imagenet_resnet50_epoch25.py 
Using MPS device for GPU acceleration
Epoch 1/25
----------
train Loss: 5.0366 Acc: 0.0720
val Loss: 4.1348 Acc: 0.2819

Epoch 2/25
----------
train Loss: 3.2563 Acc: 0.3406
val Loss: 1.7006 Acc: 0.6197

Epoch 3/25
----------
train Loss: 2.1834 Acc: 0.5065
val Loss: 1.2068 Acc: 0.7062

Epoch 4/25
----------
train Loss: 1.8635 Acc: 0.5663
val Loss: 1.0010 Acc: 0.7498

Epoch 5/25
----------
train Loss: 1.6788 Acc: 0.6029
val Loss: 0.8927 Acc: 0.7702

Epoch 6/25
----------
train Loss: 1.5723 Acc: 0.6268
val Loss: 0.8407 Acc: 0.7808

Epoch 7/25
----------
train Loss: 1.5044 Acc: 0.6390
val Loss: 0.7990 Acc: 0.7907

Epoch 8/25
----------
train Loss: 1.4324 Acc: 0.6567
val Loss: 0.7788 Acc: 0.7939

Epoch 9/25
----------
train Loss: 1.4212 Acc: 0.6571
val Loss: 0.7701 Acc: 0.7981

Epoch 10/25
----------
train Loss: 1.4054 Acc: 0.6614
val Loss: 0.7669 Acc: 0.7966

Epoch 11/25
----------
train Loss: 1.4035 Acc: 0.6615
val Loss: 0.7634 Acc: 0.7980

Epoch 12/25
----------
train Loss: 1.3995 Acc: 0.6626
val Loss: 0.7595 Acc: 0.7990

Epoch 13/25
----------
train Loss: 1.3882 Acc: 0.6647
val Loss: 0.7558 Acc: 0.7988

Epoch 14/25
----------
train Loss: 1.3747 Acc: 0.6680
val Loss: 0.7517 Acc: 0.7997

Epoch 15/25
----------
train Loss: 1.3754 Acc: 0.6683
val Loss: 0.7490 Acc: 0.8006

Epoch 16/25
----------
train Loss: 1.3685 Acc: 0.6689
val Loss: 0.7592 Acc: 0.7970

Epoch 17/25
----------
train Loss: 1.3771 Acc: 0.6681
val Loss: 0.7567 Acc: 0.8009

Epoch 18/25
----------
train Loss: 1.3690 Acc: 0.6688
val Loss: 0.7508 Acc: 0.8011

Epoch 19/25
----------
train Loss: 1.3716 Acc: 0.6694
val Loss: 0.7521 Acc: 0.8008

Epoch 20/25
----------
train Loss: 1.3729 Acc: 0.6687
val Loss: 0.7527 Acc: 0.8002

Epoch 21/25
----------
train Loss: 1.3709 Acc: 0.6689
val Loss: 0.7501 Acc: 0.8014

Epoch 22/25
----------
train Loss: 1.3706 Acc: 0.6708
val Loss: 0.7516 Acc: 0.8008

Epoch 23/25
----------
train Loss: 1.3681 Acc: 0.6696
val Loss: 0.7502 Acc: 0.8002

Epoch 24/25
----------
train Loss: 1.3725 Acc: 0.6698
val Loss: 0.7508 Acc: 0.8003

Epoch 25/25
----------
train Loss: 1.3708 Acc: 0.6696
val Loss: 0.7480 Acc: 0.8004

Best val Acc: 0.8014
Model saved as tiny_imagenet_resnet50_epoch25.pth

```

跑了4小时30分钟。

<img src="https://raw.githubusercontent.com/GMyhf/img/main/img/image-20250224171542842.png" alt="image-20250224171542842" style="zoom:50%;" />



```
% ls -lh *.pth
-rw-r--r--  1 hfyan  staff    92M Feb 24 16:02 tiny_imagenet_resnet50_epoch25.pth
```







#### 3.3 常见问题解答

##### Q1：为何每次运行都重新下载 ResNet50 权重？

PyTorch 默认缓存至 `~/.cache/torch/hub/checkpoints/`。若重复下载，请检查：

- 文件是否存在且完整（`resnet50-11ad3fa6.pth` ≈ 97MB）
- 目录写权限
- 是否使用临时环境（如容器）

可通过设置环境变量指定缓存路径：

```bash
export TORCH_HOME=/path/to/stable/cache
```

##### Q2：MPS 报错 “Cannot convert to float64”？

Apple MPS 不支持 double 精度。务必使用：

```python
accuracy = correct.float() / total  # ✅ 正确
# accuracy = correct.double() / total  # ❌ 错误
```

##### Q3：如何命名模型文件？

推荐格式：`{dataset}_{model}_{epochs}.pth`
示例：`tiny_imagenet_resnet50_epoch25.pth`

------

### 4. 模型评估

前面已经保存了模型权重，可以通过如下步骤加载模型并在验证集上进行评估：

1. **加载模型结构和权重**  
   请确保你定义的模型结构与训练时保持一致。使用 `torch.load` 加载权重，并用 `model.load_state_dict` 导入。

2. **切换到评估模式**  
   调用 `model.eval()` 确保模型关闭 BatchNorm、Dropout 等训练时特有的行为。

3. **遍历验证数据并计算准确率**  
   使用 `torch.no_grad()` 关闭梯度计算，加快验证速度，并防止内存浪费。

下面是一个完整的示例代码，`eval_tiny_imagenet_resnet50_epoch25_pth.py `：

```python
import os
import torch
import torch.nn as nn
from torchvision import datasets, models, transforms

# 数据预处理
data_transforms = {
    'val': transforms.Compose([
        transforms.Resize(256),
        transforms.CenterCrop(224),
        transforms.ToTensor(),
        transforms.Normalize([0.485, 0.456, 0.406],
                             [0.229, 0.224, 0.225])
    ]),
}

# 确保子进程安全启动
if __name__ == '__main__':
    data_dir = '/Users/hfyan/data/tiny-imagenet-200'
    val_dir = os.path.join(data_dir, 'val')
    val_dataset = datasets.ImageFolder(val_dir, data_transforms['val'])
    val_loader = torch.utils.data.DataLoader(val_dataset, batch_size=64,
                                             shuffle=False, num_workers=4)

    # 选择设备
    if torch.backends.mps.is_available():
        device = torch.device("mps")
        print("Using MPS device for GPU acceleration")
    else:
        device = torch.device("cpu")
        print("MPS device not available, using CPU")

    # 加载模型
    model_ft = models.resnet50(pretrained=False)
    num_ftrs = model_ft.fc.in_features
    model_ft.fc = nn.Linear(num_ftrs, len(val_dataset.classes))
    model_ft = model_ft.to(device)

    # 加载模型权重
    model_path = 'tiny_imagenet_resnet50_epoch25.pth'
    model_ft.load_state_dict(torch.load(model_path, map_location=device))

    # 评估模式
    model_ft.eval()

    # 模型评估
    running_corrects = 0
    total_samples = 0

    with torch.no_grad():
        for inputs, labels in val_loader:
            inputs = inputs.to(device)
            labels = labels.to(device)

            outputs = model_ft(inputs)
            _, preds = torch.max(outputs, 1)
            running_corrects += torch.sum(preds == labels.data)
            total_samples += inputs.size(0)

    val_acc = running_corrects.float() / total_samples
    print('Validation Accuracy: {:.4f}'.format(val_acc))

```

验证步骤：  

> - 加载与你训练时一致的模型结构。  
> - 使用 `model.load_state_dict()` 加载权重。  
> - 调用 `model.eval()` 进入验证模式。  
> - 遍历验证数据集，计算准确率或其他指标。
>
> 这样，你就可以加载已保存的模型并对验证集数据进行测试。
>
> ![image-20250224171857564](https://raw.githubusercontent.com/GMyhf/img/main/img/image-20250224171857564.png)
>
> 
>
> ```python
> (base) hfyan@HongfeideMac-Studio data % python eval_tiny_imagenet_resnet50_epoch25_pth.py 
> Using MPS device for GPU acceleration
> /Users/hfyan/miniconda3/lib/python3.10/site-packages/torchvision/models/_utils.py:208: UserWarning: The parameter 'pretrained' is deprecated since 0.13 and may be removed in the future, please use 'weights' instead.
>   warnings.warn(
> /Users/hfyan/miniconda3/lib/python3.10/site-packages/torchvision/models/_utils.py:223: UserWarning: Arguments other than a weight enum or `None` for 'weights' are deprecated since 0.13 and may be removed in the future. The current behavior is equivalent to passing `weights=None`.
>   warnings.warn(msg)
> Validation Accuracy: 0.8014
> (base) hfyan@HongfeideMac-Studio data % 
> ```





### 5. 扩展与优化

#### 5.1 性能对比：ImageNet vs Tiny ImageNet

| 指标      | ImageNet (ResNet50)           | Tiny ImageNet (本实验)   |
| --------- | ----------------------------- | ------------------------ |
| Top-1 Acc | ~76.5%（原始）→ 84%（优化后） | **80.14%**               |
| 训练时间  | 数天（8×V100）                | **4.5 小时**（M1 Ultra） |
| 显存需求  | >16 GB                        | <8 GB（batch=128）       |

------

#### 5.2 关于多进程与 GIL

- `DataLoader(num_workers>0)` 使用 **多进程**（非线程），绕过 Python GIL
- PyTorch 底层计算（C++/CUDA/Metal）不受 GIL 限制
- 小规模任务（如小矩阵乘法）并行可能因通信开销而变慢



#### 总结

本项目完整展示了从数据准备、模型微调到评估的全流程，适合入门者理解迁移学习与 PyTorch 实践。通过合理利用 Apple Silicon 的 MPS 加速，可在消费级设备上高效完成中等规模视觉任务。



# 5. 运行《从零构建大模型》代码

《从零构建大模型》代码，https://github.com/rasbt/LLMs-from-scratch

Build a Large Language Model (From Scratch)

可以在本地 mac 或者 window 运行，配置方法方法如： ...Setup_....md。

https://github.com/GMyhf/2025fall-cs201/tree/main/LLM





# 附录A. PyTorch教程@runoob

https://www.runoob.com/pytorch/pytorch-tutorial.html

PyTorch 是一个开源的机器学习库，主要用于进行计算机视觉（CV）、自然语言处理（NLP）、语音识别等领域的研究和开发。

PyTorch由 Facebook 的人工智能研究团队开发，并在机器学习和深度学习社区中广泛使用。

PyTorch 以其灵活性和易用性而闻名，特别适合于深度学习研究和开发。



## A.1 PyTorch安装

在已经安装好的python环境中，在terminal窗口命令行中，激活环境，并安装torch包

> Python开发环境配置指南，https://github.com/GMyhf/2025fall-cs101/blob/main/Python_Development_Setup_Mac_Windows.md

```
[hfyan@HongfeideMac-Studio MyPythonApp % source .venv/bin/activate
(.venv) hfyan@HongfeideMac-Studio MyPythonApp % uv pip install torch torchvision torchaudio

```



**验证安装**

为了确保 PyTorch 已正确安装，我们可以通过执行以下 PyTorch 代码来验证是否安装成功：

**实例**

```python
import torch

# 当前安装的 PyTorch 库的版本
print(torch.__version__)

# 检测 MPS 作为 GPU 后端是否可用（适用于 Apple Silicon）
if torch.backends.mps.is_available():
    device = torch.device("mps")
    print("Using MPS device for GPU acceleration")
else:   # 检查 CUDA 是否可用，即你的系统有 NVIDIA 的 GPU
    device = torch.device("cuda:0" if torch.cuda.is_available() else "cpu")
    print("MPS device not available, using CPU")

"""
2.9.1
Using MPS device for GPU acceleration
"""
```



一个简单的实例，构建一个随机初始化的张量：

```python
import torch
x = torch.rand(5, 3)
print(x)
```

如果安装成功，输出结果类似如下：

```
tensor([[0.8622, 0.5916, 0.8073],
        [0.8955, 0.7416, 0.3482],
        [0.8059, 0.1414, 0.2828],
        [0.0923, 0.0113, 0.4226],
        [0.4438, 0.9789, 0.9048]])
```



**实例**

下面的是 PyTorch 中一些基本的张量操作：如何创建随机张量、进行逐元素运算、访问特定元素以及计算总和和最大值。

```python
import torch

# 设置数据类型和设备
dtype = torch.float  # 张量数据类型为浮点型
device = torch.device("cpu")  # 本次计算在 CPU 上进行

# 创建并打印两个随机张量 a 和 b
a = torch.randn(2, 3, device=device, dtype=dtype)  # 创建一个 2x3 的随机张量
b = torch.randn(2, 3, device=device, dtype=dtype)  # 创建另一个 2x3 的随机张量

print("张量 a:")
print(a)

print("张量 b:")
print(b)

# 逐元素相乘并输出结果
print("a 和 b 的逐元素乘积:")
print(a * b)

# 输出张量 a 所有元素的总和
print("张量 a 所有元素的总和:")
print(a.sum())

# 输出张量 a 中第 2 行第 3 列的元素（注意索引从 0 开始）
print("张量 a 第 2 行第 3 列的元素:")
print(a[1, 2])

# 输出张量 a 中的最大值
print("张量 a 中的最大值:")
print(a.max())

"""
张量 a:
tensor([[ 0.8182,  0.4718,  0.8318],
        [ 0.8146,  0.1508, -1.7619]])
张量 b:
tensor([[-1.7713,  0.8521,  0.4598],
        [ 0.3082,  0.0558,  0.1254]])
a 和 b 的逐元素乘积:
tensor([[-1.4493,  0.4020,  0.3824],
        [ 0.2510,  0.0084, -0.2209]])
张量 a 所有元素的总和:
tensor(1.3252)
张量 a 第 2 行第 3 列的元素:
tensor(-1.7619)
张量 a 中的最大值:
tensor(0.8318)
"""
```



## A.2 PyTorch 简介

PyTorch 是一个开源的 Python 机器学习库，基于 Torch 库，底层由 C++ 实现，应用于人工智能领域，如计算机视觉和自然语言处理。

PyTorch 最初由 Meta Platforms 的人工智能研究团队开发，现在属 于Linux 基金会的一部分。

许多深度学习软件都是基于 PyTorch 构建的，包括特斯拉自动驾驶、Uber 的 Pyro、Hugging Face 的 Transformers、 PyTorch Lightning 和 Catalyst。

**PyTorch 主要有两大特征：**

- 类似于 NumPy 的张量计算，能在 GPU 或 MPS 等硬件加速器上加速。
- 基于带自动微分系统的深度神经网络。

PyTorch 包括 torch.autograd、torch.nn、torch.optim 等子模块。

PyTorch 包含多种损失函数，包括 MSE（均方误差 = L2 范数）、交叉熵损失和负熵似然损失（对分类器有用）等。

### PyTorch 特性

- **动态计算图（Dynamic Computation Graphs）**： PyTorch 的计算图是动态的，这意味着它们在运行时构建，并且可以随时改变。这为实验和调试提供了极大的灵活性，因为开发者可以逐行执行代码，查看中间结果。
- **自动微分（Automatic Differentiation）**： PyTorch 的自动微分系统允许开发者轻松地计算梯度，这对于训练深度学习模型至关重要。它通过反向传播算法自动计算出损失函数对模型参数的梯度。
- **张量计算（Tensor Computation）**： PyTorch 提供了类似于 NumPy 的张量操作，这些操作可以在 CPU 和 GPU 上执行，从而加速计算过程。张量是 PyTorch 中的基本数据结构，用于存储和操作数据。
- **丰富的 API**： PyTorch 提供了大量的预定义层、损失函数和优化算法，这些都是构建深度学习模型的常用组件。
- **多语言支持**： PyTorch 虽然以 Python 为主要接口，但也提供了 C++ 接口，允许更底层的集成和控制。

#### 动态计算图（Dynamic Computation Graph）

PyTorch 最显著的特点之一是其动态计算图的机制。

与 TensorFlow 的静态计算图（graph）不同，PyTorch 在执行时构建计算图，这意味着在每次计算时，图都会根据输入数据的形状自动变化。

**动态计算图的优点：**

- 更加灵活，特别适用于需要条件判断或递归的场景。
- 方便调试和修改，能够直接查看中间结果。
- 更接近 Python 编程的风格，易于上手。

#### 张量（Tensor）与自动求导（Autograd）

PyTorch 中的核心数据结构是 **张量（Tensor）**，它是一个多维矩阵，可以在 CPU 或 GPU 上高效地进行计算。张量的操作支持自动求导（Autograd）机制，使得在反向传播过程中自动计算梯度，这对于深度学习中的梯度下降优化算法至关重要。

**张量（Tensor）：**

- 支持在 CPU 和 GPU 之间进行切换。
- 提供了类似 NumPy 的接口，支持元素级运算。
- 支持自动求导，可以方便地进行梯度计算。

**自动求导（Autograd）：**

- PyTorch 内置的自动求导引擎，能够自动追踪所有张量的操作，并在反向传播时计算梯度。
- 通过 `requires_grad` 属性，可以指定张量需要计算梯度。
- 支持高效的反向传播，适用于神经网络的训练。

#### 模型定义与训练

PyTorch 提供了 `torch.nn` 模块，允许用户通过继承 `nn.Module` 类来定义神经网络模型。使用 `forward` 函数指定前向传播，自动反向传播（通过 `autograd`）和梯度计算也由 PyTorch 内部处理。

**神经网络模块（torch.nn）：**

- 提供了常用的层（如线性层、卷积层、池化层等）。
- 支持定义复杂的神经网络架构（包括多输入、多输出的网络）。
- 兼容与优化器（如 `torch.optim`）一起使用。

#### GPU 加速

PyTorch 完全支持在 GPU 上运行，以加速深度学习模型的训练。通过简单的 `.to(device)` 方法，用户可以将模型和张量转移到 GPU 上进行计算。PyTorch 支持多 GPU 训练，能够利用 NVIDIA CUDA 技术显著提高计算效率。

**GPU 支持：**

- 自动选择 GPU 或 CPU。
- 支持通过 CUDA 加速运算。
- 支持多 GPU 并行计算（`DataParallel` 或 `torch.distributed`）。

#### 生态系统与社区支持

PyTorch 作为一个开源项目，拥有一个庞大的社区和生态系统。它不仅在学术界得到了广泛的应用，也在工业界，特别是在计算机视觉、自然语言处理等领域中得到了广泛部署。PyTorch 还提供了许多与深度学习相关的工具和库，如：

- **torchvision**：用于计算机视觉任务的数据集和模型。
- **torchtext**：用于自然语言处理任务的数据集和预处理工具。
- **torchaudio**：用于音频处理的工具包。
- **PyTorch Lightning**：一种简化 PyTorch 代码的高层库，专注于研究和实验的快速迭代。

------

### 与其他框架的对比

PyTorch 由于其灵活性、易用性和社区支持，已经成为很多深度学习研究者和开发者的首选框架。

#### TensorFlow vs PyTorch

- PyTorch 的动态计算图使得它更加灵活，适合快速实验和研究；而 TensorFlow 的静态计算图在生产环境中更具优化空间。
- PyTorch 在调试时更加方便，TensorFlow 则在部署上更加成熟，支持更广泛的硬件和平台。
- 近年来，TensorFlow 也引入了动态图（如 TensorFlow 2.x），使得两者在功能上趋于接近。
- 其他深度学习框架，如 Keras、Caffe 等也有一定应用，但 PyTorch 由于其灵活性、易用性和社区支持，已经成为很多深度学习研究者和开发者的首选框架。

| 特性               | **TensorFlow**                                          | **PyTorch**                                                  |
| :----------------- | :------------------------------------------------------ | :----------------------------------------------------------- |
| **开发公司**       | Google                                                  | Facebook (FAIR)                                              |
| **计算图类型**     | 静态计算图（定义后再执行）                              | 动态计算图（定义即执行）                                     |
| **灵活性**         | 低（计算图在编译时构建，不易修改）                      | 高（计算图在执行时动态创建，易于修改和调试）                 |
| **调试**           | 较难（需要使用 `tf.debugging` 或外部工具调试）          | 容易（可以直接在 Python 中进行调试）                         |
| **易用性**         | 低（较复杂，API 较多，学习曲线较陡峭）                  | 高（API 简洁，语法更加接近 Python，容易上手）                |
| **部署**           | 强（支持广泛的硬件，如 TensorFlow Lite、TensorFlow.js） | 较弱（部署工具和平台相对较少，虽然有 TensorFlow 支持）       |
| **社区支持**       | 很强（成熟且庞大的社区，广泛的教程和文档）              | 很强（社区活跃，特别是在学术界，快速发展的生态）             |
| **模型训练**       | 支持分布式训练，支持多种设备（如 CPU、GPU、TPU）        | 支持分布式训练，支持多 GPU、CPU 和 TPU                       |
| **API 层级**       | 高级API：Keras；低级API：TensorFlow Core                | 高级API：TorchVision、TorchText 等；低级API：Torch           |
| **性能**           | 高（优化方面成熟，适合生产环境）                        | 高（适合研究和原型开发，生产性能也在提升）                   |
| **自动求导**       | 通过 `tf.GradientTape` 实现动态求导（较复杂）           | 通过 `autograd` 动态求导（更简洁和直观）                     |
| **调优与可扩展性** | 强（支持在多平台上运行，如 TensorFlow Serving 等）      | 较弱（虽然在学术和实验环境中表现优越，但生产环境支持相对较少） |
| **框架灵活性**     | 较低（TensorFlow 2.x 引入了动态图特性，但仍不完全灵活） | 高（动态图带来更高的灵活性）                                 |
| **支持多种语言**   | 支持多种语言（Python, C++, Java, JavaScript, etc.）     | 主要支持 Python（但也有 C++ API）                            |
| **兼容性与迁移**   | TensorFlow 2.x 与旧版本兼容性较好                       | 与 TensorFlow 兼容性差，迁移较难                             |

#### PyTorch vs NumPy

| 特性         | PyTorch            | NumPy            |
| :----------- | :----------------- | :--------------- |
| **目标**     | 深度学习专用       | 通用科学计算     |
| **GPU 支持** | 原生支持 CUDA      | 不直接支持       |
| **自动微分** | 内置自动求导       | 需要手动计算梯度 |
| **神经网络** | 丰富的神经网络模块 | 需要从零实现     |
| **学习成本** | 相对较高           | 相对较低         |

------

### PyTorch 的历史与发展

PyTorch 的前身是 Torch，这是一个基于 Lua 语言的科学计算框架。随着 Python 在机器学习领域的兴起，Facebook 团队决定将 Torch 的核心思想移植到 Python 上，从而诞生了 PyTorch。

- **2016年**：Facebook 发布 PyTorch 0.1 版本
- **2017年**：PyTorch 0.2 引入分布式训练支持
- **2018年**：PyTorch 1.0 发布，增加了生产部署能力
- **2019年**：PyTorch 1.3 引入移动端支持
- **2020年**：PyTorch 1.6 增加了自动混合精度训练
- **2021年**：PyTorch 1.9 引入 TorchScript 和 C++ 前端
- **2022年**：PyTorch 1.12 优化了性能和稳定性
- **2023年**：PyTorch 2.0 发布，引入编译模式大幅提升性能



## A.3 PyTorch 基础

PyTorch 是一个开源的深度学习框架，以其灵活性和动态计算图而广受欢迎。

PyTorch 主要有以下几个基础概念：张量（Tensor）、自动求导（Autograd）、神经网络模块（nn.Module）、优化器（optim）等。

- **张量（Tensor）**：PyTorch 的核心数据结构，支持多维数组，并可以在 CPU 或 GPU 上进行加速计算。
- **自动求导（Autograd）**：PyTorch 提供了自动求导功能，可以轻松计算模型的梯度，便于进行反向传播和优化。
- **神经网络（nn.Module）**：PyTorch 提供了简单且强大的 API 来构建神经网络模型，可以方便地进行前向传播和模型定义。
- **优化器（Optimizers）**：使用优化器（如 Adam、SGD 等）来更新模型的参数，使得损失最小化。
- **设备（Device）**：可以将模型和张量移动到 GPU 上以加速计算。

------

### PyTorch 架构总览

PyTorch 采用模块化设计，由多个相互协作的核心组件构成。理解这些组件的作用和相互关系，是掌握 PyTorch 的关键。

**PyTorch 架构图**

```
┌─────────────────────────────────────────────────────────────┐
│                    PyTorch 生态系统                          │
├─────────────────────────────────────────────────────────────┤
│  torchvision  │  torchtext  │  torchaudio  │  其他专业库     │
├─────────────────────────────────────────────────────────────┤
│                     PyTorch 核心                            │
├───────────────┬─────────────────┬───────────────────────────┤
│   torch.nn    │   torch.optim   │      torch.utils          │
│   (神经网络)   │   (优化器)      │      (工具函数)           │
├───────────────┼─────────────────┼───────────────────────────┤
│               │                 │   torch.utils.data        │
│  torch 核心   │  autograd       │   (数据加载)              │
│  (张量计算)   │  (自动微分)     │                           │
└───────────────┴─────────────────┴───────────────────────────┘
```

PyTorch 采用**分层架构**设计，从上层到底层依次为： 

**1、Python API（顶层）**

- `torch`：核心张量计算（类似NumPy，支持GPU）。 
- `torch.nn`：神经网络层、损失函数等。 
- `torch.autograd`：自动微分（反向传播）。 
- 开发者直接调用的接口，简单易用。 

**2、C++核心（中层）**

- **ATen**：张量运算核心库（400+操作）。 
- **JIT**：即时编译优化模型。 
- **Autograd引擎**：自动微分的底层实现。 
- 高性能计算，连接Python与底层硬件。 

**3、基础库（底层）**

- **TH/THNN**：C语言实现的基础张量和神经网络操作。 
- **THC/THCUNN**：对应的CUDA（GPU）版本。 
- 直接操作硬件（CPU/GPU），极致优化速度。 

**执行流程**：
Python代码 → C++核心计算 → 底层CUDA/C库加速 → 返回结果。
既保持易用性，又确保高性能。

<img src="https://raw.githubusercontent.com/GMyhf/img/main/img/iGWbOXL.png" alt="img" style="zoom:67%;" />

**张量（Tensor）**

张量（Tensor）是 PyTorch 中的核心数据结构，用于存储和操作多维数组。

张量可以视为一个多维数组，支持加速计算的操作。

在 PyTorch 中，张量的概念类似于 NumPy 中的数组，但是 PyTorch 的张量可以运行在不同的设备上，比如 CPU 和 GPU，这使得它们非常适合于进行大规模并行计算，特别是在深度学习领域。

- **维度（Dimensionality）**：张量的维度指的是数据的多维数组结构。例如，一个标量（0维张量）是一个单独的数字，一个向量（1维张量）是一个一维数组，一个矩阵（2维张量）是一个二维数组，以此类推。
- **形状（Shape）**：张量的形状是指每个维度上的大小。例如，一个形状为`(3, 4)`的张量意味着它有3行4列。
- **数据类型（Dtype）**：张量中的数据类型定义了存储每个元素所需的内存大小和解释方式。PyTorch支持多种数据类型，包括整数型（如`torch.int8`、`torch.int32`）、浮点型（如`torch.float32`、`torch.float64`）和布尔型（`torch.bool`）。

**张量创建：**

**实例**

```python
import torch

# 创建一个 2x3 的全 0 张量
a = torch.zeros(2, 3)
print(a)

# 创建一个 2x3 的全 1 张量
b = torch.ones(2, 3)
print(b)

# 创建一个 2x3 的随机数张量
c = torch.randn(2, 3)
print(c)

# 从 NumPy 数组创建张量
import numpy as np
numpy_array = np.array([[1, 2], [3, 4]])
tensor_from_numpy = torch.from_numpy(numpy_array)
print(tensor_from_numpy)

# 在指定设备（CPU/GPU）上创建张量
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
d = torch.randn(2, 3, device=device)
print(d)
```

输出结果类似如下：

```
tensor([[0., 0., 0.],
        [0., 0., 0.]])
tensor([[1., 1., 1.],
        [1., 1., 1.]])
tensor([[ 1.0189, -0.5718, -1.2814],
        [-0.5865,  1.0855,  1.1727]])
tensor([[1, 2],
        [3, 4]])
tensor([[-0.3360,  0.2203,  1.3463],
        [-0.5982, -0.2704,  0.5429]])
```

**常用张量操作：**

**实例**

```py
# 张量相加
e = torch.randn(2, 3)
f = torch.randn(2, 3)
print(e + f)

# 逐元素乘法
print(e * f)

# 张量的转置
g = torch.randn(3, 2)
print(g.t()) # 或者 g.transpose(0, 1)

# 张量的形状
print(g.shape) # 返回形状
```



**张量与设备**

PyTorch 张量可以存在于不同的设备上，包括CPU和GPU，你可以将张量移动到 GPU 上以加速计算：

```
if torch.cuda.is_available():
    tensor_gpu = tensor_from_list.to('cuda')  # 将张量移动到GPU
```

**梯度和自动微分**

PyTorch的张量支持自动微分，这是深度学习中的关键特性。当你创建一个需要梯度的张量时，PyTorch可以自动计算其梯度：

**实例**

```python
# 创建一个需要梯度的张量
tensor_requires_grad = torch.tensor([1.0], requires_grad=True)

# 进行一些操作
tensor_result = tensor_requires_grad * 2

# 计算梯度
tensor_result.backward()
print(tensor_requires_grad.grad) # 输出梯度
```



**内存和性能**

PyTorch 张量还提供了一些内存管理功能，比如.clone()、.detach() 和 .to() 方法，它们可以帮助你优化内存使用和提高性能。

------

### 自动求导（Autograd）

自动求导（Automatic Differentiation，简称Autograd）是深度学习框架中的一个核心特性，它允许计算机自动计算数学函数的导数。

在深度学习中，自动求导主要用于两个方面：**一是在训练神经网络时计算梯度**，**二是进行反向传播算法的实现**。

自动求导基于链式法则（Chain Rule），这是一个用于计算复杂函数导数的数学法则。链式法则表明，复合函数的导数是其各个组成部分导数的乘积。在深度学习中，模型通常是由许多层组成的复杂函数，自动求导能够高效地计算这些层的梯度。

**动态图与静态图：**

- **动态图（Dynamic Graph）**：在动态图中，计算图在运行时动态构建。每次执行操作时，计算图都会更新，这使得调试和修改模型变得更加容易。PyTorch使用的是动态图。
- **静态图（Static Graph）**：在静态图中，计算图在开始执行之前构建完成，并且不会改变。TensorFlow最初使用的是静态图，但后来也支持动态图。

PyTorch 提供了自动求导功能，通过 autograd 模块来自动计算梯度。

torch.Tensor 对象有一个 requires_grad 属性，用于指示是否需要计算该张量的梯度。

当你创建一个 requires_grad=True 的张量时，PyTorch 会自动跟踪所有对它的操作，以便在之后计算梯度。

创建需要梯度的张量:

**实例**

```python
# 创建一个需要计算梯度的张量
x = torch.randn(2, 2, requires_grad=True)
print(x)

# 执行某些操作
y = x + 2
z = y * y * 3
out = z.mean()

print(out)


```

输出结果类似如下：

```
tensor([[0., 0., 0.],
        [0., 0., 0.]])
tensor([[1., 1., 1.],
        [1., 1., 1.]])
tensor([[ 1.0189, -0.5718, -1.2814],
        [-0.5865,  1.0855,  1.1727]])
tensor([[1, 2],
        [3, 4]])
tensor([[-0.3360,  0.2203,  1.3463],
        [-0.5982, -0.2704,  0.5429]])
tianqixin@Mac-mini runoob-test % python3 test.py
tensor([[-0.1908,  0.2811],
        [ 0.8068,  0.8002]], requires_grad=True)
tensor(18.1469, grad_fn=<MeanBackward0>)
```

### 反向传播（Backpropagation）

一旦定义了计算图，可以通过 **.backward()** 方法来计算梯度。

**实例**

```python
# 反向传播，计算梯度
out.backward()

# 查看 x 的梯度
print(x.grad)
```

在神经网络训练中，自动求导主要用于实现反向传播算法。

反向传播是一种通过计算损失函数关于网络参数的梯度来训练神经网络的方法。在每次迭代中，网络的前向传播会计算输出和损失，然后反向传播会计算损失关于每个参数的梯度，并使用这些梯度来更新参数。

**停止梯度计算**

如果你不希望某些张量的梯度被计算（例如，当你不需要反向传播时），可以使用 **torch.no_grad()** 或设置 **requires_grad=False**。

**实例**

```python
# 使用 torch.no_grad() 禁用梯度计算
with torch.no_grad():
  y = x * 2
```



------

### 神经网络（nn.Module）

神经网络是一种模仿人脑神经元连接的计算模型，由多层节点（神经元）组成，用于学习数据之间的复杂模式和关系。

神经网络通过调整神经元之间的连接权重来优化预测结果，这一过程涉及前向传播、损失计算、反向传播和参数更新。

神经网络的类型包括前馈神经网络、卷积神经网络（CNN）、循环神经网络（RNN）和长短期记忆网络（LSTM），它们在图像识别、语音处理、自然语言处理等多个领域都有广泛应用。

PyTorch 提供了一个非常方便的接口来构建神经网络模型，即 **torch.nn.Module**。

我们可以继承 nn.Module 类并定义自己的网络层。

创建一个简单的神经网络：

**实例**

```python
import torch.nn as nn
import torch.optim as optim

# 定义一个简单的全连接神经网络
class SimpleNN(nn.Module):
  def init(self):
    super(SimpleNN, self).__init__()
    self.fc1 = nn.Linear(2, 2) # 输入层到隐藏层
    self.fc2 = nn.Linear(2, 1) # 隐藏层到输出层

  def forward(self, x):
    x = torch.relu(self.fc1(x)) # ReLU 激活函数
    x = self.fc2(x)
    return x

# 创建网络实例
model = SimpleNN()

# 打印模型结构
print(model)

```

输出结果：

```
SimpleNN(
  (fc1): Linear(in_features=2, out_features=2, bias=True)
  (fc2): Linear(in_features=2, out_features=1, bias=True)
)
```

**训练过程：**

1. **前向传播（Forward Propagation）**： 在前向传播阶段，输入数据通过网络层传递，每层应用权重和激活函数，直到产生输出。
2. **计算损失（Calculate Loss）**： 根据网络的输出和真实标签，计算损失函数的值。
3. **反向传播（Backpropagation）**： 反向传播利用自动求导技术计算损失函数关于每个参数的梯度。
4. **参数更新（Parameter Update）**： 使用优化器根据梯度更新网络的权重和偏置。
5. **迭代（Iteration）**： 重复上述过程，直到模型在训练数据上的性能达到满意的水平。

### 前向传播与损失计算

**实例**

```python
# 随机输入
x = torch.randn(1, 2)

# 前向传播
output = model(x)
print(output)

# 定义损失函数（例如均方误差 MSE）
criterion = nn.MSELoss()

# 假设目标值为 1
target = torch.randn(1, 1)

# 计算损失
loss = criterion(output, target)
print(loss)
```



### 优化器（Optimizers）

优化器在训练过程中更新神经网络的参数，以减少损失函数的值。

PyTorch 提供了多种优化器，例如 SGD、Adam 等。

使用优化器进行参数更新：

**实例**

```python
# 定义优化器（使用 Adam 优化器）
optimizer = optim.Adam(model.parameters(), lr=0.001)

# 训练步骤
optimizer.zero_grad() # 清空梯度
loss.backward() # 反向传播
optimizer.step() # 更新参数
```



------

### 训练模型

训练模型是机器学习和深度学习中的核心过程，旨在通过大量数据学习模型参数，以便模型能够对新的、未见过的数据做出准确的预测。

训练模型通常包括以下几个步骤：

1. **数据准备**：
   - 收集和处理数据，包括清洗、标准化和归一化。
   - 将数据分为训练集、验证集和测试集。
2. **定义模型**：
   - 选择模型架构，例如决策树、神经网络等。
   - 初始化模型参数（权重和偏置）。
3. **选择损失函数**：
   - 根据任务类型（如分类、回归）选择合适的损失函数。
4. **选择优化器**：
   - 选择一个优化算法，如SGD、Adam等，来更新模型参数。
5. **前向传播**：
   - 在每次迭代中，将输入数据通过模型传递，计算预测输出。
6. **计算损失**：
   - 使用损失函数评估预测输出与真实标签之间的差异。
7. **反向传播**：
   - 利用自动求导计算损失相对于模型参数的梯度。
8. **参数更新**：
   - 根据计算出的梯度和优化器的策略更新模型参数。
9. **迭代优化**：
   - 重复步骤5-8，直到模型在验证集上的性能不再提升或达到预定的迭代次数。
10. **评估和测试**：
    - 使用测试集评估模型的最终性能，确保模型没有过拟合。
11. **模型调优**：
    - 根据模型在测试集上的表现进行调参，如改变学习率、增加正则化等。
12. **部署模型**：
    - 将训练好的模型部署到生产环境中，用于实际的预测任务。

**实例**

```py
import torch
import torch.nn as nn
import torch.optim as optim

# 1. 定义一个简单的神经网络模型
class SimpleNN(nn.Module):
  def init(self):
    super(SimpleNN, self).init()
    self.fc1 = nn.Linear(2, 2) # 输入层到隐藏层
    self.fc2 = nn.Linear(2, 1) # 隐藏层到输出层

  def forward(self, x):
    x = torch.relu(self.fc1(x)) # ReLU 激活函数
    x = self.fc2(x)
    return x

# 2. 创建模型实例
model = SimpleNN()

# 3. 定义损失函数和优化器
criterion = nn.MSELoss() # 均方误差损失函数
optimizer = optim.Adam(model.parameters(), lr=0.001) # Adam 优化器

# 4. 假设我们有训练数据 X 和 Y
X = torch.randn(10, 2) # 10 个样本，2 个特征
Y = torch.randn(10, 1) # 10 个目标值

# 5. 训练循环
for epoch in range(100):  # 训练 100 轮
  optimizer.zero_grad() # 清空之前的梯度
  output = model(X) # 前向传播
  loss = criterion(output, Y) # 计算损失
  loss.backward() # 反向传播
  optimizer.step() # 更新参数

  # 每 10 轮输出一次损失
  if (epoch+1) % 10 == 0:
    print(f'Epoch [{epoch+1}/100], Loss: {loss.item():.4f}')
```

输出结果如下：

```
Epoch [10/100], Loss: 1.7180
Epoch [20/100], Loss: 1.6352
Epoch [30/100], Loss: 1.5590
Epoch [40/100], Loss: 1.4896
Epoch [50/100], Loss: 1.4268
Epoch [60/100], Loss: 1.3704
Epoch [70/100], Loss: 1.3198
Epoch [80/100], Loss: 1.2747
Epoch [90/100], Loss: 1.2346
Epoch [100/100], Loss: 1.1991
```

在每 10 轮，程序会输出当前的损失值，帮助我们跟踪模型的训练进度。随着训练的进行，损失值应该会逐渐降低，表示模型在不断学习并优化其参数。

训练模型是一个迭代的过程，需要不断地调整和优化，直到达到满意的性能。这个过程涉及到大量的实验和调优，目的是使模型在新的、未见过的数据上也能有良好的泛化能力。

------

### 设备（Device）

PyTorch 允许你将模型和数据移动到 GPU 上进行加速。

使用 **torch.device** 来指定计算设备。

将模型和数据移至 GPU:

**实例**

```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

# 将模型移动到设备
model.to(device)

# 将数据移动到设备
X = X.to(device)
Y = Y.to(device)
```

在训练过程中，所有张量和模型都应该移到同一个设备上（要么都在 CPU 上，要么都在 GPU 上）。



## A.4 PyTorch 张量（Tensor）

张量是一个多维数组，可以是标量、向量、矩阵或更高维度的数据结构。

在 PyTorch 中，张量（Tensor）是数据的核心表示形式，类似于 NumPy 的多维数组，但具有更强大的功能，例如支持 GPU 加速和自动梯度计算。

张量支持多种数据类型（整型、浮点型、布尔型等）。

张量可以存储在 CPU 或 GPU 中，GPU 张量可显著加速计算。

下图展示了不同维度的张量（Tensor）在 PyTorch 中的表示方法：

![img](https://raw.githubusercontent.com/GMyhf/img/main/img/1__D5ZvufDS38WkhK9rK32hQ.jpg)

**说明：**

- **1D Tensor / Vector（一维张量/向量）:** 最基本的张量形式，可以看作是一个数组，图中的例子是一个包含 10 个元素的向量。
- **2D Tensor / Matrix（二维张量/矩阵）:** 二维数组，通常用于表示矩阵，图中的例子是一个 4x5 的矩阵，包含了 20 个元素。
- **3D Tensor / Cube（三维张量/立方体）:** 三维数组，可以看作是由多个矩阵堆叠而成的立方体，图中的例子展示了一个 3x4x5 的立方体，其中每个 5x5 的矩阵代表立方体的一个"层"。
- **4D Tensor / Vector of Cubes（四维张量/立方体向量）:** 四维数组，可以看作是由多个立方体组成的向量，图中的例子没有具体数值，但可以理解为一个包含多个 3D 张量的集合。
- **5D Tensor / Matrix of Cubes（五维张量/立方体矩阵）:** 五维数组，可以看作是由多个4D张量组成的矩阵，图中的例子同样没有具体数值，但可以理解为一个包含多个 4D 张量的集合。

------

**创建张量**

张量创建的方式有：

| **方法**                            | **说明**                                               | **示例代码**                                |
| :---------------------------------- | :----------------------------------------------------- | :------------------------------------------ |
| `torch.tensor(data)`                | 从 Python 列表或 NumPy 数组创建张量。                  | `x = torch.tensor([[1, 2], [3, 4]])`        |
| `torch.zeros(size)`                 | 创建一个全为零的张量。                                 | `x = torch.zeros((2, 3))`                   |
| `torch.ones(size)`                  | 创建一个全为 1 的张量。                                | `x = torch.ones((2, 3))`                    |
| `torch.empty(size)`                 | 创建一个未初始化的张量。                               | `x = torch.empty((2, 3))`                   |
| `torch.rand(size)`                  | 创建一个服从均匀分布的随机张量，值在 `[0, 1)`。        | `x = torch.rand((2, 3))`                    |
| `torch.randn(size)`                 | 创建一个服从正态分布的随机张量，均值为 0，标准差为 1。 | `x = torch.randn((2, 3))`                   |
| `torch.arange(start, end, step)`    | 创建一个一维序列张量，类似于 Python 的 `range`。       | `x = torch.arange(0, 10, 2)`                |
| `torch.linspace(start, end, steps)` | 创建一个在指定范围内等间隔的序列张量。                 | `x = torch.linspace(0, 1, 5)`               |
| `torch.eye(size)`                   | 创建一个单位矩阵（对角线为 1，其他为 0）。             | `x = torch.eye(3)`                          |
| `torch.from_numpy(ndarray)`         | 将 NumPy 数组转换为张量。                              | `x = torch.from_numpy(np.array([1, 2, 3]))` |

使用 **torch.tensor()** 函数，你可以将一个列表或数组转换为张量：

**实例**

```python
import torch

tensor = torch.tensor([1, 2, 3])
print(tensor)
```

输出如下：

```
tensor([1, 2, 3])
```

如果你有一个 NumPy 数组，可以使用 torch.from_numpy() 将其转换为张量：

实例

```python
import numpy as np

np_array = np.array([1, 2, 3])
tensor = torch.from_numpy(np_array)
print(tensor)
```

输出如下：

```
tensor([1, 2, 3])
```

创建 2D 张量（矩阵）：

**实例**

```python
import torch

tensor_2d = torch.tensor([
  [-9, 4, 2, 5, 7],
  [3, 0, 12, 8, 6],
  [1, 23, -6, 45, 2],
  [22, 3, -1, 72, 6]
])
print("2D Tensor (Matrix):\n", tensor_2d)
print("Shape:", tensor_2d.shape) # 形状
```

输出如下：

```
2D Tensor (Matrix):
 tensor([[-9,  4,  2,  5,  7],
        [ 3,  0, 12,  8,  6],
        [ 1, 23, -6, 45,  2],
        [22,  3, -1, 72,  6]])
Shape: torch.Size([4, 5])
```

其他维度的创建：

```python
# 创建 3D 张量（立方体）
tensor_3d = torch.stack([tensor_2d, tensor_2d + 10, tensor_2d - 5])  # 堆叠 3 个 2D 张量
print("3D Tensor (Cube):\n", tensor_3d)
print("Shape:", tensor_3d.shape)  # 形状

# 创建 4D 张量（向量的立方体）
tensor_4d = torch.stack([tensor_3d, tensor_3d + 100])  # 堆叠 2 个 3D 张量
print("4D Tensor (Vector of Cubes):\n", tensor_4d)
print("Shape:", tensor_4d.shape)  # 形状

# 创建 5D 张量（矩阵的立方体）
tensor_5d = torch.stack([tensor_4d, tensor_4d + 1000])  # 堆叠 2 个 4D 张量
print("5D Tensor (Matrix of Cubes):\n", tensor_5d)
print("Shape:", tensor_5d.shape)  # 形状
```

------

**张量的属性**

张量的属性如下表：

| **属性**           | **说明**                         | **示例**                 |
| :----------------- | :------------------------------- | :----------------------- |
| `.shape`           | 获取张量的形状                   | `tensor.shape`           |
| `.size()`          | 获取张量的形状                   | `tensor.size()`          |
| `.dtype`           | 获取张量的数据类型               | `tensor.dtype`           |
| `.device`          | 查看张量所在的设备 (CPU/GPU)     | `tensor.device`          |
| `.dim()`           | 获取张量的维度数                 | `tensor.dim()`           |
| `.requires_grad`   | 是否启用梯度计算                 | `tensor.requires_grad`   |
| `.numel()`         | 获取张量中的元素总数             | `tensor.numel()`         |
| `.is_cuda`         | 检查张量是否在 GPU 上            | `tensor.is_cuda`         |
| `.T`               | 获取张量的转置（适用于 2D 张量） | `tensor.T`               |
| `.item()`          | 获取单元素张量的值               | `tensor.item()`          |
| `.is_contiguous()` | 检查张量是否连续存储             | `tensor.is_contiguous()` |

**实例**

```python
import torch

# 创建一个 2D 张量
tensor = torch.tensor([[1, 2, 3], [4, 5, 6]], dtype=torch.float32)

# 张量的属性
print("Tensor:\n", tensor)
print("Shape:", tensor.shape) # 获取形状
print("Size:", tensor.size()) # 获取形状（另一种方法）
print("Data Type:", tensor.dtype) # 数据类型
print("Device:", tensor.device) # 设备
print("Dimensions:", tensor.dim()) # 维度数
print("Total Elements:", tensor.numel()) # 元素总数
print("Requires Grad:", tensor.requires_grad) # 是否启用梯度
print("Is CUDA:", tensor.is_cuda) # 是否在 GPU 上
print("Is Contiguous:", tensor.is_contiguous()) # 是否连续存储

\# 获取单元素值
single_value = torch.tensor(42)
print("Single Element Value:", single_value.item())

\# 转置张量
tensor_T = tensor.T
print("Transposed Tensor:\n", tensor_T)
```

输出结果：

```
Tensor:
 tensor([[1., 2., 3.],
         [4., 5., 6.]])
Shape: torch.Size([2, 3])
Size: torch.Size([2, 3])
Data Type: torch.float32
Device: cpu
Dimensions: 2
Total Elements: 6
Requires Grad: False
Is CUDA: False
Is Contiguous: True
Single Element Value: 42
Transposed Tensor:
 tensor([[1., 4.],
         [2., 5.],
         [3., 6.]])
```

------

**张量的操作**

张量操作方法说明如下。

**基础操作：**

| **操作**                | **说明**                       | **示例代码**                  |
| :---------------------- | :----------------------------- | :---------------------------- |
| `+`, `-`, `*`, `/`      | 元素级加法、减法、乘法、除法。 | `z = x + y`                   |
| `torch.matmul(x, y)`    | 矩阵乘法。                     | `z = torch.matmul(x, y)`      |
| `torch.dot(x, y)`       | 向量点积（仅适用于 1D 张量）。 | `z = torch.dot(x, y)`         |
| `torch.sum(x)`          | 求和。                         | `z = torch.sum(x)`            |
| `torch.mean(x)`         | 求均值。                       | `z = torch.mean(x)`           |
| `torch.max(x)`          | 求最大值。                     | `z = torch.max(x)`            |
| `torch.min(x)`          | 求最小值。                     | `z = torch.min(x)`            |
| `torch.argmax(x, dim)`  | 返回最大值的索引（指定维度）。 | `z = torch.argmax(x, dim=1)`  |
| `torch.softmax(x, dim)` | 计算 softmax（指定维度）。     | `z = torch.softmax(x, dim=1)` |

形状操作

| **操作**                 | **说明**                       | **示例代码**                   |
| :----------------------- | :----------------------------- | :----------------------------- |
| `x.view(shape)`          | 改变张量的形状（不改变数据）。 | `z = x.view(3, 4)`             |
| `x.reshape(shape)`       | 类似于 `view`，但更灵活。      | `z = x.reshape(3, 4)`          |
| `x.t()`                  | 转置矩阵。                     | `z = x.t()`                    |
| `x.unsqueeze(dim)`       | 在指定维度添加一个维度。       | `z = x.unsqueeze(0)`           |
| `x.squeeze(dim)`         | 去掉指定维度为 1 的维度。      | `z = x.squeeze(0)`             |
| `torch.cat((x, y), dim)` | 按指定维度连接多个张量。       | `z = torch.cat((x, y), dim=1)` |

**实例**

```python
import torch

# 创建一个 2D 张量
tensor = torch.tensor([[1, 2, 3], [4, 5, 6]], dtype=torch.float32)
print("原始张量:\n", tensor)

# 1. 索引和切片操作
print("\n【索引和切片】")
print("获取第一行:", tensor[0]) # 获取第一行
print("获取第一行第一列的元素:", tensor[0, 0]) # 获取特定元素
print("获取第二列的所有元素:", tensor[:, 1]) # 获取第二列所有元素

# 2. 形状变换操作
print("\n【形状变换】")
reshaped = tensor.view(3, 2) # 改变张量形状为 3x2
print("改变形状后的张量:\n", reshaped)
flattened = tensor.flatten() # 将张量展平成一维
print("展平后的张量:\n", flattened)

# 3. 数学运算操作
print("\n【数学运算】")
tensor_add = tensor + 10 # 张量加法
print("张量加 10:\n", tensor_add)
tensor_mul = tensor * 2 # 张量乘法
print("张量乘 2:\n", tensor_mul)
tensor_sum = tensor.sum() # 计算所有元素的和
print("张量元素的和:", tensor_sum.item())

# 4. 与其他张量的操作
print("\n【与其他张量操作】")
tensor2 = torch.tensor([[1, 1, 1], [1, 1, 1]], dtype=torch.float32)
print("另一个张量:\n", tensor2)
tensor_dot = torch.matmul(tensor, tensor2.T) # 张量矩阵乘法
print("矩阵乘法结果:\n", tensor_dot)

# 5. 条件判断和筛选
print("\n【条件判断和筛选】")
mask = tensor > 3 # 创建一个布尔掩码
print("大于 3 的元素的布尔掩码:\n", mask)
filtered_tensor = tensor[tensor > 3] # 筛选出符合条件的元素
print("大于 3 的元素:\n", filtered_tensor)
```

输出结果：

```
原始张量:
 tensor([[1., 2., 3.],
         [4., 5., 6.]])

【索引和切片】
获取第一行: tensor([1., 2., 3.])
获取第一行第一列的元素: tensor(1.)
获取第二列的所有元素: tensor([2., 5.])

【形状变换】
改变形状后的张量:
 tensor([[1., 2.],
         [3., 4.],
         [5., 6.]])
展平后的张量:
 tensor([1., 2., 3., 4., 5., 6.])

【数学运算】
张量加 10:
 tensor([[11., 12., 13.],
         [14., 15., 16.]])
张量乘 2:
 tensor([[ 2.,  4.,  6.],
         [ 8., 10., 12.]])
张量元素的和: 21.0

【与其他张量操作】
另一个张量:
 tensor([[1., 1., 1.],
         [1., 1., 1.]])
矩阵乘法结果:
 tensor([[ 6.,  6.],
         [15., 15.]])

【条件判断和筛选】
大于 3 的元素的布尔掩码:
 tensor([[False, False, False],
         [ True,  True,  True]])
大于 3 的元素:
 tensor([4., 5., 6.])
```

------

**张量的 GPU 加速**

将张量转移到 GPU：

```python
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
x = torch.tensor([1.0, 2.0, 3.0], device=device)
```

检查 GPU 是否可用：

```python
torch.cuda.is_available()  # 返回 True 或 False
```

------

**张量与 NumPy 的互操作**

张量与 NumPy 的互操作如下表所示：

| **操作**                    | **说明**                                   | **示例代码**                     |
| :-------------------------- | :----------------------------------------- | :------------------------------- |
| `torch.from_numpy(ndarray)` | 将 NumPy 数组转换为张量。                  | `x = torch.from_numpy(np_array)` |
| `x.numpy()`                 | 将张量转换为 NumPy 数组（仅限 CPU 张量）。 | `np_array = x.numpy()`           |

**实例**

```python
import torch
import numpy as np

# 1. NumPy 数组转换为 PyTorch 张量
print("1. NumPy 转为 PyTorch 张量")
numpy_array = np.array([[1, 2, 3], [4, 5, 6]])
print("NumPy 数组:\n", numpy_array)

# 使用 torch.from_numpy() 将 NumPy 数组转换为张量
tensor_from_numpy = torch.from_numpy(numpy_array)
print("转换后的 PyTorch 张量:\n", tensor_from_numpy)

# 修改 NumPy 数组，观察张量的变化（共享内存）
numpy_array[0, 0] = 100
print("修改后的 NumPy 数组:\n", numpy_array)
print("PyTorch 张量也会同步变化:\n", tensor_from_numpy)

# 2. PyTorch 张量转换为 NumPy 数组
print("\n2. PyTorch 张量转为 NumPy 数组")
tensor = torch.tensor([[7, 8, 9], [10, 11, 12]], dtype=torch.float32)
print("PyTorch 张量:\n", tensor)

# 使用 tensor.numpy() 将张量转换为 NumPy 数组
numpy_from_tensor = tensor.numpy()
print("转换后的 NumPy 数组:\n", numpy_from_tensor)

# 修改张量，观察 NumPy 数组的变化（共享内存）
tensor[0, 0] = 77
print("修改后的 PyTorch 张量:\n", tensor)
print("NumPy 数组也会同步变化:\n", numpy_from_tensor)

# 3. 注意：不共享内存的情况（需要复制数据）
print("\n3. 使用 clone() 保证独立数据")
tensor_independent = torch.tensor([[13, 14, 15], [16, 17, 18]], dtype=torch.float32)
numpy_independent = tensor_independent.clone().numpy() # 使用 clone 复制数据
print("原始张量:\n", tensor_independent)
tensor_independent[0, 0] = 0 # 修改张量数据
print("修改后的张量:\n", tensor_independent)
print("NumPy 数组（不会同步变化）:\n", numpy_independent)
```

输出结果：

```
1. NumPy 转为 PyTorch 张量
NumPy 数组:
 [[1 2 3]
 [4 5 6]]
转换后的 PyTorch 张量:
 tensor([[1, 2, 3],
         [4, 5, 6]])

修改后的 NumPy 数组:
 [[100   2   3]
 [  4   5   6]]
PyTorch 张量也会同步变化:
 tensor([[100,   2,   3],
         [  4,   5,   6]])

2. PyTorch 张量转为 NumPy 数组
PyTorch 张量:
 tensor([[ 7.,  8.,  9.],
         [10., 11., 12.]])
转换后的 NumPy 数组:
 [[ 7.  8.  9.]
 [10. 11. 12.]]

修改后的 PyTorch 张量:
 tensor([[77.,  8.,  9.],
         [10., 11., 12.]])
NumPy 数组也会同步变化:
 [[77.  8.  9.]
 [10. 11. 12.]]

3. 使用 clone() 保证独立数据
原始张量:
 tensor([[13., 14., 15.],
         [16., 17., 18.]])
修改后的张量:
 tensor([[ 0., 14., 15.],
         [16., 17., 18.]])
NumPy 数组（不会同步变化）:
 [[13. 14. 15.]
 [16. 17. 18.]]
```



## A.5 PyTorch 神经网络基础

神经网络是一种模仿人脑处理信息方式的计算模型，它由许多相互连接的节点（神经元）组成，这些节点按层次排列。

神经网络的强大之处在于其能够自动从大量数据中学习复杂的模式和特征，无需人工设计特征提取器。

随着深度学习的发展，神经网络已经成为解决许多复杂问题的关键技术。

**神经元（Neuron）**

神经元是神经网络的基本单元，它接收输入信号，通过加权求和后与偏置（bias）相加，然后通过激活函数处理以产生输出。

神经元的权重和偏置是网络学习过程中需要调整的参数。

**输入和输出:**

- **输入（Input）**：输入是网络的起始点，可以是特征数据，如图像的像素值或文本的词向量。
- **输出（Output）**：输出是网络的终点，表示模型的预测结果，如分类任务中的类别标签。

神经元接收多个输入（例如x1, x2, ..., xn），如果输入的加权和大于激活阈值（activation potential），则产生二进制输出。

![img](https://raw.githubusercontent.com/GMyhf/img/main/img/1_upfpVueoUuKPkyX3PR3KBg.png)

神经元的输出可以看作是输入的加权和加上偏置（bias），神经元的数学表示：

<img src="https://raw.githubusercontent.com/GMyhf/img/main/img/f0b929045ae6eef23514bd7024be62f0.png" alt="img" style="zoom:50%;" />

这里，**wj** 是权重，**xj** 是输入，而 **Bias** 是偏置项。

**层（Layer）**

输入层和输出层之间的层被称为隐藏层，层与层之间的连接密度和类型构成了网络的配置。

神经网络由多个层组成，包括：

- **输入层（Input Layer）**：接收原始输入数据。
- **隐藏层（Hidden Layer）**：对输入数据进行处理，可以有多个隐藏层。
- **输出层（Output Layer）**：产生最终的输出结果。

典型的神经网络架构:

<img src="https://raw.githubusercontent.com/GMyhf/img/main/img/1_3fA77_mLNiJTSgZFhYnU0Q3K5DV4.webp" alt="img" style="zoom: 50%;" />



**前馈神经网络（Feedforward Neural Network，FNN）**

前馈神经网络（Feedforward Neural Network，FNN）是神经网络家族中的基本单元。

前馈神经网络特点是数据从输入层开始，经过一个或多个隐藏层，最后到达输出层，全过程没有循环或反馈。

![img](https://raw.githubusercontent.com/GMyhf/img/main/img/neural-net.png)

**前馈神经网络的基本结构：**

- **输入层：** 数据进入网络的入口点。输入层的每个节点代表一个输入特征。
- **隐藏层：**一个或多个层，用于捕获数据的非线性特征。每个隐藏层由多个神经元组成，每个神经元通过激活函数增加非线性能力。
- **输出层：**输出网络的预测结果。节点数和问题类型相关，例如分类问题的输出节点数等于类别数。
- **连接权重与偏置：**每个神经元的输入通过权重进行加权求和，并加上偏置值，然后通过激活函数传递。



**循环神经网络（Recurrent Neural Network, RNN）**

循环神经网络（Recurrent Neural Network, RNN）络是一类专门处理序列数据的神经网络，能够捕获输入数据中时间或顺序信息的依赖关系。

RNN 的特别之处在于它具有"记忆能力"，可以在网络的隐藏状态中保存之前时间步的信息。

循环神经网络用于处理随时间变化的数据模式。

在 RNN 中，相同的层被用来接收输入参数，并在指定的神经网络中显示输出参数。

<img src="https://raw.githubusercontent.com/GMyhf/img/main/img/0_xs3Dya3qQBx6IU7C.png" alt="img" style="zoom:67%;" />

PyTorch 提供了强大的工具来构建和训练神经网络。

神经网络在 PyTorch 中是通过 **torch.nn** 模块来实现的。

**torch.nn** 模块提供了各种网络层（如全连接层、卷积层等）、损失函数和优化器，让神经网络的构建和训练变得更加方便。

![img](https://raw.githubusercontent.com/GMyhf/img/main/img/1_3DUs-90altOgaBcVJ9LTGg.png)

在 PyTorch 中，构建神经网络通常需要继承 nn.Module 类。

nn.Module 是所有神经网络模块的基类，你需要定义以下两个部分：

- **`__init__()`**：定义网络层。
- **`forward()`**：定义数据的前向传播过程。

简单的全连接神经网络（Fully Connected Network）：

**实例**

```python
import torch
import torch.nn as nn

# 定义一个简单的神经网络模型
class SimpleNN(nn.Module):
  def init(self):
    super(SimpleNN, self).init()
    # 定义一个输入层到隐藏层的全连接层
    self.fc1 = nn.Linear(2, 2) # 输入 2 个特征，输出 2 个特征
    # 定义一个隐藏层到输出层的全连接层
    self.fc2 = nn.Linear(2, 1) # 输入 2 个特征，输出 1 个预测值

  def forward(self, x):
    # 前向传播过程
    x = torch.relu(self.fc1(x)) # 使用 ReLU 激活函数
    x = self.fc2(x) # 输出层
    return x

# 创建模型实例
model = SimpleNN()

# 打印模型
print(model)
```

输出结果如下：

```
SimpleNN(
  (fc1): Linear(in_features=2, out_features=2, bias=True)
  (fc2): Linear(in_features=2, out_features=1, bias=True)
)
```

PyTorch 提供了许多<mark>常见的神经网络层</mark>，以下是几个常见的：

- **`nn.Linear(in_features, out_features)`**：全连接层，输入 `in_features` 个特征，输出 `out_features` 个特征。
- **`nn.Conv2d(in_channels, out_channels, kernel_size)`**：2D 卷积层，用于图像处理。
- **`nn.MaxPool2d(kernel_size)`**：2D 最大池化层，用于降维。
- **`nn.ReLU()`**：ReLU 激活函数，常用于隐藏层。
- **`nn.Softmax(dim)`**：Softmax 激活函数，通常用于输出层，适用于多类分类问题。



**激活函数（Activation Function）**

激活函数决定了神经元是否应该被激活。它们是非线性函数，使得神经网络能够学习和执行更复杂的任务。常见的激活函数包括：

- Sigmoid：用于二分类问题，输出值在 0 和 1 之间。
- Tanh：输出值在 -1 和 1 之间，常用于输出层之前。
- ReLU（Rectified Linear Unit）：目前最流行的激活函数之一，定义为 `f(x) = max(0, x)`，有助于解决梯度消失问题。
- Softmax：常用于多分类问题的输出层，将输出转换为概率分布。

**实例**

```python
import torch.nn.functional as F

# ReLU 激活
output = F.relu(input_tensor)

# Sigmoid 激活
output = torch.sigmoid(input_tensor)

# Tanh 激活
output = torch.tanh(input_tensor)
```



**损失函数（Loss Function）**

损失函数用于衡量模型的预测值与真实值之间的差异。

常见的损失函数包括：

- **均方误差（MSELoss）**：回归问题常用，计算输出与目标值的平方差。
- **交叉熵损失（CrossEntropyLoss）**：分类问题常用，计算输出和真实标签之间的交叉熵。
- **BCEWithLogitsLoss**：二分类问题，结合了 Sigmoid 激活和二元交叉熵损失。

**实例**

```python
# 均方误差损失
criterion = nn.MSELoss()

# 交叉熵损失
criterion = nn.CrossEntropyLoss()

# 二分类交叉熵损失
criterion = nn.BCEWithLogitsLoss()
```



**优化器（Optimizer）**

<mark>优化器负责在训练过程中更新网络的权重和偏置</mark>。

常见的优化器包括：

- SGD（随机梯度下降）
- Adam（自适应矩估计）
- RMSprop（均方根传播）

**实例**

```python
import torch.optim as optim

# 使用 SGD 优化器
optimizer = optim.SGD(model.parameters(), lr=0.01)

# 使用 Adam 优化器
optimizer = optim.Adam(model.parameters(), lr=0.001)
```



**训练过程（Training Process）**

训练神经网络涉及以下步骤：

1. **准备数据**：通过 `DataLoader` 加载数据。
2. **定义损失函数和优化器**。
3. **前向传播**：计算模型的输出。
4. **计算损失**：与目标进行比较，得到损失值。
5. **反向传播**：通过 `loss.backward()` 计算梯度。
6. **更新参数**：通过 `optimizer.step()` 更新模型的参数。
7. **重复上述步骤**，直到达到预定的训练轮数。

**实例**

```python
\# 假设已经定义好了模型、损失函数和优化器

\# 训练数据示例
X = torch.randn(10, 2) # 10 个样本，每个样本有 2 个特征
Y = torch.randn(10, 1) # 10 个目标标签

\# 训练过程
for epoch in range(100):  # 训练 100 轮
  model.train() # 设置模型为训练模式
  optimizer.zero_grad() # 清除梯度
  output = model(X) # 前向传播
  loss = criterion(output, Y) # 计算损失
  loss.backward() # 反向传播
  optimizer.step() # 更新权重
  
  if (epoch + 1) % 10 == 0:  # 每 10 轮输出一次损失
    print(f'Epoch [{epoch + 1}/100], Loss: {loss.item():.4f}')
```



**测试与评估**

训练完成后，需要对模型进行测试和评估。

常见的步骤包括：

- **计算测试集的损失**：测试模型在未见过的数据上的表现。
- **计算准确率（Accuracy）**：对于分类问题，计算正确预测的比例。

**实例**

```python
# 假设你有测试集 X_test 和 Y_test
model.eval() # 设置模型为评估模式
with torch.no_grad():  # 在评估过程中禁用梯度计算
  output = model(X_test)
  loss = criterion(output, Y_test)
  print(f'Test Loss: {loss.item():.4f}')
```



**神经网络类型**

1. **前馈神经网络（Feedforward Neural Networks）**：数据单向流动，从输入层到输出层，无反馈连接。
2. **卷积神经网络（Convolutional Neural Networks, CNNs）**：适用于图像处理，使用卷积层提取空间特征。
3. **循环神经网络（Recurrent Neural Networks, RNNs）**：适用于序列数据，如时间序列分析和自然语言处理，允许信息反馈循环。
4. **长短期记忆网络（Long Short-Term Memory, LSTM）**：一种特殊的RNN，能够学习长期依赖关系。



## A.6 PyTorch 第一个神经网络

本章节我们将介绍如何用 PyTorch 实现一个简单的前馈神经网络，完成一个二分类任务。

以下实例展示了如何使用 PyTorch 实现一个简单的神经网络进行二分类任务训练。

网络结构包括输入层、隐藏层和输出层，使用了 ReLU 激活函数和 Sigmoid 激活函数。

采用了均方误差损失函数和随机梯度下降优化器。

训练过程是通过前向传播、计算损失、反向传播和参数更新来逐步调整模型参数。

**实例**

```python
# 导入PyTorch库
import torch
import torch.nn as nn

# 定义输入层大小、隐藏层大小、输出层大小和批量大小
n_in, n_h, n_out, batch_size = 10, 5, 1, 10

# 创建虚拟输入数据和目标数据
x = torch.randn(batch_size, n_in) # 随机生成输入数据
y = torch.tensor([[1.0], [0.0], [0.0],
         [1.0], [1.0], [1.0], [0.0], [0.0], [1.0], [1.0]]) # 目标输出数据

# 创建顺序模型，包含线性层、ReLU激活函数和Sigmoid激活函数
model = nn.Sequential(
  nn.Linear(n_in, n_h), # 输入层到隐藏层的线性变换
  nn.ReLU(),       # 隐藏层的ReLU激活函数
  nn.Linear(n_h, n_out), # 隐藏层到输出层的线性变换
  nn.Sigmoid()      # 输出层的Sigmoid激活函数
)

# 定义均方误差损失函数和随机梯度下降优化器
criterion = torch.nn.MSELoss()
optimizer = torch.optim.SGD(model.parameters(), lr=0.01) # 学习率为0.01

# 执行梯度下降算法进行模型训练
for epoch in range(50):  # 迭代50次
  y_pred = model(x) # 前向传播，计算预测值
  loss = criterion(y_pred, y) # 计算损失
  print('epoch: ', epoch, 'loss: ', loss.item()) # 打印损失值

  optimizer.zero_grad() # 清零梯度
  loss.backward() # 反向传播，计算梯度
  optimizer.step() # 更新模型参数
```

输出结果类似如下：

```
epoch:  0 loss:  0.2302265167236328
epoch:  1 loss:  0.23012931644916534
epoch:  2 loss:  0.23003216087818146
epoch:  3 loss:  0.22993502020835876
epoch:  4 loss:  0.22983793914318085
...
```

定义网络参数：

```
n_in, n_h, n_out, batch_size = 10, 5, 1, 10
```

- `n_in`：输入层大小为 10，即每个数据点有 10 个特征。
- `n_h`：隐藏层大小为 5，即隐藏层包含 5 个神经元。
- `n_out`：输出层大小为 1，即输出一个标量，表示二分类结果（0 或 1）。
- `batch_size`：每个批次包含 10 个样本。

生成输入数据和目标数据：

```python
x = torch.randn(batch_size, n_in)  # 随机生成输入数据
y = torch.tensor([[1.0], [0.0], [0.0], 
                 [1.0], [1.0], [1.0], [0.0], [0.0], [1.0], [1.0]])  # 目标输出数据
```

- `x`：随机生成一个形状为 `(10, 10)` 的输入数据矩阵，表示 10 个样本，每个样本有 10 个特征。
- `y`：目标输出数据（标签），表示每个输入样本的类别标签（0 或 1），是一个 10×1 的张量。

定义神经网络模型：

```python
model = nn.Sequential(
   nn.Linear(n_in, n_h),  # 输入层到隐藏层的线性变换
   nn.ReLU(),            # 隐藏层的ReLU激活函数
   nn.Linear(n_h, n_out),  # 隐藏层到输出层的线性变换
   nn.Sigmoid()           # 输出层的Sigmoid激活函数
)
```

`nn.Sequential` 用于按顺序定义网络层。

- `nn.Linear(n_in, n_h)`：定义输入层到隐藏层的线性变换，输入特征是 10 个，隐藏层有 5 个神经元。
- `nn.ReLU()`：在隐藏层后添加 ReLU 激活函数，增加非线性。
- `nn.Linear(n_h, n_out)`：定义隐藏层到输出层的线性变换，输出为 1 个神经元。
- `nn.Sigmoid()`：输出层使用 Sigmoid 激活函数，将结果映射到 0 到 1 之间，用于二分类任务。

定义损失函数和优化器：

```python
criterion = torch.nn.MSELoss()  # 使用均方误差损失函数
optimizer = torch.optim.SGD(model.parameters(), lr=0.01)  # 使用随机梯度下降优化器，学习率为 0.01
```

训练循环：

```python
for epoch in range(50):  # 训练50轮
   y_pred = model(x)  # 前向传播，计算预测值
   loss = criterion(y_pred, y)  # 计算损失
   print('epoch: ', epoch, 'loss: ', loss.item())  # 打印损失值

   optimizer.zero_grad()  # 清零梯度
   loss.backward()  # 反向传播，计算梯度
   optimizer.step()  # 更新模型参数
```

- `for epoch in range(50)`：进行 50 次训练迭代。
- `y_pred = model(x)`：进行前向传播，使用当前模型参数计算输入数据 `x` 的预测值。
- `loss = criterion(y_pred, y)`：计算预测值和目标值 `y` 之间的损失。
- `optimizer.zero_grad()`：清除上一轮训练时的梯度值。
- `loss.backward()`：反向传播，计算损失函数相对于模型参数的梯度。
- `optimizer.step()`：根据计算出的梯度更新模型参数。

可视化代码：

**实例**

```python
import torch
import torch.nn as nn
import matplotlib.pyplot as plt

# 定义输入层大小、隐藏层大小、输出层大小和批量大小
n_in, n_h, n_out, batch_size = 10, 5, 1, 10

# 创建虚拟输入数据和目标数据
x = torch.randn(batch_size, n_in) # 随机生成输入数据
y = torch.tensor([[1.0], [0.0], [0.0],
         [1.0], [1.0], [1.0], [0.0], [0.0], [1.0], [1.0]]) # 目标输出数据

# 创建顺序模型，包含线性层、ReLU激活函数和Sigmoid激活函数
model = nn.Sequential(
  nn.Linear(n_in, n_h), # 输入层到隐藏层的线性变换
  nn.ReLU(),       # 隐藏层的ReLU激活函数
  nn.Linear(n_h, n_out), # 隐藏层到输出层的线性变换
  nn.Sigmoid()      # 输出层的Sigmoid激活函数
)

# 定义均方误差损失函数和随机梯度下降优化器
criterion = torch.nn.MSELoss()
optimizer = torch.optim.SGD(model.parameters(), lr=0.01) # 学习率为0.01

# 用于存储每轮的损失值
losses = []

# 执行梯度下降算法进行模型训练
for epoch in range(50):  # 迭代50次
  y_pred = model(x) # 前向传播，计算预测值
  loss = criterion(y_pred, y) # 计算损失
  losses.append(loss.item()) # 记录损失值
  print(f'Epoch [{epoch+1}/50], Loss: {loss.item():.4f}') # 打印损失值

  optimizer.zero_grad() # 清零梯度
  loss.backward() # 反向传播，计算梯度
  optimizer.step() # 更新模型参数

# 可视化损失变化曲线
plt.figure(figsize=(8, 5))
plt.plot(range(1, 51), losses, label='Loss')
plt.xlabel('Epoch')
plt.ylabel('Loss')
plt.title('Training Loss Over Epochs')
plt.legend()
plt.grid()
plt.show()

# 可视化预测结果与实际目标值对比
y_pred_final = model(x).detach().numpy() # 最终预测值
y_actual = y.numpy() # 实际值

plt.figure(figsize=(8, 5))
plt.plot(range(1, batch_size + 1), y_actual, 'o-', label='Actual', color='blue')
plt.plot(range(1, batch_size + 1), y_pred_final, 'x--', label='Predicted', color='red')
plt.xlabel('Sample Index')
plt.ylabel('Value')
plt.title('Actual vs Predicted Values')
plt.legend()
plt.grid()
plt.show()
```

显示如下所示：

![img](https://raw.githubusercontent.com/GMyhf/img/main/img/first_n_runoob_1.png)



![a6fa1566dbdce1daa784f116d603c117](https://raw.githubusercontent.com/GMyhf/img/main/img/a6fa1566dbdce1daa784f116d603c117.png)



**另外一个实例**

我们假设有一个二维数据集，目标是根据点的位置将它们分类到两个类别中（例如，红色和蓝色点）。

以下实例展示了如何使用神经网络完成简单的二分类任务，为更复杂的任务奠定了基础，通过 PyTorch 的模块化接口，神经网络的构建、训练和可视化都非常直观。

**1、数据准备**

首先，我们生成一些简单的二维数据：

**实例**

```python
import torch
import torch.nn as nn
import torch.optim as optim
import matplotlib.pyplot as plt

# 生成一些随机数据
n_samples = 100
data = torch.randn(n_samples, 2) # 生成 100 个二维数据点
labels = (data[:, 0]**2 + data[:, 1]**2 < 1).float().unsqueeze(1) # 点在圆内为1，圆外为0

# 可视化数据
plt.scatter(data[:, 0], data[:, 1], c=labels.squeeze(), cmap='coolwarm')
plt.title("Generated Data")
plt.xlabel("Feature 1")
plt.ylabel("Feature 2")
plt.show()
```

**数据说明：**

- `data` 是输入的二维点，每个点有两个特征。
- `labels` 是目标分类，点在圆形区域内为 1，否则为 0。

显示如下：

![cfe5820ca03600fe0c1c18945556a892](https://raw.githubusercontent.com/GMyhf/img/main/img/cfe5820ca03600fe0c1c18945556a892.png)



**2、定义神经网络**

用 PyTorch 创建一个简单的前馈神经网络。

前馈神经网络使用了一层隐藏层，通过简单的线性变换和激活函数捕获数据的非线性模式。

**实例**

```python
class SimpleNN(nn.Module):
  def __init__(self):
    super(SimpleNN, self).__init__()
    # 定义神经网络的层
    self.fc1 = nn.Linear(2, 4) # 输入层有 2 个特征，隐藏层有 4 个神经元
    self.fc2 = nn.Linear(4, 1) # 隐藏层输出到 1 个神经元（用于二分类）
    self.sigmoid = nn.Sigmoid() # 二分类激活函数

  def forward(self, x):
    x = torch.relu(self.fc1(x)) # 使用 ReLU 激活函数
    x = self.sigmoid(self.fc2(x)) # 输出层使用 Sigmoid 激活函数
    return x

# 实例化模型
model = SimpleNN()
```



**3、定义损失函数和优化器**

**实例**

```python
# 定义二分类的损失函数和优化器
criterion = nn.BCELoss() # 二元交叉熵损失
optimizer = optim.SGD(model.parameters(), lr=0.1) # 使用随机梯度下降优化器
```



**4、训练模型**

用数据训练模型，让它学会分类。

**实例**

```python
# 训练
epochs = 100
for epoch in range(epochs):
  # 前向传播
  outputs = model(data)
  loss = criterion(outputs, labels)

  # 反向传播
  optimizer.zero_grad()
  loss.backward()
  optimizer.step()

  # 每 10 轮打印一次损失
  if (epoch + 1) % 10 == 0:
    print(f'Epoch [{epoch + 1}/{epochs}], Loss: {loss.item():.4f}')
```



**5、测试模型并可视化结果**

我们测试模型，并在图像上绘制决策边界。

**实例**

```python
# 可视化决策边界
def plot_decision_boundary(model, data):
  x_min, x_max = data[:, 0].min() - 1, data[:, 0].max() + 1
  y_min, y_max = data[:, 1].min() - 1, data[:, 1].max() + 1
  xx, yy = torch.meshgrid(torch.arange(x_min, x_max, 0.1), torch.arange(y_min, y_max, 0.1), indexing='ij')
  grid = torch.cat([xx.reshape(-1, 1), yy.reshape(-1, 1)], dim=1)
  predictions = model(grid).detach().numpy().reshape(xx.shape)
  plt.contourf(xx, yy, predictions, levels=[0, 0.5, 1], cmap='coolwarm', alpha=0.7)
  plt.scatter(data[:, 0], data[:, 1], c=labels.squeeze(), cmap='coolwarm', edgecolors='k')
  plt.title("Decision Boundary")
  plt.show()

plot_decision_boundary(model, data)
```



**6、完整代码**

完整代码如下：

实例

```python
import torch
import torch.nn as nn
import torch.optim as optim
import matplotlib.pyplot as plt

# 生成一些随机数据
n_samples = 100
data = torch.randn(n_samples, 2)  # 生成 100 个二维数据点
labels = (data[:, 0]**2 + data[:, 1]**2 < 1).float().unsqueeze(1)  # 点在圆内为1，圆外为0

# 可视化数据
plt.scatter(data[:, 0], data[:, 1], c=labels.squeeze(), cmap='coolwarm')
plt.title("Generated Data")
plt.xlabel("Feature 1")
plt.ylabel("Feature 2")
plt.show()

# 定义前馈神经网络
class SimpleNN(nn.Module):
    def __init__(self):
        super(SimpleNN, self).__init__()
        # 定义神经网络的层
        self.fc1 = nn.Linear(2, 4)  # 输入层有 2 个特征，隐藏层有 4 个神经元
        self.fc2 = nn.Linear(4, 1)  # 隐藏层输出到 1 个神经元（用于二分类）
        self.sigmoid = nn.Sigmoid()  # 二分类激活函数

    def forward(self, x):
        x = torch.relu(self.fc1(x))  # 使用 ReLU 激活函数
        x = self.sigmoid(self.fc2(x))  # 输出层使用 Sigmoid 激活函数
        return x

# 实例化模型
model = SimpleNN()

# 定义损失函数和优化器
criterion = nn.BCELoss()  # 二元交叉熵损失
optimizer = optim.SGD(model.parameters(), lr=0.1)  # 使用随机梯度下降优化器

# 训练
epochs = 2000
for epoch in range(epochs):
    # 前向传播
    outputs = model(data)
    loss = criterion(outputs, labels)

    # 反向传播
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()

    # 每 10 轮打印一次损失
    if (epoch + 1) % 10 == 0:
        print(f'Epoch [{epoch + 1}/{epochs}], Loss: {loss.item():.4f}')

# 可视化决策边界
def plot_decision_boundary(model, data):
    x_min, x_max = data[:, 0].min() - 1, data[:, 0].max() + 1
    y_min, y_max = data[:, 1].min() - 1, data[:, 1].max() + 1
    xx, yy = torch.meshgrid(torch.arange(x_min, x_max, 0.1), torch.arange(y_min, y_max, 0.1), indexing='ij')
    grid = torch.cat([xx.reshape(-1, 1), yy.reshape(-1, 1)], dim=1)
    predictions = model(grid).detach().numpy().reshape(xx.shape)
    plt.contourf(xx, yy, predictions, levels=[0, 0.5, 1], cmap='coolwarm', alpha=0.7)
    plt.scatter(data[:, 0], data[:, 1], c=labels.squeeze(), cmap='coolwarm', edgecolors='k')
    plt.title("Decision Boundary")
    plt.show()

plot_decision_boundary(model, data)
```

训练时的损失输出：

```
Epoch [10/2000], Loss: 0.6547
Epoch [20/2000], Loss: 0.6451
Epoch [30/2000], Loss: 0.6363
...
Epoch [1980/2000], Loss: 0.0664
Epoch [1990/2000], Loss: 0.0662
Epoch [2000/2000], Loss: 0.0659
```

图中显示了原始数据点（红色和蓝色），以及模型学习到的分类边界。

![e9e452ad8bc0bc8b241d0c6c2d7d5d31](https://raw.githubusercontent.com/GMyhf/img/main/img/e9e452ad8bc0bc8b241d0c6c2d7d5d31.png)





# 参考文献

[1] Dartmouth workshop - Wikipedia

https://en.wikipedia.org/wiki/Dartmouth_workshop

[2]OpenAI Presents GPT-3, a 175 Billion Parameters Language Model | NVIDIA Technical Blog. July 07, 2020.

https://developer.nvidia.com/blog/openai-presents-gpt-3-a-175-billion-parameters-language-model/

[3] GPT-4 Technical Report. March 27, 2023.

https://cdn.openai.com/papers/gpt-4.pdf

[4] Transformer (deep learning architecture) - Wikipedia

https://en.wikipedia.org/wiki/Transformer_(deep_learning_architecture)

[5] GPT-4 | OpenAI. March 14, 2023.

https://openai.com/index/gpt-4-research/