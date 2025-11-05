# 人工智能概览

*Updated 2025-11-05 16:04 GMT+8*  
*Compiled by Hongfei Yan (2025 Summer)*    
https://github.com/GMyhf/2025fall-cs201/





人工智能（AI）是研究和开发能够执行通常需要人类智能的任务的技术和方法的学科，包括语音识别、图像理解、自然语言处理、机器人等[1] [2]。早在1950年，艾伦·图灵提出了检验机器智能的“模仿游戏”（即**图灵测试**），检验机器是否能让人分不清其与人类对话的区别。1956年达特茅斯会议（**Dartmouth AI Workshop**）召开，被认为是人工智能领域的创始时刻，约翰·麦卡锡等人首次正式提出“人工智能”这一术语[1]。此后，AI发展经历了多次高潮与低谷，到21世纪依赖于强大的计算资源、海量数据和新算法的**深度学习**技术实现突破，推动AI进入广泛应用阶段。



# 1. AI三大流派

人工智能的发展思想分为三个主要流派：

- **符号主义（Symbolic     AI）**：核心观点是通过符号表示和逻辑推理来实现智能。典型方法包括专家系统、搜索算法、逻辑推理（如一阶逻辑）、规划系统等。代表人物有艾伦·纽厄尔、赫伯特·西蒙、约翰·麦卡锡等。符号主义强调可解释性强，适用于有明确规则的任务（如数学推理、棋类游戏）。其代表成果包括20世纪80年代的专家系统（如DEC公司的XCON系统，显著提高了配置效率）以及IBM的棋类程序**深蓝（Deep Blue）**，1997年击败国际象棋冠军卡斯帕罗夫。但符号主义的缺点是学习能力弱，难以处理模糊信息，需要大量手工编码规则。

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

**示例：使用预训练模型进行问答**。以Hugging Face Transformer为例，下述代码载入本地中文预训练模型进行问答推理：



> | 模型                                     | 适用语言 | 用途     |
>| ---------------------------------------- | -------- | -------- |
> | `distilbert-base-cased-distilled-squad`  | 英文     | 英文问答 |
> | `uer/roberta-base-chinese-extractive-qa` | 中文     | 中文问答 |
> 
> Q: 如何用**浏览器手动下载** `uer/roberta-base-chinese-extractive-qa` 模型，做到完全 **离线部署** 的步骤：
>
> 🔗 1. 打开模型页面
>
> 浏览器访问：https://huggingface.co/uer/roberta-base-chinese-extractive-qa
>
> ------
>
> 📁 2. 进入 “Files and versions” 页面，手动下载以下几个关键文件：
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
> ------
>
> 🗂️ 3. 下载后，把它们放入一个本地文件夹，例如：
>
> ```
>./models/roberta-chinese-qa/
> ├── config.json
> ├── pytorch_model.bin
> ├── tokenizer_config.json
> ├── vocab.txt
> ├── special_tokens_map.json
> ├── tokenizer.json
> ```



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

上述代码中，我们指定了本地下载的中文问答模型目录，通过pipeline接口直接进行抽取式问答推理。在真实应用中，可替换为更强大的模型（如GPT-4）并结合语言提示（Prompt）实现更复杂的自然语言任务。

> 安装 深度学习框架 PyTorch  
> pip install -U transformers  
> pip install torch



> 用一个本地的中文问答模型，在一段文本里提取问题的答案。
>
> ✅ 1. 引入 Hugging Face 的 `pipeline`
>
> ```python
>from transformers import pipeline
> ```
> 
> 这是 Hugging Face `transformers` 提供的简洁 API，用于快速构建 NLP 任务管道，例如文本分类、问答、翻译等。
>
> 
>
> ✅ 2. 构造问答任务的 pipeline（使用本地模型）
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
> 📝 `tokenizer` 会自动从模型目录中加载，无需单独指定。
>
> ------
>
> ✅ 3. 运行问答推理
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

深度学习是连接主义流派的重要组成，主要使用多层神经网络自动学习特征和模式。本节重点介绍神经网络的关键算法与实战示例。

## 4.1 反向传播算法

