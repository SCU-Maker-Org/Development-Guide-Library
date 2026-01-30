# Renode 仿真

Renode 是面向嵌入式与异构硬件的开源仿真平台，可在无实物硬件的情况下进行固件开发、系统级调试与自动化测试。

## 工业界运用
虽然在国内大众视野中 Renode 相对小众，但在全球嵌入式与半导体顶尖领域，它正逐渐成为标准工具栈的一部分，掌握它意味着接触最前沿的开发模式：

- **Google (TensorFlow Lite / Zephyr)**：Google 使用 Renode 进行 TensorFlow Lite for Microcontrollers (TFLM) 的持续集成测试，确保机器学习模型在不同嵌入式平台上的兼容性。同时，Zephyr RTOS 项目官方 CI 也大量使用 Renode 进行多架构（ARM, RISC-V, Xtensa等）的每日构建测试。
- **Microchip (PolarFire SoC)**：作为半导体巨头，Microchip 官方推荐使用 Renode 开发其 PolarFire SoC FPGA 平台。这允许开发者在拿到物理芯片前就开始 Linux 和裸机软件开发，重新定义了“左移（Shift-left）”开发流程。
- **RISC-V 生态系统的核心支柱**：由于 RISC-V 架构的开放性，定制指令集层出不穷。Renode 被 RISC-V International 官方大力推广，用于软硬件协同设计（Co-design），验证新的指令集扩展（ISA extensions）而无需等待流片。
- **航天与高可靠性领域**：由于太空环境难以复现，部分商业航天项目利用 Renode 仿真卫星上的抗辐射芯片，在地面进行全系统模拟测试与故障注入测试。

这些应用表明，Renode 不仅仅是一个“玩具”，而是构建现代、可测试、敏捷的嵌入式 DevOps 流程的关键一环。

> 现在教学上依然常用的Proteus则是玩具。

## 对个人的帮助
- **降低入门成本**：无需实体硬件即可学习与验证。
- **提升调试效率**：可重复的仿真环境便于问题定位。
- **支持自动化**：脚本化测试帮助构建个人级持续验证流程。

## 文档计划

1. 基本的Renode使用
2. Renode仿真SoC中的裸机开发
3. Renode仿真SoC中的RTOS开发
4. Renode仿真SoC中的神经网络模型部署

完成这四个基本的文档作为例子之后我将会提出 doc request issue 来请求更多文档。

