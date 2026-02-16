# Init Project Skill

## Description
Initialize a new AI agent project using the agent-api-cookiecutter template by gathering requirements through interactive questions.

## Usage
```
@init-project [optional: brief description of the agent]
```

## What This Skill Does
1. Uses AskUserQuestion to gather project requirements
2. Collects information about the agent's purpose, tools, and features
3. Generates appropriate cookiecutter parameters
4. Provides guidance on running the cookiecutter command
5. Offers next steps for development

## Workflow

### Step 1: Understand the Goal
Ask the user about their agent project:
- What is the agent supposed to do?
- Who are the primary users?
- What's the expected scale (prototype, MVP, production)?

### Step 2: Gather Project Details

Use `AskUserQuestion` to collect:

**Basic Information:**
- Project name (human-readable)
- Package name (Python package format, e.g., "my-agent-api")
- Short description (one sentence)
- Your name (for attribution)

**Technical Requirements:**
- Which LLM provider(s)? (OpenAI, Anthropic, local models, etc.)
- Need for vector database? (Pinecone, Weaviate, Chroma, etc.)
- Need for traditional database? (PostgreSQL, MongoDB, etc.)
- Authentication required?
- Deployment target? (Docker, K8s, serverless, local)

**Agent Capabilities:**
- What tools/capabilities does the agent need?
  - Web search
  - Code execution
  - File operations
  - API integrations
  - Custom domain tools
- Does it need memory/conversation history?
- RAG (Retrieval-Augmented Generation) required?
- Multi-step reasoning or simple Q&A?

**Special Requirements:**
- Real-time requirements?
- Streaming responses needed?
- Evaluation/testing requirements?
- Monitoring/observability needs?

### Step 3: Create Project Initialization Guide

Based on gathered information, provide:

1. **Cookiecutter Command:**
```bash
cookiecutter https://github.com/neural-maze/agent-api-cookiecutter.git \
  --no-input \
  full_name="[User Name]" \
  package_name="[package-name]" \
  project_name="[Project Name]" \
  project_short_description="[Description]" \
  first_version="0.1.0"
```

2. **Required Dependencies:**
List additional packages needed beyond the template defaults:
```toml
[project]
dependencies = [
    # Template defaults
    "typer",
    "fastapi[standard]",
    "loguru",
    "pydantic",
    "pydantic-settings",
    "ipykernel",
    
    # Add based on requirements:
    # "openai",  # for OpenAI
    # "anthropic",  # for Claude
    # "pinecone-client",  # for vector store
    # "psycopg2-binary",  # for PostgreSQL
    # etc.
]
```

3. **Environment Variables:**
Create `.env.example` content:
```
# LLM Configuration
OPENAI_API_KEY=your_key_here
MODEL_NAME=gpt-4-turbo-preview

# Database (if needed)
DATABASE_URL=postgresql://user:pass@localhost/dbname

# Vector Store (if needed)
PINECONE_API_KEY=your_key_here
PINECONE_ENVIRONMENT=us-west1-gcp

# Application Settings
LOG_LEVEL=INFO
MAX_CONVERSATION_HISTORY=10
```

4. **Initial Architecture Decisions:**
Document key decisions:
- Which layer implements what
- Tool organization strategy
- Memory management approach
- Error handling patterns

### Step 4: Generate Next Steps Document

Create a prioritized development plan:

**Phase 1: Setup & Configuration**
- [ ] Run cookiecutter command
- [ ] Create virtual environment
- [ ] Install dependencies
- [ ] Set up .env file
- [ ] Run initial tests to verify setup

**Phase 2: Core Infrastructure**
- [ ] Configure LLM provider client(s)
- [ ] Set up database connections (if needed)
- [ ] Implement basic logging and monitoring
- [ ] Create health check endpoint

**Phase 3: Domain Layer**
- [ ] Define core tools (list specific tools)
- [ ] Create prompt templates
- [ ] Design memory structure
- [ ] Implement domain exceptions

**Phase 4: Application Layer**
- [ ] Implement chat service
- [ ] Add tool orchestration
- [ ] Implement memory management
- [ ] Add evaluation logic (if needed)

**Phase 5: API Layer**
- [ ] Complete API endpoints
- [ ] Add request validation
- [ ] Implement error responses
- [ ] Add authentication (if needed)

**Phase 6: Testing & Refinement**
- [ ] Write unit tests
- [ ] Create integration tests
- [ ] Test tool execution
- [ ] Perform end-to-end testing

**Phase 7: Documentation & Deployment**
- [ ] Update README with specific details
- [ ] Document API endpoints
- [ ] Create deployment guide
- [ ] Set up CI/CD (optional)

### Step 5: Tool Specifications

For each identified tool, create a specification:

