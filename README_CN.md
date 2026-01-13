# Antigravity Prompts: 客观技术终端 (Objective Technical Terminal)

![状态](https://img.shields.io/badge/状态-活跃-success)
![核心](https://img.shields.io/badge/核心-架构与设计-blueviolet)
![AI原生](https://img.shields.io/badge/AI-原生-000000)

## 简介

**Antigravity Prompts** 是一套复杂且前沿的提示词工程系统与配置套件，旨在将 AI 编程助手转化为高级 **架构导师**。

**客观技术终端 (Objective Technical Terminal)** 不仅仅是一个简单的代码生成器，它的人格设定专注于通过苏格拉底式教学和严格的代码审查，最大化用户的架构理解能力和编码水平。

## 核心哲学

在 AI 时代，死记硬背语法的价值正在递减。本系统的核心在于将开发者的思维从“如何修复语法”转变为 **“驾驭 AI”**。

1.  **架构与设计模式**：优先考虑 SOLID 原则、Feature-Sliced Design (FSD) 和数据流。你决定结构，AI 负责填充代码。
2.  **问题拆解**：将模糊的需求转化为精确的技术原子和逻辑流的能力。
3.  **代码审查**：培养发现 AI 生成代码中“代码异味 (Code Smells)”和逻辑错误的能力。
4.  **意图优于语法**：从“设计意图”和“实际应用”的角度探讨创新的类型工具，而非陷入复杂的语法细节。
5.  **工作流**：`我设计 (逻辑/流程) -> AI 实现 (编码) -> 我审查 (审计)`。

## 项目结构

本仓库分为用于定义 AI 身份的全局规则和特定于项目的配置。

### `global-rules/` (全局规则)

包含 AI 人格及其技能的核心定义。

- **`GEMINI.md`**：根配置文件，定义了“客观技术终端”的身份、基本规则和技能编排。
- **`skills/`**：模块化的技能库，AI 会根据上下文动态激活这些技能。
  - **`tech-mentor/`**：实施苏格拉底式教学法，引导用户理解复杂概念。
  - **`communication-protocol/`**：确保标准化和高效的交互。
  - **`code-quality-standard/`**：强制执行严格的代码质量标准和审计。

### `project-rules/` (项目规则)

包含目标项目的具体规范和工作流。

- **`rules/project-specs.md`**：详细的技术规范，包括 "Fluid & Focus" 产品愿景、技术栈 (React 19, Tailwind v4, FSD-Lite) 和架构分层。
- **`workflows/`**：常见任务的操作指南。
  - **`refactor-component-to-fsd.md`**：将组件重构为 FSD 架构的分步指南。
  - **`scaffold-feature.md`**：新功能脚手架搭建的工作流。

## 关键特性

### Feature-Sliced Design (FSD-Lite)

本系统强制执行 FSD-Lite 架构，以确保清晰的边界和可维护性：

- **App 层**：初始化和 Providers。
- **Pages 层**：轻量的路由组件。
- **Widgets 层**：独立的完整功能区块。
- **Features 层**：核心业务交互。
- **Entities 层**：业务领域模型 (类型, 纯展示组件)。
- **Shared 层**：通用的基础设施。

### 类型驱动开发 (TyDD)

- **类型优先**：在编写逻辑之前，必须先在 `model/types.ts` 中定义接口。
- **严格类型**：严禁使用 `any`。在类型困难时使用 `unknown` 并配合类型守卫 (Type Guard)。

### AI & Vibe Coding 协议

- **状态优先**：在增加功能前必须先更新 Roadmap。
- **代码审计员**：AI 生成的代码必须经过严格审查，防止“意大利面条式”代码。

## 快速开始

1.  **集成**：将你的 AI 助手 (如 Antigravity) 指向 `.gemini/GEMINI.md` 作为其系统提示词 (System Prompt) 或 "Rules for AI"。
2.  **激活**：系统会根据你的提问自动激活特定技能 (例如，问“为什么？”会触发 Tech Mentor)。
3.  **验证**：使用 `/verify` 等命令触发认知对齐检查，AI 将评估你对特定概念的理解程度。

## 贡献

这是一个有生命力的系统。对提示词架构的更新应在 `global-rules` 或 `project-rules` 中的相应 markdown 文件中进行。请保持全局身份与项目细节之间的关注点分离。

---
