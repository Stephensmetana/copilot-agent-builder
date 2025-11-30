---
description: "Create a new custom agent with instructions and prompts"
name: "generate-agent"
argument-hint: "specialization=data-science format=agent"
agent: "architecture-builder"
tools: ['fetch', 'new', 'edit', 'search']
---

# Generate Custom Agent

Create a complete custom agent with supporting instructions and prompt files.

## Task

Generate a full Three-Layer Architecture component set for the specified specialization.

## Parameters

- **Specialization**: ${input:specialization:data-science}
- **Format**: ${input:format:agent} (options: `agent` or `chatmode`)
- **Include Prompts**: ${input:includePrompts:yes} (options: `yes` or `no`)

## Requirements

1. Research best practices for the specialization
2. Create appropriate folder structure in `.github/`
3. Generate agent file with:
   - Clear purpose and workflow
   - Appropriate tool selection
   - Communication guidelines
   - Examples
4. Generate instruction file with:
   - Domain-specific guidelines
   - Code standards
   - Best practices
5. If includePrompts=yes, generate at least one prompt file

## Output Structure

The agent should create:

```
.github/
  agents/
    <specialization>.agent.md (or .chatmode.md)
  instructions/
    <specialization>.instructions.md
  prompts/
    <verb-noun>.prompt.md (if requested)
```

## File Naming

- Agent: `${input:specialization}.agent.md`
- Instructions: `${input:specialization}.instructions.md`
- Prompts: Based on common tasks for the specialization

## Quality Expectations

- Files should be production-ready
- Follow Beast Mode patterns
- Include concrete examples
- Use appropriate tools for role
- Document constraints clearly

## References

Follow [architecture standards](../instructions/architecture-components.instructions.md)
Follow [project guidelines](../copilot-instructions.md)
