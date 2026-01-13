---
description: Create a new FSD Feature slice with standard directory structure (UI, Model, API).
---

# Scaffold New Feature Slice

This workflow creates a new feature slice in `src/features/<feature-name>` following FSD-Lite standards.
Replace `<feature-name>` with the actual name provided by the user (kebab-case).

1.  **Validate Name**: Ensure the feature name is in kebab-case (e.g., `add-task`, not `AddTask`).
2.  **Create Directory Structure**:
    - Run command to create directories: `src/features/<feature-name>/ui`, `src/features/<feature-name>/model`.
3.  **Create Schema/Types (TyDD)**:
    - Create `src/features/<feature-name>/model/types.ts`.
    - Content: Export an empty interface named after the feature (e.g., `export interface AddTaskProps {}`).
4.  **Create Main Component**:
    - Create `src/features/<feature-name>/ui/index.tsx`.
    - Content: A basic React functional component.
    - **Crucial**: Use strict absolute imports if importing internal types.
5.  **Create Public API**:
    - Create `src/features/<feature-name>/index.ts`.
    - Content: `export * from './ui';` (and optionally export types).
6.  **Verify**:
    - Check if `src/features/<feature-name>/index.ts` exists.
