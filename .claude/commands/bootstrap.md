# Project Bootstrap - PRD to GitHub Issues Creator

## Overview

**You are an AI assistant tasked with converting comprehensive PRD and Technical Architecture documents into a structured GitHub issue backlog. Your goal is to transform epics, requirements, and technical components into actionable development tasks that follow best practices and project conventions.**

## Input Format

You will work with the existing project documentation in this repository:

- `docs/PRD.md` - Product Requirements Document with epics and requirements
- `docs/TechnicalArchitecture.md` - Technical design and component breakdown
- `.claude/CLAUDE.md` - Project context and development guidelines

## Process Steps

Follow these steps to complete the task, make a todo list and think ultrahard:

### 1. Parse and analyze project documentation:

- Read `.claude/CLAUDE.md` for project overview and development context
- **Deep parse `docs/PRD.md`**:
  - Extract ALL epics (dynamic detection, not fixed count)
  - Parse each functional requirement for implementation complexity
  - Identify acceptance criteria and success metrics
  - Map UI design goals to specific implementation needs
  - Extract non-functional requirements (performance, security, etc.)
- **Deep parse `docs/TechnicalArchitecture.md`**:
  - Identify exact tech stack and architecture patterns
  - Extract component relationships and dependencies
  - Parse data flow requirements for implementation order
  - Identify external service integrations and APIs
  - Extract security and performance considerations
- **Cross-reference documents**: Ensure every PRD requirement has technical implementation path

### 2. Research GitHub issue best practices:

- Search for current best practices in writing GitHub issues for project initialization
- Look for examples of well-structured development backlogs in similar projects
- Focus on breaking down epics into actionable, developer-ready tasks

### 3. Present a detailed implementation plan:

- Map each PRD epic to specific technical architecture components
- Break down complex functional requirements into 2-4 hour implementation tasks
- Identify common patterns (auth, API integration, UI components, data management)
- Create issue dependency graph based on technical requirements
- Size issues for developer productivity (max 1-2 days each)
- Present this plan in `<plan>` tags with exact issue breakdown

### 4. Generate detailed, actionable GitHub issues:

- Transform each functional requirement into specific implementation tasks
- Include exact files to create/modify, API specifications, and code patterns
- Break down each epic into 4-8 granular, developer-ready issues
- Add implementation steps, code examples, and testing requirements
- Ensure each issue is immediately actionable without additional research
- Cross-reference all issues to original PRD sections and technical components

### 5. Format each detailed issue with:

- **Title**: Specific, actionable task (e.g., "Create login form component with validation")
- **Epic Reference**: Link to original PRD epic and functional requirement
- **Description**: Detailed implementation requirements with context
- **Implementation Steps**: Numbered, specific steps to complete the task
- **Files to Create/Modify**: Exact file paths and purposes
- **Code Patterns**: Starter code snippets, API signatures, or component structure
- **Acceptance Criteria**: Specific, testable requirements (3-6 criteria)
- **Technical Notes**: Architecture constraints, patterns, and best practices
- **Dependencies**: References to prerequisite issues with issue numbers
- **Testing Requirements**: What needs to be tested and how
- **Labels**: Dynamic labeling based on detected epics, tech stack, and component types

### 6. Setup GitHub repository and labels:

- Verify GitHub CLI authentication and repository setup
- Create all required labels for the project before creating issues
- Handle any setup errors gracefully with clear instructions

### 7. Create and execute GitHub issues:

- Execute the GitHub issue creation process automatically
- Create issues in dependency order to maintain proper sequencing
- Provide real-time feedback on issue creation progress
- Handle any creation errors and provide fallback options

## Important Guidelines

- Each issue should be completable in 2-4 hours by a developer (max 1 day)
- Break down large functional requirements into multiple granular tasks
- Reference specific PRD sections and technical architecture components
- Ensure issues are immediately actionable without additional research
- Include exact implementation details: files, APIs, code patterns, testing
- Map every functional requirement to specific implementation tasks
- Consider tech stack constraints and architecture patterns in all issues
- Generate 3x more issues than traditional approach for maximum detail
- Issues should read like step-by-step implementation guides

## Dynamic Project Analysis

The bootstrap command will:

- **Auto-detect epics** from PRD (no hardcoded assumptions)
- **Parse tech stack** from Technical Architecture document
- **Identify patterns** (auth, APIs, databases, UI components)
- **Generate appropriate labels** based on detected project structure
- **Size issues properly** based on functional requirement complexity
- **Create dependency chains** based on technical architecture flows

## CRITICAL REQUIREMENT

**The bootstrap process MUST create ALL detailed issues needed for complete project implementation. Do NOT stop after creating "examples" or "key issues." The goal is a COMPLETE development backlog that covers every functional requirement from the PRD.**

**Typical project scope: 40-60 detailed issues covering all epics and requirements.**

**NEVER compromise on completeness - the entire value of bootstrap is providing a ready-to-develop backlog with no gaps.**

## Bootstrap Success Criteria

The bootstrap process is ONLY successful when ALL of the following criteria are met:

- [ ] Every PRD functional requirement has corresponding implementation issues
- [ ] Every Technical Architecture component has implementation tasks
- [ ] All epics broken down into 2-4 hour tasks
- [ ] Complete dependency chain established from infrastructure to final features
- [ ] Ready-to-develop backlog created with no gaps requiring additional planning
- [ ] All issues include specific implementation steps, file paths, and code patterns
- [ ] Issue dependencies are properly sequenced for development workflow
- [ ] Every issue is immediately actionable without additional research

## Final Requirements

Your task is to fully execute the bootstrap process, not just generate commands. You must:

1. **Verify Prerequisites**: Check GitHub CLI authentication and repository setup
2. **Create Labels**: Automatically create all required labels before issue creation
3. **Execute Issue Creation**: Actually run the `gh issue create` commands and create ALL issues
4. **Provide Status Updates**: Give real-time feedback on progress and any errors
5. **Handle Errors**: Gracefully handle and report any setup or creation failures
6. **Ensure Completeness**: Create the FULL backlog - typically 40-60 detailed issues

The bootstrap process is complete only when all GitHub issues have been successfully created in the repository. Do not just provide commands - execute the full workflow.

Begin by analyzing the documentation, then execute the complete bootstrap process including setup, label creation, and issue creation.
