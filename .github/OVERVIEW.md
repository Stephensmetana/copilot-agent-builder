# Architecture Builder System - Complete Overview

## What Was Created

A comprehensive system for generating GitHub Copilot Three-Layer Architecture components, inspired by Burke Holland's Beast Mode.

## Files Created

### Core Agent System
1. **`architecture-builder.agent.md`** - Main generator agent
   - Researches best practices before generating
   - Creates proper folder structures
   - Generates agents, instructions, and prompts
   - Follows Beast Mode patterns

2. **`architecture-components.instructions.md`** - Quality standards
   - Naming conventions
   - File structure guidelines
   - Best practices and anti-patterns
   - Quality checklist

3. **`generate-agent.prompt.md`** - Quick command interface
   - Usage: `/generate-agent specialization=name`
   - Parameters for format and prompts
   - References standards automatically

4. **`copilot-instructions.md`** - Project-wide guidelines
   - General conventions
   - File naming patterns
   - Quality standards
   - Reference links

### Documentation
5. **`README.md`** - Complete usage guide
   - Quick start instructions
   - Detailed examples
   - Troubleshooting guide
   - Best practices

6. **`QUICK_REFERENCE.md`** - Fast lookup guide
   - Common commands
   - Tool selection patterns
   - Naming conventions
   - Quick tips

### Example Agent
7. **`planner.agent.md`** - Sample generated agent
   - Demonstrates proper structure
   - Shows Beast Mode influence
   - Includes handoffs and examples
   - Full workflow documentation

## How to Use

### Quick Start
1. Open VS Code Chat
2. Select `architecture-builder` from dropdown
3. Say: "Create a [specialization] agent"
4. Review generated files in `.github/` folder

### Using the Prompt
```bash
/generate-agent specialization=python-tester format=agent includePrompts=yes
```

## Key Features

### 1. Research-Driven Generation
- Uses `fetch_webpage` to research current best practices
- Searches documentation and community examples
- Ensures generated content is current and accurate

### 2. Proper Structure
- Creates correct folder hierarchy
- Follows VS Code conventions
- Uses kebab-case naming
- Includes proper YAML frontmatter

### 3. Beast Mode Patterns
- Autonomous execution approach
- Clear workflow structures
- Tool usage guidelines
- Communication standards
- Todo list management

### 4. Quality Assurance
- Built-in quality checklist
- Appropriate tool selection
- Concrete examples
- Clear constraints

### 5. Multi-Agent Workflows
- Handoff support
- Complementary agents (planner → implementer → tester)
- Pre-filled prompts

## Generated Component Types

### Agents (.agent.md)
- Purpose and role description
- Core directives
- Step-by-step workflows
- Tool usage guidelines
- Communication style
- Examples

### Instructions (.instructions.md)
- Domain-specific guidelines
- Code standards
- Best practices
- `applyTo` glob patterns
- Examples

### Prompts (.prompt.md)
- Task templates
- Input variables
- Requirements
- Output format
- References

## Example Workflows

### 1. Create Python Data Science Agent
**Input**: "Create a Python data science agent with Jupyter support"

**Generated**:
- `data-scientist.agent.md` with tools: search, fetch, runNotebooks, edit, new
- `python-data-science.instructions.md` with pandas/numpy guidelines
- `analyze-dataset.prompt.md` for common analysis tasks

### 2. Create Security Reviewer
**Input**: "Create a security review agent (read-only)"

**Generated**:
- `security-reviewer.agent.md` with tools: search, fetch only
- `security-review.instructions.md` with OWASP guidelines
- `review-security.prompt.md` for vulnerability checks

### 3. Create Multi-Agent Workflow
**Input**: "Create planner → implementer → tester workflow"

**Generated**:
- `planner.agent.md` (read-only tools, hands off to implementer)
- `implementer.agent.md` (write tools, hands off to tester)
- `tester.agent.md` (testing tools)
- Supporting instructions and prompts

## Tool Selection Patterns

