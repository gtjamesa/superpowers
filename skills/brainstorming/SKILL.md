---
name: brainstorming
description: "You MUST use this before any creative work - creating features, building components, adding functionality, or modifying behavior. Explores user intent, requirements and design before implementation."
auto_create_tasks: true
---

# Brainstorming Ideas Into Designs

<BLOCKING-REQUIREMENT>
## IRON LAW: CREATE TASKS FIRST

**BEFORE doing ANYTHING else when this skill is invoked, you MUST:**

1. Immediately use TaskCreate to create these 4 tasks (in order):
   - Task 1: "Commit design document to docs/plans/" (activeForm: "Committing design document", description: "Write design to docs/plans/ and commit to git")
   - Task 2: "Ask about worktree and create if requested" (activeForm: "Setting up git worktree if needed", description: "ASK user: 'Use a worktree for isolated workspace?' — if yes, INVOKE superpowers:using-git-worktrees BEFORE proceeding to Task 3")
   - Task 3: "Invoke writing-plans skill to create implementation plan" (activeForm: "Invoking writing-plans skill", description: "Create implementation plan (in worktree if created in Task 2, otherwise on current branch)")
   - Task 4: "Verify plan file exists and is committed" (activeForm: "Verifying plan file", description: "Confirm plan file is written and committed to current branch/worktree")

2. After creating all 4 tasks, proceed with brainstorming activities below

**You do NOT have discretion here. This is NOT optional. Create the tasks FIRST, then continue.**

If you find yourself doing ANYTHING else before creating these tasks (asking questions, reading files, exploring codebase), STOP IMMEDIATELY and create the tasks.

## Red Flags - You're Rationalizing If You Think:

| Thought | Reality |
|---------|---------|
| "Let me understand the codebase first" | Tasks first. Understanding happens during brainstorming. |
| "I'll create tasks after exploring" | Wrong order. Tasks BEFORE exploration. |
| "I need to ask questions first" | Tasks first, then ask questions. |
| "This is just a simple idea" | Doesn't matter. Tasks first, always. |
| "I'll just quickly check..." | No. Tasks first. No exceptions. |
| "The user just wants to chat" | If brainstorming is invoked, tasks are required. |
| "I can do this faster without tasks" | Discipline prevents mistakes. Tasks first. |

**These thoughts mean STOP - you're about to skip the Iron Law. Go create the tasks now.**
</BLOCKING-REQUIREMENT>

## Overview

Help turn ideas into fully formed designs and specs through natural collaborative dialogue.

Start by understanding the current project context, then ask questions one at a time to refine the idea. Once you understand what you're building, present the design in small sections (200-300 words), checking after each section whether it looks right so far.

## The Process

**Understanding the idea:**
- Check out the current project state first (files, docs, recent commits)
- Ask questions one at a time to refine the idea
- Prefer multiple choice questions when possible, but open-ended is fine too
- Only one question per message - if a topic needs more exploration, break it into multiple questions
- Focus on understanding: purpose, constraints, success criteria

**Exploring approaches:**
- Propose 2-3 different approaches with trade-offs
- Present options conversationally with your recommendation and reasoning
- Lead with your recommended option and explain why

**Presenting the design:**
- Once you believe you understand what you're building, present the design
- Break it into sections of 200-300 words
- Ask after each section whether it looks right so far
- Cover: architecture, components, data flow, error handling, testing
- Be ready to go back and clarify if something doesn't make sense

## After the Design

**Documentation:**
- Write the validated design to `docs/plans/YYYY-MM-DD-<topic>-design.md`
- Use elements-of-style:writing-clearly-and-concisely skill if available
- Commit the design document to git

**Implementation (if continuing):**
- Ask: "Ready to set up for implementation?"

<VERIFICATION-CHECKPOINT>
**BEFORE PROCEEDING:** Confirm you created the 4 required tasks when this skill was loaded.

Run TaskList to verify. You should see:
- Task for committing design document
- Task for asking about git worktree
- Task for invoking writing-plans skill
- Task for verifying plan file

If these tasks don't exist, CREATE THEM NOW before continuing.
</VERIFICATION-CHECKPOINT>

### Implementation Checklist

**NOTE:** When this skill was invoked, these tasks were automatically created for you via the Iron Law above. Work through them in order using TaskUpdate to mark progress.

The pre-created tasks track this checklist:

- [ ] Design document committed to `docs/plans/` (committed to main/current branch)
- [ ] ASK user: "Use a worktree for isolated workspace?" — **if yes, INVOKE Skill tool with `superpowers:using-git-worktrees` BEFORE creating plan**
- [ ] INVOKE Skill tool with `superpowers:writing-plans` to create implementation plan (in worktree if created, otherwise on current branch)
- [ ] Plan file exists and is committed (to worktree or current branch)

<HARD-STOP>
Do NOT write implementation code until all checklist items are complete.

If you catch yourself writing code without completing this checklist, STOP IMMEDIATELY and invoke the missing skills.
</HARD-STOP>

## Key Principles

- **One question at a time** - Don't overwhelm with multiple questions
- **Multiple choice preferred** - Easier to answer than open-ended when possible
- **YAGNI ruthlessly** - Remove unnecessary features from all designs
- **Explore alternatives** - Always propose 2-3 approaches before settling
- **Incremental validation** - Present design in sections, validate each
- **Be flexible** - Go back and clarify when something doesn't make sense
