# Monorepo Memory Bank Routing & Developer Rules

This project is a monorepo containing multiple independent services. To keep the context of each service clean and isolated, we apply a **Local Memory Bank** pattern for each subdirectory instead of a shared global Memory Bank at the root.

## 📁 Service Folder Structure

- **Go Backend:** `./go/` -> Manages Go backend logic.
- **Node.js Backend:** `./node/` -> Manages Node.js backend logic.
- **Agent Service:** `./agent/` -> Manages AI Agent logic (C# / Python).

---

## 🧠 Memory Bank Rules (MANDATORY)

1. **No Root Memory Bank:**

   - Avoid creating or updating `.context` or `memory-bank` files directly at the workspace root directory `/`.
2. **Context Routing:**

   - Each subdirectory (`./go/`, `./node/`, `./agent/`) has its own `memory-bank/` directory.
   - When you (the AI) perform a task, determine which service the task belongs to, and **only read/write** to the `memory-bank/` directory of that specific service.
   - For example, if editing files in `./go/`, you must read `./go/memory-bank/activeContext.md` to load the current context, and update `./go/memory-bank/progress.md` after completion.
3. **Synchronous Updates:**

   - Before coding: Always read `activeContext.md` of the directory you are working in.
   - After completing a task: Update `activeContext.md` and `progress.md` of that directory to preserve the latest state for subsequent AI agents.

---

## 🛠️ Instructions for AI IDEs (Cursor / Roo Code / Cline / Antigravity)

- **At startup:** Read this rule file to understand the project structure.
- **When switching tasks between services:** Actively switch contexts by reading the corresponding Memory Bank files of the new service.
