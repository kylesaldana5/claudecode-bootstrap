# Review Command - Automated Pull Request Review

## Overview

**You are an AI assistant tasked with conducting a comprehensive code review of a GitHub pull request. Your goal is to analyze all changes, provide detailed feedback, and submit a formal review with actionable recommendations.**

## Input Format

The command will be called with a pull request number:

```
/review 123
```

## Process Steps

Follow these steps to complete the pull request review:

### 1. Fetch pull request details:

- Use `gh pr view {pr_number}` to read the complete PR details
- Parse PR title, description, linked issues, and file changes
- Understand the scope and purpose of the changes
- Note the feature branch and target branch information

### 2. Analyze the code changes:

- Use `gh pr diff {pr_number}` to view all code changes
- Review each modified file for:
  - Code quality and adherence to project standards
  - Logic correctness and potential bugs
  - Security considerations and vulnerabilities
  - Performance implications
  - Documentation and comment quality
  - Test coverage adequacy

### 3. Validate implementation requirements:

- Compare changes against linked issue requirements
- Verify all acceptance criteria are met
- Check for completeness of implementation
- Ensure no scope creep or missing functionality
- Validate architectural consistency with project patterns

### 4. Check technical standards:

- **TypeScript/JavaScript**: Type safety, modern syntax, error handling
- **Astro Components**: Component structure, props validation, slot usage
- **CSS/Styling**: Consistency with design system, responsive design
- **File Organization**: Proper directory structure, naming conventions
- **Import/Export**: Clean import paths, proper module exports

### 5. Assess quality factors:

- **Maintainability**: Clear code structure, readable logic
- **Reusability**: Component design, utility function patterns
- **Performance**: Optimization opportunities, bundle size impact
- **Accessibility**: ARIA attributes, semantic HTML, keyboard navigation
- **SEO**: Meta tags, structured data, content optimization

### 6. Submit comprehensive review:

- Use `gh pr review {pr_number}` to submit formal review
- Include specific line comments for individual issues
- Provide overall summary with recommendations
- Choose appropriate review action: APPROVE, REQUEST_CHANGES, or COMMENT

## Review Categories

### Code Quality ⭐

- Clean, readable, and maintainable code
- Consistent formatting and style
- Appropriate comments and documentation
- Error handling and edge cases

### Functionality ✅

- Requirements fully implemented
- Logic correctness and completeness
- Proper integration with existing systems
- User experience considerations

### Security & Performance 🔒

- Input validation and sanitization
- Authentication and authorization
- Performance optimizations
- Bundle size and loading efficiency

### Testing & Validation 🧪

- Unit test coverage for new functionality
- Integration test considerations
- Manual testing verification
- Build and deployment validation

## Review Comment Templates

### Positive Feedback

```
✅ **Great implementation!** This solution elegantly handles [specific aspect] and follows our established patterns.
```

### Improvement Suggestions

```
💡 **Suggestion:** Consider [specific improvement] to enhance [maintainability/performance/readability].
```

### Critical Issues

```
⚠️ **Issue:** This could lead to [specific problem]. Recommend [specific solution].
```

### Questions

```
❓ **Question:** Could you clarify the reasoning behind [specific implementation choice]?
```

## Review Decision Framework

### APPROVE ✅

- All requirements met completely
- Code quality meets or exceeds standards
- No significant issues or concerns
- Ready for merge

### REQUEST_CHANGES ❌

- Critical bugs or security issues
- Requirements not fully met
- Significant code quality concerns
- Breaking changes to existing functionality

### COMMENT 💬

- Minor suggestions for improvement
- Questions about implementation choices
- Non-blocking feedback
- General observations and recommendations

## GitHub CLI Commands

```bash
# View pull request details
gh pr view {pr_number}

# View code changes
gh pr diff {pr_number}

# Review specific files
gh pr diff {pr_number} --name-only
gh pr diff {pr_number} src/components/

# Submit review with approval
gh pr review {pr_number} --approve --body "Review summary..."

# Submit review requesting changes
gh pr review {pr_number} --request-changes --body "Issues found..."

# Submit comment-only review
gh pr review {pr_number} --comment --body "Suggestions..."
```

## Success Criteria

The review command is successful when:

- [ ] PR details and changes thoroughly analyzed
- [ ] All code quality aspects evaluated
- [ ] Implementation completeness verified
- [ ] Technical standards compliance checked
- [ ] Comprehensive review submitted to GitHub
- [ ] Actionable feedback provided for any issues
- [ ] Review decision clearly justified

## Command Usage

```
/review {pr_number}
```

Example:

```
/review 45  # Reviews pull request #45 with comprehensive analysis
```

This command provides systematic code review to maintain high quality standards and ensure proper implementation of features before merging.