反向传播（Backpropagation）是训练神经网络的核心算法。其思想是通过前向传播计算输出，然后反向传播误差并更新网络权重，以最小化损失函数[4]。前向传播阶段，从输入层经过加权求和、激活函数（如ReLU、Softmax）逐层计算输出；反向传播阶段，利用链式法则计算损失对每个参数的梯度，然后采用梯度下降或自适应优化器（如Adam）更新权重。反向传播使得多层深度网络的训练成为可能，是深度学习兴起的基石[3]。

**算法流程概述**： 

1. **前向传播**：将输入数据逐层传递，计算每层神经元输出并最终得到预测结果。 
2. **误差计算**：使用损失函数（如交叉熵、均方误差）计算预测输出与真实标签之间的误差。 
3. **反向传播**：从输出层向输入层反向传播误差，通过链式法则计算每个参数的梯度。 
4. **参数更新**：根据梯度对权重和偏置进行更新（如$w \leftarrow w - \eta \frac{\partial L}{\partial w}$），常用优化算法有随机梯度下降、Adam等。 
5. **重复迭代**：对所有训练样本多次迭代（多个epoch），直到损失收敛或达到训练轮次上限。

反向传播的引入极大提高了网络训练效率，使得多层深度网络成为可行。需要注意的是，深层网络可能面临**梯度消失**或**梯度爆炸**等问题（尤其使用Sigmoid/Tanh激活函数时），现代实践常用ReLU及批归一化等方法缓解。



> 阅读：PyTorch 教程，https://www.runoob.com/pytorch/pytorch-tutorial.html
>
> 使用PyTorch实现5个从基础模型到较复杂模型的训练与应用。相关代码及说明文档已整理于 Markdown 文件中，详见项目仓库：https://github.com/GMyhf/2025spring-cs201/tree/main/LLM
>
> 1. `0_xor_bp_neural_net_manual`：手动实现反向传播的简单神经网络，用于异或问题。
> 2. `1_iris_neural_network`：构建并训练用于鸢尾花分类的数据驱动神经网络。
> 3. `2_mnist_resnet18`：使用 ResNet18 模型对 MNIST 手写数字进行分类。
> 4. `3_cifar10_resnet18`：将 ResNet18 应用于 CIFAR-10 图像分类任务。
> 5. `4_tiny_imagenet_resnet50`：基于 ResNet50 模型处理 Tiny ImageNet 图像分类任务。

## 4.2 实例：异或问题（XOR）

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



## 4.3 实例：Iris数据集分类

**任务描述**：使用全连接神经网络对经典的Iris（鸢尾花）数据集进行多分类。数据集包含150个样本，每个样本4个特征（花萼和花瓣长度/宽度），分为3个类别。

**关键步骤**：数据预处理（标准化、训练/测试集划分）、模型构建、训练与评估。示例代码（PyTorch）：

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

**输出示例：**

```
$ python iris_neural_network.py 
Epoch [ 10/100], Loss: 0.2363
Epoch [ 20/100], Loss: 0.0899
Epoch [ 30/100], Loss: 0.0614
Epoch [ 40/100], Loss: 0.0634
Epoch [ 50/100], Loss: 0.0498
Epoch [ 60/100], Loss: 0.0492
Epoch [ 70/100], Loss: 0.0492
Epoch [ 80/100], Loss: 0.0451
Epoch [ 90/100], Loss: 0.0479
Epoch [100/100], Loss: 0.0436

✅ Test Accuracy: 100.00%
🔍 Sample Prediction: True = 0, Predicted = 0
```

该网络经过训练后，通常能在测试集上达到90%以上的准确率。实验结果表明，使用多层全连接网络即可较好解决该多分类任务（Iris数据集规模小，网络不需过深）。



**可视化：监督学习 + 无监督学习（Iris 数据集）**

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.linear_model import LogisticRegression
from sklearn.cluster import KMeans
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import accuracy_score

# 1. 加载数据
iris = load_iris()
X = iris.data
y = iris.target

# 2. 标准化数据
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# 3. 划分训练集和测试集（用于监督学习）
train_x, test_x, train_y, test_y = train_test_split(X_scaled, y, test_size=0.3, random_state=42)

# 4. 监督学习：逻辑回归分类
clf = LogisticRegression(max_iter=200)
clf.fit(train_x, train_y)
pred = clf.predict(test_x)
print("Logistic Regression Accuracy:", accuracy_score(test_y, pred))

