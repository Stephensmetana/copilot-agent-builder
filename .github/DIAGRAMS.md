# Architecture Builder System Diagram

## System Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                           USER REQUEST                               │
│  "Create a Python data science agent with Jupyter support"          │
└───────────────────────────────┬─────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────────┐
│                    ARCHITECTURE BUILDER AGENT                        │
│  • Parses user request                                               │
│  • Determines: agent, instructions, prompts needed                   │
│  • Identifies specialization and tools required                      │
└───────────────────────────────┬─────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────────┐
│                        RESEARCH PHASE                                │
│  ┌───────────────────────────────────────────────────────┐          │
│  │ fetch_webpage tool                                     │          │
│  │ • Python data science best practices 2025             │          │
│  │ • Jupyter notebook documentation                       │          │
│  │ • pandas/numpy/matplotlib patterns                     │          │
│  │ • Community examples and MCP tools                     │          │
│  └───────────────────────────────────────────────────────┘          │
└───────────────────────────────┬─────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────────┐
│                      GENERATION PHASE                                │
│                                                                      │
│  ┌────────────────────────────────────────────────────────┐         │
│  │ 1. Create Folder Structure                             │         │
│  │    .github/agents/                                     │         │
│  │    .github/instructions/                               │         │
│  │    .github/prompts/                                    │         │
│  └────────────────────────────────────────────────────────┘         │
│                                                                      │
│  ┌────────────────────────────────────────────────────────┐         │
│  │ 2. Generate Agent File                                 │         │
│  │    • YAML frontmatter (name, tools, model)             │         │
│  │    • Purpose and directives                            │         │
│  │    • Workflow steps                                     │         │
│  │    • Tool usage guidelines                             │         │
│  │    • Communication style                               │         │
│  │    • Examples                                          │         │
│  └────────────────────────────────────────────────────────┘         │
│                                                                      │
│  ┌────────────────────────────────────────────────────────┐         │
│  │ 3. Generate Instructions File                          │         │
│  │    • applyTo: "**/*.py"                                │         │
│  │    • Python coding standards                           │         │
│  │    • Data science best practices                       │         │
│  │    • Library-specific guidelines                       │         │
│  │    • Examples (good/bad)                               │         │
│  └────────────────────────────────────────────────────────┘         │
│                                                                      │
│  ┌────────────────────────────────────────────────────────┐         │
│  │ 4. Generate Prompt Files                               │         │
│  │    • analyze-dataset.prompt.md                         │         │
│  │    • create-visualization.prompt.md                    │         │
│  │    • clean-data.prompt.md                              │         │
│  └────────────────────────────────────────────────────────┘         │
└───────────────────────────────┬─────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────────┐
│                         OUTPUT FILES                                 │
│                                                                      │
│  .github/                                                            │
│    agents/                                                           │
│      data-scientist.agent.md                                         │
│    instructions/                                                     │
│      python-data-science.instructions.md                             │
│    prompts/                                                          │
│      analyze-dataset.prompt.md                                       │
│      create-visualization.prompt.md                                  │
└───────────────────────────────┬─────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────────┐
│                      READY TO USE                                    │
│  User can now:                                                       │
│  • Select "data-scientist" from agent dropdown                       │
│  • Run /analyze-dataset command                                      │
│  • Files follow all standards automatically                          │
└─────────────────────────────────────────────────────────────────────┘
```

## Component Relationships

```
┌──────────────────────────────────────────────────────────────────┐
│                     ARCHITECTURE BUILDER                          │
│                    (Generator Agent)                              │
└───────────┬─────────────────────────┬────────────────────────────┘
            │                         │
            │ creates                 │ follows
            │                         │
            ▼                         ▼
┌─────────────────────────┐  ┌──────────────────────────────────────┐
│   GENERATED AGENTS       │  │  ARCHITECTURE STANDARDS              │
│   (.agent.md files)      │  │  (.instructions.md)                  │
│                          │  │                                      │
│  • data-scientist        │  │  • Naming conventions                │
│  • security-reviewer     │◄─┤  • File structure                    │
│  • react-developer       │  │  • Tool selection                    │
│  • planner               │  │  • Quality checklist                 │
└───────────┬──────────────┘  └──────────────────────────────────────┘
            │
            │ references
            │
            ▼
┌─────────────────────────┐
│   INSTRUCTIONS          │
│   (.instructions.md)    │
│                         │
│  • Domain guidelines    │
│  • Code standards       │
│  • Best practices       │
│  • applyTo patterns     │
└───────────┬─────────────┘
            │
            │ used by
            │
            ▼
┌─────────────────────────┐
│   PROMPTS               │
│   (.prompt.md)          │
│                         │
│  • Quick commands       │
│  • Task templates       │
│  • Variable inputs      │
│  • Agent selection      │
└─────────────────────────┘
```

## Multi-Agent Workflow Pattern

```
┌─────────────────────┐
│      PLANNER        │
│  (Read-Only)        │
│                     │
│  Tools:             │
│  • search           │
│  • fetch            │
│  • githubRepo       │
│  • usages           │
└──────────┬──────────┘
           │
           │ handoff: "Implement Plan"
           │
           ▼
