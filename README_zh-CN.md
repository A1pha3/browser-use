# Browser Use - AI 浏览器代理

<picture>
  <source media="(prefers-color-scheme: light)" srcset="https://github.com/user-attachments/assets/2ccdb752-22fb-41c7-8948-857fc1ad7e24">
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/user-attachments/assets/774a46d5-27a0-490c-b7d0-e65fcbbfa358">
  <img alt="Browser Use Logo" src="https://github.com/user-attachments/assets/2ccdb752-22fb-41c7-8948-857fc1ad7e24" width="full">
</picture>

<div align="center">
    <picture>
    <source media="(prefers-color-scheme: light)" srcset="https://github.com/user-attachments/assets/9955dda9-ede3-4971-8ee0-91cbc3850125">
    <source media="(prefers-color-scheme: dark)" srcset="https://github.com/user-attachments/assets/6797d09b-8ac3-4cb9-ba07-b289e080765a">
    <img alt="AI Browser Agent" src="https://github.com/user-attachments/assets/9955dda9-ede3-4971-8ee0-91cbc3850125" width="400">
    </picture>
</picture>

<div align="center">
<a href="https://cloud.browser-use.com"><img src="https://media.browser-use.tools/badges/package" height="48" alt="Browser-Use 下载统计"></a>
</div>

---

<div align="center">
<a href="#演示"><img src="https://media.browser-use.tools/badges/demos" alt="演示"></a>
<img width="16" height="1" alt="">
<a href="https://docs.browser-use.com"><img src="https://media.browser-use.tools/badges/docs" alt="文档"></a>
<img width="16" height="1" alt="">
<a href="https://browser-use.com/posts"><img src="https://media.browser-use.tools/badges/blog" alt="博客"></a>
<img width="16" height="1" alt="">
<a href="https://browsermerch.com"><img src="https://media.browser-use.tools/badges/merch" alt="周边"></a>
<img width="100" height="1" alt="">
<a href="https://github.com/browser-use/browser-use"><img src="https://media.browser-use.tools/badges/github" alt="GitHub Stars"></a>
<img width="4" height="1" alt="">
<a href="https://x.com/intent/user?screen_name=browser_use"><img src="https://media.browser-use.tools/badges/twitter" alt="Twitter"></a>
<img width="4" height="1" alt="">
<a href="https://link.browser-use.com/discord"><img src="https://media.browser-use.tools/badges/discord" alt="Discord"></a>
<img width="4" height="1" alt="">
<a href="https://cloud.browser-use.com"><img src="https://media.browser-use.tools/badges/cloud" height="48" alt="Browser Use Cloud"></a>
</div>

</br>

