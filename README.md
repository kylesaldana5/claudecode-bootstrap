# ClaudeCode Bootstrap

A GitHub template repository for rapidly bootstrapping new development projects with Claude Code integration, automated workflows, and comprehensive development tooling.

## 🚀 Quick Start

### 1. Use This Template
Click the **"Use this template"** button above to create a new repository from this template.

### 2. Clone and Initialize
```bash
git clone https://github.com/yourusername/your-new-project.git
cd your-new-project
chmod +x kickstart
./kickstart "My Awesome Project"
```

### 3. Add Your Documentation
Place your project documentation in the `docs/` directory:
- `docs/PRD.md` - Product Requirements Document
- `docs/TechnicalArchitecture.md` - Technical Architecture Document

### 4. Start Development
```bash
# Create GitHub issues from your PRD
claude --file .claude/commands/bootstrap.md

# Implement features systematically
claude --file .claude/commands/work.md

# Review pull requests thoroughly
claude --file .claude/commands/review.md
```

## 📋 What's Included

### 🤖 Claude Code Integration
- **CLAUDE.md** - Project context and development guidelines
- **Automation Commands** - Pre-built workflows for common development tasks
- **MCP Configurations** - Enhanced AI capabilities with file system, GitHub, and web search

### ⚡ Development Automation
- **Bootstrap Command** - Converts PRD and Technical Architecture into comprehensive GitHub issue backlog
- **Work Command** - Automated feature implementation with full Git workflow (branching, commits, PRs)
- **Review Command** - Comprehensive automated code review for pull requests
- **Issues Command** - Creates individual GitHub issues from feature descriptions

### 🛠️ Project Structure
```
your-project/
├── .claude/
│   └── commands/           # Claude Code automation commands
│       ├── bootstrap.md    # PRD → GitHub issues conversion
│       ├── work.md         # Automated feature implementation
│       ├── review.md       # Automated code review
│       └── issues.md       # Individual issue creation
├── .github/
│   ├── ISSUE_TEMPLATE/     # Bug report and feature request templates
│   └── workflows/          # CI/CD automation
├── docs/                   # Project documentation
│   ├── PRD.md             # Product Requirements (add your own)
│   └── TechnicalArchitecture.md  # Technical design (add your own)
├── .mcp.json              # Model Context Protocol configurations
├── kickstart              # Project initialization script
└── README.md              # This file (will be updated for your project)
```

## 🔧 Detailed Setup

### Prerequisites
- [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code) installed
- [GitHub CLI](https://cli.github.com/) (optional, for enhanced GitHub integration)
- Git configured with your credentials

### Kickstart Script
The `./kickstart "Project Name"` script automatically:
- ✅ Replaces template placeholders with your project details
- ✅ Initializes Claude Code with proper configuration
- ✅ Creates documentation directory structure
- ✅ Provides clear next steps for development

### MCP Integration Setup
The template includes pre-configured MCP servers for enhanced AI capabilities:

1. **File System Access** (auto-configured)
   - Full project directory access for Claude Code

2. **GitHub Integration** (requires setup)
   - Get a token: https://github.com/settings/tokens
   - Replace `your_github_token_here` in `.mcp.json`

3. **Web Search** (requires setup)
   - Get API key: https://api.search.brave.com/app/keys
   - Replace `your_brave_api_key_here` in `.mcp.json`

## 🎯 Development Workflow

### 1. Planning Phase
- Create comprehensive PRD with epics and requirements
- Design technical architecture with component breakdown
- Place both documents in `docs/` directory

### 2. Issue Generation
```bash
claude --file .claude/commands/bootstrap.md
```
- Automatically converts PRD into structured GitHub issues
- Maps requirements to implementation tasks
- Creates proper issue labels and milestones

### 3. Feature Implementation
```bash
claude --file .claude/commands/work.md
```
- Systematic issue implementation
- Automated Git workflow (branch → commit → PR)
- Consistent code quality and documentation

### 4. Code Review
```bash
claude --file .claude/commands/review.md
```
- Comprehensive PR analysis
- Security and performance review
- Automated feedback and suggestions

### 5. Iteration
Repeat the work/review cycle for continuous development.

## 📖 Command Reference

### Core Commands
- `./kickstart "Project Name"` - Initialize new project from template
- `claude --file .claude/commands/bootstrap.md` - Generate GitHub issues from PRD
- `claude --file .claude/commands/work.md` - Implement features systematically
- `claude --file .claude/commands/review.md` - Review pull requests
- `claude --file .claude/commands/issues.md` - Create individual issues

### File Structure Commands
After running kickstart, your project will have:
- Clear documentation structure in `docs/`
- Automated development workflows in `.claude/commands/`
- GitHub templates and CI/CD in `.github/`
- MCP configurations for enhanced AI capabilities

## 🎨 Customization

### Adding Custom Commands
Create new `.md` files in `.claude/commands/` following this pattern:
```markdown
# Command Name

Your Claude Code prompt here...

## Context
- Describe what this command does
- List any prerequisites
- Explain expected outcomes
```

### Modifying MCP Configurations
Edit `.mcp.json` to add or modify MCP servers:
```json
{
  "mcpServers": {
    "your-custom-server": {
      "command": "npx",
      "args": ["@your/mcp-server"],
      "env": {
        "API_KEY": "your_key_here"
      }
    }
  }
}
```

### Tech Stack Templates
The template is framework-agnostic. Add tech-stack-specific configurations as needed:
- Package managers (package.json, requirements.txt, etc.)
- Build tools and configurations
- Testing frameworks
- Deployment configurations

## 🚀 Why Use This Template?

### Before ClaudeCode Bootstrap
- ❌ Manual Claude Code setup for each project
- ❌ Repetitive MCP configuration
- ❌ Inconsistent development workflows
- ❌ Time-consuming GitHub issue creation
- ❌ Ad-hoc project structure

### After ClaudeCode Bootstrap
- ✅ **One-command setup** → Fully configured project ready for development
- ✅ **Automated workflows** → Consistent development processes
- ✅ **AI-enhanced development** → Leverage Claude Code's full capabilities
- ✅ **Rapid prototyping** → From idea to implementation faster
- ✅ **Scalable structure** → Organized foundation that grows with your project

## 🎯 Perfect For

- **Rapid Prototyping** - Get from idea to working prototype faster
- **Client Projects** - Professional setup with consistent workflows
- **Team Development** - Standardized processes and structure
- **Learning Projects** - Best practices built-in from day one
- **Production Applications** - Scalable foundation with proper tooling

## 🤝 Contributing

This template evolves with development best practices. Contributions welcome!

1. Fork the template repository
2. Make improvements to automation commands or project structure
3. Test with real projects
4. Submit pull requests with clear descriptions

## 📄 License

MIT License - Use this template for any project, commercial or personal.

## 🔗 Links

- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)
- [Model Context Protocol](https://modelcontextprotocol.io/)
- [GitHub CLI](https://cli.github.com/)
- [Template Repository](https://github.com/kylesaldana5/claudecode-bootstrap)

---

**Ready to accelerate your development?** Click "Use this template" and run `./kickstart "Your Project Name"` to get started!