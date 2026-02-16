# Claude Skills for agent-api-cookiecutter

This directory contains Claude Code skills to help you efficiently initialize and develop projects using the agent-api-cookiecutter template.

## Available Skills

### 1. `init-project.md`
**Purpose:** Initialize a new AI agent project by gathering requirements through interactive questions.

**Usage:**
```
@init-project [optional: brief description of the agent]
```

**What it does:**
- Uses AskUserQuestion to gather project requirements
- Collects information about the agent's purpose, tools, and features
- Generates appropriate cookiecutter parameters
- Provides guidance on running the cookiecutter command
- Offers next steps for development

**Best for:**
- Starting a new project from scratch
- Understanding what information is needed
- Getting guidance on project setup

---

### 2. `generate-prd.md`
**Purpose:** Generate a comprehensive Product Requirements Document (PRD) for your AI agent project.

**Usage:**
```
@generate-prd [optional: project context or existing requirements]
```

**What it does:**
- Creates detailed functional and non-functional requirements
- Documents user personas and use cases
- Defines success metrics and acceptance criteria
- Establishes technical constraints and assumptions
- Provides a foundation for implementation planning

**Best for:**
- Converting ideas into structured requirements
- Documenting project scope and objectives
- Creating a reference for development teams
- Establishing clear success criteria

---

### 3. `create-plan.md`
**Purpose:** Create a detailed, actionable development plan for implementing your AI agent project.

**Usage:**
```
@create-plan [optional: reference to PRD or project context]
```

**What it does:**
- Analyzes project requirements and architecture
- Creates a prioritized, phased implementation plan
- Breaks down work into manageable tasks
- Identifies dependencies and critical path
- Provides effort estimates and milestones
- Maps tasks to the cookiecutter template structure

**Best for:**
- Converting requirements into actionable tasks
- Planning sprints and milestones
- Understanding implementation dependencies
- Resource allocation and scheduling

---

## Recommended Workflow

### Option 1: Comprehensive Approach
Perfect for complex projects or teams that need detailed planning:

```
1. @init-project → Gather basic requirements
2. @generate-prd → Create detailed specifications
3. @create-plan → Develop implementation roadmap
4. Start coding → Use the plan to guide development
```

### Option 2: Quick Start
For experienced developers or simple projects:

```
1. @init-project → Quick setup
2. Start coding → Begin implementation immediately
3. @generate-prd or @create-plan → Add detail as needed
```

### Option 3: Iterative Approach
For evolving requirements:

```
1. @init-project → Initial setup
2. @create-plan → High-level plan
3. Develop MVP → Build core features
4. @generate-prd → Document learnings
5. @create-plan → Plan next phase
```

---

## How to Use These Skills

### In Claude Code / Claude Chat:

1. **Reference the skill** using the `@` symbol:
   ```
   @init-project I want to build a customer support agent
   ```

2. **Provide context** when available:
   ```
   @generate-prd 
   Context: We have a SaaS product with 10k users. 
   Need an agent to handle tier-1 support questions.
   ```

3. **Chain skills together**:
   ```
   @init-project Create a RAG agent for documentation
   [After completion]
   @generate-prd Use the information from init-project
   ```

### Tips for Best Results:

1. **Be Specific:** Provide as much context as possible
   - ❌ "Create an agent"
   - ✅ "Create a customer support agent that handles billing questions using our Stripe API"

2. **Answer Questions Thoughtfully:** Skills use `AskUserQuestion` - take time to provide complete answers

3. **Review and Iterate:** Generated documents are starting points - review and refine them

4. **Keep Documents Together:** Save generated PRDs and plans in your project's `docs/` directory

5. **Update as You Go:** Keep plans and PRDs updated as requirements change

---

## Customizing Skills

These skills are markdown files - you can customize them:

1. **Fork the repository**
2. **Edit the skill files** in `.claude/skills/`
3. **Adjust prompts, questions, and templates** to match your workflow
4. **Add new skills** by creating new `.md` files in this directory

---

## Example: Complete Workflow

### Scenario: Building a Documentation Q&A Agent

**Step 1: Initialize Project**
```
@init-project Build a documentation Q&A agent with RAG
```

Claude will ask questions about:
- Project name and details
- LLM provider (OpenAI, Anthropic, etc.)
- Vector database choice
- Required capabilities
- Deployment target

**Step 2: Generate PRD**
```
@generate-prd Create a PRD for the documentation agent we discussed
```

Claude will produce a comprehensive PRD including:
- Problem statement and solution overview
- User personas (developers, support team, end-users)
- Functional requirements (search, answer, cite sources)
- Non-functional requirements (response time, accuracy)
- Success metrics
- Implementation phases

**Step 3: Create Development Plan**
```
@create-plan Use the PRD to create a 6-week development plan with 2 developers
```

Claude will generate:
- 6 phases of development
- Detailed task breakdown
- Dependency graph
- Resource allocation
- Risk management plan
- Testing strategy

**Step 4: Execute**

Run the cookiecutter:
```bash
cookiecutter https://github.com/neural-maze/agent-api-cookiecutter.git
```

Follow the implementation plan, phase by phase.

---

## Additional Resources

- **agents.md** - Comprehensive guide to building agents with this cookiecutter
- **CLAUDE.md** - Claude-specific development guidance
- **README.md** - Main repository documentation

---

## Contributing

Have ideas for new skills or improvements? Contributions are welcome!

1. Create a new skill file in `.claude/skills/`
2. Follow the format of existing skills
3. Include clear descriptions, usage examples, and workflows
4. Test with Claude Code
5. Submit a pull request

---

## Support

For questions or issues:
- Review the main documentation: `agents.md` and `CLAUDE.md`
- Check the repository: [neural-maze/agent-api-cookiecutter](https://github.com/neural-maze/agent-api-cookiecutter)
- Join the discussion: [The Neural Maze Newsletter](https://theneuralmaze.substack.com/)

---

**Happy Building! 🚀**