# 5. 无监督学习：KMeans 聚类（聚成3类）
kmeans = KMeans(n_clusters=3, random_state=42)
clusters = kmeans.fit_predict(X_scaled)

# 6. 可视化聚类（降维到二维）
from sklearn.decomposition import PCA
pca = PCA(n_components=2)
X_2d = pca.fit_transform(X_scaled)

plt.figure(figsize=(10, 5))

# 聚类结果
plt.subplot(1, 2, 1)
plt.scatter(X_2d[:, 0], X_2d[:, 1], c=clusters, cmap='viridis', s=50)
plt.title("KMeans Clustering (unsupervised)")

# 原始标签
plt.subplot(1, 2, 2)
plt.scatter(X_2d[:, 0], X_2d[:, 1], c=y, cmap='Set1', s=50)
plt.title("Ground Truth Labels (supervised)")

plt.show()

```

> 使用 `LogisticRegression` 训练一个有监督分类器，并输出测试集准确率；
>
> 使用 `KMeans` 进行无监督聚类；
>
> 使用 PCA 将 4 维数据降维为 2 维，以便可视化聚类结果和真实标签；
>

如图所示，通过使用PCA将特征降至二维，可视化聚类效果与真实分类的对比：



<img src="https://raw.githubusercontent.com/GMyhf/img/main/img/image-20250727143806445.png" alt="image-20250727143806445" style="zoom: 67%;" />

<center>图：Iris 数据聚类（左：网络聚类结果；右：真实类别）</center>



## 4.4 实例：MNIST手写数字识别

MNIST是手写数字分类的基准数据集，包含60000张28×28的训练手写数字图片（0–9共10类）。我们使用经典的CNN（如ResNet18）来进行分类训练。

关键点：加载MNIST数据集，定义卷积神经网络（例如预训练ResNet18或自定义小型CNN），训练多个epoch后评估。下面是示例代码：

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

> 如果无法使用GPU
> 
> **在运行时强制使用CPU调试**
> 
> ```
>  CUDA_VISIBLE_DEVICES="" python mnist_resnet18.py
> ```
> 
> 这样禁用CUDA，使用CPU。
>
> 



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
> [7,   100] loss: 0.039
> [7,   200] loss: 0.000
> [7,   300] loss: 0.022
> [7,   400] loss: 0.014
> [7] Avg Loss: 0.018
> [8,   100] loss: 0.001
> [8,   200] loss: 0.044
> [8,   300] loss: 0.021
> [8,   400] loss: 0.002
> [8] Avg Loss: 0.019
> No improvement. Patience: 1/10
> [9,   100] loss: 0.002
> [9,   200] loss: 0.020
> [9,   300] loss: 0.002
> [9,   400] loss: 0.007
> [9] Avg Loss: 0.017
> [10,   100] loss: 0.027
> [10,   200] loss: 0.034
> [10,   300] loss: 0.031
> [10,   400] loss: 0.004
> [10] Avg Loss: 0.016
> [11,   100] loss: 0.003
> [11,   200] loss: 0.004
> [11,   300] loss: 0.005
> [11,   400] loss: 0.003
> [11] Avg Loss: 0.015
> [12,   100] loss: 0.011
> [12,   200] loss: 0.000
> [12,   300] loss: 0.031
> [12,   400] loss: 0.003
> [12] Avg Loss: 0.015
> No improvement. Patience: 1/10
> [13,   100] loss: 0.002
> [13,   200] loss: 0.002
> [13,   300] loss: 0.002
> [13,   400] loss: 0.019
> [13] Avg Loss: 0.013
> [14,   100] loss: 0.019
> [14,   200] loss: 0.004
> [14,   300] loss: 0.025
> [14,   400] loss: 0.003
> [14] Avg Loss: 0.013
> No improvement. Patience: 1/10
> [15,   100] loss: 0.003
> [15,   200] loss: 0.001
> [15,   300] loss: 0.011
> [15,   400] loss: 0.056
> [15] Avg Loss: 0.013
> [16,   100] loss: 0.034
> [16,   200] loss: 0.008
> [16,   300] loss: 0.001
> [16,   400] loss: 0.003
> [16] Avg Loss: 0.011
> [17,   100] loss: 0.008
> [17,   200] loss: 0.001
> [17,   300] loss: 0.001
> [17,   400] loss: 0.001
> [17] Avg Loss: 0.011
> [18,   100] loss: 0.009
> [18,   200] loss: 0.015
> [18,   300] loss: 0.002
> [18,   400] loss: 0.036
> [18] Avg Loss: 0.013
> No improvement. Patience: 1/10
> [19,   100] loss: 0.019
> [19,   200] loss: 0.001
> [19,   300] loss: 0.023
> [19,   400] loss: 0.005
> [19] Avg Loss: 0.011
> [20,   100] loss: 0.002
> [20,   200] loss: 0.007
> [20,   300] loss: 0.007
> [20,   400] loss: 0.005
> [20] Avg Loss: 0.011
> No improvement. Patience: 1/10
> [21,   100] loss: 0.001
> [21,   200] loss: 0.008
> [21,   300] loss: 0.012
> [21,   400] loss: 0.005
> [21] Avg Loss: 0.011
> [22,   100] loss: 0.007
> [22,   200] loss: 0.001
> [22,   300] loss: 0.001
> [22,   400] loss: 0.002
> [22] Avg Loss: 0.011
> No improvement. Patience: 1/10
> [23,   100] loss: 0.003
> [23,   200] loss: 0.002
> [23,   300] loss: 0.001
> [23,   400] loss: 0.014
> [23] Avg Loss: 0.011
> No improvement. Patience: 2/10
> [24,   100] loss: 0.003
> [24,   200] loss: 0.001
> [24,   300] loss: 0.003
> [24,   400] loss: 0.002
> [24] Avg Loss: 0.010
> [25,   100] loss: 0.016
> [25,   200] loss: 0.002
> [25,   300] loss: 0.010
> [25,   400] loss: 0.000
> [25] Avg Loss: 0.009
> [26,   100] loss: 0.001
> [26,   200] loss: 0.002
> [26,   300] loss: 0.006
> [26,   400] loss: 0.021
> [26] Avg Loss: 0.008
> [27,   100] loss: 0.002
> [27,   200] loss: 0.002
> [27,   300] loss: 0.017
> [27,   400] loss: 0.000
> [27] Avg Loss: 0.010
> No improvement. Patience: 1/10
> [28,   100] loss: 0.001
> [28,   200] loss: 0.012
> [28,   300] loss: 0.009
> [28,   400] loss: 0.000
> [28] Avg Loss: 0.008
> No improvement. Patience: 2/10
> [29,   100] loss: 0.001
> [29,   200] loss: 0.008
> [29,   300] loss: 0.009
> [29,   400] loss: 0.031
> [29] Avg Loss: 0.010
> No improvement. Patience: 3/10
> [30,   100] loss: 0.038
> [30,   200] loss: 0.001
> [30,   300] loss: 0.031
> [30,   400] loss: 0.001
> [30] Avg Loss: 0.011
> No improvement. Patience: 4/10
> [31,   100] loss: 0.017
> [31,   200] loss: 0.013
> [31,   300] loss: 0.029
> [31,   400] loss: 0.032
> [31] Avg Loss: 0.010
> No improvement. Patience: 5/10
> [32,   100] loss: 0.002
> [32,   200] loss: 0.000
> [32,   300] loss: 0.003
> [32,   400] loss: 0.001
> [32] Avg Loss: 0.009
> No improvement. Patience: 6/10
> [33,   100] loss: 0.009
> [33,   200] loss: 0.018
> [33,   300] loss: 0.001
> [33,   400] loss: 0.007
> [33] Avg Loss: 0.010
> No improvement. Patience: 7/10
> [34,   100] loss: 0.001
> [34,   200] loss: 0.001
> [34,   300] loss: 0.001
> [34,   400] loss: 0.011
> [34] Avg Loss: 0.010
> No improvement. Patience: 8/10
> [35,   100] loss: 0.004
> [35,   200] loss: 0.005
> [35,   300] loss: 0.009
> [35,   400] loss: 0.010
> [35] Avg Loss: 0.011
> No improvement. Patience: 9/10
> [36,   100] loss: 0.001
> [36,   200] loss: 0.004
> [36,   300] loss: 0.013
> [36,   400] loss: 0.007
> [36] Avg Loss: 0.008
> [37,   100] loss: 0.008
> [37,   200] loss: 0.003
> [37,   300] loss: 0.007
> [37,   400] loss: 0.002
> [37] Avg Loss: 0.010
> No improvement. Patience: 1/10
> [38,   100] loss: 0.002
> [38,   200] loss: 0.002
> [38,   300] loss: 0.011
> [38,   400] loss: 0.004
> [38] Avg Loss: 0.009
> No improvement. Patience: 2/10
> [39,   100] loss: 0.006
> [39,   200] loss: 0.003
> [39,   300] loss: 0.002
> [39,   400] loss: 0.001
> [39] Avg Loss: 0.008
> No improvement. Patience: 3/10
> [40,   100] loss: 0.000
> [40,   200] loss: 0.012
> [40,   300] loss: 0.011
> [40,   400] loss: 0.001
> [40] Avg Loss: 0.009
> No improvement. Patience: 4/10
> [41,   100] loss: 0.010
> [41,   200] loss: 0.008
> [41,   300] loss: 0.006
> [41,   400] loss: 0.002
> [41] Avg Loss: 0.008
> No improvement. Patience: 5/10
> [42,   100] loss: 0.005
> [42,   200] loss: 0.003
> [42,   300] loss: 0.014
> [42,   400] loss: 0.005
> [42] Avg Loss: 0.010
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
> [7,   200] loss: 0.018
> [7,   300] loss: 0.002
> [7,   400] loss: 0.079
> [7] Avg Loss: 0.022
> [8,   100] loss: 0.002
> [8,   200] loss: 0.005
> [8,   300] loss: 0.044
> [8,   400] loss: 0.004
> [8] Avg Loss: 0.018
> [9,   100] loss: 0.016
> [9,   200] loss: 0.009
> [9,   300] loss: 0.030
> [9,   400] loss: 0.014
> [9] Avg Loss: 0.015
> [10,   100] loss: 0.004
> [10,   200] loss: 0.023
> [10,   300] loss: 0.027
> [10,   400] loss: 0.023
> [10] Avg Loss: 0.017
> No improvement. Patience: 1/10
> [11,   100] loss: 0.025
> [11,   200] loss: 0.034
> [11,   300] loss: 0.012
> [11,   400] loss: 0.016
> [11] Avg Loss: 0.014
> [12,   100] loss: 0.004
> [12,   200] loss: 0.002
> [12,   300] loss: 0.014
> [12,   400] loss: 0.005
> [12] Avg Loss: 0.013
> [13,   100] loss: 0.002
> [13,   200] loss: 0.022
> [13,   300] loss: 0.019
> [13,   400] loss: 0.003
> [13] Avg Loss: 0.013
> [14,   100] loss: 0.010
> [14,   200] loss: 0.004
> [14,   300] loss: 0.028
> [14,   400] loss: 0.018
> [14] Avg Loss: 0.013
> No improvement. Patience: 1/10
> [15,   100] loss: 0.009
> [15,   200] loss: 0.002
> [15,   300] loss: 0.118
> [15,   400] loss: 0.011
> [15] Avg Loss: 0.012
> [16,   100] loss: 0.025
> [16,   200] loss: 0.001
> [16,   300] loss: 0.058
> [16,   400] loss: 0.005
> [16] Avg Loss: 0.011
> [17,   100] loss: 0.000
> [17,   200] loss: 0.008
> [17,   300] loss: 0.015
> [17,   400] loss: 0.034
> [17] Avg Loss: 0.013
> No improvement. Patience: 1/10
> [18,   100] loss: 0.002
> [18,   200] loss: 0.015
> [18,   300] loss: 0.001
> [18,   400] loss: 0.001
> [18] Avg Loss: 0.010
> [19,   100] loss: 0.011
> [19,   200] loss: 0.011
> [19,   300] loss: 0.001
> [19,   400] loss: 0.010
> [19] Avg Loss: 0.011
> No improvement. Patience: 1/10
> [20,   100] loss: 0.013
> [20,   200] loss: 0.000
> [20,   300] loss: 0.006
> [20,   400] loss: 0.001
> [20] Avg Loss: 0.010
> No improvement. Patience: 2/10
> [21,   100] loss: 0.008
> [21,   200] loss: 0.005
> [21,   300] loss: 0.036
> [21,   400] loss: 0.047
> [21] Avg Loss: 0.012
> No improvement. Patience: 3/10
> [22,   100] loss: 0.001
> [22,   200] loss: 0.006
> [22,   300] loss: 0.003
> [22,   400] loss: 0.001
> [22] Avg Loss: 0.011
> No improvement. Patience: 4/10
> [23,   100] loss: 0.001
> [23,   200] loss: 0.006
> [23,   300] loss: 0.001
> [23,   400] loss: 0.002
> [23] Avg Loss: 0.010
> No improvement. Patience: 5/10
> [24,   100] loss: 0.008
> [24,   200] loss: 0.010
> [24,   300] loss: 0.047
> [24,   400] loss: 0.056
> [24] Avg Loss: 0.009
> [25,   100] loss: 0.009
> [25,   200] loss: 0.012
> [25,   300] loss: 0.002
> [25,   400] loss: 0.027
> [25] Avg Loss: 0.010
> No improvement. Patience: 1/10
> [26,   100] loss: 0.017
> [26,   200] loss: 0.000
> [26,   300] loss: 0.011
> [26,   400] loss: 0.003
> [26] Avg Loss: 0.012
> No improvement. Patience: 2/10
> [27,   100] loss: 0.024
> [27,   200] loss: 0.004
> [27,   300] loss: 0.009
> [27,   400] loss: 0.019
> [27] Avg Loss: 0.009
> No improvement. Patience: 3/10
> [28,   100] loss: 0.004
> [28,   200] loss: 0.005
> [28,   300] loss: 0.029
> [28,   400] loss: 0.029
> [28] Avg Loss: 0.011
> No improvement. Patience: 4/10
> [29,   100] loss: 0.031
> [29,   200] loss: 0.008
> [29,   300] loss: 0.022
> [29,   400] loss: 0.003
> [29] Avg Loss: 0.009
> [30,   100] loss: 0.055
> [30,   200] loss: 0.009
> [30,   300] loss: 0.002
> [30,   400] loss: 0.010
> [30] Avg Loss: 0.010
> No improvement. Patience: 1/10
> [31,   100] loss: 0.001
> [31,   200] loss: 0.006
> [31,   300] loss: 0.019
> [31,   400] loss: 0.005
> [31] Avg Loss: 0.010
> No improvement. Patience: 2/10
> [32,   100] loss: 0.001
> [32,   200] loss: 0.007
> [32,   300] loss: 0.001
> [32,   400] loss: 0.001
> [32] Avg Loss: 0.009
> No improvement. Patience: 3/10
> [33,   100] loss: 0.000
> [33,   200] loss: 0.004
> [33,   300] loss: 0.001
> [33,   400] loss: 0.001
> [33] Avg Loss: 0.009
> [34,   100] loss: 0.002
> [34,   200] loss: 0.003
> [34,   300] loss: 0.020
> [34,   400] loss: 0.002
> [34] Avg Loss: 0.010
> No improvement. Patience: 1/10
> [35,   100] loss: 0.002
> [35,   200] loss: 0.000
> [35,   300] loss: 0.019
> [35,   400] loss: 0.015
> [35] Avg Loss: 0.009
> No improvement. Patience: 2/10
> [36,   100] loss: 0.002
> [36,   200] loss: 0.080
> [36,   300] loss: 0.001
> [36,   400] loss: 0.010
> [36] Avg Loss: 0.012
> No improvement. Patience: 3/10
> [37,   100] loss: 0.016
> [37,   200] loss: 0.028
> [37,   300] loss: 0.004
> [37,   400] loss: 0.007
> [37] Avg Loss: 0.008
> [38,   100] loss: 0.001
> [38,   200] loss: 0.001
> [38,   300] loss: 0.002
> [38,   400] loss: 0.004
> [38] Avg Loss: 0.008
> [39,   100] loss: 0.001
> [39,   200] loss: 0.008
> [39,   300] loss: 0.002
> [39,   400] loss: 0.003
> [39] Avg Loss: 0.008
> No improvement. Patience: 1/10
> [40,   100] loss: 0.001
> [40,   200] loss: 0.008
> [40,   300] loss: 0.006
> [40,   400] loss: 0.003
> [40] Avg Loss: 0.010
> No improvement. Patience: 2/10
> [41,   100] loss: 0.006
> [41,   200] loss: 0.001
> [41,   300] loss: 0.006
> [41,   400] loss: 0.006
> [41] Avg Loss: 0.009
> No improvement. Patience: 3/10
> [42,   100] loss: 0.004
> [42,   200] loss: 0.005
> [42,   300] loss: 0.010
> [42,   400] loss: 0.002
> [42] Avg Loss: 0.009
> No improvement. Patience: 4/10
> [43,   100] loss: 0.001
> [43,   200] loss: 0.002
> [43,   300] loss: 0.021
> [43,   400] loss: 0.001
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
>   plt.show()
> ```
>
> 



