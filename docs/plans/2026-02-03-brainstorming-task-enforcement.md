# Brainstorming Skill Task Enforcement Implementation

**Date:** 2026-02-03
**Status:** Implemented
**Approach:** In-Skill Enforcement (Approach 2 from plan)

## Problem

When `/brainstorming` was invoked, the Implementation Checklist was not consistently followed. Tasks were supposed to be created via TaskCreate, but agents could skip this step through rationalization.

## Solution

Since Claude Code's Skill tool cannot be modified from this repository, implemented maximum-strength in-skill enforcement following rigid discipline skill patterns (TDD, systematic-debugging).

## Changes Made

### 1. Added `auto_create_tasks: true` Frontmatter Flag

```yaml
---
name: brainstorming
description: "..."
auto_create_tasks: true
---
```

This flag:
- Documents intent for future infrastructure improvements
- Could enable automatic task creation if Skill tool is enhanced later
- Signals to readers that tasks should be auto-created

### 2. Added IRON LAW: CREATE TASKS FIRST Section

Placed at the very top of skill content (lines 9-39) with:

- `<BLOCKING-REQUIREMENT>` wrapper for maximum visibility
- Explicit numbered instructions to create 4 specific tasks
- Task specifications with exact subjects and activeForms
- Non-negotiable language: "You do NOT have discretion here"
- Immediate stop instruction if attempting other actions first

### 3. Added Red Flags Table

Lists 7 common rationalization patterns:
- "Let me understand the codebase first"
- "I'll create tasks after exploring"
- "I need to ask questions first"
- "This is just a simple idea"
- "I'll just quickly check..."
- "The user just wants to chat"
- "I can do this faster without tasks"

Each has a "Reality" column correcting the rationalization.

### 4. Added Verification Checkpoint

Before "Implementation Checklist" section (lines 78-88):

- `<VERIFICATION-CHECKPOINT>` wrapper
- Explicit instruction to run TaskList
- Lists expected task subjects
- Fallback instruction: if tasks don't exist, create them NOW

### 5. Updated Implementation Checklist Documentation

Changed from:
> "You MUST complete this checklist before writing any code. Use TaskCreate for each checklist item:"

To:
> "**NOTE:** When this skill was invoked, these tasks were automatically created for you via the Iron Law above. Work through them in order using TaskUpdate to mark progress."

## 4 Required Tasks

When brainstorming is invoked, these tasks MUST be created immediately:

1. **Subject:** "Commit design document to docs/plans/"
   **ActiveForm:** "Committing design document"
   **Description:** Design doc creation and commit step

2. **Subject:** "Ask user about git worktree setup"
   **ActiveForm:** "Asking user about git worktree setup"
   **Description:** Determine if worktree isolation is needed

3. **Subject:** "Invoke writing-plans skill to create implementation plan"
   **ActiveForm:** "Invoking writing-plans skill"
   **Description:** Create structured implementation plan

4. **Subject:** "Verify plan file exists and is committed"
   **ActiveForm:** "Verifying plan file"
   **Description:** Confirm plan is written and committed

## Enforcement Mechanism

**Multi-layered enforcement:**

1. **Frontmatter signal** - `auto_create_tasks: true` documents intent
2. **Iron Law at top** - First thing agent reads when skill loads
3. **BLOCKING-REQUIREMENT tags** - High visibility wrapper
4. **Red Flags table** - Pre-emptively counters rationalizations
5. **Verification checkpoint** - Safety net before implementation
6. **Updated checklist language** - Reinforces that tasks should exist

## Testing

**Manual test procedure:**

1. Note current TaskList state
2. Invoke `/brainstorming` in a new context
3. Verify Claude creates 4 tasks immediately (before asking questions or exploring code)
4. Verify task subjects match specification
5. Verify brainstorming proceeds only after task creation

**Expected behavior:**

First action after skill invocation should be 4 TaskCreate calls, not questions or file reads.

## Why Not Automatic Task Creation?

The plan originally proposed modifying Claude Code's Skill tool to automatically create tasks when brainstorming is loaded. This was not feasible because:

1. Skill tool is part of Claude Code core, not this repository
2. This repository only contains skill content files
3. Cannot modify tool execution infrastructure from skill content

However, the `auto_create_tasks: true` frontmatter flag enables future implementation if Claude Code adds this capability.

## Future Extensions

This pattern could be applied to other rigid discipline skills:

- `writing-skills` - Auto-create skill creation checklist tasks
- `subagent-driven-development` - Auto-create task tracking
- `executing-plans` - Auto-create tasks from plan file

Flag these with `auto_create_tasks: true` when ready.

## Alternative Approaches Considered

See original plan for full analysis. Other approaches:

1. **Automatic Task Creation** (Approach 1) - Requires modifying Claude Code
2. **Strengthen In-Skill Enforcement** (Approach 2) - ✅ IMPLEMENTED
3. **Pre-Flight Checklist Pattern** (Approach 3) - Similar to #2, less structured
4. **Hybrid** (Approach 4) - Would do #1 + #2 together

Chose Approach 2 because it's implementable immediately and provides strong enforcement without infrastructure changes.

## Files Modified

- `skills/brainstorming/SKILL.md` - Added enforcement sections

## Commit

```
feat(brainstorming): enforce automatic task creation via Iron Law

Add BLOCKING-REQUIREMENT section at top of skill that mandates
immediate TaskCreate calls before any other activities.
```

Commit: 21547dff40d07265a08ff5a1d96d27279d3f8978