🌤️ 想要跳过繁琐的设置？使用我们的**[云服务](https://cloud.browser-use.com)**实现更快、更可扩展的浏览器自动化！

# 🤖 面向 LLM 的快速开始

1. 让你的 AI 编程助手（Cursor、Claude Code 等）参考 [Agents.md](https://docs.browser-use.com/llms-full.txt)
2. 开始提示即可！

<br/>

# 👋 快速上手指南

**1. 使用 [uv](https://docs.astral.sh/uv/) 创建 Python 环境（Python>=3.11）：**

```bash
uv init
```

**2. 安装 Browser-Use 包：**

```bash
# 我们每天更新 - 使用最新版本！
uv add browser-use
uv sync
```

**3. 从 [Browser Use Cloud](https://cloud.browser-use.com/new-api-key) 获取 API 密钥，并添加到 `.env` 文件（新用户获得 10 美元免费额度）：**

```
# .env
BROWSER_USE_API_KEY=your-key
```

**4. 安装 Chromium 浏览器：**

```bash
uvx browser-use install
```

**5. 运行你的第一个代理：**

```python
from browser_use import Agent, Browser, ChatBrowserUse
import asyncio

async def example():
    browser = Browser(
        # use_cloud=True,  # 取消注释以使用 Browser Use Cloud 的隐身浏览器
    )

    llm = ChatBrowserUse()

    agent = Agent(
        task="查看 browser-use 仓库的星标数量",
        llm=llm,
        browser=browser,
    )

    history = await agent.run()
    return history

if __name__ == "__main__":
    history = asyncio.run(example())
```

查看[完整文档](https://docs.browser-use.com)和[云服务文档](https://docs.cloud.browser-use.com)了解更多详情！

<br/>

# 🔥 生产环境部署

我们处理代理、浏览器、持久化、身份认证、Cookie 和 LLM。代理与浏览器并行运行，实现最低延迟。

```python
from browser_use import Browser, sandbox, ChatBrowserUse
from browser_use.agent.service import Agent
import asyncio

@sandbox()
async def my_task(browser: Browser):
    agent = Agent(task="查找 Hacker News 热门帖子", browser=browser, llm=ChatBrowserUse())
    await agent.run()

# 就像调用普通异步函数一样
asyncio.run(my_task())
```

查看[生产环境部署指南](https://docs.browser-use.com/production)了解更多详情。

<br/>

# 🚀 模板快速启动

**想要更快上手？** 生成一个可直接运行的模板：

```bash
uvx browser-use init --template default
```

这会创建一个 `browser_use_default.py` 文件，其中包含可运行的示例。可用模板：

- `default` - 最小配置，快速上手
- `advanced` - 所有配置选项及详细注释
- `tools` - 自定义工具和扩展代理的示例

你也可以指定自定义输出路径：

```bash
uvx browser-use init --template default --output my_agent.py
```

<br/>

# 💻 命令行工具

快速、持久的浏览器自动化命令行工具：

```bash
browser-use open https://example.com    # 导航到 URL
browser-use state                       # 查看可点击元素
browser-use click 5                     # 点击索引为 5 的元素
browser-use type "Hello"                # 输入文本
browser-use screenshot page.png         # 截图
browser-use close                       # 关闭浏览器
```

命令行工具在多次命令之间保持浏览器运行，实现快速迭代。查看[命令行文档](browser_use/skill_cli/README.md)了解所有命令。

### Claude Code 技能

对于 [Claude Code](https://claude.ai/code)，安装技能以启用 AI 辅助浏览器自动化：

```bash
mkdir -p ~/.claude/skills/browser-use
curl -o ~/.claude/skills/browser-use/SKILL.md \
  https://raw.githubusercontent.com/browser-use/browser-use/main/skills/browser-use/SKILL.md
```

<br/>

# 演示

### 📋 表单填写
#### 任务 = "用我的简历和信息填写这份工作申请表"
![工作申请表演示](https://github.com/user-attachments/assets/57865ee6-6004-49d5-b2c2-6dff39ec2ba9)
[示例代码 ↗](https://github.com/browser-use/browser-use/blob/main/examples/use-cases/apply_to_job.py)

### 🍎 购物
#### 任务 = "把这个清单上的商品加入我的购物车"

https://github.com/user-attachments/assets/a6813fa7-4a7c-40a6-b4aa-382bf88b1850

[示例代码 ↗](https://github.com/browser-use/browser-use/blob/main/examples/use-cases/buy_groceries.py)

### 💻 个人助手
#### 任务 = "帮我找到定制电脑的配件"

https://github.com/user-attachments/assets/ac34f75c-057a-43ef-ad06-5b2c9d42bf06

[示例代码 ↗](https://github.com/browser-use/browser-use/blob/main/examples/use-cases/pcpartpicker.py)

### 💡 [查看更多示例 ↗](https://docs.browser-use.com/examples) 别忘了给我们点个 Star！

<br/>

## 集成、托管、自定义工具、MCP 等更多内容请查看[文档 ↗](https://docs.browser-use.com)

<br/>

# 常见问题解答

<details>
<summary><b>最好使用什么模型？</b></summary>

我们专门针对浏览器自动化任务优化了 **ChatBrowserUse()**。平均而言，它完成任务的速度比其他模型快 3-5 倍，且准确率业界领先。

**价格（每百万 token）：**
- 输入 token：0.20 美元
- 缓存输入 token：0.02 美元
- 输出 token：2.00 美元

查看[支持的模型文档](https://docs.browser-use.com/supported-models)了解其他 LLM 提供商。
</details>

<details>
<summary><b>我可以使用自定义工具吗？</b></summary>

可以！你可以添加自定义工具来扩展代理的功能：

```python
from browser_use import Tools

tools = Tools()

@tools.action(description='描述这个工具的功能')
def custom_tool(param: str) -> str:
    return f"结果: {param}"

agent = Agent(
    task="你的任务",
    llm=llm,
    browser=browser,
    tools=tools,
)
```

</details>

<details>
<summary><b>可以免费使用吗？</b></summary>

可以！Browser-Use 是开源软件，可以免费使用。你只需要选择一个 LLM 提供商（如 OpenAI、Google、ChatBrowserUse，或使用 Ollama 运行本地模型）。
</details>

<details>
<summary><b>如何处理身份认证？</b></summary>

查看我们的身份认证示例：
- [使用真实浏览器配置文件](https://github.com/browser-use/browser-use/blob/main/examples/browser/real_browser.py) - 重用已保存登录信息的 Chrome 配置文件
- 如果需要临时账户邮箱，请选择 AgentMail
- 要将你的认证配置文件与远程浏览器同步，运行 `curl -fsSL https://browser-use.com/profile.sh | BROWSER_USE_API_KEY=XXXX sh`（将 XXXX 替换为你的 API 密钥）

这些示例展示了如何无缝维护会话和处理身份认证。
</details>

<details>
<summary><b>如何解决验证码？</b></summary>

要处理验证码，你需要更好的浏览器指纹和代理。请使用[ Browser Use Cloud](https://cloud.browser-use.com)，它提供专门设计的隐身浏览器，可避免检测和验证码挑战。
</details>

<details>
<summary><b>如何投入生产使用？</b></summary>

Chrome 可能占用大量内存，并行运行多个代理也可能难以管理。

对于生产环境用例，请使用我们的 [Browser Use Cloud API](https://cloud.browser-use.com)，它提供：
- 可扩展的浏览器基础设施
- 内存管理
- 代理轮换
- 隐身浏览器指纹
- 高性能并行执行
</details>

<br/>

<div align="center">

**告诉计算机该做什么，然后它就能完成。**

<img src="https://github.com/user-attachments/assets/06fa3078-8461-4560-b434-445510c1766f" width="400"/>

[![Twitter Follow](https://img.shields.io/twitter/follow/Magnus?style=social)](https://x.com/intent/user?screen_name=mamagnus00)
&emsp;&emsp;&emsp;
[![Twitter Follow](https://img.shields.io/twitter/follow/Gregor?style=social)](https://x.com/intent/user?screen_name=gregpr07)

</div>

<div align="center"> 用 ❤️ 在苏黎世和旧金山制作 </div>
