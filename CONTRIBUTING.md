# SCU Maker 贡献指南 (Contributing Guide)

🎉 首先，感谢你要为 SCU Maker 做出贡献！

SCU Maker 致力于通过开源精神推动校园创客文化。无论你是修复了一个 Typro、添加了新功能，还是完善了文档，我们都非常欢迎。

为了让协作更加高效，请在提交代码前花几分钟阅读以下指南。

## 📋 目录

1. [行为准则](#行为准则)
2. [如何参与](#如何参与)
    - [提交 Issue](#提交-issue)
    - [提交 Pull Request (PR)](#提交-pull-request-pr)
3. [开发规范](#开发规范)
    - [分支管理](#分支管理)
    - [Commit 信息规范](#commit-信息规范)
    - [代码风格](#代码风格)
4. [仓库整理与文件命名](#仓库整理与文件命名)

---

## 行为准则

请保持友善、包容和专业。我们在交流中互帮互助，尊重不同的观点。严禁任何形式的骚扰或歧视。

## 如何参与

### 提交 Issue

在提交 Issue 之前：

1. **先搜索**：请检查 Issue 列表，确保没有重复的 Issue。
2. **使用模板**：请使用我们要提供的 Issue 模板（Bug 报告或功能建议）。
3. **清晰描述**：
    - 如果是 Bug，请提供复现步骤、环境信息（OS, 语言版本等）和报错截图。
    - 如果是 Feature，请描述背景、动机以及预期的效果。

### 提交 Pull Request (PR)

所有的代码变更都必须通过 PR 合并。

1. **Fork 仓库**：将本仓库 Fork 到你的个人账号下。
2. **创建分支**：在你的仓库中创建新的分支（命名规范见下文）。
3. **提交修改**：进行代码开发，并确保代码能跑通，如果有测试用例，请确保通过测试。
4. **提交 PR**：
    - 将 PR 提交到 `main` (或 `dev`) 分支。具体情况请各仓库Owner注明。
    - 填写 PR 模板，关联相关的 Issue (例如：`Closes #123`)。
5. **Code Review**：等待维护者（Maintainers）的 Review。如果此时有人提出修改建议，请在原分支继续 commit，PR 会自动更新。

---

## 开发规范

### 分支管理

请勿直接在 `main` 分支上开发。分支命名请遵循 `类型/描述` 的格式，全部小写，使用连字符分隔。

- **功能开发**：`feat/add-login-module`
- **Bug 修复**：`fix/memory-leak-issue`
- **文档修改**：`docs/update-readme`
- **重构**：`refactor/optimize-database`

### Commit 信息规范

我们遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范。格式如下：

```text
<type>(<scope>): <subject>
```

**Type 列表：**

- `feat`: 新功能
- `fix`: 修复 Bug
- `docs`: 文档变更
- `style`: 代码格式调整（不影响逻辑，如空格、分号）
- `refactor`: 代码重构（既不修复错误也不添加功能）
- `perf`: 性能优化
- `test`: 添加或修改测试
- `chore`: 构建过程或辅助工具的变动

**示例：**

- `feat(user): 添加用户注册接口`
- `fix(ui): 修复首页按钮对齐问题`
- `docs: 更新安装说明文档`

### 代码风格

为了保持代码库整洁，原则上请遵守以下原则：

1. **语言规范**：
   - **Python**: 遵循 PEP 8 规范。建议使用 `black` 或 `flake8` 格式化。
   - **C/C++**: 推荐 Google C++ Style，或遵循项目根目录下的 `.clang-format`。
   - **JavaScript/TS**: 遵循 StandardJS 或 Airbnb 规范。
2. **注释**：关键逻辑必须添加注释。对外接口必须编写文档注释（Docstring）。
3. **命名**：变量名应具有描述性，避免使用 `a`, `b`, `tmp` 等无意义命名。

---

## 仓库整理与文件命名

### 文件命名规则

- **推荐**：`snake_case` (如 `data_processor.py`) 或 `kebab-case` (如 `style-guide.md`)。
- **避免**：`数据处理.py`, `My File.cpp`。

### 目录结构参考

一个较好的项目结构应如下所示：

```text
project-name/
├── src/                # 源代码
│   ├── main.cc
│   ├── main.py
│   └── utils/
├── docs/               # 文档 (设计文档, API说明)
│   ├── images/         # 文档图片
│   └── user_guide.md
├── tests/              # 测试代码
├── examples/           # 示例代码 (Demo)
├── .gitignore          # Git 忽略文件
├── LICENSE             # 开源协议 (MIT/GPL等)
├── README.md           # 项目主页介绍
└── pyproject.toml      # 依赖说明
```

---

## 📚 推荐阅读与资源

如果你对以上流程感到陌生，或者想进一步提升代码协作能力，我们强烈推荐阅读以下资料：

### 🛠 Git 与 GitHub 基础

- **[Learn Git Branching](https://learngitbranching.js.org/?locale=zh_CN)**: 一个像游戏一样的交互式 Git 学习网站，通关后你将不再害怕合并冲突。
- **[Pro Git (中文版)](https://git-scm.com/book/zh/v2)**: 权威的 Git 参考书，遇到不懂的命令可以在这里查阅。
- **[GitHub Flow](https://docs.github.com/cn/get-started/quickstart/github-flow)**: 理解为什么我们要用分支、PR 以及 Code Review。

### 📝 代码规范与风格

- **Python**: [PEP 8 风格指南](https://www.python.org/dev/peps/pep-0008/) | [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)
- **C++**: [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)
- **JavaScript**: [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- **Commit 信息**: [How to Write a Git Commit Message](https://cbea.ms/git-commit/) (经典必读)

### 📄 文档编写

- **[Markdown 指南](https://docs.github.com/cn/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)**: GitHub 官方的 Markdown 语法速查表。

---

感谢你的贡献，让我们一起创造精彩！🚀
