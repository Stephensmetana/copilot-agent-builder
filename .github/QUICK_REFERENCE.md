# Quick Reference: Architecture Builder

## 🚀 Quick Install

### Clone to Your Project
```bash
cd your-project
git clone https://github.com/Stephensmetana/copilot-agent-builder .github
```

Then reload VS Code: `Ctrl+Shift+P` → "Developer: Reload Window"

### Verify Installation
1. Open Chat panel
2. Check agent dropdown for `architecture-builder`
3. Try: "Create a Python testing agent"

## Usage

### Method 1: Direct Agent Chat
1. Select `architecture-builder` from agent dropdown
2. Describe what you need: "Create a [specialization] agent"
3. Agent researches and generates all files

### Method 2: Prompt Command
```
/generate-agent specialization=<name> format=<agent|chatmode> includePrompts=<yes|no>
```

## Common Commands

### Create Basic Agent
```
Create a Python testing agent
```

### Create Agent with Specific Tools
```
Create a code reviewer that only reads code (no modifications)
```

### Create Multi-Agent Workflow
```
Create a planner agent that hands off to an implementer and then to a tester
```

### Create Domain-Specific Agent
```
Create a React component generator with TypeScript, Mantine UI, and zod validation
```

## Generated Files

### Agent File (`.agent.md`)
- Purpose and role description
- Core directives (persistence, autonomy, verification)
- Step-by-step workflow
- Tool usage guidelines
- Communication style
- Concrete examples

### Instructions File (`.instructions.md`)
- Domain-specific guidelines
- Code standards
- Best practices from research
- Good/bad examples
- `applyTo` glob patterns

### Prompt File (`.prompt.md`)
- Task description
- Input variables
- Requirements
- Expected output
- References to instructions

## Folder Structure

```
.github/
├── agents/
│   ├── architecture-builder.agent.md    # Generator
│   └── <your-agent>.agent.md            # Your agents
├── instructions/
│   ├── architecture-components.instructions.md
│   └── <your-domain>.instructions.md
├── prompts/
│   ├── generate-agent.prompt.md
│   └── <your-task>.prompt.md
└── copilot-instructions.md
```

## Tool Selection by Role

### Planner/Researcher (Read-Only)
```yaml
tools: ['search', 'fetch', 'githubRepo', 'usages']
```

### Implementer
```yaml
tools: ['new', 'edit', 'search', 'runCommands']
```

### Tester
```yaml
tools: ['runCommands', 'runTasks', 'search', 'edit']
```

### Reviewer
```yaml
tools: ['search', 'fetch']
```

## Naming Conventions

| Type | Pattern | Example |
|------|---------|---------|
| Agent | `<role>.agent.md` | `data-scientist.agent.md` |
| Instructions | `<domain>.instructions.md` | `python-data-science.instructions.md` |
| Prompt | `<verb-noun>.prompt.md` | `create-component.prompt.md` |

## Quick Tips

✅ **Do:**
- Be specific about specialization
- Mention tech stack details
- Request read-only for reviewers
- Ask for multi-agent workflows

❌ **Avoid:**
- Vague requests ("make an agent")
- Overly generic agents
- Giving all tools to all agents

## Examples

### Data Science
```
Create a data science agent for Python with pandas, numpy, and Jupyter notebook support
```

### Security
```
Create a security review agent that analyzes code for OWASP vulnerabilities
```

### Frontend
```
Create a React developer agent using shadcn/ui components with TypeScript
```

### DevOps
```
Create a CI/CD agent that works with GitHub Actions and Docker
```

## Handoff Patterns

### Plan → Implement → Test
```yaml
# In planner.agent.md
handoffs:
  - label: "Implement Plan"
    agent: "implementer"
    prompt: "Implement the plan outlined above."
    send: false

# In implementer.agent.md
handoffs:
  - label: "Run Tests"
    agent: "tester"
    prompt: "Test the implementation."
    send: true
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Agent not in dropdown | Reload window (`Ctrl+Shift+P` → Reload Window) |
| YAML errors | Check frontmatter formatting |
| Path errors | Verify relative paths are correct |
| Tools not working | Check VS Code Copilot tool names |

## References

- [Full README](./.github/README.md)
- [Architecture Guide](../GitHub_Copilot_Three_Layer_Architecture_Guide.md)
- [Beast Mode](https://gist.github.com/burkeholland/88af0249c4b6aff3820bf37898c8bacf)
