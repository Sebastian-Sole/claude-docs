# Advanced Context Engineering for Claude Code

This repository demonstrates **advanced context engineering** techniques for Claude Code using the `.claude` directory structure. Advanced context engineering is the practice of providing Claude Code with specialized instructions, custom agents, project rules, and structured workflows to enhance its capabilities and tailor its behavior to your specific project needs.

## What is Advanced Context Engineering?

Advanced context engineering leverages Claude Code's `.claude` directory to:

- Define **custom agents** with specialized roles (e.g., codebase analysis, pattern finding)
- Create **slash commands** for common workflows (e.g., creating tickets, generating plans)
- Establish **project rules** that apply to all interactions (e.g., coding standards, testing requirements)
- Maintain a **knowledge base** of experiences, plans, and tickets
- Build a **structured workflow** for software development tasks

This approach transforms Claude Code from a general-purpose assistant into a specialized development partner that understands your project's context, conventions, and processes.

## Directory Structure

```
.claude/
├── agents/           # Specialized agent prompts for different research tasks
├── commands/         # Custom slash commands for common workflows
├── rules/            # Project-wide rules and coding standards
├── tickets/          # Feature requests, bugs, and task tracking
├── plans/            # Detailed implementation plans
└── experiences/      # Knowledge base of research and decisions
```

### `/agents` - Specialized Agents

Contains prompts that define specialized agent behaviors for different types of work:

- `codebase-analyzer.md` - Analyzes how code works (traces data flow, identifies patterns)
- `codebase-locator.md` - Finds relevant files and code for specific features
- `codebase-pattern-finder.md` - Discovers similar implementations to model after
- `experience-locator.md` - Searches the knowledge base for relevant past work
- `experience-analyzer.md` - Extracts insights from experience documents

These agents are invoked by slash commands to perform focused research tasks.

### `/commands` - Custom Slash Commands

Defines custom workflows accessible via slash commands:

- `/create-ticket` - Creates structured tickets for features, bugs, or tasks
- `/create-plan` - Generates detailed implementation plans with research
- `/implement-plan` - Executes implementation plans step-by-step
- `/research-codebase` - Conducts thorough codebase investigation
- `/commit` - Creates well-formatted git commits
- `/purge-tickets` - Cleans up completed tickets

### `/rules` - Project Rules

Contains rules that apply to all Claude Code interactions:

- `general.mdc` - Core coding standards and best practices
- `coding-standards.md` - Variable naming, code quality guidelines
- `documentation-workflow.md` - How to document code and decisions
- `unit-testing.md` - Unit testing requirements and patterns
- `integration-testing.md` - Integration testing standards
- `project-scope.md` - Project boundaries and focus areas

### `/tickets` - Task Tracking

Stores structured tickets for features, bugs, and enhancements. Each ticket includes:

- Description and user story
- Technical context and requirements
- Acceptance criteria
- Testing requirements
- Definition of done
- Priority and labels

Format: `XXXX-descriptive-name.md` (e.g., `0001-dark-mode-toggle.md`)

### `/plans` - Implementation Plans

Contains detailed implementation plans created from tickets. Each plan includes:

- Current state analysis with file:line references
- Phased implementation approach
- Specific code changes required
- Success criteria (automated and manual)
- Testing strategy
- References to related tickets and research

### `/experiences` - Knowledge Base

Stores research findings, architectural decisions, and lessons learned. This becomes your project's institutional memory that Claude Code can reference in future work.

## Step-by-Step Workflow

### 1. Define Project Rules

Start by customizing the rules in `.claude/rules/` to match your project:

```bash
# Edit existing rules or create new ones
```

### 2. Create a Ticket

When you identify a new feature or bug, create a structured ticket:

```bash
# Use the create-ticket command
/create-ticket

# Or with parameters
/create-ticket "Add dark mode toggle" with high priority
```

This creates a ticket in `.claude/tickets/` with:

- Clear description and acceptance criteria
- Technical requirements
- Testing needs
- Priority level

### 3. Research and Plan

Before implementation, create a detailed plan. You have three options:

