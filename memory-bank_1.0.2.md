----

**Auth:** xlee1162

**Version:** 1.0.2

**Date Release:** 2026-07-01

**Target Agent:** Any (Cline, Cursor, Antigravity, Codex

---

# 🧠 MEMORY BANK RULES

You are an expert AI engineer. You MUST strictly adhere to the following rules regarding the `memory-bank/` directory.

---

## 1. 🔄 SMART INITIALIZATION

- At the start of EVERY session, read ONLY `memory-bank/activeContext.md` and `memory-bank/currentPlan.md` (if exists).
- Do NOT read all files blindly to save tokens. Read other files only when the task specifically requires their context.
- If `memory-bank/` is missing, prompt: *"Memory Bank not found. Initialize it?"*

---

## 2. 📂 FILE ROLES & STRICT BOUNDARIES

Every file MUST start with YAML frontmatter (`last_updated`, `status`).
---
last_updated: YYYY-MM-DD
status: active | archived
---

- **`projectbrief.md`**: Core goals, scope, and requirements.
- **`systemPatterns.md`**: Architecture, design patterns, and component relationships.
- **`techContext.md`**: Tech stack, setup instructions, and `## Lessons Learned`.
- **`progress.md`**: Current sprint checklist (`- [x]`, `- [ ]`). **DO NOT** log history here.
- **`changelog.md`**: Long-term archive for completed milestones and detailed logs.
- **`activeContext.md`**: Immediate focus. Max **15 high-level events** (milestones, major decisions) OR **800 words**.
- **`currentPlan.md`**: **TEMPORARY** file for Plan-First workflow. **MUST BE DELETED** after task completion.

---

## 3. 🗑️ ANTI-BLOAT & GARBAGE COLLECTION
- **Rolling Log Rule:** activeContext.md is strictly for immediate focus and must never exceed 15 events OR 800 words.
- **No-Code-Duplication:** NEVER paste source code into Memory Bank. Reference file paths only.
- **Auto-Archive Rule:** When `activeContext.md` reaches 15 events OR 800 words:
  1. Summarize the oldest event into 1-2 sentences.
  2. Move it to `changelog.md`.
  3. Delete it from `activeContext.md`.

---

## 4. 🗺️ PLAN-FIRST & LIFECYCLE

- **Trigger:** Task requires >3 files OR >50 lines of code, OR user says "deep-plan", "lập kế hoạch", I must switch to planning mode.
- **Action:** Create `memory-bank/currentPlan.md` (Goal, Steps, Risks). **STOP** and wait for approval.
- **Cleanup:** Once the plan is successfully executed, migrate key architectural updates to `systemPatterns.md`, bugs/fixes to `techContext.md`, and completely clear or **DELETE** `currentPlan.md`.

---

## 5. 💬 CONTEXT MANAGEMENT COMMANDS (EXPLICIT TRIGGERS)

You MUST respond to these user commands with specific actions:

### Command: "update memory bank"

**Action Required:**
1. Review ALL 7 files in `memory-bank/`.
2. Update checklists in `progress.md` based on completed work.
3. Append new events to `activeContext.md` (max 15 events).
4. If `activeContext.md` exceeds limits → Auto-Archive to `changelog.md`.
5. Update YAML `last_updated` timestamps in all modified files.
6. Confirm completion: *"Memory Bank updated. [X] files modified."*

### Command: "compress context" OR "new task"

**Action Required:**
1. Summarize the current state from `activeContext.md`.
2. Ensure all completed items are moved to `progress.md` with `- [x]`.
3. Run Garbage Collection on `activeContext.md` (archive old events).
4. Clear `activeContext.md` of completed items, keeping only ongoing work.
5. Confirm: *"Context compressed. Ready for new task."*

### Command: "save" OR "end session"

**Action Required:**
1. Run full "update memory bank" procedure.
2. Ensure `currentPlan.md` is deleted if plan is complete.
3. Update all YAML timestamps to current date.
4. Confirm: *"Session saved. Memory Bank synchronized."*

---

## 6. ⚡ AUTO-TRIGGERS (AUTOMATIC ACTIONS)

- **File Creation:** New core file created? → Append 1-sentence description to `systemPatterns.md`.
- **Hard Bug Fixed:** Bug took >3 attempts? → Log root cause & fix in `techContext.md` under `## Lessons Learned`.
- **Plan Execution:** After completing a planned task? → Migrate learnings and DELETE `currentPlan.md`.

---

## 7. 🔄 UPDATE MEMORY BANK FLOW (CONDITIONAL LOGIC)

When executing "update memory bank", follow this decision tree:

**START** → Review all Memory Bank files
<br>↓<br>
Update checklists in `progress.md`
<br>↓<br>
Append new event to `activeContext.md`
<br>↓<br>
**Check:** Does `activeContext.md` exceed 15 events OR 800 words?
<br>↓<br>
- **YES** → Summarize oldest event → Move to `changelog.md` → Delete from `activeContext.md`
- **NO** → Keep as is
<br>↓<br>
Update YAML timestamps in all modified files
<br>↓<br>
**END** → Confirm completion to user

**You MUST follow this exact flow when updating the Memory Bank.**

---
