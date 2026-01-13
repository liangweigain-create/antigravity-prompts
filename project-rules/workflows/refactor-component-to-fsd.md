---
description: Safely migrate a legacy component to the FSD architecture (Feature, Entity, or Shared).
---

# Refactor Component to FSD

This workflow guides the migration of a component from `src/components` to the appropriate FSD layer (`features`, `entities`, or `shared/ui`).

1.  **Analyze & Categorize**:
    - Read the component code.
    - **Decision Gate**:
      - IF it has business logic (effects, API calls) -> Target: `features/<name>`.
      - IF it is a dumb UI component -> Target: `shared/ui/<name>` or `entities/<name>/ui`.
2.  **Create Destination**:
    - If Target is Feature/Entity: Create directory structure (`ui`, `model`, `index.ts`).
    - If Target is Shared: Create `src/shared/ui/<name>.tsx`.
3.  **Move & Adapt**:
    - Move code to the new location.
    - **Refactor Imports**: Update all internal imports in the new file to use `@/` absolute paths.
4.  **Update References (CRITICAL)**:
    - Run `grep_search` to find ALL files that imported the old component path.
    - Update each file to import from the NEW location (e.g., `import { X } from '@/features/X'`).
5.  **Cleanup**:
    - Delete the old file in `src/components`.
6.  **Verify**:
    - Run user's build or type-check command to ensure no broken links.
