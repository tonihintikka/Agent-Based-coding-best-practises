# Vibe Coding with Cursor: A Structured Workflow Guide

## Introduction to Vibe Coding

"Vibe coding," a term popularized by Andrej Karpathy in 2025, refers to using AI to generate code through natural language prompts, enabling non-technical users to build applications. While this approach has democratized programming, it often results in "house of cards code" – code that appears functional but is structurally fragile.

This guide presents a structured workflow for vibe coding using Cursor with Claude 3.7 Sonnet that addresses common pitfalls through a dual-role system approach.

## Key Challenges in Vibe Coding

1. **Error Propagation**: Fixing one error often creates another, leading to an "infinite death loop of errors"
2. **Fragile Code Structures**: AI-generated code without proper planning can result in poorly integrated components
3. **Context Limitations**: AI may not fully understand project scope or requirements without structured guidance
4. **Debugging Difficulties**: Non-technical users struggle to interpret and address error messages
5. **Documentation Gaps**: Generated code often lacks sufficient documentation and explanation

## The Dual-Role System Workflow

This workflow establishes two distinct roles for Cursor AI: Planner and Executor. This separation creates a more methodical, reliable approach to vibe coding.

### Role Definitions

#### Planner
- **Purpose**: Strategic oversight and task management
- **Responsibilities**: Breaking down tasks, defining success criteria, evaluating progress
- **Model Recommendation**: Claude 3.7 Sonnet in "thinking" mode for deeper reasoning

#### Executor
- **Purpose**: Implementation of specific coding tasks
- **Responsibilities**: Writing code, running tests, reporting progress
- **Model Recommendation**: Claude 3.7 Sonnet in standard mode for code generation

## Workflow Implementation

### Step 1: Set Clear Goals, Not Commands

**What to Do**: 
- Describe what you want to achieve, not how to achieve it
- Example: "I want to get stronger. How would you approach building a workout tracking app?"
- Ask discovery questions: "How would you make this?" or "What do you need from me?"

**Why It Works**:
- Allows AI to leverage its understanding of architecture and best practices
- Prevents constraining the solution with potentially incorrect technical assumptions
- Reveals gaps in requirements through AI-initiated questions

### Step 2: Configure Cursor Rules for the Dual-Role System

**What to Do**:
- Create a rule file in `.cursor/rules/dual-role-system.md` using our template
- You can find a ready-to-use template here: [Dual-Role System Rules Template](./templates/dual-role-system-rules.md)
- The template contains the following content:

```markdown
---
Description: Dual-Role System (Planner and Executor) for Vibe Coding
Globs: **/*
---

# Dual-Role System Rules

You are a multi-agent system coordinator, playing two roles: Planner and Executor.

## Planner Role
- Break down tasks into manageable steps
- Define clear success criteria for each task
- Create and maintain a project roadmap
- Update the scratchpad (.cursor/scratchpad.md) with project status
- Review progress before proceeding to the next task
- Flag issues or inconsistencies for the Executor to address

## Executor Role
- Implement one task at a time from the Planner's roadmap
- Write code following project standards and best practices
- Run tests to verify functionality after each implementation
- Report issues or blockers encountered during implementation
- Follow Test-Driven Development principles where appropriate

## Workflow Guidelines
1. Always start with Planner mode to establish a clear plan
2. Switch to Executor mode only when a well-defined task is ready
3. Return to Planner mode after task completion for verification
4. Use the scratchpad as the source of truth for project status
5. Follow the "check console" approach for detailed error information
6. Revert to the last working state instead of fixing complex errors
7. Document lessons learned to avoid repeating mistakes
```

**Why It Works**:
- Establishes clear boundaries between planning and implementation
- Creates a structured approach that prevents error cascades
- Documents progress and learning for future reference

### Step 3: Initialize the Scratchpad

**What to Do**:
- Create a `.cursor/scratchpad.md` file using our template
- You can find a ready-to-use template here: [Vibe Coding Scratchpad Template](./templates/vibe-coding-scratchpad.md)
- The basic structure looks like this:

```markdown
# Project Scratchpad

## Project Status Board
- [ ] Task 1: Description (Status)
- [ ] Task 2: Description (Status)
- [ ] Task 3: Description (Status)

## Current Focus
[Description of the current task being implemented]

## Implementation Notes
[Details about the current implementation approach]

## Lessons Learned
- Lesson 1: [Description]
- Lesson 2: [Description]

## Questions & Blockers
- Question 1: [Description]
- Blocker 1: [Description]
```

**Why It Works**:
- Provides a central location for tracking progress
- Documents lessons learned to prevent repeated mistakes
- Creates a historical record of development decisions

### Step 4: Start with Planner Mode

**What to Do**:
- Invoke Planner mode: "Invoke planner mode and create a plan based on my goal"
- Use Claude 3.7 Sonnet in thinking mode for deeper reasoning
- Ask the Planner to outline the entire solution before any coding begins

**Why It Works**:
- Creates a comprehensive plan before implementation begins
- Identifies potential issues before they manifest in code
- Establishes clear success criteria for evaluating progress

