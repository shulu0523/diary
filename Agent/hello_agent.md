开发 Agent
理解什么是智能体，学会如何去开发智能体

# 智能体概述

## 什么是智能体
- agents manage how (and how well) information flows through a system.
- agents can evaluate what they know, decide what they still need, select the right tools, 
and adjust their strategy when things go wrong.

## 智能体的构成与运行原理

- 智能体的任务环境定义

- 智能体的运行机制

- 智能体的感知与行动

智能体的任务环境、核心运行机制以及 Thought-Action-Observation 交互范式

## 智能体应用的协作模式



## 遵循我们刚刚学到的理论循环，编写一个简单的 Python 智能体
为了能从 Python 程序中访问网络 API，我们需要一个 HTTP 库。requests是 Python 社区中最流行、最易用的选择。tavily-python是一个强大的 AI 搜索 API 客户端，用于获取实时的网络搜索结果，可以在官网注册后获取 API。openai是 OpenAI 官方提供的 Python SDK，用于调用 GPT 等大语言模型服务。请先通过以下命令安装它们：：

pip install requests tavily-python openai

# 智能体经典的构建范式
1、React 范式
2、Plan-and-Solve 范式
3、Reflect 范式

# 构建智能体框架
- 已有框架 AutoGen
- 已有框架 LangChain
- 自定义框架
  
# 记忆与检索
- 需要补充知识 如何实现记忆与检索
- 向量数据库和图数据库
- 知识模型

# 上下文工程
- 什么是上下文工程
Designing the systems that control what information reaches the model and how it maintains coherence.

Context Engineering is the discipline of designing the architecture that feeds an LLM the right information at the right time. It s not about changing the model itself, but about building the bridges that connect it to the outside world, 
retrieving external data, connecting it to live tools, and giving it a memory to ground its responses in facts, 
not just its training data.

它关注的是“在每一次模型调用前，如何以可复用、可度量、可演进的方式，拼装并优化输入上下文”，从而提升正确性、鲁棒性与效率[1][2]。


- 为什么需要上下文工程
大模型具有的问题：
 It can't answer questions about your private documents. 
 It has no knowledge of events that happened yesterday. 
 It confidently makes things up when it doesn't know an answer. 

 Agents are both the architects of their contexts and the users of those contexts.
However, they need good practices and systems to guide them, because managing context well is difficult, 
and getting it wrong quickly sabotages everything else the agent can do.

- 如何实现上下文工程
we’re looking at how we architect entire context systems.

Agents don’t just need memory and tools; 
they also need to monitor and manage the quality of their own context. 
That means avoiding overload, detecting irrelevant or conflicting information,pruning or compressing as needed, 
and keeping their in-context memory clean enough to reason effectively.

Q:LLMs have limited information capacity

Need:
1、What information should remain active in the context window
2、What should be stored externally and retrieved when needed
3、What can be summarized or compressed to save space
4、How much space to reserve for reasoning and planning

拆分大模型思考步骤：
一、need to understand user intent:
Query augmentation (查询增强 )
One of the most important steps of context engineering is how you prepare and present
the user s query. Without knowing exactly what the user is asking, the LLM cannot provide an accurate response.

1、Query rewriting transforms the original user query into a more effective version for information retrieval
2、Query expansion enhances retrieval by generating multiple related queries from a single user input. 
3、Query decomposition breaks down complex, multi-faceted questions into simpler,
focused sub-queries that can be processed independently. 

二、 feed them the right external information at the right time （检索）
The challenge is simple in concept but tricky in practice: a raw dataset of documents is
almost always too large to fit into an LLM's limited context window (the inputs given to an
AI model).
1、we must first break our documents down into smaller, manageable parts
Chunking Techniques：Fixded-Size、Recursive Chunking、Document-Based Chunking、Semantic Chunking、LLM-Based Chunking、
Agentic Chunking、Hierarchical Chunking、Late Chunking

三、Prompt engineering is the practice of designing, refining, and optimizing inputs (prompts)
given to Large Language Models (LLMs) to get your desired output. （提示词技术）

四、Memory

五、Tool


Context engineering is made up of the components described in this ebook:

Agents to act as the system's decision-making brain.

Query Augmentation to translate messy human requests into actionable intent.

Retrieval to connect the model to facts and knowledge bases.

Memory to give your system a sense of history and the power to learn.

