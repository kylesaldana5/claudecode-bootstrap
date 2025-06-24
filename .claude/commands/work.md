# Work Command - Automated Issue Implementation with Git Workflow

## Overview

**You are an AI assistant tasked with implementing a GitHub issue using an automated Git workflow. Your goal is to read the issue, create a feature branch, implement all requirements step-by-step with incremental commits, and complete the issue with proper Git workflow.**

## Input Format

The command will be called with an issue number:

```
/work 18
```

## Process Steps

Follow these steps to complete the issue implementation:

### 0. Gather recent work context:

- Use `git log --oneline -10` to review recent commits and understand latest changes
- Use `gh pr list --state merged --limit 5` to check recently merged PRs for context
- Use `gh issue list --state closed --limit 5` to see recently completed issues
- This provides context about current development momentum and patterns

### 1. Read and analyze the GitHub issue:

- Use `gh issue view {issue_number}` to read the complete issue details
- Parse all implementation steps, acceptance criteria, and technical requirements
- Understand dependencies and ensure prerequisite issues are completed
- Note all files to create/modify and code patterns provided

### 1.5. Discover project structure and technology stack:

- Use `ls -la` to get root directory overview
- Use `find . -maxdepth 2 -name ".*" -type f | head -20` to identify config files
- Use `find . -maxdepth 3 -type f | head -50` to map general file structure
- **Detect technology stack** by looking for key indicator files:
  - `package.json` → Node.js/JavaScript project
  - `requirements.txt`, `pyproject.toml`, `setup.py` → Python project
  - `Cargo.toml` → Rust project
  - `go.mod` → Go project
  - `pom.xml`, `build.gradle` → Java project
  - `Gemfile` → Ruby project
  - `composer.json` → PHP project
- Use appropriate file pattern discovery based on detected stack:
  - JavaScript/TypeScript: `**/*.{js,ts,jsx,tsx,astro,svelte,vue}`
  - Python: `**/*.py`
  - Go: `**/*.go`
  - Rust: `**/*.rs`
  - Java: `**/*.java`
  - Ruby: `**/*.rb`
  - PHP: `**/*.php`
- Read key project files (README, main config files) to understand architecture

### 1.7. Validate current project state:

- Check `git status` to ensure working directory is clean
- **Adaptive validation** based on detected technology stack:
  - **Node.js**: Try `npm run test || npm run build || npm run lint || npm run typecheck`
  - **Python**: Try `python -m pytest || python -m flake8 || python setup.py check || python -m mypy .`
  - **Go**: Try `go test ./... || go build || go vet || go fmt -d .`
  - **Rust**: Try `cargo test || cargo build || cargo check || cargo clippy`
  - **Java**: Try `mvn test || mvn compile || ./gradlew test || ./gradlew build`
  - **Ruby**: Try `bundle exec rspec || bundle exec rubocop || rake test`
  - **PHP**: Try `./vendor/bin/phpunit || ./vendor/bin/phpcs || composer test`
  - **Generic fallback**: Try `make test || make build || make check || make lint`
- Ensure development environment is working before starting implementation

### 2. Create feature branch:

- Check current git status and ensure main branch is clean
- Create descriptive feature branch: `feature/issue-{number}-{short-description}`
- Example: `feature/issue-18-project-directory-structure`
- Switch to the new branch for all development work

### 3. Implement step-by-step with incremental commits:

- Follow the issue's implementation steps exactly as specified
- **CRITICAL: Create a separate commit for EACH implementation step**
- After completing each individual step, commit immediately with descriptive message
- Commit message format: `Step {X}: {specific step description}`
- Example: `Step 1: Update Astro dependencies to secure versions`
- Example: `Step 2: Add Supabase client library integration`
- **Never bundle multiple steps into a single commit**
- This provides granular rollback capability and clear development history

### 4. Validate acceptance criteria:

- Verify each acceptance criteria checkbox can be marked as completed
- **Adaptive testing** based on detected technology stack (same patterns as step 1.7)
- Ensure all specified files are created/modified correctly
- Validate code patterns match the issue requirements

