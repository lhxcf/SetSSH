# 远程环境配置向导任务

你好，Claude。请你扮演“环境配置助手”，协助我完成 SSH 远程开发协议的初始化。请严格按照以下步骤执行：

## 第一步：信息收集（逐个提问）
请你**逐个**向我询问以下 4 个核心映射参数。**注意：每次只能问一个问题**，等待我回答后，再问下一个。提问时可以附带示例以供参考。

需要收集的参数列表：
1. **SERVER_ALIAS**（服务器别名，例如：`server-gpu`，即配置在 `.ssh/config` 中的 Host）
2. **CONDA_ENV**（远程服务器的 Conda 环境名，例如：`base`）
3. **LOCAL_ROOT**（本地 Windows 项目的绝对路径，例如：`C:\Users\32858\Projects\MK-UNet_RAG`）
4. **REMOTE_ROOT**（远程 Linux 项目的绝对路径，例如：`/home/liuhaoxiong/data/MK-unet`）

## 第二步：组装协议文本
当我提供完这 4 个参数后，你需要找到用户目录下的conda环境初始化文件（如：“”），对应为参数CONDA_INIT_PATH。请将它们无缝替换到下方 `<template>` 标签内的对应占位符（即 `[请填入...]` 的部分）中。

<template>

# 远程开发环境执行协议 (SSH-Mode)

## 1. 核心映射参数 (配置区)
请以这里的映射关系为准，处理所有文件路径和环境交互。
- **SERVER_ALIAS**: [SERVER_ALIAS]
- **CONDA_ENV**: [CONDA_ENV]
- **LOCAL_ROOT**: [LOCAL_ROOT]
- **REMOTE_ROOT**: [REMOTE_ROOT]
- **本地操作系统**: Windows 11
- **远程操作系统**: Linux (Ubuntu/CentOS)

## 2. 路径映射与转换规则 (CRITICAL)
当用户要求执行本地代码、读写文件或指定路径时（例如 `./train.py`, `.\utils\loss.py`），你**必须**在执行前进行路径翻译：

1. **提取相对路径**：计算用户给出的文件相对于 `LOCAL_ROOT` 的相对路径。如果用户直接给出 `./train.py`，则相对路径为 `train.py`。
2. **拼接远程路径**：将提取到的相对路径拼接到 `REMOTE_ROOT` 之后。
3. **格式化路径**：强制将所有 Windows 风格的路径分隔符 `\` 转换为 Linux 风格的 `/`。
   - *示例映射*：本地 `.\train.py` -> 远程 `[REMOTE_ROOT]/train.py`

## 3. Shell 执行指令规范
当你需要执行任何 shell 命令时，**严禁直接在本地 Windows 终端中运行**。你必须按以下标准格式通过 SSH 发送命令：

### 标准执行模板：
```bash
ssh <SERVER_ALIAS> "source <CONDA_INIT_PATH> && conda activate <CONDA_ENV> && cd <REMOTE_ROOT> && <转换后的命令>"
```
### 实际转换示例（供你学习参考）：

**场景 A：用户说 "运行一下本地的 ./train.py"**

- 内部思考：`./train.py` 位于项目根目录。替换为 `<REMOTE_ROOT>/train.py`。因为我们要先 `cd <REMOTE_ROOT>`，所以直接执行 `python train.py` 即可。
- 最终命令： `ssh <SERVER_ALIAS> "source <CONDA_INIT_PATH> && conda activate <CONDA_ENV> && cd <REMOTE_ROOT> && python train.py"`

**场景 B：用户说 "执行 .\scripts\evaluate.py"**

- 内部思考：路径映射为 `<REMOTE_ROOT>/scripts/evaluate.py`。
- 最终命令： `ssh <SERVER_ALIAS> "source <CONDA_INIT_PATH> && conda activate <CONDA_ENV> && cd <REMOTE_ROOT> && python scripts/evaluate.py"`

</template>

## 第三步：自动追加到文件
完成模板组装后，请使用你的工具能力（终端或文件写入），将完整的 Markdown 文本**追加（Append）**到我当前项目根目录下的 `./CLAUDE.md` 文件末尾。
> **注意**：如果 `.CLAUDE.md` 文件不存在，请创建它。如果已存在，请在文件末尾追加两行空行后再写入。

追加完成后，请回复我：“配置已成功写入 ./CLAUDE.md。以后你可以直接要求我运行脚本，我会自动将其转换为服务器指令。”

**现在，请向我提出第一个问题，开始收集 SERVER_ALIAS。**