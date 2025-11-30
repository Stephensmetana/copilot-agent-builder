---
description: "Guidelines for creating Copilot Three-Layer Architecture components"
name: "architecture-components-standards"
applyTo: ".github/**/*.{agent.md,chatmode.md,instructions.md,prompt.md}"
---

# Copilot Architecture Component Standards

When creating or editing agents, instructions, or prompts, follow these standards to ensure quality and consistency.

## File Structure Standards

### Folder Organization
```
.github/
  agents/                          # All custom agents
    *.agent.md                     # New format (preferred)
    *.chatmode.md                  # Legacy format (still supported)
  instructions/                    # Instruction files
    *.instructions.md              # Conditional instructions
  prompts/                         # Prompt files
    *.prompt.md                    # Reusable prompts
  copilot-instructions.md          # Project-wide instructions
```

## Naming Conventions

### File Names
- **Use kebab-case**: `data-scientist.agent.md`, not `DataScientist.agent.md`
- **Be descriptive**: `python-data-science.instructions.md`, not `python.instructions.md`
- **Use verbs for prompts**: `create-component.prompt.md`, not `component.prompt.md`

### Agent Names (in frontmatter)
- Use Title Case: `"Data Scientist"`, `"React Developer"`
- Keep it concise: 1-3 words maximum
- Make it role-based: Focus on what the agent does

### Command Names (for prompts)
- Use kebab-case: `create-react-form`, `review-security`
- Be action-oriented: Start with a verb
- Be specific: `create-mantine-form` better than `create-form`

## YAML Frontmatter Standards

### Agent Frontmatter
```yaml
---
description: "Single sentence describing purpose"
name: "Agent Name"
argument-hint: "Brief guide for user input"
tools: ['tool1', 'tool2', 'tool3']
model: "Claude Sonnet 4"
temperature: 0.3
handoffs:
  - label: "Next Step"
    agent: "target-agent"
    prompt: "Pre-filled prompt text"
    send: false
---
```

**Required Fields:**
- `description`: Short, actionable description (appears as placeholder)
- `name`: Agent name in dropdown

**Optional but Recommended:**
- `tools`: List of allowed tools (restricts capabilities)
- `model`: Preferred AI model
- `temperature`: 0.1-0.3 for code, 0.5-0.7 for general, 0.8-1.0 for creative
- `handoffs`: Enable multi-agent workflows

### Instruction Frontmatter
```yaml
---
description: "Brief description"
name: "Display name"
applyTo: "**/*.py"
---
```

**ApplyTo Patterns:**
- Python files: `"**/*.py"`
- React components: `"src/components/**/*.tsx"`
- All TypeScript: `"**/*.{ts,tsx}"`
- Specific folder: `"src/backend/**/*"`

### Prompt Frontmatter
```yaml
---
description: "Task description"
name: "command-name"
argument-hint: "param=value"
agent: "agent-name"
tools: ['search', 'edit', 'new']
---
```

## Content Structure Standards

### Agent Body Structure

Follow this proven structure from Beast Mode:

```markdown
# Agent Name

<Purpose paragraph>

## Core Directives
<Key behaviors and constraints>

## Workflow
<Step-by-step process>

## Output Format
<How to format responses>

## Communication Style
<Tone and verbosity>

## Tool Usage Guidelines
<When and how to use each tool>

## Examples
<Concrete examples>
```

### Instruction Body Structure
```markdown
# Instruction Set Title

<Overview>

## Category 1
- Guideline 1
- Guideline 2

## Category 2
- Guideline 1
- Guideline 2

## Examples
<Good and bad examples>
```

### Prompt Body Structure
```markdown
# Prompt Title

<What this does>

## Task
<Detailed task description>

## Requirements
<List requirements>

## Input
<Variables and parameters>

## Output
<Expected result format>

## References
<Links to instructions>
```

## Tool Selection Guidelines

### Read-Only Agents (Planners, Reviewers, Researchers)
```yaml
tools: ['search', 'fetch', 'githubRepo', 'usages']
```

### Implementation Agents
```yaml
tools: ['new', 'edit', 'search', 'runCommands']
```

### Testing Agents
```yaml
tools: ['runCommands', 'runTasks', 'edit', 'search']
```

### Restricted Agents (Safety)
```yaml
tools: ['search']  # Read-only, no modifications
```

## Best Practices