┌─────────────────────┐
│   IMPLEMENTER       │
│  (Write Access)     │
│                     │
│  Tools:             │
│  • new              │
│  • edit             │
│  • search           │
│  • runCommands      │
└──────────┬──────────┘
           │
           │ handoff: "Run Tests"
           │
           ▼
┌─────────────────────┐
│      TESTER         │
│  (Test Tools)       │
│                     │
│  Tools:             │
│  • runCommands      │
│  • runTasks         │
│  • search           │
│  • edit             │
└──────────┬──────────┘
           │
           │ handoff: "Review Code"
           │
           ▼
┌─────────────────────┐
│     REVIEWER        │
│  (Read-Only)        │
│                     │
│  Tools:             │
│  • search           │
│  • fetch            │
└─────────────────────┘
```

## File Generation Flow

```
User Input
    │
    ▼
┌───────────────────────────────┐
│ Parse Specialization          │
│ "Python data science"         │
└───────────┬───────────────────┘
            │
            ▼
┌───────────────────────────────┐
│ Research Best Practices       │
│ • fetch documentation         │
│ • search for patterns         │
│ • identify tools needed       │
└───────────┬───────────────────┘
            │
            ├─────────────────────────────┐
            │                             │
            ▼                             ▼
┌─────────────────────┐    ┌──────────────────────────┐
│ Agent Template      │    │ Instructions Template     │
│ • Name              │    │ • applyTo pattern         │
│ • Tools             │    │ • Guidelines             │
│ • Workflow          │    │ • Examples               │
│ • Examples          │    └────────────┬─────────────┘
└──────────┬──────────┘                 │
           │                             │
           │    ┌────────────────────────┘
           │    │
           ▼    ▼
┌─────────────────────────────────────────┐
│ Fill Templates with Research Data       │
│ • Insert domain-specific guidelines     │
│ • Add tool selection logic              │
│ • Include best practices found          │
│ • Add concrete examples                 │
└───────────┬─────────────────────────────┘
            │
            ▼
┌─────────────────────────────────────────┐
│ Write Files                             │
│ • data-scientist.agent.md               │
│ • python-data-science.instructions.md   │
│ • analyze-dataset.prompt.md             │
└───────────┬─────────────────────────────┘
            │
            ▼
┌─────────────────────────────────────────┐
│ Validate & Report                       │
│ • Check YAML frontmatter                │
│ • Verify file structure                 │
│ • Confirm naming conventions            │
│ • Report completion to user             │
└─────────────────────────────────────────┘
```

## Tool Selection Matrix

```
┌─────────────────────────────────────────────────────────────┐
│                     TOOL SELECTION                          │
├─────────────┬───────────────────────────────────────────────┤
│             │            Agent Role                         │
│    Tool     ├────────┬─────────┬─────────┬─────────────────┤
│             │Planner │Implement│ Tester  │   Reviewer      │
├─────────────┼────────┼─────────┼─────────┼─────────────────┤
│ search      │   ✓    │    ✓    │    ✓    │       ✓         │
│ fetch       │   ✓    │    ✓    │         │       ✓         │
│ githubRepo  │   ✓    │         │         │       ✓         │
│ usages      │   ✓    │         │         │       ✓         │
│ new         │        │    ✓    │         │                 │
│ edit        │        │    ✓    │    ✓    │                 │
│ runCommands │        │    ✓    │    ✓    │                 │
│ runTasks    │        │         │    ✓    │                 │
│ runNotebooks│        │    ✓    │    ✓    │                 │
└─────────────┴────────┴─────────┴─────────┴─────────────────┘

✓ = Recommended for this role
```

## Quality Assurance Flow

```
Generated File
     │
     ▼
┌─────────────────────┐
│ YAML Validation     │
│ • Valid syntax?     │
│ • All fields?       │
│ • Correct types?    │
└─────────┬───────────┘
          │ ✓
          ▼
┌─────────────────────┐
│ Naming Check        │
│ • kebab-case?       │
│ • Descriptive?      │
│ • Correct extension?│
└─────────┬───────────┘
          │ ✓
          ▼
┌─────────────────────┐
│ Structure Check     │
│ • Purpose stated?   │
│ • Workflow clear?   │
│ • Examples included?│
└─────────┬───────────┘
          │ ✓
          ▼
┌─────────────────────┐
│ Tool Appropriateness│
│ • Right tools?      │
│ • Not too many?     │
│ • Not too few?      │
└─────────┬───────────┘
          │ ✓
          ▼
┌─────────────────────┐
│ Content Quality     │
│ • Research-based?   │
│ • Specific?         │
│ • Actionable?       │
└─────────┬───────────┘
          │ ✓
          ▼
     APPROVED
```

## Legend

```
┌─────┐
│ Box │  = Component or Process
└─────┘

   │
   ▼     = Flow direction

   ┼     = Decision point or branch

   ✓     = Successful validation
```

---

These diagrams show how the Architecture Builder system works at different levels of detail, from high-level architecture to specific generation flows.