### Step 5: Gather API Documentation

**What to Do**:
- Use the `@web` tag in Cursor to fetch up-to-date API documentation
- Ask the AI to create .md files for reference documentation
- Store these files in a `/docs` directory for easy reference

**Why It Works**:
- Ensures AI has access to current, accurate API information
- Prevents errors caused by outdated or incorrect API understanding
- Creates a persistent reference that can be used throughout development

### Step 6: Switch to Executor Mode

**What to Do**:
- Once the plan is ready, switch to Executor mode: "Invoke executor mode and begin implementing the first task"
- Use Claude 3.7 Sonnet in normal mode for implementation
- Have the Executor complete one task at a time with clear testing after each step

**Why It Works**:
- Focuses implementation on well-defined, manageable tasks
- Enforces testing of each component before moving on
- Creates clear checkpoints throughout development

### Step 7: Alternate Between Planner and Executor

**What to Do**:
- After the Executor completes a task, switch back to Planner mode
- Verify success: "Task X is complete. What evidence do you have that it was done successfully?"
- If successful, the Planner queues the next task; if not, it flags issues for the Executor to address

**Why It Works**:
- Ensures each component works before building upon it
- Prevents error cascades by catching issues early
- Maintains development momentum through clear task progression

### Step 8: Debug Effectively

**What to Do**:
- When errors occur, ask the AI to "check the console" to read error messages directly
- Let the AI interpret the error messages rather than describing them manually
- Focus questions on understanding the root cause rather than symptoms

**Why It Works**:
- Provides the AI with direct access to error information
- Reduces information loss through manual error description
- Leverages AI's ability to interpret technical error messages

### Step 9: Revert Changes Instead of Fixing Errors

**What to Do**:
- If an error persists, revert to the last working checkpoint
- Rethink the prompt: "What do you need to feel 100% confident you can implement this?"
- Restart implementation with a clearer understanding of requirements

**Why It Works**:
- Prevents compounding errors through repeated fix attempts
- Creates a clean slate for implementation
- Often faster than trying to debug complex, interconnected issues

### Step 10: Scale Down if Necessary

**What to Do**:
- If implementation continues to fail, reduce the scope or complexity
- Ask the Planner to simplify the architecture or features
- Focus on building a minimal viable solution before adding complexity

**Why It Works**:
- Ensures a working foundation before adding complexity
- Provides incremental success experiences
- Creates a stable codebase that can be extended

## Advanced Techniques

### Using AI-Driven Test-Driven Development

**What to Do**:
- Instruct the Executor to write tests before implementation
- Have tests verify both functionality and edge cases
- Implement just enough code to pass tests

**Why It Works**:
- Creates clear success criteria for implementation
- Prevents feature creep during implementation
- Results in more robust, well-tested code

### Project Checkpoints Management

**What to Do**:
- Create git commits after each successful task completion
- Use descriptive commit messages that reference the task
- Tag significant milestones in the development process

**Why It Works**:
- Creates recoverable points throughout development
- Provides a history of implementation decisions
- Enables easy rollback to any successful state

### Documentation Generation

**What to Do**:
- After completing implementation, ask the Planner to create comprehensive documentation
- Include setup instructions, usage examples, and architecture diagrams
- Document known limitations and future improvement opportunities

**Why It Works**:
- Creates valuable documentation that often gets neglected
- Ensures understanding of the codebase beyond the current development cycle
- Facilitates onboarding of other team members

## Case Study: Workout Tracking App

### Example Implementation

1. **Initial Goal Statement**:
   "I want to get stronger. How would you approach building a workout tracking app?"

2. **Planner Role Analysis**:
   - Identified key requirements: exercise logging, progress tracking, workout planning
   - Recommended a React-based PWA with local storage
   - Broke down implementation into 8 discrete tasks

3. **Executor Task Implementation**:
   - Task 1: Set up project scaffold with Create React App
   - Task 2: Implement data models for exercises and workouts
   - Task 3: Create exercise logging component

4. **Error Management**:
   - When an error occurred in the data persistence layer, reverted to the last checkpoint
   - Planner reassessed the approach and recommended a different storage strategy
   - Executor implemented the new strategy successfully

5. **Final Outcome**:
   - A functional workout tracking application
   - Well-documented codebase with clear component separation
   - Robust error handling and data validation

## Conclusion

The dual-role system for vibe coding transforms an often chaotic process into a structured, methodical approach. By separating planning from execution and establishing clear checkpoints throughout development, this workflow addresses the key challenges of vibe coding.

While this approach requires more initial setup and discipline than ad-hoc vibe coding, it delivers more reliable, maintainable results with significantly less frustration. By adopting this workflow, even non-technical users can successfully create functional applications without getting trapped in the "infinite death loop of errors" that often characterizes less structured approaches.

Remember that effective vibe coding still requires critical thinking and active participation. The AI is a powerful assistant, but the human remains the director of the development process, making key decisions and evaluating progress at each step.