| Role | Tools | Purpose |
|------|-------|---------|
| Planner | search, fetch, githubRepo, usages | Research and analysis |
| Implementer | new, edit, search, runCommands | Code creation |
| Tester | runCommands, runTasks, search | Testing |
| Reviewer | search, fetch | Analysis only |

## Naming Conventions

```
Agents:        <role>.agent.md              (data-scientist.agent.md)
Instructions:  <domain>.instructions.md     (python-data-science.instructions.md)
Prompts:       <verb-noun>.prompt.md        (create-component.prompt.md)
```

## Quality Standards

Every generated component:
- ✅ Follows VS Code conventions
- ✅ Uses kebab-case naming
- ✅ Includes YAML frontmatter
- ✅ Has clear purpose and constraints
- ✅ Contains concrete examples
- ✅ Uses appropriate tools
- ✅ Is production-ready

## Compatibility

### Format Support
- **`.agent.md`**: New format (preferred)
- **`.chatmode.md`**: Legacy format (still supported)
- Functionality identical, only naming differs

### VS Code Version
- Requires VS Code with GitHub Copilot
- Tested with Copilot Chat (2025)
- Compatible with Claude Sonnet 4, GPT-4.1, GPT-5

## Extending the System

### Add Your Own Templates
1. Create template files in `.github/templates/`
2. Modify `architecture-builder.agent.md` to use templates
3. Customize for your tech stack

### Create Domain-Specific Generators
Ask the Architecture Builder to create specialized generators:
```
Create a FastAPI backend generator that creates agents specialized in SQLAlchemy and Pydantic
```

### Add Company Standards
Edit `architecture-components.instructions.md` to include:
- Company coding standards
- Required tools and frameworks
- Security requirements
- Compliance guidelines

## Best Practices

### ✅ Do
- Be specific about specialization
- Mention tech stack and tools
- Request read-only for reviewers
- Create multi-agent workflows
- Review and customize generated files

### ❌ Avoid
- Vague requests ("make an agent")
- Overly generic agents
- Giving all tools to all agents
- Skipping the research phase
- Using for trivial tasks

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Agent not visible | Reload VS Code window |
| YAML errors | Check frontmatter syntax |
| Path errors | Verify relative paths |
| Tools not working | Check VS Code tool names |
| No research happening | Verify fetch tool access |

## References

### Documentation
- [VS Code Copilot Customization](https://code.visualstudio.com/docs/copilot/customization/overview)
- [Custom Agents Guide](https://code.visualstudio.com/docs/copilot/customization/custom-agents)
- [Three-Layer Architecture Guide](../GitHub_Copilot_Three_Layer_Architecture_Guide.md)

### Inspiration
- [Beast Mode Gist](https://gist.github.com/burkeholland/88af0249c4b6aff3820bf37898c8bacf)
- [Awesome Copilot](https://github.com/github/awesome-copilot)

## Project Structure

```
.github/
├── agents/
│   ├── architecture-builder.agent.md    # Main generator
│   ├── planner.agent.md                 # Example agent
│   └── (your generated agents)
├── instructions/
│   ├── architecture-components.instructions.md  # Standards
│   └── (your generated instructions)
├── prompts/
│   ├── generate-agent.prompt.md         # Quick command
│   └── (your generated prompts)
├── copilot-instructions.md              # Project guidelines
├── README.md                            # Full documentation
└── QUICK_REFERENCE.md                   # Fast lookup
```

## Summary

This system provides everything needed to create high-quality, production-ready GitHub Copilot customizations:

1. **Research-driven**: Generates content based on current best practices
2. **Structure-focused**: Creates proper folder hierarchy and naming
3. **Beast Mode inspired**: Follows proven autonomous execution patterns
4. **Quality-assured**: Built-in standards and checklists
5. **Flexible**: Supports any domain, language, or framework
6. **Extensible**: Easy to customize and expand

Start by using the Architecture Builder agent to generate your first specialized agent, then iterate and customize as needed.

---

**Created**: November 2025  
**Version**: 1.0  
**Compatibility**: VS Code with GitHub Copilot (Claude Sonnet 4, GPT-4.1, GPT-5)