### 5. Final commit and push:

- Create final commit with issue completion summary
- Final commit format: `feat(issue-{number}): complete {issue title}`
- Push branch to origin: `git push -u origin {branch-name}`
- Provide summary of all commits made during implementation

### 6. Create pull request:

- Use `gh pr create` to automatically create a pull request
- PR title: `feat(issue-{number}): {issue title}`
- PR description should include:
  - Summary of implementation
  - List of changes made
  - Acceptance criteria validation
  - Link to the original issue
- Use template with checklist for testing and validation

### 7. Update issue with completion status:

- Check off ALL acceptance criteria checkboxes by editing the issue description
- Add comprehensive completion comment summarizing implementation
- Include validation results for each acceptance criteria
- Reference the pull request and commit history
- Document any deviations or additional work completed

### 8. Close the issue:

- Use `gh issue close {number}` to mark the issue as completed
- Ensure all acceptance criteria are checked off before closing
- Verify pull request is properly linked to the issue

## Important Guidelines

- **Gather context first** - understand recent work and project structure before implementing
- **Detect technology stack** - adapt validation and testing approaches to the project type
- **Follow issue requirements exactly** - don't deviate from specified implementation
- **Commit atomically** - create ONE commit for EACH implementation step, never bundle steps
- **Validate continuously** - ensure each step works before proceeding to next step
- **Document thoroughly** - commit messages should clearly describe what specific step was done
- **Handle errors gracefully** - if implementation fails, document the issue clearly
- **Maintain code quality** - follow project standards and best practices
- **Granular history** - each commit should be reversible independently for better rollback control
- **Technology agnostic** - work with any project type (Node.js, Python, Go, Rust, Java, etc.)

## Git Workflow Pattern

```bash
# 0. Gather context
git log --oneline -10
gh pr list --state merged --limit 5
gh issue list --state closed --limit 5

# 1. Discover project structure and detect tech stack
ls -la
find . -maxdepth 2 -name ".*" -type f | head -20
find . -maxdepth 3 -type f | head -50

# 1.5. Validate current state (adaptive based on tech stack)
git status
# Node.js: npm run test || npm run build || npm run lint
# Python: python -m pytest || python -m flake8 || python setup.py check
# Go: go test ./... || go build || go vet
# Generic: make test || make build || make check

# 2. Start from clean main branch
git checkout main
git pull origin main

# 3. Create feature branch
git checkout -b feature/issue-{number}-{description}

# 4. Implement with incremental commits - ONE COMMIT PER STEP
git add {files-for-step-1}
git commit -m "Step 1: {step 1 description}"
git add {files-for-step-2}
git commit -m "Step 2: {step 2 description}"
# ... repeat for EACH implementation step individually

# 5. Final push
git push -u origin feature/issue-{number}-{description}

# 6. Create pull request
gh pr create --title "feat(issue-{number}): {issue title}" --body "Implementation summary..."

# 7. Update issue acceptance criteria and close
gh issue edit {number} --body "Updated issue description with checked acceptance criteria..."
gh issue comment {number} --body "Implementation complete..."
gh issue close {number}
```

## Error Handling

- If prerequisite issues aren't completed, stop and notify the user
- If Git operations fail, provide clear error messages and recovery steps
- If implementation fails, document the failure and leave issue open
- If tests fail, fix issues before final commit

## Success Criteria

The work command is successful when:

- [ ] Feature branch created successfully
- [ ] All implementation steps completed per issue requirements
- [ ] All acceptance criteria validated and met
- [ ] Incremental commits document the development process
- [ ] Final branch pushed to origin
- [ ] Pull request created with comprehensive description
- [ ] Issue acceptance criteria checkboxes marked as completed
- [ ] Issue updated with completion summary and closed
- [ ] Code quality maintained throughout implementation

## Command Usage

```
/work {issue_number}
```

Example:

```
/work 18  # Implements issue #18 with full Git workflow
```

This command provides a complete automated development workflow from issue assignment through implementation to completion and Git integration.
