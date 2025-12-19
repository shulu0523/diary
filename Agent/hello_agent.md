开发 Agent
理解什么是智能体，学会如何去开发智能体

# 智能体概述

## 什么是智能体

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