## 4.5 实例：CIFAR-10图像分类

CIFAR-10数据集包含60000张32×32彩色图像，共10个类别。由于图像更复杂，我们继续使用更强的模型（如ResNet18或ResNet34）进行训练。流程类似MNIST，但输入通道为3。训练后，现代架构通常能达到70%–90%的测试准确率（取决于网络深度和训练策略）。该实验帮助学生理解小型彩色图像集上的卷积网络训练要点（如数据增强、学习率调整）。

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

    # 2. 设置设备和模型
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

    # 3. 训练过程
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



> 详细训练日志：
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
>
> <img src="https://raw.githubusercontent.com/GMyhf/img/main/img/202507280020181.jpg" alt="d561be986280572516ac1023e9ff715c" style="zoom:50%;" />
>
> 



## 4.6 实例：Tiny ImageNet 图像分类

Tiny ImageNet是一个更大规模的图像分类任务，包含200个类别的64×64彩色图像，每类约500张训练图像。我们使用更深的网络（如ResNet50或更大模型）和更充分的训练迭代来解决。该任务需要更多算力（GPU支持）和技术（比如学习率调度、正则化）。完成后学生将掌握从代码实现到实战调优的完整流程，体会训练高复杂度模型的工程挑战。

### 1.准备Tiny ImageNet数据集

