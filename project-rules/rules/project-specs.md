---
trigger: always_on
---

# Todo App Specification & Engineering Design

> **Status**: Living Document
> **Version**: 0.2.0 (FSD-Lite Transition)
> **Last Updated**: 2026-01-13

## 1. Product Vision (愿景)

打造一款 **"Fluid & Focus"** 的任务管理应用。
不仅仅是一个 Todo List，而是一个展示 **React 19**、**Tailwind v4** 和 **Agentic Workflow** 最佳实践的工程标杆。核心在于极致的微交互（Micro-interactions）和无干扰的用户体验。

## 2. Technical Stack (技术栈)

| Category         | Technology        | Rationale                                                         |
| :--------------- | :---------------- | :---------------------------------------------------------------- |
| **Architecture** | **FSD-Lite**      | Feature-Sliced Design optimized for AI context & maintainability. |
| **Core**         | React 19 + Vite   | Latest concurrent features, fast HMR.                             |
| **Language**     | TypeScript        | Strict types (TyDD) for robust architecture.                      |
| **Styling**      | Tailwind CSS v4   | Zero-runtime, composable utility-first CSS.                       |
| **UI Library**   | Shadcn/ui (Radix) | Accessible, headless primitives, fully customizable.              |
| **State**        | Zustand           | Atomic, hook-based state management.                              |
| **Validation**   | Zod               | Runtime validation for Forms and Complex State.                   |

## 3. Architecture: Feature-Sliced Design (FSD-Lite)

本项目采用 **FSD-Lite** 架构，专为提升 AI 协作效率（明确的上下文边界）和代码可维护性而设计。
如果用户要求需要更新 roadmap 或是修改宪法，直接去 doc/agent_rule_copy.md 文件中修改

### 3.1 Layers (层级)

代码库严格分为 6 个层级，**依赖只能自上而下**（Single Directional Flow）：

1.  **app (App Layer)**
    - 入口点、全局样式、Providers 配置 (Router, Theme, Store)。
    - _Role_: 初始化应用。
2.  **pages (Page Layer)**
    - 路由组件。
    - _Rule_: **必须非常“薄”**。严禁包含具体业务逻辑。只负责组合 Widgets/Features/Entities 进行布局。
3.  **widgets (Widget Layer)**
    - 独立的、完整的功能区块 (e.g., `Header`, `Sidebar`, `TaskListBoard`)。
    - _Rule_: 组合 Features 和 Entities。
4.  **features (Feature Layer)**
    - **业务交互的核心** (e.g., `AuthByEmail`, `AddTask`, `ToggleTask`)。
    - 包含：UI 组件、状态逻辑 (Hooks)、Zod Schema。
    - _Scope_: 响应用户操作，带来业务价值。
5.  **entities (Entity Layer)**
    - **业务领域模型** (e.g., `User`, `Task`, `List`)。
    - 包含：TypeScript 类型定义、只读的展示组件 (e.g., `TaskCard`)。
    - _Rule_: **严禁包含复杂业务逻辑**。
6.  **shared (Shared Layer)**
    - 通用的基础设施 (e.g., `ui/` (Shadcn), `lib/` (Utils), `api/`)。
    - _Rule_: 与具体业务解耦。

### 3.2 Directory Structure (目录规范)

```text
src/
├── app/
│   ├── providers/
│   ├── router/
│   └── styles/
├── pages/
│   ├── home/
│   └── list-detail/
├── widgets/            # Complex standalone blocks
│   ├── sidebar/
│   └── task-list/      # Using FSD naming, avoiding generic names
├── features/           # User interactions
│   ├── add-task/       # Each feature is a slice
│   │   ├── ui/
│   │   ├── model/      # Hooks / State
│   │   └── index.ts    # Public API
│   ├── toggle-task/
│   └── create-list/
├── entities/           # Domain models
│   ├── task/
│   │   ├── ui/         # e.g., TaskCard (dumb component)
│   │   ├── model/      # Types, Selectors
│   │   └── index.ts
│   └── list/
├── shared/
│   ├── ui/             # Shadcn Components (Button, Input)
│   ├── lib/            # Utils (cn, dates)
│   └── assets/
```

### 3.3 Rules & Boundaries (规则与边界)

1.  **Public API (公共入口)**

    - 每个 Slice (e.g., `features/add-task`) **必须** 有一个 `index.ts`。
    - **Rule**: 外部只能通过 `index.ts` 访问 (e.g., `import { AddTask } from '@/features/add-task'`)。
    - **Ban**: 严禁深入内部引用 (e.g., 🚫 `import ... from '@/features/add-task/ui/Form'`)。

2.  **Slice Isolation (切片隔离)**

    - **Rule**: **同层级 Slice 严禁相互引用** (e.g., `features/A` 不能引用 `features/B`)。
    - **Solution**: 如需共享，必须下沉到 `shared` 层，或在上层 (`widgets`/`pages`) 进行组合。
    - **Why**: 防止业务逻辑耦合，保持 Slice 独立并可插拔。

3.  **Import Path Strategy (路径规范)**
    - **Rule**: **必须** 使用 `@/` 绝对路径别名 (e.g., `import ... from '@/entities/task'`)。
    - **Ban**: 严禁使用跨层级的相对路径 (e.g., 🚫 `../../shared/ui`)。仅允许同一目录下的相对引用 (e.g., `./types`).

## 4. Engineering Standards (工程规范)

### 4.1 AI & Vibe Coding Protocol

- **State First**: 增加、完善功能前必须先更新`./doc/roadmap-n-core-entities.md`
- **Code Auditor**: AI 生成的代码必须经过严格审查，禁止“意大利面条式”代码。如果有复杂逻辑，必须拆分到 `lib` 或 hook 中。

### 4.2 Type-Driven Development (TyDD)

- **Types First**: 在编写任何逻辑组件前，必须先在 `model/types.ts` 或 `index.ts` 中定义 TypeScript 接口。
- **No Any**: 严禁使用 `any`。如果类型困难，使用 `unknown` 并配合 Type Guard。

### 4.3 Component Design

- **Headless Priority**: 优先使用 Radix UI 等 Headless 组件，通过 Tailwind CSS 注入样式。
- **Co-location**: 组件所需的 Hooks、Utils 如果只被该组件使用，应当尽量靠近该组件（放在同一个 Slice 中），而不是丢到全局 `shared`。
