# SCU Maker 项目维护者指南 (Maintainer Guide)

👋 欢迎成为 SCU Maker 项目的维护者 (Owner/Maintainer)！

作为 Owner，你的角色不仅仅是写代码，更多的是**服务**——服务贡献者，服务用户，以及保证项目的健康与可持续性。本手册旨在帮助你高效地管理项目。

## 目录

1. [项目初始化清单](#1-项目初始化清单)
2. [权限管理原则](#2-权限管理原则)
3. [日常维护流程](#3-日常维护流程)
    - [Issue 筛选 (Triage)](#issue-筛选-triage)
    - [Code Review 指南](#code-review-指南)
4. [版本发布规范](#4-版本发布规范)
5. [交接与传承](#5-交接与传承)

---

## 1. 项目初始化清单

当你创建一个新仓库或接手一个旧仓库时，请确保仓库包含以下“标配”文件。这能体现我们的专业度。

- [ ] **README.md**: 必须包含项目简介、安装步骤、快速开始 (Quick Start)。
- [ ] **LICENSE**: 开源协议。通常推荐 `MIT` (宽松) 或 `GPLv3` (传染性，保护开源)。严禁无协议裸奔。
- [ ] **.gitignore**: 防止提交垃圾文件 (`__pycache__`, `.DS_Store`, `node_modules` 等)。
- [ ] **CONTRIBUTING.md**: 引用组织的通用贡献指南或自行编写。
- [ ] **.github/** 目录**: 可选包含 Issue 和 PR 模板或自动化构建/测试。

> 💡 **提示**: 仓库描述 (Description) 和 标签 (Topics) 也要填写，方便别人检索。

## 2. 权限管理原则

为了项目安全，请遵循“最小权限原则”：

- **Maintainer (你)**: 拥有合并代码、发布版本、管理 Issue 的权限。
- **Collaborator (核心开发)**: 拥有 Write 权限，可以提交代码，但**禁止直接 Push 到 main 分支**。
- **Contributor (普通贡献者)**: 无需赋予仓库权限，通过 Fork + PR 的方式贡献。
- **Secrets 管理**: 如果项目涉及 API Key 或密码，**绝对不能**硬编码在代码里！请使用 GitHub Secrets 并在代码中通过环境变量读取。

## 3. 日常维护流程

### Issue 筛选 (Triage)

不要让 Issue 列表变成垃圾场。建议每周抽出 30 分钟进行整理：

1. **打标签 (Labeling)**:
   - `bug`: 确认为错误的。
   - `enhancement`: 新功能建议。
   - `question`: 使用咨询。
   - `good first issue`: **非常重要！** 留给新手的简单任务，用于吸引新新人加入。
   - `wontfix`: 不打算修复或不符合项目定位，并礼貌关闭。
   - `duplicate`: 重复的问题。

2. **回复**: 即使不能马上修复，也要在 48 小时内回复一句“收到，我们会尽快查看”，这能极大提升社区好感度。

### Code Review 指南

Code Review (代码审查) 是保证代码质量的最重要环节。在合并 PR 之前：

1. **CI 检查**: 确保自动化测试通过（如果有）。
2. **逻辑检查**: 代码是否真的解决了问题？有没有引入新 Bug？
3. **规范检查**: 变量命名是否规范？是否有注释？
4. **态度**:
   - ❌ 错误示范：“这代码写得太烂了，重写。”
   - ✅ 正确示范：“这里逻辑好像有点复杂，如果用 xxx 方法是不是会更清晰？另外记得加一下注释。”
   - **总是感谢贡献者的付出**，即使你拒绝了这个 PR。

## 4. 版本发布规范

请不要随意更改版本号。我们遵循 **[Semantic Versioning (语义化版本)](https://semver.org/)** 规范：`Major.Minor.Patch` (例如 v1.2.3)

- **Major (主版本)**: 做了不兼容的 API 修改 (v1.0.0 -> v2.0.0)。
- **Minor (次版本)**: 做了向下兼容的功能性新增 (v1.2.0 -> v1.3.0)。
- **Patch (修订号)**: 做了向下兼容的问题修正 (v1.2.1 -> v1.2.2)。

**发布流程：**

1. 在 GitHub 侧边栏点击 **Releases** -> **Draft a new release**。
2. Tag version 填写 `v1.x.x`。
3. 标题填写版本号。
4. 内容生成 Release Notes (GitHub 可自动生成，但建议手动润色，列出主要变更)。

## 5. 交接与传承

SCU Maker 是学生组织，为了避免毕业后项目“死亡”，请做好以下准备：

1. **文档化**: 所有的配置、部署流程、架构设计，**必须**写在文档里 (Wiki 或 `/docs` 目录)。“我记在脑子里”等于没有。
2. **培养副手**: 在你大三/大四时，有意识地从活跃贡献者中物色大二的继任者，给他们 Maintainer 权限尝试管理。
3. **凭证移交**: 如果你无心继续维护项目，移交可能存在的相关的账号密码、服务器 SSH Key、域名管理权到下任Maintainer。

---

## 📚 推荐阅读材料

作为 Maintainer，你的视野决定了项目的高度。以下资源能帮助你更好地理解开源维护工作：

### ⚖️ 协议与规范

- **[Choose a License](https://choosealicense.com/)**: 即使你不是法律专家，这个网站也能帮你搞懂 MIT、Apache 和 GPL 的区别，选对协议很重要。
- **[Semantic Versioning (语义化版本)](https://semver.org/lang/zh-CN/)**: 详细解释了为什么版本号是 `1.0.0` 而不是随便写的，这是软件工程的通用语言。

### 📖 文档与写作

- **[Make a README](https://www.makeareadme.com/)**: 一个好的 README 是项目的门面，这里教你通过简单的结构写出专业的介绍。
- **[Diátaxis Framework](https://diataxis.fr/)**: (进阶) 教你如何科学地组织文档结构（教程、指南、参考、解释），让文档不再是一团乱麻。

### ❤️ 社区建设与运营

- **[Open Source Guides](https://opensource.guide/zh-cn/)**: (必读) GitHub 官方出品的开源指南。重点推荐阅读：
  - [如何创建开源社区](https://opensource.guide/zh-cn/building-community/)
  - [维护者最佳实践](https://opensource.guide/zh-cn/best-practices/)
- **[The Art of Comments](https://stackoverflow.blog/2021/12/23/best-practices-for-writing-code-comments/)**: StackOverflow 关于如何写好注释和 Review 建议的文章，有助于提升 Review 质量。

### 🤖 自动化 (CI/CD)

- **[GitHub Actions 官方文档](https://docs.github.com/cn/actions)**: 学习如何配置自动化工作流，解放你的双手。

---
❤️ 感谢你为 SCU Maker 社区的付出！
