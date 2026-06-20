---
description: Memory Bank Core System & Workflow — Maintaining precise context across sessions
globs: memory-bank/**/*.md, *
alwaysApply: true
---

# 易 MEMORY BANK MASTER RULES

My memory resets completely between sessions. This is not a limitation—it is the reason I maintain rigorous, accurate documentation. After every reset, I MUST read all files in the `memory-bank/` directory before starting any task. This is non-negotiable.

## 1.  STANDARD FILE STRUCTURE (Core Files)
The system consists of the following files. Any new file created here MUST include a YAML Frontmatter (`last_updated`, `status`):
- `projectbrief.md`: Core goals & requirements of the project.
- `productContext.md`: The problem being solved, UX/UI directions.
- `systemPatterns.md`: Architecture, design patterns, and rules. (Auto-append a 1-sentence description when creating new core files).
- `techContext.md`: Tech stack and dependencies. (Includes a `## Lessons Learned` section, auto-updated when a difficult bug takes >3 attempts to fix).
- `progress.md`: Milestones and task checklists (`- [x]`, `- [ ]`). DO NOT use this for historical logging.
- `activeContext.md`: Current immediate focus. Strictly limited to the 10 most recent events (Hard limit: < 600 words).
- `changelog.md`: The Archive repository.

## 2. ️ GARBAGE COLLECTION (ANTI-BLOAT)
- **Auto-Trigger:** When `activeContext.md` reaches 11 events OR exceeds 800 words.
- **Action:** Summarize the oldest event(s) into 1-2 sentences, move them to `changelog.md`, and completely delete them from `activeContext.md`.
- **No-Code-Duplication Rule:** Never copy-paste code blocks into the Memory Bank. Reference file paths instead of cloning code patterns via prose.

## 3. ️ PLANNING & HANDOFF WORKFLOW
- **Deep-Plan Trigger:** Before implementing any task requiring >50 lines of code or touching >3 files, use `/deep-planning` to create/update a temporary `memory-bank/currentPlan.md` file.
- **Stop & Wait:** After generating the plan, you MUST ask the user "Approved?" or wait for confirmation before writing any implementation code.
- **Post-Task Cleanup:** After completing a major feature, merge architectural summaries from the plan into `systemPatterns.md`, append any crucial fixes to `techContext.md`, and delete/clear the temporary plan file.
- **Context Handoff:** Between continuous tasks, use `/newtask` for a clean handoff. Use `/smol` to compress context locally if the context window gets bloated mid-task (do not write unfinalized junk to the Memory Bank).

## 4.  WHEN TO UPDATE DIRECTLY
1. When discovering new patterns or making architectural decisions.
2. After completing a significant change or milestone.
3. When the user types **"update memory bank"** — at this point, you MUST review ALL 7 files.

```mermaid
flowchart TD
    A[User triggers: update memory bank] --> B[Review all Memory Bank files]
    B --> C[Update Checklists in progress.md]
    C --> D[Append new event to activeContext.md]
    D --> E{Exceeds 10 events or 600 words?}
    E -- Yes --> F[Archive oldest items to changelog.md]
    E -- No --> G[Update complete]