### Agent Design
- **Single Responsibility**: Each agent has ONE clear purpose
- **Appropriate Tools**: Only include tools needed for the role
- **Clear Constraints**: Explicitly state what the agent can/cannot do
- **Handoffs**: Use handoffs for multi-step workflows
- **Examples**: Include concrete usage examples

### Instruction Design
- **Specific Patterns**: Use `applyTo` to target specific files
- **Actionable Guidelines**: Each guideline should be clear and testable
- **No Duplication**: Don't repeat what's in copilot-instructions.md
- **Examples**: Show good vs. bad code examples

### Prompt Design
- **Variables**: Use `${input:name:placeholder}` for user input
- **References**: Link to instructions for consistency
- **Agent Selection**: Specify which agent should handle the prompt
- **Clear Task**: Make the task unambiguous

## Quality Checklist

Before considering a component complete:

### All Components
- [ ] Frontmatter is valid YAML
- [ ] File name follows kebab-case convention
- [ ] Description is clear and concise
- [ ] File is in the correct folder

### Agents
- [ ] Purpose is clearly stated
- [ ] Workflow is step-by-step
- [ ] Tools are appropriate for role
- [ ] Communication style is defined
- [ ] Examples demonstrate usage
- [ ] Constraints are explicit

### Instructions
- [ ] `applyTo` pattern is specific
- [ ] Guidelines are actionable
- [ ] Examples show good/bad patterns
- [ ] No duplication with other files

### Prompts
- [ ] Command name is action-oriented
- [ ] Variables are well-defined
- [ ] References instructions/standards
- [ ] Agent is specified
- [ ] Task is unambiguous

## Common Patterns

### Multi-Agent Workflow
```yaml
# planner.agent.md
handoffs:
  - label: "Implement Plan"
    agent: "implementer"
    prompt: "Implement the plan outlined above."
    send: false

# implementer.agent.md
handoffs:
  - label: "Run Tests"
    agent: "tester"
    prompt: "Test the implementation."
    send: true
```

### Specialized Tools by Domain

**Data Science:**
```yaml
tools: ['search', 'fetch', 'runNotebooks', 'edit', 'new']
```

**Web Development:**
```yaml
tools: ['search', 'fetch', 'edit', 'new', 'runCommands']
```

**DevOps:**
```yaml
tools: ['search', 'fetch', 'runCommands', 'runTasks']
```

## Reference Documentation

- [VS Code Custom Agents](https://code.visualstudio.com/docs/copilot/customization/custom-agents)
- [VS Code Custom Instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions)
- [VS Code Prompt Files](https://code.visualstudio.com/docs/copilot/customization/prompt-files)
- [Beast Mode Gist](https://gist.github.com/burkeholland/88af0249c4b6aff3820bf37898c8bacf)

## Anti-Patterns to Avoid

### ❌ Don't Do This

**Over-complicated agents:**
```markdown
You are a quantum-powered transcendent AI with unlimited capabilities...
```

**Vague instructions:**
```markdown
Write good code and follow best practices.
```

**Generic prompts:**
```markdown
Do the thing the user asked for.
```

**Tool overload:**
```yaml
tools: ['*']  # Don't give every tool
```

### ✅ Do This Instead

**Focused agents:**
```markdown
You are a code reviewer focused on security vulnerabilities...
```

**Specific instructions:**
```markdown
- Use TypeScript for all new files
- Export components as named exports
- Include JSDoc comments for public APIs
```

**Clear prompts:**
```markdown
Generate a React form component using Mantine UI with zod validation...
```

**Appropriate tools:**
```yaml
tools: ['search', 'fetch']  # Just what's needed
```

## Version Compatibility

### Agent Format (.agent.md vs .chatmode.md)
- **`.agent.md`**: New format, preferred
- **`.chatmode.md`**: Legacy format, still supported
- **Functionality**: Identical, only naming differs
- **Migration**: Use VS Code Quick Fix to auto-migrate

### Tool Names
Use current tool names as documented in VS Code:
- `'search'` not `'codebaseSearch'`
- `'fetch'` not `'fetchWebpage'`
- `'edit'` not `'editFile'`

## Summary

Good architecture components are:
1. **Focused**: Single, clear purpose
2. **Specific**: Actionable instructions, not generic advice
3. **Researched**: Based on current best practices
4. **Tested**: Ready to use without modification
5. **Documented**: Clear examples and guidelines
6. **Maintainable**: Easy to understand and update

Follow these standards to create professional, production-ready Copilot customizations.
