# ClaudeCode Bootstrap

A GitHub template repository for rapidly bootstrapping new development projects with Claude Code || Curosr integration, automated workflows, and comprehensive development tooling.

## 🚀 Quick Start

### 1. Use This Template
Click the **"Use this template"** button above to create a new repository from this template.

### 2. Clone and Initialize
```bash
git clone https://github.com/yourusername/your-new-project.git
cd your-new-project
run claude then  /init 
```

### 3. Generate Your Documentation
This repository includes comprehensive example documents that you can use as templates:

- **`docs/PRD.md`** - Complete Product Requirements Document (using a to-do app example)
- **`docs/TechnicalArchitecture.md`** - Detailed Technical Architecture Document (using a to-do app example)

**Need help generating in-depth PRDs and technical architecture?** Use this repository as a reference! The included documents demonstrate best practices for:
- Requirements gathering and specification
- Technical system design and architecture
- Component breakdown and data flow
- Security and performance considerations
- Development workflow planning

#### 💡 My Personal Workflow for Document Generation
For generating comprehensive PRDs and technical documentation, I personally use the [BMAD Method](https://github.com/bmadcode/BMAD-METHOD). This systematic approach helps create thorough, professional documentation through AI-assisted development workflows.

**Quick setup:**
The BMAD Method provides specialized agents (`/pm`, `/architect`, `/analyst`) that work together to create detailed project documentation, which I then use as the foundation for projects in this template.

Simply copy the structure from the example documents and adapt the content for your specific project needs.

### 4. Start Development
```bash
# Create GitHub issues from your PRD
/bootstrap

# Implement features systematically
/work

# Review pull requests thoroughly
/review
```

### 4. Cursor IDE Setup & Fast GitHub Issue Access

Follow these steps to configure Cursor and make GitHub issues instantly accessible:

1. **Open this repository in Cursor**  
   (If Cursor isn't installed yet, download it from https://cursor.sh or use your preferred installation method.)  

2. **Generate your GitHub issues**  
   Use the `/bootstrap` command via Claude Code to turn your PRD into issues:

   ```bash
   /bootstrap
   ```

3. **Teach Cursor to remember the quick-view command**  
   After the issues are created, tell the Cursor assistant:

   ```
   When I say "Get GitHub issue <number>", run:
   bash -lc 'GH_PAGER= gh issue view <number>'
   ```

   Cursor will store this as a memory so you can simply type, for example, `Get GitHub issue 42` and see the issue immediately inside the IDE.

4. **Verify**  
   Ask Cursor: `Get GitHub issue 1` — it should display the issue details without any extra flags.

This setup lets you stay inside Cursor while inspecting and working on issues, streamlining your workflow.

## 📋 What's Included

### 🤖 Claude Code Integration
- **CLAUDE.md** - Project context and development guidelines
- **Automation Commands** - Pre-built workflows for common development tasks
- **MCP Configurations** - Enhanced AI capabilities with Context7 documentation

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
└── README.md              # This file (will be updated for your project)
```

## 🔧 Detailed Setup

### Prerequisites
- [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code) installed
- [GitHub CLI](https://cli.github.com/) (optional, for enhanced GitHub integration)
- Git configured with your credentials


### MCP Integration Setup
The template includes two MCP servers for enhanced development capabilities:

**Context7 Documentation** (auto-configured)
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
- `/bootstrap` - Generate GitHub issues from PRD
- `/work` - Implement features systematically
- `/review` - Review pull requests
- `/issues` - Create individual issues

### File Structure Commands
After running project setup:
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


## 🎯 Perfect For

- **Rapid Prototyping** - Get from idea to working prototype faster
- **Client Projects** - Professional setup with consistent workflows
- **Team Development** - Standardized processes and structure
- **Learning Projects** - Best practices built-in from day one
- **Production Applications** - Scalable foundation with proper tooling
- **Documentation Templates** - Use example PRDs and architecture docs as starting points for any project

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
