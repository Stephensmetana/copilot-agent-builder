# Architecture Builder - Documentation Index

## Quick Access

| What You Want | Where to Look |
|---------------|---------------|
| **Get started fast** | [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) |
| **Understand the system** | [OVERVIEW.md](./OVERVIEW.md) |
| **Full documentation** | [README.md](./README.md) |
| **Visual diagrams** | [DIAGRAMS.md](./DIAGRAMS.md) |
| **See examples** | [planner.agent.md](./agents/planner.agent.md) |

## File Structure

```
.github/
├── INDEX.md                                  ← You are here
├── README.md                                 ← Full documentation
├── OVERVIEW.md                               ← System summary
├── QUICK_REFERENCE.md                        ← Fast lookup
├── DIAGRAMS.md                               ← Visual guides
├── copilot-instructions.md                   ← Project guidelines
│
├── agents/
│   ├── architecture-builder.agent.md         ← Main generator
│   └── planner.agent.md                      ← Example agent
│
├── instructions/
│   └── architecture-components.instructions.md  ← Standards
│
└── prompts/
    └── generate-agent.prompt.md              ← Quick command
```

## Documentation by Purpose

### 🚀 Getting Started
1. Read [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) (5 min)
2. Try: Open Chat → Select `architecture-builder` → Say "Create a Python testing agent"
3. Review generated files
4. Read [README.md](./README.md) for details

### 📚 Understanding the System
- **High-level overview**: [OVERVIEW.md](./OVERVIEW.md)
- **How it works**: [DIAGRAMS.md](./DIAGRAMS.md)
- **Example agent**: [planner.agent.md](./agents/planner.agent.md)

### 🔧 Using the System
- **Quick commands**: [QUICK_REFERENCE.md](./QUICK_REFERENCE.md)
- **Full usage guide**: [README.md](./README.md)
- **Prompt interface**: [generate-agent.prompt.md](./prompts/generate-agent.prompt.md)

### 📖 Reference Material
- **Quality standards**: [architecture-components.instructions.md](./instructions/architecture-components.instructions.md)
- **Project guidelines**: [copilot-instructions.md](./copilot-instructions.md)
- **Three-Layer Architecture**: [../GitHub_Copilot_Three_Layer_Architecture_Guide.md](../GitHub_Copilot_Three_Layer_Architecture_Guide.md)

### 🛠️ Customization
- **Modify generator**: Edit [architecture-builder.agent.md](./agents/architecture-builder.agent.md)
- **Change standards**: Edit [architecture-components.instructions.md](./instructions/architecture-components.instructions.md)
- **Add templates**: Create new files in respective folders

## Common Tasks

### Create Your First Agent
```
1. Open VS Code Chat
2. Select "architecture-builder"
3. Say: "Create a [specialization] agent"
```
→ See [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) for more commands

### Use the Quick Command
```
/generate-agent specialization=data-science format=agent includePrompts=yes
```
→ See [generate-agent.prompt.md](./prompts/generate-agent.prompt.md) for parameters

### Understand How It Works
1. Read [OVERVIEW.md](./OVERVIEW.md)
2. Review [DIAGRAMS.md](./DIAGRAMS.md)
3. Examine [planner.agent.md](./agents/planner.agent.md)

### Learn Best Practices
- [architecture-components.instructions.md](./instructions/architecture-components.instructions.md) - Quality standards
- [README.md](./README.md) - Best practices section
- [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) - Quick tips

### Troubleshoot Issues
- [README.md](./README.md) - Troubleshooting section
- [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) - Common issues table

## By Role

### I'm a Developer
- Start: [QUICK_REFERENCE.md](./QUICK_REFERENCE.md)
- Examples: [README.md](./README.md) - Examples section
- Reference: [architecture-components.instructions.md](./instructions/architecture-components.instructions.md)

### I'm a Team Lead
- Overview: [OVERVIEW.md](./OVERVIEW.md)
- Standards: [architecture-components.instructions.md](./instructions/architecture-components.instructions.md)
- Customization: [README.md](./README.md) - Customization section

### I'm Learning
- Start: [QUICK_REFERENCE.md](./QUICK_REFERENCE.md)
- Theory: [OVERVIEW.md](./OVERVIEW.md)
- Visuals: [DIAGRAMS.md](./DIAGRAMS.md)
- Details: [README.md](./README.md)

## Document Sizes

| Document | Length | Read Time |
|----------|--------|-----------|
| INDEX.md | 1 page | 2 min |
| QUICK_REFERENCE.md | 3 pages | 5 min |
| OVERVIEW.md | 5 pages | 10 min |
| DIAGRAMS.md | 4 pages | 8 min |
| README.md | 12 pages | 20 min |

## Key Concepts

### Three-Layer Architecture
Agents → Prompts → Instructions

Learn more: [../GitHub_Copilot_Three_Layer_Architecture_Guide.md](../GitHub_Copilot_Three_Layer_Architecture_Guide.md)

### Beast Mode Patterns
Autonomous execution, research-driven, workflow-structured

Reference: [Beast Mode Gist](https://gist.github.com/burkeholland/88af0249c4b6aff3820bf37898c8bacf)

### Tool Selection
Read-only (planner) vs. Write (implementer) vs. Test (tester)

See: [DIAGRAMS.md](./DIAGRAMS.md) - Tool Selection Matrix

### Quality Standards
Naming, structure, tools, examples, constraints

Details: [architecture-components.instructions.md](./instructions/architecture-components.instructions.md)

## External Resources

### Official Documentation
- [VS Code Copilot Customization](https://code.visualstudio.com/docs/copilot/customization/overview)
- [Custom Agents Guide](https://code.visualstudio.com/docs/copilot/customization/custom-agents)
- [Custom Instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions)
- [Prompt Files](https://code.visualstudio.com/docs/copilot/customization/prompt-files)

### Community Resources
- [Beast Mode Gist](https://gist.github.com/burkeholland/88af0249c4b6aff3820bf37898c8bacf)
- [Awesome Copilot](https://github.com/github/awesome-copilot)

## Version Information

- **Created**: November 2025
- **Version**: 1.0
- **Compatibility**: VS Code with GitHub Copilot
- **Models**: Claude Sonnet 4, GPT-4.1, GPT-5

## Need Help?

### Quick Questions
→ [QUICK_REFERENCE.md](./QUICK_REFERENCE.md)

### Understanding Concepts
→ [OVERVIEW.md](./OVERVIEW.md) and [DIAGRAMS.md](./DIAGRAMS.md)

### Detailed Usage
→ [README.md](./README.md)

### Quality Standards
→ [architecture-components.instructions.md](./instructions/architecture-components.instructions.md)

### Examples
→ [README.md](./README.md) Examples section
→ [planner.agent.md](./agents/planner.agent.md)

---

**Start here**: [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) → Try it → Read [README.md](./README.md) for details
