# Architecture Builder - Custom Agent Generator

A specialized GitHub Copilot agent that creates high-quality Three-Layer Architecture components (agents, instructions, and prompts) based on user specifications.

## Overview

The Architecture Builder agent helps you quickly create production-ready Copilot customizations modeled after Burke Holland's Beast Mode and VS Code best practices. It researches current best practices, generates proper folder structures, and creates well-documented agent files.

## What's Included

This package includes:

- **Architecture Builder Agent** (`.github/agents/architecture-builder.agent.md`)
  - Specialized agent for generating Copilot components
  - Researches best practices before generating
  - Creates proper folder structures
  - Uses good naming conventions

- **Architecture Standards** (`.github/instructions/architecture-components.instructions.md`)
  - Guidelines for creating quality components
  - Naming conventions and best practices
  - Quality checklist
  - Common patterns and anti-patterns

- **Generate Agent Prompt** (`.github/prompts/generate-agent.prompt.md`)
  - Quick command to generate new agents
  - Usage: `/generate-agent specialization=data-science`

- **Project Instructions** (`.github/copilot-instructions.md`)
  - Project-wide guidelines
  - References and documentation

## Quick Start

### Using the Agent Directly

1. Open VS Code Chat
2. Select `architecture-builder` from the agent dropdown
3. Describe what you want: "Create a Python data science agent"
4. The agent will research, create folders, and generate all necessary files

### Using the Prompt

1. In VS Code Chat, type: `/generate-agent`
2. Provide parameters:
   ```
   /generate-agent specialization=react-developer format=agent includePrompts=yes
   ```
3. Files are created automatically

## Examples

### Example 1: Create a Code Review Agent

**Input:**
```
Create a code review agent that can check out repositories and review code quality
```

**Output:**
- `.github/agents/code-reviewer.agent.md`
- `.github/instructions/code-review.instructions.md`
- `.github/prompts/review-pull-request.prompt.md`

The agent will:
1. Research code review best practices and standards
2. Create appropriate folder structure
3. Generate agent with tools: `['search', 'fetch', 'githubRepo']` (read-only for safety)
4. Include guidelines for code quality, security, performance, and maintainability
5. Add checklist format for systematic reviews
6. Create prompts for PR reviews and codebase audits

### Example 2: Create a Data Science Agent

**Input:**
```
Create a Python data science agent with Jupyter notebook support
```

**Output:**
- `.github/agents/data-scientist.agent.md`
- `.github/instructions/python-data-science.instructions.md`
- `.github/prompts/analyze-dataset.prompt.md`

The agent will:
1. Research Python data science best practices
2. Create appropriate folder structure
3. Generate agent with tools: `['search', 'fetch', 'runNotebooks', 'edit', 'new']`
4. Include guidelines for pandas, numpy, matplotlib
5. Create sample analysis prompt

### Example 3: Create a Security Reviewer

**Input:**
```
Create a security review agent that only reads code and doesn't make changes
```

**Output:**
- `.github/agents/security-reviewer.agent.md`
- `.github/instructions/security-review.instructions.md`
- `.github/prompts/review-security.prompt.md`

The agent will:
1. Research security review best practices
2. Restrict tools to: `['search', 'fetch']` (read-only)
3. Include OWASP guidelines
4. Add examples of common vulnerabilities
5. Create security review checklist

### Example 4: Create a Multi-Agent Workflow

**Input:**
```
Create a planner agent that hands off to an implementer agent
```

**Output:**
- `.github/agents/planner.agent.md` (with handoff to implementer)
- `.github/agents/implementer.agent.md` (with handoff to tester)
- `.github/instructions/planning.instructions.md`
- `.github/instructions/implementation.instructions.md`

## Agent Capabilities

The Architecture Builder agent can create:

### Agent Files (.agent.md / .chatmode.md)
- ✅ Research-informed content
- ✅ Appropriate tool selection
- ✅ Clear workflows and constraints
- ✅ Communication guidelines
- ✅ Handoffs for multi-agent workflows
- ✅ Concrete examples

### Instruction Files (.instructions.md)
- ✅ Domain-specific guidelines
- ✅ Code standards and best practices
- ✅ Glob patterns for file targeting
- ✅ Good/bad code examples

### Prompt Files (.prompt.md)
- ✅ Reusable task templates
- ✅ Variable inputs
- ✅ Agent selection
- ✅ References to instructions

## Supported Specializations

The agent can create components for any domain, including:

