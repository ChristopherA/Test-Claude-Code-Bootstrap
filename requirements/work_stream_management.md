# Work Stream Management Requirements

This document defines how work streams are managed across branches.

## Work Stream Definition

- A work stream is a series of related tasks
- Each work stream has a dedicated branch
- Work streams have clear requirements and deliverables

## Task Tracking

- WORK_STREAM_TASKS.md is the central task document
- Tasks are organized by branch
- Each task has a clear owner and status
- Tasks follow a consistent format

## Status Tracking

- Use checkboxes to indicate completion: [ ] vs [x]
- Include completion dates for finished items
- Use consistent priority labels
- Mark critical path items

## Branch Context

- Each work stream has a context file
- Context files capture current status
- Context files provide guidance for Claude
- Update context when switching branches
- Properly close context when completing work

## Context Management Protocol

The following protocol should be followed to maintain context continuity across Claude sessions:

### Closing a Context Session

When ending a work session or switching branches, properly "close" context by:

1. **Save Current State:**
   - Commit important files to Git if appropriate
   - Document current state in relevant context files
   - Ensure any temporary files are properly backed up

2. **Capture Progress and Learnings:**
   - Update task lists with completed items (mark with [x] and add completion date)
   - Document any bugs encountered and their solutions
   - Note partial progress on in-progress tasks
   - Record key decisions made during the session

3. **Update Planning Documents:**
   - Revise requirements files if new requirements were discovered
   - Update task lists with any new tasks identified
   - Adjust priorities based on session learnings
   - Add clarifications to ambiguous requirements

4. **Improve Documentation:**
   - Update context files with new information
   - Enhance error handling sections with new scenarios
   - Add useful code snippets or commands discovered

5. **Record Technical Details:**
   - Document exact commands that worked (and those that failed)
   - Note environment-specific issues
   - Record version information for relevant tools

6. **Update Development History:**
   - Add a new entry in the Development History section
   - Focus on substantive achievements, not minor details
   - Include date and authorship information
   - Summarize key changes and their implications
   - Note any major problems solved and their solutions
   - Document specific testing results with evidence

7. **Create Context Closure Section by EDITING THE ACTUAL CONTEXT FILE:**
   - IMPORTANT: You MUST use the Edit tool to update the context file itself, not just report in chat
   - Add or update the Context Closure section with current date
   - Include a detailed Completed Work Summary with all achievements
   - Document specific Testing Results with evidence
   - Add detailed Next Steps for Future Sessions
   - Update the context file's last-updated date in the metadata
   - Use actual file editing tools to make these changes to the file

8. **Prepare Restart Instructions:**
   - Create clear instructions for resuming work
   - Document the exact command to restart Claude CLI
   - Note files that should be loaded first
   - Include reminders about the current branch and state

### Session Management

- Use standardized restart command for Claude:
  ```
  claude "load CLAUDE.md and follow its instructions, identify our current branch, and continue with the next task on that branch"
  ```
- Between sessions, perform these Git operations:
  - Switch to main and pull updates: `git checkout main && git pull`
  - Fetch all remote branches: `git fetch --all`
  - Switch back to working branch before restarting Claude: `git checkout <branch-name>`
- When to use `/compact` vs `/exit`:
  - Use `/compact` when conversation is getting long but you need to continue
  - Use `/exit` when completing a work session entirely

## Work Stream Coordination

- Coordinate dependencies between branches
- Manage branch merging sequence
- Use cherry-picking for selective updates
- Keep main branch authoritative