Tiny ImageNet。它包含 200 个类别，每个类别 500 张训练图片，总数据量大约 500MB，非常适合实验和调试。

下载 `wget http://cs231n.stanford.edu/tiny-imagenet-200.zip`，记237MB。

验证集通常解压后所有图片会在同一个文件夹中，而 ImageFolder 要求每个类别有独立子文件夹。你需要根据官方提供的 验证集标签文件，如 val_annotations.txt，对图片进行分类整理。常见的做法是编写一个脚本，根据文件中的类别信息将图片移动到对应的子文件夹中。

脚本`tinyimagenet.sh`

```sh
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



运行`sh tinyimagenet.sh`，数据解压并分类准备好，记472MB。

```
% ls -l
total 5200
drwxrwxr-x    3 hfyan  staff       96 Dec 12  2014 test
drwxrwxr-x  202 hfyan  staff     6464 Dec 12  2014 train
drwxrwxr-x  203 hfyan  staff     6496 Feb 24 11:09 val
-rw-rw-r--    1 hfyan  staff     2000 Feb  9  2015 wnids.txt
-rw-------    1 hfyan  staff  2655750 Feb  9  2015 words.txt
(base) hfyan@HongfeideMac-Studio tiny-imagenet-200 % pwd
/Users/hfyan/data/tiny-imagenet-200