Tools to give your application hands to interact with live data and APIs.


# Agent Skills
拥有数据库连接能力，不等于智能体知道如何编写高效且安全的SQL；
能够访问文件系统，不意味着它理解特定项目的代码结构和开发规范。
这就像给一个新手程序员开通了所有系统的访问权限，但没有提供操作手册和最佳实践。
What:
Agent Skills 是一种标准化的程序性知识封装格式
如果说 MCP 为智能体提供了"手"来操作工具，那么 Skills 就提供了"操作手册"或"SOP（标准作业程序）"，教导智能体如何正确使用这些工具

MCP 的职责：提供标准化的访问接口，让智能体能够"够得着"外部世界的数据和工具
Skills 的职责：提供领域专业知识，告诉智能体在特定场景下"如何组合使用这些工具"

MCP 定义的是 Agent 与外部工具和数据的连接（USB协议），使 Agent 和外部工具建立连接
而 Skills 像是软件应用程序，它定义了如何使用这些连接的设备来完成具体任务

Why:
关注点分离：MCP 专注于"能力"，Skills 专注于"智慧"
成本优化：渐进式加载大幅降低 token 消耗
可维护性：业务逻辑（Skills）与基础设施（MCP）解耦
复用性：同一个 MCP 服务器可以被多个 Skills 使用

How:
1. 精准的 Description
2. 模块化与单一职责
3. 确定性优先原则
4. 渐进式披露策略

## Agents require web search because LLMs:

• Are frozen in time due to knowledge cutoffs

• Hallucinate without grounding

• Cannot keep up with real-world changes

• Have limited context capacity

• Need to validate information for accuracy

• Rely on multi-step search for complex reasoning

• Benefit from access to specialized or niche sources

## You've learned the three main search types:

• Keyword search matches exact words but struggles with meaning

• Semantic search matches concepts and intent but may be broad

• Hybrid search combines both for high relevance and precision


# 构建大语言模型智能体











## 1、Python 版本管理
   推荐使用 pyenv 来管理 Python 版本。
   pyenv 可以在同一台机器上安装多个 Python 版本，并可以方便地切换不同的版本。

### 1.1 pyenv 安装方法（macOS）

#### 使用 Homebrew 安装（推荐）
```bash
# 更新 Homebrew
brew update

# 安装 pyenv
brew install pyenv
```

#### 手动安装
```bash
# 克隆 pyenv 仓库
git clone https://github.com/pyenv/pyenv.git ~/.pyenv

# 配置环境变量
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init --path)"' >> ~/.zshrc

# 重新加载 shell
source ~/.zshrc
```

### 1.2 pyenv 基本使用

#### 查看可用的 Python 版本
```bash
pyenv install --list
```

#### 安装指定版本的 Python
```bash
# 安装 Python 3.10.0
pyenv install 3.10.0

# 安装 Python 3.9.7
pyenv install 3.9.7
```

#### 查看已安装的 Python 版本
```bash
pyenv versions
```

#### 设置全局 Python 版本
```bash
# 设置全局默认使用 Python 3.10.0
pyenv global 3.10.0
```

#### 设置局部 Python 版本（当前目录）
```bash
# 在当前目录下使用 Python 3.9.7
pyenv local 3.9.7
```

#### 临时使用特定 Python 版本
```bash
# 临时使用 Python 3.8.10
pyenv shell 3.8.10
```

### 1.3 注意事项

1. **依赖安装**：在安装 Python 版本前，需要确保已安装必要的依赖
   ```bash
   brew install openssl readline sqlite3 xz zlib
   ```

2. **版本切换**：切换 Python 版本后，pip 也会自动切换到对应版本

3. **虚拟环境**：可以结合 pyenv-virtualenv 插件创建隔离的虚拟环境
   ```bash
   # 安装 pyenv-virtualenv
   brew install pyenv-virtualenv
   
   # 配置 pyenv-virtualenv
   echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc
   source ~/.zshrc
   
   # 创建虚拟环境
   pyenv virtualenv 3.10.0 my-project-env
   
   # 激活虚拟环境
   pyenv activate my-project-env
   
   # 退出虚拟环境
   pyenv deactivate
   ```

4. **更新 pyenv**：
   ```bash
   # Homebrew 安装方式更新
   brew upgrade pyenv
   
   # 手动安装方式更新
   cd ~/.pyenv && git pull
   ```
