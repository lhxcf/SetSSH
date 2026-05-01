# 🇺🇸 English Version

# Claude SSH-Mode Command: Local to Remote Command Mapping Wizard

A powerful custom slash command (`/set_ssh`) for your Claude terminal. It acts as an interactive wizard that seamlessly maps your local Windows development environment to your remote Linux server. Once configured, it allows Claude to automatically translate local file paths and execute commands directly on your server via SSH.

Perfect for developers and AI researchers using local IDEs (like PyCharm) while running heavy computations (e.g., PyTorch training) on remote GPU servers.

## ✨ Features

- ⚡ **Slash Command Invocation**: Instantly trigger the setup wizard in any project by typing `/set_ssh`.
- 🧙‍♂️ **Interactive Setup Wizard**: Claude asks you for configurations step-by-step to avoid formatting errors.
- 🔄 **Automatic Path Translation**: Seamlessly converts Windows relative/absolute paths (`.\train.py`) to Linux server paths (`/home/user/project/train.py`).
- 🛡️ **Execution Guardrails**: Strictly prevents Claude from accidentally running remote Linux commands on your local Windows CMD/PowerShell.
- 📝 **Auto-Save Protocol**: Automatically generates and appends the final execution protocol to a `./CLAUDE.md` file in your project root for long-term memory.

## 🚀 How to Configure the Custom Command

To use this as a quick slash command (`/`), you need to add it to your Claude terminal or extension settings:

1. **Prepare the file**: Directly download the `set_ssh.md` file to your local machine, or save the prompt template from this project as a local file named `set_ssh.md`.

2. **Add the custom command**:

   - Open the `.claude` folder in your user directory

     - On Windows, open the "C:\Users\user_id\.claude" directory

     - On Linux, execute the following command:

       - ```shell
         cd ~/.claude
         ```

   - Create a new folder in the current directory and name it `commands`

     - On Linux, execute the following command:

       - ```shell
         mkdir commands
         ```

   - Copy `set_ssh.md` into the `commands` directory

## 💻 How to Use

### Prerequisites

1. You have a Windows local machine and a remote Linux server.
2. You have configured SSH Key-Based Authentication (passwordless login) and an SSH alias in your Windows `~/.ssh/config`.
3. You are using Claude (Desktop App is recommended as it supports local terminal execution tools).

### Step 1: Trigger the Wizard

In your Claude terminal, simply type:

```text
/set_ssh
```

### Step 2: Answer Claude's Questions

Claude will act as an "Environment Configuration Assistant" and ask you for 4 parameters one by one:

1. `SERVER_ALIAS` (e.g., `server-gpu`)
2. `CONDA_ENV` (e.g., `base`)
3. `LOCAL_ROOT` (e.g., `C:\Users\Name\Projects\MyCode`)
4. `REMOTE_ROOT` (e.g., `/home/user/data/MyCode`)

### Step 3: Enjoy Seamless Remote Execution!

Once Claude writes the rules to `./CLAUDE.md`, you can talk to it naturally:

> *"Run `.\train.py` for me."*

Claude will automatically translate and execute:

```bash
ssh server-gpu "source ~/.bashrc && conda activate base && cd /home/user/data/MyCode && python train.py"
```

---

---

# 🇨🇳 中文版本

# Claude SSH-Mode Command: 本地到远程服务器映射向导命令

这是一个专为 Claude 终端/客户端设计的自定义快捷命令（Slash Command）。通过输入 `/set_ssh`，它可以唤醒一个交互式向导，无缝建立本地 Windows 开发环境与远程 Linux 服务器的映射关系。配置完成后，Claude 能够自动翻译本地路径，并通过 SSH 直接在你的远程服务器上执行代码。

非常适合使用本地 IDE（如 PyCharm/VSCode）进行代码编写，但在远程 GPU 服务器上运行深度学习任务的开发者。

## ✨ 核心特性

- ⚡ **快捷命令触发**：在任意项目中，只需输入 `/set_ssh` 即可瞬间唤醒配置向导。
- 🧙‍♂️ **交互式配置**：Claude 会一步步询问你的配置参数，确保格式正确，拒绝填表式出错。
- 🔄 **智能路径翻译**：自动将 Windows 风格的相对/绝对路径（如 `.\train.py`）转化为 Linux 服务器绝对路径（如 `/home/user/project/train.py`）。
- 🛡️ **执行安全护栏**：严格禁止 Claude 在本地 Windows 终端中误执行 Linux 专属命令。
- 📝 **协议自动固化**：配置完成后，自动将执行协议追加到项目根目录的 `./CLAUDE.md` 中，形成项目的持久记忆。

## 🚀 如何配置该自定义命令

要让它变成可以通过 `/` 调用的命令，你需要将其添加到你的 Claude 终端或相关开发辅助工具中：

1. **准备文件**：直接下载 `set_ssh.md`文件到本地，或将本项目中的提示词模板保存为本地文件 `set_ssh.md`。

2. **添加自定义命令**：

   - 打开你的用户目录下的`.claude`文件夹

     - windows打开"C:\Users\user_id\.claude"目录

     - Linux执行如下命令：

       - ```shell
         cd ~/.claude
         ```

   - 在当前目录下新建一个文件夹，命名为 `commands`

     - Linux执行如下命令：

       - ```shell
         mkdir commands
         ```

   - 将 `set_ssh.md` 复制到commands目录下

## 💻 使用指南

### 前置要求

1. 本地使用 Windows 11/10，远程机器为 Linux 系统。
2. 已在 Windows 本地的 `~/.ssh/config` 中配置了 SSH 免密登录和服务器别名。
3. 正在使用 Claude（推荐使用 Claude Desktop 客户端，以支持自动操作本地终端执行工具）。

### 第一步：唤醒向导

在 Claude 对话框中直接输入：

```text
/set_ssh
```

### 第二步：跟随向导填写参数

Claude 会化身“环境配置助手”，逐个向你提问以下 4 个核心参数：

1. `SERVER_ALIAS`（服务器别名，例如：`server-gpu`）
2. `CONDA_ENV`（远程 Conda 环境名，例如：`base`）
3. `LOCAL_ROOT`（本地 Windows 项目根目录，例如：`C:\Users\Name\Projects\MK-UNet`）
4. `REMOTE_ROOT`（远程 Linux 项目根目录，例如：`/home/user/data/MK-UNet`）

### 第三步：享受无缝远程开发！

当 Claude 自动将映射配置写入当前项目的 `./CLAUDE.md` 后，你就可以像在本地一样自由下达指令了：

> *"帮我运行一下 `.\train.py` 测试一下损失函数。"*

Claude 会自动阅读规则，将其翻译并执行为：

```bash
ssh server-gpu "source ~/.bashrc && conda activate base && cd /home/user/data/MK-UNet && python train.py"
```

---

## 🤝 Contributing

Feel free to open issues or submit pull requests if you have ideas to improve this command!
欢迎提交 Issue 或 Pull Request 来完善这个快捷命令工具！

## 📄 License

MIT License
