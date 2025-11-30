# Copilot Architecture Builder

**Automatically generate high-quality GitHub Copilot agents, instructions, and prompts**

A research-driven agent generator inspired by [Burke Holland's Beast Mode](https://gist.github.com/burkeholland/88af0249c4b6aff3820bf37898c8bacf) that creates production-ready Three-Layer Architecture components for VS Code.

## 🚀 Quick Install

### Option 1: Clone to Workspace (Recommended)

Clone directly into your project to use immediately:

```bash
cd your-project
git clone https://github.com/Stephensmetana/copilot-agent-builder .github
```

This installs all agents and configurations into `.github/` where VS Code expects them.

### Option 2: Clone and Copy

```bash
git clone https://github.com/Stephensmetana/copilot-agent-builder
cp -r copilot-agent-builder/.github your-project/.github
```

### After Installation

1. Reload VS Code: `Ctrl+Shift+P` → "Developer: Reload Window"
2. Open Chat panel
3. Select `architecture-builder` from agent dropdown
4. Start generating: "Create a Python testing agent"

## ✨ What You Get

- **Architecture Builder Agent** - Generates custom agents on demand
- **Quality Standards** - Best practices and naming conventions
- **Example Agents** - Pre-built planner agent
- **Quick Commands** - `/generate-agent` for fast generation
- **Complete Documentation** - Guides, references, and examples

## 📖 Usage

### Generate an Agent

```
# Method 1: Direct chat
Select "architecture-builder" → "Create a React developer agent"

# Method 2: Quick command
/generate-agent specialization=data-science format=agent includePrompts=yes
```

### What Gets Generated

```
.github/
  agents/
    your-agent.agent.md
  instructions/
    your-domain.instructions.md
  prompts/
    your-task.prompt.md
```

## 📚 Documentation

- **[Quick Reference](.github/QUICK_REFERENCE.md)** - Fast lookup (5 min read)
- **[Complete Guide](.github/README.md)** - Full documentation (20 min read)
- **[System Overview](.github/OVERVIEW.md)** - How it works (10 min read)
- **[Visual Diagrams](.github/DIAGRAMS.md)** - Architecture diagrams (8 min read)
- **[Three-Layer Guide](docs/GitHub_Copilot_Three_Layer_Architecture_Guide.md)** - Deep dive into architecture

Start here: [.github/INDEX.md](.github/INDEX.md)

## 🎯 Examples

### Code Review Agent
```
Create a code review agent that can check out repositories and review code quality
```
→ Generates read-only agent with githubRepo access and review checklist

### Multi-Agent Workflow
```
Create a planner → implementer → tester workflow
```
→ Generates 3 agents with handoffs for sequential development

### Domain-Specific
```
Create a FastAPI backend agent with SQLAlchemy and Pydantic
```
→ Researches FastAPI best practices and generates specialized agent

## 🔧 Requirements

- VS Code with GitHub Copilot extension
- Compatible with Claude Sonnet 4, GPT-4.1, GPT-5
- Internet access for research phase

## 🌟 Features

- ✅ **Research-Driven** - Fetches current best practices (2025)
- ✅ **Beast Mode Inspired** - Autonomous execution patterns
- ✅ **Quality-First** - Built-in standards and validation
- ✅ **Production-Ready** - No editing required
- ✅ **Extensible** - Easy to customize

## 📦 What's Included

| Component | Description | Lines |
|-----------|-------------|-------|
| **architecture-builder.agent.md** | Main generator agent | 450+ |
| **architecture-components.instructions.md** | Quality standards | 350+ |
| **generate-agent.prompt.md** | Quick command | 70+ |
| **planner.agent.md** | Example agent | 500+ |
| **Documentation** | Guides and references | 2700+ |

## 🛠️ Customization

Edit `.github/agents/architecture-builder.agent.md` to:
- Change research strategy
- Modify generation templates
- Add your own conventions
- Include company standards

See [.github/README.md](.github/README.md#customization) for details.

## 💡 Use Cases

Perfect for:
- Creating specialized development agents
- Setting up project Copilot customizations
- Building multi-agent workflows
- Standardizing team conventions
- Teaching Three-Layer Architecture

## 📖 Learn More

- [VS Code Copilot Customization](https://code.visualstudio.com/docs/copilot/customization/overview)
- [Custom Agents Guide](https://code.visualstudio.com/docs/copilot/customization/custom-agents)
- [Beast Mode Gist](https://gist.github.com/burkeholland/88af0249c4b6aff3820bf37898c8bacf)

## 🤝 Contributing

This is a starting point - customize for your needs:
- Add your own templates
- Include domain-specific patterns
- Share improvements via issues/PRs

## 📄 License

MIT License - See [LICENSE](LICENSE) for details

Inspired by [Burke Holland's Beast Mode](https://gist.github.com/burkeholland/88af0249c4b6aff3820bf37898c8bacf) and the VS Code Copilot community.

## 🙏 Credits

- [Burke Holland](https://github.com/burkeholland) - Beast Mode inspiration
- VS Code Copilot Team - Three-Layer Architecture
- GitHub Copilot Community - Best practices and patterns

---

**Quick Start**: `git clone` into your project's `.github/` folder → Reload VS Code → Select `architecture-builder` → Start generating!