```



### 2. 训练模型

基于 PyTorch 和 torchvision 库的示例代码，该代码演示了如何加载 ImageNet 数据集、构建基于预训练 ResNet 模型的神经网络，并进行微调训练实现图像分类。

代码`tiny_imagenet_resnet50_epoch25.py`

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

    # 设置 num_workers 为 4 以利用多进程数据加载
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



> **2025/2/24 11:30开始运行，16:00结束**
>
> ```
> (base) hfyan@HongfeideMac-Studio data % python tiny_imagenet_resnet50_epoch25.py 
> Using MPS device for GPU acceleration
> Epoch 1/25
> ----------
> train Loss: 5.0366 Acc: 0.0720
> val Loss: 4.1348 Acc: 0.2819
> 
> Epoch 2/25
> ----------
> train Loss: 3.2563 Acc: 0.3406
> val Loss: 1.7006 Acc: 0.6197
> 
> Epoch 3/25
> ----------
> train Loss: 2.1834 Acc: 0.5065
> val Loss: 1.2068 Acc: 0.7062
> 
> Epoch 4/25
> ----------
> train Loss: 1.8635 Acc: 0.5663
> val Loss: 1.0010 Acc: 0.7498
> 
> Epoch 5/25
> ----------
> train Loss: 1.6788 Acc: 0.6029
> val Loss: 0.8927 Acc: 0.7702
> 
> Epoch 6/25
> ----------
> train Loss: 1.5723 Acc: 0.6268
> val Loss: 0.8407 Acc: 0.7808
> 
> Epoch 7/25
> ----------
> train Loss: 1.5044 Acc: 0.6390
> val Loss: 0.7990 Acc: 0.7907
> 
> Epoch 8/25
> ----------
> train Loss: 1.4324 Acc: 0.6567
> val Loss: 0.7788 Acc: 0.7939
> 
> Epoch 9/25
> ----------
> train Loss: 1.4212 Acc: 0.6571
> val Loss: 0.7701 Acc: 0.7981
> 
> Epoch 10/25
> ----------
> train Loss: 1.4054 Acc: 0.6614
> val Loss: 0.7669 Acc: 0.7966
> 
> Epoch 11/25
> ----------
> train Loss: 1.4035 Acc: 0.6615
> val Loss: 0.7634 Acc: 0.7980
> 
> Epoch 12/25
> ----------
> train Loss: 1.3995 Acc: 0.6626
> val Loss: 0.7595 Acc: 0.7990
> 
> Epoch 13/25
> ----------
> train Loss: 1.3882 Acc: 0.6647
> val Loss: 0.7558 Acc: 0.7988
> 
> Epoch 14/25
> ----------
> train Loss: 1.3747 Acc: 0.6680
> val Loss: 0.7517 Acc: 0.7997
> 
> Epoch 15/25
> ----------
> train Loss: 1.3754 Acc: 0.6683
> val Loss: 0.7490 Acc: 0.8006
> 
> Epoch 16/25
> ----------
> train Loss: 1.3685 Acc: 0.6689
> val Loss: 0.7592 Acc: 0.7970
> 
> Epoch 17/25
> ----------
> train Loss: 1.3771 Acc: 0.6681
> val Loss: 0.7567 Acc: 0.8009
> 
> Epoch 18/25
> ----------
> train Loss: 1.3690 Acc: 0.6688
> val Loss: 0.7508 Acc: 0.8011
> 
> Epoch 19/25
> ----------
> train Loss: 1.3716 Acc: 0.6694
> val Loss: 0.7521 Acc: 0.8008
> 
> Epoch 20/25
> ----------
> train Loss: 1.3729 Acc: 0.6687
> val Loss: 0.7527 Acc: 0.8002
> 
> Epoch 21/25
> ----------
> train Loss: 1.3709 Acc: 0.6689
> val Loss: 0.7501 Acc: 0.8014
> 
> Epoch 22/25
> ----------
> train Loss: 1.3706 Acc: 0.6708
> val Loss: 0.7516 Acc: 0.8008
> 
> Epoch 23/25
> ----------
> train Loss: 1.3681 Acc: 0.6696
> val Loss: 0.7502 Acc: 0.8002
> 
> Epoch 24/25
> ----------
> train Loss: 1.3725 Acc: 0.6698
> val Loss: 0.7508 Acc: 0.8003
> 
> Epoch 25/25
> ----------
> train Loss: 1.3708 Acc: 0.6696
> val Loss: 0.7480 Acc: 0.8004
> 
> Best val Acc: 0.8014
> Model saved as tiny_imagenet_resnet50_epoch25.pth
> 
> ```
>
> 跑了4小时30分钟。
>
> <img src="https://raw.githubusercontent.com/GMyhf/img/main/img/image-20250224171542842.png" alt="image-20250224171542842" style="zoom:50%;" />
>
> 
>
> ```
> % ls -lh *.pth
> -rw-r--r--  1 hfyan  staff    92M Feb 24 16:02 tiny_imagenet_resnet50_epoch25.pth
> ```
>



### 3.加载训练好的的模型并进行验证

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

> **验证步骤**：  
>
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
>



# 5. 运行《从零构建大模型》代码

《从零构建大模型》代码，https://github.com/rasbt/LLMs-from-scratch

Build a Large Language Model (From Scratch)

可以在本地 mac 或者 window 运行，配置方法方法如： ...Setup_....md。

https://github.com/GMyhf/2025fall-cs201/tree/main/LLM



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