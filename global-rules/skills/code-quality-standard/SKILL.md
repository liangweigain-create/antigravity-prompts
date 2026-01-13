---
name: code-quality-standard
description: Snippets that defines What is considered good code quality.
---

## Role: The Gatekeeper. Only exports what is needed.

```typescript
// src/features/toggle-task/index.ts
export { TaskCheckbox } from "./ui/TaskCheckbox";
// Note: We do NOT export the internal hook 'useToggleTask' unless absolutely necessary.
```

## Role: The Contract. Explicitly defined props, no 'any'.

```typescript
// src/features/toggle-task/model/types.ts
export interface TaskCheckboxProps {
  taskId: string;
  isCompleted: boolean;
  className?: string; // Allow style extension for layout flexibility
}
```

## Role: The Brain. Encapsulates store interactions and side effects.

```typescript
// src/features/toggle-task/model/useToggleTask.ts
import { useAppStore } from "@/stores/TaskStore";
export const useToggleTask = () => {
  // Select only the specific action needed to minimize re-renders
  const toggleTask = useAppStore((state) => state.toggleTask);

  // Return a stable interface. The UI doesn't need to know it came from Zustand.
  return { toggle: toggleTask };
};
```

## Role: The Face. pure functional component, accessible, styled with Tailwind v4.

```typescript
// src/features/toggle-task/ui/TaskCheckbox.tsx
import { Check } from "lucide-react";
import { cn } from "@/shared/lib/utils";
import { useToggleTask } from "../model/useToggleTask";
import type { TaskCheckboxProps } from "../model/types"; // Import from local model
export const TaskCheckbox = ({
  taskId,
  isCompleted,
  className,
}: TaskCheckboxProps) => {
  // Logic is delegated to the hook
  const { toggle } = useToggleTask();
  const handleToggle = (e: React.MouseEvent) => {
    e.stopPropagation(); // Critical: Prevent bubbling to parent row click
    toggle(taskId);
  };
  return (
    <button
      onClick={handleToggle}
      className={cn(
        // Base styles: Flex center, fixed size, transition
        "flex items-center justify-center w-6 h-6 outline-none rounded-sm border-2 transition-all duration-200",
        // Conditional styles: Dynamic based on state
        isCompleted
          ? "bg-primary border-primary"
          : "border-muted-foreground/30 hover:border-primary/50",
        className
      )}
      aria-label={isCompleted ? "Mark as incomplete" : "Mark as completed"}
    >
      {isCompleted && (
        <Check
          className="w-3.5 h-3.5 text-primary-foreground"
          strokeWidth={3}
        />
      )}
    </button>
  );
};
```
