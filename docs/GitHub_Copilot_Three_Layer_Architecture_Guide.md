# GitHub Copilot Three-Layer Architecture Guide

**A Complete Guide to Building Powerful AI Workflows with Custom Agents, Prompts, and Instructions**

---

## Table of Contents

1. [Introduction](#introduction)
2. [The Three Layers Explained](#the-three-layers-explained)
3. [Layer 1: Custom Instructions](#layer-1-custom-instructions)
4. [Layer 2: Prompt Files](#layer-2-prompt-files)
5. [Layer 3: Custom Agents](#layer-3-custom-agents)
6. [How the Layers Work Together](#how-the-layers-work-together)
7. [Implementation Examples](#implementation-examples)
8. [Best Practices](#best-practices)
9. [Migration Guide: Chat Modes to Custom Agents](#migration-guide-chat-modes-to-custom-agents)
10. [Advanced Patterns](#advanced-patterns)

---

## Introduction

GitHub Copilot in VS Code supports a powerful three-layer architecture for customizing AI behavior. This architecture enables you to create consistent, repeatable, and specialized workflows that adapt to your project's needs.

**The Three Layers:**
1. **Custom Instructions** — Persistent guidelines applied automatically
2. **Prompt Files** — Reusable, on-demand task templates
3. **Custom Agents** — Specialized AI personas with specific tools and behaviors

Together, these layers let you build sophisticated AI workflows without manually repeating context in every chat request.

---

## The Three Layers Explained

### Visual Overview

```
┌─────────────────────────────────────────────────────────────┐
│                     Custom Agent (Layer 3)                  │
│  • Specialized persona (planner, reviewer, implementer)     │
│  • Defines available tools and capabilities                 │
│  • Can reference prompts and instructions                   │
│  • Includes handoffs for workflow orchestration             │
└─────────────────────────────────────────────────────────────┘
                              │
                              ├─ Uses
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                     Prompt Files (Layer 2)                  │
│  • Reusable task templates                                  │
│  • Triggered on-demand with /command                        │
│  • Can reference custom instructions                        │
│  • Can specify which agent to use                           │
└─────────────────────────────────────────────────────────────┘
                              │
                              ├─ Uses
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                  Custom Instructions (Layer 1)              │
│  • Base guidelines and coding standards                     │
│  • Applied automatically or manually                        │
│  • Can target specific file types with glob patterns        │
│  • Shared across agents and prompts                         │
└─────────────────────────────────────────────────────────────┘
```

### Decision Matrix

| Use Case | Best Layer | Why |
|----------|-----------|-----|
| Project-wide coding standards | Custom Instructions | Always applies automatically |
| Python-specific rules | Custom Instructions + glob | Targets specific file types |
| Generate React components | Prompt Files | Reusable, on-demand task |
| Plan before implementing | Custom Agent | Specialized persona with limited tools |
| Code review workflow | Custom Agent + Handoffs | Sequential workflow with transitions |

---

## Layer 1: Custom Instructions

### What Are Custom Instructions?

Custom instructions define persistent guidelines that influence how AI generates code and handles development tasks. They apply automatically or can be manually attached to specific chat requests.

### Types of Instruction Files

#### 1. `.github/copilot-instructions.md`
- **Location:** Project root
- **Scope:** All chat requests in the workspace
- **When to use:** Project-wide standards and conventions

**Example:**
```markdown
# Project Coding Standards

## Code Style
- Use TypeScript for all new code
- Follow ESLint rules defined in .eslintrc.json
- Prefer functional components over class components

## Testing
- Write tests for all new features
- Use Jest and React Testing Library
- Aim for 80% code coverage

## Documentation
- Add JSDoc comments for all public APIs
- Update README.md when adding new features
```

#### 2. `.instructions.md` Files
- **Location:** `.github/instructions/` or user profile
- **Scope:** Conditional based on `applyTo` glob pattern
- **When to use:** Language or framework-specific rules

**Example: `python-style.instructions.md`**
```markdown
---
description: "Python coding standards"
name: "Python Style Guide"
applyTo: "**/*.py"
---

# Python Coding Standards

- Follow PEP 8 style guide
- Use type hints for all function parameters and return values
- Write docstrings using Google style
- Use `black` for code formatting
- Prefer `pathlib` over `os.path`
```

#### 3. `AGENTS.md` Files
- **Location:** Project root (experimental: subfolders)
- **Scope:** All AI agents in the workspace
- **When to use:** Multi-agent workflows

**Example:**
```markdown
# Agent Guidelines

All agents in this project should:
- Never commit code without running tests first
- Always check for TypeScript errors before completing tasks
- Use semantic commit messages following Conventional Commits
```

### File Structure

```markdown
---
description: "Brief description"
name: "Display name"
applyTo: "**/*.js"  # Optional glob pattern
---

# Instructions Body

Your instructions in natural language using Markdown.
You can reference files with [links](./path/to/file.md).
```

### When Instructions Apply

- **Automatic:** Files matching `applyTo` pattern when editing/creating code
- **Manual:** Attached via "Add Context > Instructions" in Chat view
- **Priority:** Multiple instruction files combine (order not guaranteed)

### Best Practices

1. **Keep instructions short and self-contained**
   - Each instruction should be a single, simple statement
   - If you need multiple pieces of info, use multiple instructions

2. **Use glob patterns for specificity**
   ```markdown
   ---
   applyTo: "src/components/**/*.tsx"
   ---
   ```

3. **Reference, don't duplicate**
   - Link to instructions files in prompts and agents
   - Avoid copying the same rules everywhere

4. **Store wisely**
   - Project-specific → workspace (`.github/instructions/`)
   - Personal preferences → user profile

---

## Layer 2: Prompt Files

### What Are Prompt Files?

Prompt files are standalone, reusable prompts for common development tasks. Unlike instructions that apply broadly, prompts are triggered on-demand for specific tasks.

### File Structure

```markdown
---
description: "Generate a React form component"
name: "create-react-form"
argument-hint: "formName=MyForm"
agent: "agent"  # or custom agent name
model: "Claude Sonnet 4"
tools: ['search', 'edit', 'new']
---

# Create React Form Component

Generate a complete React form component using Mantine UI.

Requirements:
- Use TypeScript
- Implement form validation with zod
- Include proper error handling
- Add accessibility attributes
- Follow project coding standards in [standards](../.github/copilot-instructions.md)

Form name: ${input:formName:MyForm}
Selected text: ${selectedText}
```

### Prompt File Metadata

| Field | Description | Example |
|-------|-------------|---------|
| `description` | Short description shown in UI | "Generate React form" |
| `name` | Command name (type `/name` in chat) | "create-react-form" |
| `argument-hint` | Guide for user input | "formName=MyForm" |
| `agent` | Which agent to use | "agent", "ask", "edit", or custom |
| `model` | AI model to use | "Claude Sonnet 4" |
| `tools` | Available tools | `['search', 'edit', 'new']` |

### Variables in Prompts

Prompts support dynamic variables using `${variableName}` syntax:

**Workspace Variables:**
- `${workspaceFolder}` — Workspace root path
- `${workspaceFolderBasename}` — Workspace folder name

**Selection Variables:**
- `${selection}` — Currently selected text
- `${selectedText}` — Same as selection

**File Variables:**
- `${file}` — Full file path
- `${fileBasename}` — File name with extension
- `${fileDirname}` — Directory containing file
- `${fileBasenameNoExtension}` — File name without extension

**Input Variables:**
- `${input:variableName}` — Prompt user for input
- `${input:variableName:placeholder}` — With placeholder text

### Creating Prompt Files

1. **Via UI:**
   - Chat view → Configure Chat (gear icon) → Prompt Files → New prompt file
   - Choose location: Workspace or User Profile

2. **Via Command Palette:**
   - `Ctrl+Shift+P` → "Chat: New Prompt File"

3. **Manual Creation:**
   - Create `.prompt.md` file in `.github/prompts/`
   - Add YAML frontmatter and prompt body

### Using Prompt Files

**Option 1: Type `/` in Chat**
```
/create-react-form formName=LoginForm
```

**Option 2: Command Palette**
- `Ctrl+Shift+P` → "Chat: Run Prompt"
- Select prompt from list

**Option 3: Editor Play Button**
- Open prompt file in editor
- Click play button in title bar
- Choose: current session or new session

### Example Prompt Files

#### Security Review Prompt

```markdown
---
description: "Perform security review of REST API"
name: "security-review"
agent: "agent"
tools: ['search', 'githubRepo']
---

# Security Review: REST API

Review the selected REST API code for security vulnerabilities.

Check for:
- SQL injection vulnerabilities
- XSS attack vectors
- Authentication bypass issues
- Rate limiting implementation
- Input validation gaps
- Sensitive data exposure

File to review: ${file}
Selected code:
\`\`\`
${selection}
\`\`\`

Provide:
1. List of vulnerabilities found
2. Severity rating for each
3. Recommended fixes
4. Code examples of secure implementation
```

#### Component Generator

```markdown
---
description: "Generate shadcn/ui component"
name: "shadcn-component"
argument-hint: "componentName"
tools: ['fetch', 'edit', 'new']
---

# Generate shadcn/ui Component

Use the fetch tool to lookup latest docs at https://ui.shadcn.com/docs/components/${input:componentName}

Generate component: ${input:componentName}
Location: ${workspaceFolder}/src/components/ui/

Requirements:
- Follow latest shadcn/ui patterns from docs
- Include TypeScript types
- Add accessibility attributes
- Follow [project standards](../.github/copilot-instructions.md)
```

---

## Layer 3: Custom Agents

### What Are Custom Agents?

Custom agents are specialized AI personas tailored to specific development roles. Each agent has its own behavior, available tools, and instructions.

**Important:** Custom Agents are the replacement for Chat Modes (`.chatmode.md`). The functionality is identical, but the terminology and file extension have been updated.

### Migration from Chat Modes

VS Code still recognizes `.chatmode.md` files in `.github/chatmodes/` as custom agents. You can use a Quick Fix action to automatically rename and move them to `.github/agents/` with the `.agent.md` extension.

### File Structure

```markdown
---
description: "Generate implementation plan without making edits"
name: "Planner"
argument-hint: "describe the feature"
tools: ['fetch', 'githubRepo', 'search', 'usages']
model: "Claude Sonnet 4"
target: "vscode"
handoffs:
  - label: "Implement Plan"
    agent: "agent"
    prompt: "Implement the plan outlined above."
    send: false
---

# Planning Agent Instructions

You are in planning mode. Your role is to generate detailed implementation plans.

## Constraints
- DO NOT make any code edits
- DO NOT create or modify files
- Use ONLY read-only tools

## Output Format
Generate a Markdown document with:
1. **Overview** — Brief feature description
2. **Requirements** — List of functional requirements
3. **Implementation Steps** — Detailed, numbered steps
4. **Testing Strategy** — How to verify the implementation
5. **Risks & Considerations** — Potential issues

## Tool Usage
- Use #tool:search to find relevant code
- Use #tool:githubRepo to understand project structure
- Use #tool:fetch to research best practices

## Example Plan Structure
\`\`\`markdown
# Implementation Plan: [Feature Name]

## Overview
[One paragraph summary]

## Requirements
- Requirement 1
- Requirement 2

## Implementation Steps
1. Step 1
2. Step 2

## Testing Strategy
- Unit tests for X
- Integration tests for Y

## Risks
- Risk 1 and mitigation
\`\`\`
```

### Agent Metadata

| Field | Description | Example |
|-------|-------------|---------|
| `description` | Agent purpose (shown as placeholder) | "Plan features" |
| `name` | Agent name in dropdown | "Planner" |
| `argument-hint` | Guide for user input | "describe the feature" |
| `tools` | Available tools | `['search', 'fetch']` |
| `model` | Preferred AI model | "Claude Sonnet 4" |
| `target` | Target environment | "vscode" or "github-copilot" |
| `mcp-servers` | MCP server configs (GitHub Copilot) | JSON config |
| `handoffs` | Workflow transitions | See Handoffs section |

### Handoffs: Sequential Workflows

Handoffs enable guided workflows that transition between agents with pre-filled prompts.

**Example: Plan → Implement → Review**

```markdown
---
name: "Planner"
tools: ['search', 'fetch', 'githubRepo']
handoffs:
  - label: "Start Implementation"
    agent: "implementer"
    prompt: "Implement the plan outlined above."
    send: false
  - label: "Request Review"
    agent: "reviewer"
    prompt: "Review the implementation for quality and security."
    send: false
---
```

After the agent completes, handoff buttons appear:
- **Start Implementation** → Switches to `implementer` agent with pre-filled prompt
- **Request Review** → Switches to `reviewer` agent with pre-filled prompt

**Handoff Properties:**
- `label` — Button text shown to user
- `agent` — Target agent identifier
- `prompt` — Pre-filled prompt text
- `send` — Auto-submit? (`true` or `false`)

### Creating Custom Agents

1. **Via UI:**
   - Select agent dropdown → Configure Custom Agents → Create new custom agent
   - Choose location: Workspace or User Profile

2. **Via Command Palette:**
   - `Ctrl+Shift+P` → "Chat: New Custom Agent"

3. **Manual Creation:**
   - Create `.agent.md` file in `.github/agents/`
   - Add YAML frontmatter and agent instructions

### Example Custom Agents

#### Code Review Agent

```markdown
---
description: "Perform thorough code reviews"
name: "Reviewer"
tools: ['search', 'fetch', 'githubRepo']
model: "Claude Sonnet 4"
handoffs:
  - label: "Fix Issues"
    agent: "agent"
    prompt: "Fix the issues identified in the review."
    send: false
---

# Code Review Agent

You are a senior code reviewer. Your reviews are thorough, constructive, and focus on:

## Review Checklist
- [ ] Code quality and readability
- [ ] Security vulnerabilities
- [ ] Performance issues
- [ ] Test coverage
- [ ] Documentation completeness
- [ ] Error handling
- [ ] Edge cases

## Review Format
For each file reviewed, provide:

### 🟢 Strengths
- What's done well
- Good patterns to continue

### 🟡 Suggestions
- Nice-to-have improvements
- Style preferences

### 🔴 Issues (Must Fix)
- Security vulnerabilities
- Bugs or logic errors
- Missing error handling

## Communication Style
- Be specific: cite line numbers and code snippets
- Be constructive: explain *why* and suggest *how to fix*
- Be encouraging: recognize good work
```

#### Database Agent

```markdown
---
description: "Database design and query optimization"
name: "DB Expert"
tools: ['search', 'fetch', 'database/*']
model: "Claude Sonnet 4"
---

# Database Expert Agent

You are a database architect and query optimization specialist.

## Expertise
- Schema design and normalization
- Query optimization
- Index strategy
- Migration planning
- Performance tuning

## Guidelines
- Always explain trade-offs in design decisions
- Provide migration scripts for schema changes
- Include rollback strategies
- Consider scalability implications
- Use #tool:database to interact with databases

## Response Format
When designing schemas:
1. Show Entity-Relationship diagram (Markdown)
2. Provide CREATE TABLE statements
3. Explain relationships and constraints
4. Suggest appropriate indexes
5. Include sample queries
```

---

## How the Layers Work Together

### Tool Priority Order

When determining available tools:

1. **Tools in Prompt File** (if running a prompt)
2. **Tools from Custom Agent** (if prompt references an agent)
3. **Default Tools** (for the selected agent)

### Layered Example: React Development Workflow

#### Layer 1: Instructions

`.github/copilot-instructions.md`
```markdown
# React Project Standards

- Use TypeScript for all components
- Use Mantine UI library
- Follow functional component patterns
- Write tests with React Testing Library
```

`.github/instructions/react-style.instructions.md`
```markdown
---
applyTo: "src/**/*.tsx"
---

# React Component Standards

- Use named exports
- Props interface must be exported
- Include displayName for debugging
- Add PropTypes for runtime validation
```

#### Layer 2: Prompts

`.github/prompts/create-component.prompt.md`
```markdown
---
description: "Create React component"
name: "create-component"
agent: "implementer"
tools: ['new', 'edit']
---

# Create React Component

Create a new React component: ${input:componentName}

Follow [React standards](../.github/copilot-instructions.md)
Follow [component patterns](../instructions/react-style.instructions.md)

Location: src/components/${input:componentName}/
```

#### Layer 3: Agents

`.github/agents/implementer.agent.md`
```markdown
---
description: "Implement features based on plans"
name: "Implementer"
tools: ['new', 'edit', 'runCommands', 'runTasks']
handoffs:
  - label: "Run Tests"
    agent: "tester"
    prompt: "Run tests for the new component."
    send: true
---

# Implementation Agent

You implement features following the project plan.

## Workflow
1. Read requirements carefully
2. Create necessary files
3. Write clean, tested code
4. Follow project [coding standards](../.github/copilot-instructions.md)

## Before Completing
- [ ] All files created
- [ ] Code follows standards
- [ ] No syntax errors
- [ ] Ready for testing
```

### Usage Flow

1. User selects "Planner" agent
2. User asks: "Plan a user profile page"
3. Planner generates plan (no code edits)
4. User clicks "Start Implementation" handoff
5. Switches to "Implementer" agent
6. User runs `/create-component componentName=UserProfile`
7. Prompt loads, references instructions automatically
8. Component created following all guidelines
9. User clicks "Run Tests" handoff
10. Switches to "Tester" agent with auto-submit

---

## Implementation Examples

### Example 1: Python Data Science Project

**File Structure:**
```
.github/
  copilot-instructions.md           # General standards
  instructions/
    python-data.instructions.md     # Python data standards
    notebook.instructions.md        # Jupyter notebook guidelines
  prompts/
    create-analysis.prompt.md       # Generate analysis
    create-viz.prompt.md            # Generate visualizations
  agents/
    researcher.agent.md             # Research and explore
    analyst.agent.md                # Analyze data
    reporter.agent.md               # Create reports
```

**copilot-instructions.md:**
```markdown
# Data Science Project Standards

## Environment
- Python 3.11+
- Use conda for environment management
- Document dependencies in environment.yml

## Code Style
- Follow PEP 8
- Use type hints
- Add docstrings (NumPy style)

## Data
- Store raw data in data/raw/
- Store processed data in data/processed/
- Never commit large data files
```

**python-data.instructions.md:**
```markdown
---
applyTo: "**/*.py"
---

# Python Data Science Standards

- Use pandas for tabular data
- Use numpy for numerical operations
- Use matplotlib/seaborn for visualization
- Always validate data before processing
- Include null handling strategy
```

**researcher.agent.md:**
```markdown
---
name: "Researcher"
description: "Explore data and research approaches"
tools: ['search', 'fetch', 'runNotebooks']
handoffs:
  - label: "Start Analysis"
    agent: "analyst"
    prompt: "Analyze the dataset based on research findings."
    send: false
---

# Research Agent

Explore data and research methodologies.

## Tasks
- Load and inspect datasets
- Research statistical approaches
- Document findings
- Propose analysis strategies

## Constraints
- Read-only operations
- No data modifications
- Focus on exploration
```

### Example 2: Full-Stack Web App

**File Structure:**
```
.github/
  copilot-instructions.md
  instructions/
    frontend.instructions.md      # React/TypeScript
    backend.instructions.md       # Node/Express
    api.instructions.md           # API design
  prompts/
    create-api-endpoint.prompt.md
    create-react-component.prompt.md
    create-test-suite.prompt.md
  agents/
    architect.agent.md            # Design system
    frontend-dev.agent.md         # Frontend work
    backend-dev.agent.md          # Backend work
    tester.agent.md               # Testing
```

**architect.agent.md:**
```markdown
---
name: "Architect"
description: "Design system architecture"
tools: ['search', 'fetch', 'githubRepo']
model: "Claude Sonnet 4"
handoffs:
  - label: "Build Frontend"
    agent: "frontend-dev"
    prompt: "Implement the frontend based on architecture."
    send: false
  - label: "Build Backend"
    agent: "backend-dev"
    prompt: "Implement the backend API based on architecture."
    send: false
---

# System Architect

Design scalable, maintainable architectures.

## Deliverables
- System architecture diagrams
- API contracts
- Data models
- Component hierarchy
- Integration points

## Focus Areas
- Separation of concerns
- Scalability
- Security
- Performance
- Maintainability
```

---

## Best Practices

### General Principles

1. **Start Simple**
   - Begin with basic instructions
   - Add prompts for repeated tasks
   - Create agents when you need specialized workflows

2. **Keep It DRY (Don't Repeat Yourself)**
   - Store common guidelines in instructions
   - Reference instructions from prompts and agents
   - Use Markdown links: `[standards](../.github/copilot-instructions.md)`

3. **Be Specific**
   - Clear, concrete instructions work best
   - Include examples when possible
   - Avoid ambiguous language

4. **Test and Iterate**
   - Try your customizations with real tasks
   - Refine based on results
   - Get feedback from team members

### Instructions Best Practices

- ✅ Short, self-contained statements
- ✅ Use glob patterns for specificity
- ✅ Store project rules in workspace
- ✅ Store personal preferences in user profile
- ❌ Don't duplicate guidelines
- ❌ Don't make instructions too verbose

### Prompt Best Practices

- ✅ Clear description of task
- ✅ Provide input/output examples
- ✅ Use variables for flexibility
- ✅ Reference instructions for consistency
- ❌ Don't duplicate agent logic
- ❌ Don't make prompts too generic

### Agent Best Practices

- ✅ Focused, single-purpose agents
- ✅ Appropriate tool restrictions
- ✅ Clear handoff workflows
- ✅ Consistent communication style
- ❌ Don't create "do everything" agents
- ❌ Don't duplicate instructions in agent body

---

## Migration Guide: Chat Modes to Custom Agents

### What Changed?

**Before:** `.chatmode.md` files in `.github/chatmodes/`
**After:** `.agent.md` files in `.github/agents/`

The functionality is identical — only the naming and location changed.

### Automatic Migration

VS Code detects existing `.chatmode.md` files and offers a Quick Fix:

1. Open a `.chatmode.md` file
2. Look for the Quick Fix light bulb
3. Select "Rename to .agent.md and move to .github/agents/"
4. VS Code handles the migration

### Manual Migration

If you prefer manual migration:

1. **Create new directory:**
   ```bash
   mkdir -p .github/agents
   ```

2. **Copy and rename files:**
   ```bash
   cp .github/chatmodes/mymode.chatmode.md .github/agents/mymode.agent.md
   ```

3. **Update references:**
   - Update any documentation
   - Update prompt files that reference the agent

4. **Test:**
   - Reload VS Code
   - Verify agent appears in dropdown
   - Test functionality

### Updating Documentation

If you have team documentation or setup guides, update references:

**Old:**
```markdown
Create a custom chat mode in `.github/chatmodes/planner.chatmode.md`
```

**New:**
```markdown
Create a custom agent in `.github/agents/planner.agent.md`
```

---

## Advanced Patterns

### Pattern 1: Multi-Stage Workflow

Create a sequence of agents with handoffs:

```
Plan → Design → Implement → Test → Review → Deploy
```

Each agent:
- Has specialized tools
- Receives context from previous stage
- Hands off to next stage

**Example: `planner.agent.md`**
```markdown
---
name: "Planner"
tools: ['search', 'fetch']
handoffs:
  - label: "Design System"
    agent: "designer"
    prompt: "Design the system architecture for: ${input}"
    send: false
---
```

**Example: `designer.agent.md`**
```markdown
---
name: "Designer"
tools: ['search', 'fetch', 'new']
handoffs:
  - label: "Start Implementation"
    agent: "implementer"
    prompt: "Implement the design outlined above."
    send: false
---
```

### Pattern 2: Specialized Tool Sets

Create agents with specific tool combinations:

**Read-Only Agent (Planning/Research):**
```markdown
---
tools: ['search', 'fetch', 'githubRepo', 'usages']
---
```

**Write-Only Agent (Implementation):**
```markdown
---
tools: ['new', 'edit']
---
```

**Testing Agent:**
```markdown
---
tools: ['runCommands', 'runTasks', 'edit']
---
```

### Pattern 3: Contextual Instructions

Use glob patterns to apply different rules in different contexts:

```
.github/instructions/
  frontend-react.instructions.md    → applyTo: "src/frontend/**/*.tsx"
  backend-node.instructions.md      → applyTo: "src/backend/**/*.ts"
  tests.instructions.md             → applyTo: "**/*.test.ts"
  docs.instructions.md              → applyTo: "docs/**/*.md"
```

### Pattern 4: Prompt Library

Build a library of reusable prompts:

```
.github/prompts/
  generators/
    create-api-endpoint.prompt.md
    create-react-component.prompt.md
    create-database-model.prompt.md
  reviews/
    security-review.prompt.md
    performance-review.prompt.md
    accessibility-review.prompt.md
  utilities/
    refactor-code.prompt.md
    add-tests.prompt.md
    generate-docs.prompt.md
```

### Pattern 5: Model Selection

Choose the right model for each agent:

```markdown
---
# Fast model for simple tasks
name: "Quick Fixer"
model: "GPT-4o"
---
```

```markdown
---
# Powerful model for complex reasoning
name: "Architect"
model: "Claude Sonnet 4"
---
```

### Pattern 6: MCP Integration

Integrate Model Context Protocol servers:

```markdown
---
name: "Database Expert"
tools: ['database/*', 'fetch']
mcp-servers: |
  {
    "database-server": {
      "url": "http://localhost:3000/mcp"
    }
  }
---
```

---

## Conclusion

The three-layer architecture (Instructions → Prompts → Agents) provides a flexible, powerful framework for customizing GitHub Copilot to your exact needs.

**Start your journey:**
1. Add project-wide coding standards in `.github/copilot-instructions.md`
2. Create a prompt for your most common task
3. Build a specialized agent for a specific workflow

**Key Takeaways:**
- Instructions = persistent guidelines
- Prompts = reusable task templates
- Agents = specialized AI personas
- Custom Agents replace Chat Modes (same functionality, new name)
- Layers work together through references and tool priorities
- Start simple, add complexity as needed

---

## Additional Resources

- [VS Code Copilot Customization Docs](https://code.visualstudio.com/docs/copilot/customization/overview)
- [Custom Instructions Guide](https://code.visualstudio.com/docs/copilot/customization/custom-instructions)
- [Prompt Files Guide](https://code.visualstudio.com/docs/copilot/customization/prompt-files)
- [Custom Agents Guide](https://code.visualstudio.com/docs/copilot/customization/custom-agents)
- [Awesome Copilot Repository](https://github.com/github/awesome-copilot)
- [Burke Holland's Beast Mode](https://gist.github.com/burkeholland/88af0249c4b6aff3820bf37898c8bacf)

---

**Document Version:** 1.0  
**Last Updated:** November 26, 2025  
**Author:** GitHub Copilot Agent Architecture Working Group