**Option A: Plan from ticket only (includes research)**
```bash
/create-plan .claude/tickets/0001-dark-mode-toggle.md
```
Claude will ask if you want to conduct research in the same session or separately in a fresh context window.

**Option B: Plan from ticket + research document (skips automatic research)**
```bash
/create-plan .claude/tickets/0001-dark-mode-toggle.md .claude/experiences/research/dark-mode-analysis.md
```
Claude relies on the provided research and skips automatic research spawning (unless critical gaps are found).

**Option C: Plan from research document only (no ticket required)**
```bash
/create-plan .claude/experiences/research/dark-mode-analysis.md
```
Claude creates a plan based on the research document alone.

**Option D: Start from scratch**
```bash
/create-plan
```
Claude will guide you through providing the necessary information.

The planning process (varies based on option):

1. Reads all provided files completely
2. Conditionally spawns specialized agents to research the codebase in parallel (skipped if research document provided)
3. Identifies existing patterns and integration points
4. Asks clarifying questions about ambiguities
5. Proposes implementation phases
6. Creates a detailed plan with file:line references

### 4. Review and Refine

Review the generated plan:

- Check that phases are properly scoped
- Verify success criteria are specific and measurable
- Ensure all technical details are accurate
- Identify any missing considerations

Iterate with Claude Code to refine the plan until it's complete and actionable.

### 5. Implement

Execute the plan step-by-step:

```bash
# Use the implement command
/implement-plan .claude/plans/0001-dark-mode-toggle.md

# Or manually work through phases
```

During implementation:

- Follow the phased approach in the plan
- Run automated tests after each phase
- Verify manual success criteria
- Document any deviations or discoveries

### 6. Test and Verify

Validate the implementation:

```bash
# Automated verification
pnpm test
pnpm lint
pnpm build

# Manual verification
# - UI/UX testing
# - Performance testing
# - Edge case testing
```

### 7. Document and Commit

Capture your work:

```bash
# Create well-formatted commits
/commit

# Document key learnings in experiences/
# This builds your project's knowledge base
```

### 8. Research When Needed

**For creating research documents (before planning):**

When you have a ticket and want to research thoroughly before creating a plan:

```bash
# Conduct research and save findings
/research-codebase "how authentication works"
```

Save the research output to `.claude/experiences/research/<description>.md`, then use it with `/create-plan`:

```bash
/create-plan .claude/tickets/0001-auth-feature.md .claude/experiences/research/auth-analysis.md
```

**For ad-hoc investigation:**

When you need quick answers without creating a formal plan:

```bash
# Understand specific areas
/research-codebase "how the API endpoints are structured"

# Find patterns
/research-codebase "find all database migration patterns"
```

## Key Benefits

1. **Consistency** - Rules ensure consistent code quality and patterns
2. **Efficiency** - Custom commands streamline repetitive workflows
3. **Knowledge Retention** - Experiences directory preserves context across sessions
4. **Thorough Planning** - Agents perform comprehensive research before implementation
5. **Structured Process** - Clear workflow from ticket to implementation to documentation

## Customization

This repository serves as a template. Customize it for your project:

1. Modify agents to match your analysis needs
2. Create slash commands for your specific workflows
3. Define rules that reflect your team's standards
4. Adapt ticket and plan templates to your process
5. Build your experiences knowledge base over time

## Getting Started

1. Clone or fork this repository
2. Review and customize `.claude/rules/` for your project
3. Try creating a ticket with `/create-ticket`
4. Generate a plan with `/create-plan`
5. Start building your project's knowledge base

## Learn More

- [Claude Code Documentation](https://docs.claude.com/en/docs/claude-code)
- [Custom Agents Guide](https://docs.claude.com/en/docs/claude-code/agents)
- [Slash Commands Reference](https://docs.claude.com/en/docs/claude-code/commands)
- [Project Rules Overview](https://docs.claude.com/en/docs/claude-code/rules)

---

This repository demonstrates the power of advanced context engineering to transform Claude Code into a specialized development partner that understands your project's unique needs and workflows.
