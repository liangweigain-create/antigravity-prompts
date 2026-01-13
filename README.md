# Antigravity Prompts: The Objective Technical Terminal

![Status](https://img.shields.io/badge/Status-Active-success)
![Focus](https://img.shields.io/badge/Focus-Architecture%20%26%20Design-blueviolet)
![AI-Native](https://img.shields.io/badge/AI-Native-000000)

## Introduction

**Antigravity Prompts** is a sophisticated prompt engineering system and configuration suite designed to transform AI coding assistants into high-level **Architectural Mentors**.

Instead of acting as a simple code generator, the **Objective Technical Terminal** persona focuses on maximizing the user's architectural understanding and coding proficiency through Socratic teaching and rigorous code audits.

## Core Philosophy

In the AI era, the value of memorizing syntax is diminishing. The focus of this system is to shift the developer's mindset from "How to fix syntax" to **"Controlling AI"**.

1.  **Architecture & Design Patterns**: Prioritizing SOLID principles, Feature-Sliced Design (FSD), and Data Flow. You decide the structure; AI fills in the code.
2.  **Problem Decomposition**: Translating vague requirements into precise technical logic flows.
3.  **Code Review**: Developing the capability to spot "Code Smells" and logic errors in AI-generated code.
4.  **Intent Over Syntax**: Discussing innovative types and utilities in terms of "Design Intent" and "Real-world Application".
5.  **Workflow**: `Design (Logic/Flow) -> AI Implements (Coding) -> Review (Audit)`.

## Project Structure

This repository is organized into global rules for the AI identity and project-specific configurations.

### `global-rules/`

Contains the core definition of the AI persona and its skills.

- **`GEMINI.md`**: The root configuration file defining the "Objective Technical Terminal" identity, fundamental rules, and skill orchestration.
- **`skills/`**: Modularized skills that the AI dynamically activates based on context.
  - **`tech-mentor/`**: Implements the Socratic teaching method to guide users through complex concepts.
  - **`communication-protocol/`**: Ensures standardized and effective interaction.
  - **`code-quality-standard/`**: Enforces strict code quality and rigorous auditing.

### `project-rules/`

Contains specific specifications and workflows for the target project.

- **`rules/project-specs.md`**: Detailed technical specifications, including the "Fluid & Focus" product vision, Tech Stack (React 19, Tailwind v4, FSD-Lite), and Architecture Layers.
- **`workflows/`**: Actionable guides for common tasks.
  - **`refactor-component-to-fsd.md`**: Step-by-step guide to refactoring components into the Feature-Sliced Design architecture.
  - **`scaffold-feature.md`**: Workflow for scaffolding new features.

## Key Features

### Feature-Sliced Design (FSD-Lite)

The system enforces a strict implementation of FSD-Lite to ensure clear boundaries and maintainability:

- **App Layer**: Initialization and providers.
- **Pages**: Thin routing components.
- **Widgets**: Standalone functional blocks.
- **Features**: Core business interactions.
- **Entities**: Domain models (types, dumb components).
- **Shared**: Evaluation-agnostic infrastructure.

### Type-Driven Development (TyDD)

- **Types First**: Interface definition in `model/types.ts` before logic implementation.
- **Strict Typing**: No `any`. Use of `unknown` with type guards where necessary.

### AI & Vibe Coding Protocol

- **State First**: Roadmap updates before feature implementation.
- **Code Auditor**: Mandatory review of AI-generated code to prevent "spaghetti code".

## Getting Started

1.  **Integration**: Point your AI assistant (e.g., Cursor, Windsurf) to the `global-rules/GEMINI.md` as its system prompt or "Rules for AI".
2.  **Activation**: The system automatically activates specific skills based on your queries (e.g., asking "Why?" triggers the Tech Mentor).
3.  **Verification**: Use commands like `/verify` to trigger a cognitive alignment check where the AI assesses your understanding of a concept.

## Contributing

This is a living system. Updates to the prompt architecture should be made in the respective markdown files within `global-rules` or `project-rules`. Maintain the separation of concerns between global identity and project specifics.

---

_Built for the creators of tomorrow._
