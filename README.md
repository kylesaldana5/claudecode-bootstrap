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
/bootstrap

# Implement features systematically
/work

# Review pull requests thoroughly
/review
```

## 📋 What's Included

### 🤖 Claude Code Integration
- **CLAUDE.md** - Project context and development guidelines
- **Automation Commands** - Pre-built workflows for common development tasks
- **MCP Configurations** - Enhanced AI capabilities with Serena IDE assistant and Context7 documentation

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
The template includes two MCP servers for enhanced development capabilities:

1. **Serena IDE Assistant** (auto-configured)
   - Intelligent code completion and analysis
   - Project-aware development assistance
   - Requires `uvx` package manager (install with `curl -LsSf https://astral.sh/uv/install.sh | sh`)
   - No additional API keys required

2. **Context7 Documentation** (auto-configured)
   - Access to comprehensive library documentation
   - Smart library ID resolution
   - Requires Node.js ≥ v18.0.0
   - No additional API keys required

## 🎯 Development Workflow

### 1. Planning Phase
- Create comprehensive PRD with epics and requirements
- Design technical architecture with component breakdown
- Place both documents in `docs/` directory

### 2. Issue Generation
```bash
/bootstrap
```
- Automatically converts PRD into structured GitHub issues
- Maps requirements to implementation tasks
- Creates proper issue labels and milestones

### 3. Feature Implementation
```bash
/work
```
- Systematic issue implementation
- Automated Git workflow (branch → commit → PR)
- Consistent code quality and documentation

### 4. Code Review
```bash
/review
```
- Comprehensive PR analysis
- Security and performance review
- Automated feedback and suggestions

### 5. Iteration
Repeat the work/review cycle for continuous development.

## 📖 Command Reference

### Core Commands
- `./kickstart "Project Name"` - Initialize new project from template
- `/bootstrap` - Generate GitHub issues from PRD
- `/work` - Implement features systematically
- `/review` - Review pull requests
- `/issues` - Create individual issues

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
Edit `.mcp.json` to add or modify MCP servers. Current configuration includes:
```json
{
  "mcpServers": {
    "serena": {
      "command": "uvx",
      "args": ["--from", "git+https://github.com/oraios/serena", "serena-mcp-server", "--context", "ide-assistant", "--project", "{{PROJECT_SLUG}}"]
    },
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp@latest"]
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