- **Languages**: Python, JavaScript, TypeScript, Go, Rust, Java, etc.
- **Frameworks**: React, Vue, Angular, Django, Flask, FastAPI, etc.
- **Domains**: Data Science, DevOps, Security, Testing, Documentation, etc.
- **Workflows**: Planning, Implementation, Review, Testing, Deployment

## How It Works

### Research Phase
1. Parses user request to understand specialization
2. Uses `fetch_webpage` to research:
   - Current documentation
   - Best practices (2025+)
   - Community examples
   - Recommended tools

### Generation Phase
1. Creates folder structure following VS Code conventions
2. Generates agent file with Beast Mode patterns:
   - Purpose and directives
   - Step-by-step workflow
   - Tool usage guidelines
   - Communication style
   - Examples
3. Generates instructions with domain-specific guidelines
4. Optionally generates prompt files for common tasks

### Quality Assurance
- Follows naming conventions (kebab-case)
- Uses appropriate tools for role
- Includes concrete examples
- Documents constraints clearly
- Ready to use without editing

## File Structure

After using the Architecture Builder, your project will have:

```
.github/
  agents/
    architecture-builder.agent.md      # The generator agent itself
    <your-agent>.agent.md              # Your generated agents
  instructions/
    architecture-components.instructions.md  # Standards
    <your-domain>.instructions.md      # Your generated instructions
  prompts/
    generate-agent.prompt.md           # Quick generation command
    <your-task>.prompt.md              # Your generated prompts
  copilot-instructions.md              # Project-wide guidelines
```

## Customization

### Modify the Generator

Edit `.github/agents/architecture-builder.agent.md` to:
- Change research strategy
- Adjust generation templates
- Add new component types
- Modify quality standards

### Modify Standards

Edit `.github/instructions/architecture-components.instructions.md` to:
- Add your own conventions
- Include company-specific guidelines
- Adjust quality criteria

## Best Practices

### When to Use
- ✅ Creating new specialized agents
- ✅ Setting up project-specific Copilot customizations
- ✅ Building multi-agent workflows
- ✅ Standardizing team conventions

### When Not to Use
- ❌ For simple one-off prompts (just use chat directly)
- ❌ When you need something very generic (use default agent)
- ❌ For quick prototyping (manually create is faster)

### Tips for Best Results

1. **Be Specific**: "React component generator with TypeScript and Mantine UI" is better than "React agent"

2. **Mention Constraints**: "Read-only security reviewer" tells the agent to restrict tools

3. **Request Workflows**: "Planner that hands off to implementer" creates multi-agent setups

4. **Include Tech Stack**: "Python data science with pandas, numpy, and scikit-learn" gets better research

5. **Review and Iterate**: Generated files are starting points - review and customize as needed

## Troubleshooting

### Agent Not Appearing in Dropdown
- Reload VS Code window: `Ctrl+Shift+P` → "Developer: Reload Window"
- Check file is in `.github/agents/` folder
- Verify YAML frontmatter is valid

### Generated Files Have Errors
- The agent follows linting rules but may need adjustments
- Review lint errors and fix paths/names as needed
- Check tool names match current VS Code documentation

### Agent Doesn't Research
- Ensure `fetch` tool is available and working
- Check internet connectivity
- The agent may skip research for very common domains

## Advanced Usage

### Create Domain-Specific Generators

You can create specialized generator agents for your domain:

```
Create a generator agent that creates FastAPI backend agents with SQLAlchemy and Pydantic
```

This creates a generator that specializes in your stack.

### Template-Based Generation

Modify the agent to use your company's templates:

1. Create template files in `.github/templates/`
2. Update Architecture Builder to reference templates
3. Fill templates with research-based content

### MCP Integration

Add MCP server recommendations to generated agents:

```
Create an agent that uses the database MCP server for schema design
```

## References

- [VS Code Copilot Customization](https://code.visualstudio.com/docs/copilot/customization/overview)
- [Custom Agents Guide](https://code.visualstudio.com/docs/copilot/customization/custom-agents)
- [Beast Mode Gist](https://gist.github.com/burkeholland/88af0249c4b6aff3820bf37898c8bacf)
- [Three-Layer Architecture Guide](./GitHub_Copilot_Three_Layer_Architecture_Guide.md)

## Contributing

This is a starting point. Customize it for your needs:
- Add your own templates
- Include company-specific guidelines
- Create domain-specific variants
- Share improvements with your team

## License

This configuration is provided as-is for educational and professional use. Inspired by the open-source work of Burke Holland and the VS Code team.

---

**Version**: 1.0  
**Last Updated**: November 2025  
**Compatibility**: VS Code with GitHub Copilot
