# GitHub Copilot Project Instructions

This workspace uses the Three-Layer Architecture for GitHub Copilot customization.

## General Guidelines

- Follow VS Code Copilot documentation conventions
- Use kebab-case for file names
- Keep components focused and single-purpose
- Reference this file from agents and prompts using relative links

## Architecture Components

This project contains:
- **Agents** (`.github/agents/`): Specialized AI personas for specific tasks
- **Instructions** (`.github/instructions/`): Conditional guidelines applied based on file patterns
- **Prompts** (`.github/prompts/`): Reusable task templates

## File Naming Conventions

- Agents: `<role-name>.agent.md` or `<role-name>.chatmode.md`
- Instructions: `<domain-name>.instructions.md`
- Prompts: `<verb-noun>.prompt.md`

## Quality Standards

When creating or modifying architecture components:
1. Use clear, descriptive names
2. Include concrete examples
3. Specify appropriate tools for the role
4. Document constraints explicitly
5. Add handoffs for multi-step workflows

## Beast Mode Influence

Components in this project are inspired by Burke Holland's Beast Mode:
- Autonomous execution patterns
- Clear workflow structures
- Research-driven development
- Todo list management
- Communication guidelines

## References

- [VS Code Copilot Docs](https://code.visualstudio.com/docs/copilot/customization/overview)
- [Beast Mode Gist](https://gist.github.com/burkeholland/88af0249c4b6aff3820bf37898c8bacf)
- [Architecture Guide](../GitHub_Copilot_Three_Layer_Architecture_Guide.md)