```markdown
## Tool: [Tool Name]

**Purpose:** [What the tool does]

**Location:** `src/{project}/domain/tools/{tool_name}.py`

**Function Signature:**
```python
async def {tool_name}({parameters}) -> {return_type}:
    """[Description]"""
```

**LLM Schema:**
```python
{
    "name": "{tool_name}",
    "description": "[Description for LLM]",
    "parameters": {
        "type": "object",
        "properties": {
            # parameter definitions
        },
        "required": ["param1", "param2"]
    }
}
```

**Dependencies:** [External APIs, databases, etc.]

**Error Handling:** [Expected errors and how to handle them]

**Tests:** [Test cases to implement]
```

### Step 6: Prompt Template Suggestions

Based on agent purpose, suggest prompt structures:

```python
# src/{project}/domain/prompts/system_prompt.py

SYSTEM_PROMPT = """
You are [agent description].

Your capabilities include:
- [Capability 1]
- [Capability 2]
- [Capability 3]

Guidelines:
- [Guideline 1]
- [Guideline 2]

When using tools:
- [Tool usage guideline]
"""

USER_PROMPT_TEMPLATE = """
Context: {context}

User Query: {query}

Conversation History:
{history}

Please respond appropriately.
"""
```

## Example Interaction

**User:** "@init-project I want to create a customer support agent"

**Claude (using this skill):**

Great! Let me help you initialize a customer support agent project. I'll need to gather some information.

**Question 1: Project Details**
What would you like to name this project? (e.g., "Customer Support Agent")

> [User responds: "SmartSupport Agent"]

What package name should we use? (lowercase with hyphens, e.g., "smart-support-agent")

> [User responds: "smart-support-agent"]

Please provide a brief description:

> [User responds: "AI-powered customer support agent with ticket management"]

Your name for project attribution:

> [User responds: "Jane Smith"]

**Question 2: LLM Configuration**
Which LLM provider do you want to use?
1. OpenAI (GPT-4/GPT-3.5)
2. Anthropic (Claude)
3. Both
4. Other

> [User responds: "1"]

**Question 3: Data Storage**
Does your agent need to:
- Store customer conversation history? (yes/no)
- Access a knowledge base? (yes/no)
- Search through documents? (yes/no)

> [User responds: "yes, yes, yes"]

**Question 4: Required Capabilities**
What tools does your agent need? (select all that apply)
- [ ] Search knowledge base
- [ ] Create support tickets
- [ ] Update ticket status
- [ ] Send notifications
- [ ] Escalate to human agent
- [ ] Custom: [specify]

> [User responds: checks first 4 options]

**Question 5: Deployment**
How will you deploy this?
1. Docker (local or cloud)
2. Kubernetes
3. Serverless
4. Direct deployment

> [User responds: "1"]

---

Based on your responses, here's your initialization guide:

[Provides complete initialization guide with commands, configuration, and next steps]

## Output Format

The skill should generate:
1. **project-init-guide.md** - Complete setup guide
2. **requirements-summary.md** - Gathered requirements
3. **architecture-decisions.md** - Key design decisions
4. **development-roadmap.md** - Phased implementation plan

All documents should be saved in a `docs/` directory for reference during development.

## Integration with Other Skills

This skill works with:
- `@generate-prd` - Creates a detailed PRD from gathered requirements
- `@create-plan` - Develops a detailed implementation plan
- Implementation skills - Uses the gathered information for code generation

## Best Practices

1. **Be Interactive:** Ask clarifying questions rather than making assumptions
2. **Provide Examples:** Show examples for each answer to guide users
3. **Explain Choices:** Help users understand implications of their decisions
4. **Suggest Defaults:** Offer reasonable defaults for common scenarios
5. **Document Everything:** Create comprehensive documentation for future reference
6. **Validate Input:** Ensure package names, versions, etc. follow conventions
7. **Consider Scale:** Ask about expected usage to guide architecture decisions

## Common Scenarios

### Scenario 1: RAG-based Agent
Focus on:
- Vector database selection
- Document chunking strategy
- Embedding model choice
- Retrieval optimization

### Scenario 2: Tool-heavy Agent
Focus on:
- Tool organization
- Error handling between tools
- Tool result formatting
- Caching strategies

### Scenario 3: Multi-agent System
Focus on:
- Agent coordination
- Shared context management
- Task routing
- Result aggregation

### Scenario 4: Production-grade Agent
Focus on:
- Monitoring and observability
- Error tracking
- Performance optimization
- Security considerations
- Rate limiting
- Scaling strategy

## Notes

- This skill is designed to be the **first step** in project creation
- It should gather information, not implement code
- All gathered data should be documented for use by other skills
- The output should be actionable and specific
- Consider the user's expertise level and provide appropriate detail
