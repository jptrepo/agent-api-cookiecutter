# 🎭 Using agent-api-cookiecutter with Claude Code

This guide helps you leverage Claude (and other AI coding assistants) to build AI Agent APIs efficiently using the agent-api-cookiecutter template.

## 🎯 Purpose

This document provides Claude-specific guidance for:
- Understanding and navigating the three-layer architecture
- Implementing agent features with AI assistance
- Following best practices during AI-assisted development
- Efficiently using the cookiecutter template structure

## 🧭 Architecture Guide for Claude

When working with this template, understand the **three-layer separation**:

### Layer 1: Infrastructure (`src/{project}/infrastructure/`)
**What it contains:** External system interactions
- API endpoints (FastAPI)
- Database connections
- LLM provider clients (OpenAI, Anthropic, etc.)
- MCP (Model Context Protocol) clients
- Monitoring and logging

**When to modify:**
- Adding new API endpoints
- Integrating new LLM providers
- Changing database schemas
- Adding authentication/authorization
- Implementing caching strategies

### Layer 2: Application (`src/{project}/application/`)
**What it contains:** Business logic and service orchestration
- Chat service (main conversational flow)
- Evaluation service (testing & metrics)
- Document ingestion service
- Memory management service

**When to modify:**
- Implementing core agent behavior
- Orchestrating multi-step workflows
- Adding new services
- Defining business rules

### Layer 3: Domain (`src/{project}/domain/`)
**What it contains:** Pure business logic, no external dependencies
- Memory models and strategies
- Prompt templates
- Tool definitions
- Custom exceptions
- Utility functions

**When to modify:**
- Creating new agent tools
- Designing prompt templates
- Defining domain models
- Adding business validations

## 🤖 Claude-Assisted Development Workflow

### Phase 1: Project Initialization

**Prompt Example:**
```
I want to create a new AI agent project using agent-api-cookiecutter.
The agent should [describe your use case].

Please help me:
1. Determine the key features needed
2. Identify required tools/capabilities
3. Plan the implementation approach
```

**What Claude should help with:**
- Understanding requirements
- Choosing appropriate tools
- Planning the architecture
- Identifying dependencies

### Phase 2: Configuration Setup

**Prompt Example:**
```
Help me set up the configuration for my agent project.
I need to integrate with:
- OpenAI GPT-4 for the main agent
- Pinecone for vector storage
- PostgreSQL for conversation history

Please update config.py with appropriate settings.
```

**What Claude should generate:**
```python
# src/your_project/config.py
from pydantic_settings import BaseSettings, SettingsConfigDict

class Settings(BaseSettings):
    model_config = SettingsConfigDict(
        env_file=".env",
        extra="ignore",
        env_file_encoding="utf-8"
    )
    
    # OpenAI Configuration
    openai_api_key: str
    openai_model: str = "gpt-4-turbo-preview"
    openai_temperature: float = 0.7
    
    # Pinecone Configuration
    pinecone_api_key: str
    pinecone_environment: str
    pinecone_index_name: str
    
    # PostgreSQL Configuration
    database_url: str
    
    # Application Settings
    max_conversation_history: int = 10
    enable_logging: bool = True

settings = Settings()
```

### Phase 3: Tool Development

**Prompt Example:**
```
I need to create a tool that searches through documentation.
The tool should:
- Accept a query string
- Search a vector database
- Return top 3 relevant chunks
- Handle errors gracefully

Please implement this following the template structure.
```

**Expected Implementation:**
```python
# src/your_project/domain/tools/search_docs.py

from typing import List, Dict
from your_project.infrastructure.db.vector_store import vector_store
from your_project.domain.exceptions import ToolExecutionError

async def search_documentation(query: str, top_k: int = 3) -> List[Dict]:
    """
    Search through documentation using vector similarity.
    
    Args:
        query: Search query
        top_k: Number of results to return
    
    Returns:
        List of relevant document chunks
    """
    try:
        results = await vector_store.search(
            query=query,
            top_k=top_k
        )
        return [
            {
                "content": r.content,
                "metadata": r.metadata,
                "score": r.score
            }
            for r in results
        ]
    except Exception as e:
        raise ToolExecutionError(f"Documentation search failed: {str(e)}")

# Tool schema for LLM
SEARCH_DOCS_SCHEMA = {
    "name": "search_documentation",
    "description": "Search through the documentation to find relevant information",
    "parameters": {
        "type": "object",
        "properties": {
            "query": {
                "type": "string",
                "description": "The search query"
            },
            "top_k": {
                "type": "integer",
                "description": "Number of results (default: 3)"
            }
        },
        "required": ["query"]
    }
}
```

### Phase 4: Service Implementation

**Prompt Example:**
```
Implement the chat service that:
1. Retrieves conversation history
2. Builds context with system prompt
3. Calls OpenAI with tools
4. Processes tool calls
5. Saves to memory
6. Returns response

Follow the application layer pattern.
```

**Key Points for Claude:**
- Keep application layer focused on orchestration
- Delegate to domain layer for business logic
- Use infrastructure layer for external calls
- Handle errors appropriately
- Add logging for debugging

### Phase 5: API Endpoints

**Prompt Example:**
```
Add API endpoints for:
1. POST /chat - main conversation endpoint
2. POST /ingest - document ingestion
3. GET /conversations/{id} - retrieve history
4. DELETE /conversations/{id} - clear history

Include request/response models and proper error handling.
```

## 📋 Best Practices for AI-Assisted Development

### 1. Clear Context
Always provide Claude with:
- The specific layer you're working on
- Existing code structure
- Dependencies being used
- Expected behavior

### 2. Incremental Changes
Request changes in small, testable increments:
```
First, let's add the tool definition in domain/tools/
Then we'll integrate it in the application layer.
Finally, we'll expose it via the API.
```

### 3. Follow the Template Patterns
Ask Claude to:
- Match existing code style
- Use the same patterns for similar features
- Maintain layer separation
- Keep consistent naming conventions

### 4. Request Tests
Always ask for tests alongside implementation:
```
Please also create tests for this service in tests/test_chat_service.py
```

### 5. Documentation
Request inline documentation:
```
Add docstrings following Google style for all functions
```

## 🔍 Common Development Tasks

### Adding a New Tool

**Claude Prompt:**
```
Create a new tool called {tool_name} that {description}.
Include:
- Implementation in domain/tools/
- Tool schema for LLM
- Error handling
- Unit tests
- Integration with the chat service
```

### Integrating a New LLM Provider

**Claude Prompt:**
```
Add support for Anthropic Claude in infrastructure/llm_providers/.
It should:
- Support streaming responses
- Handle tool calls
- Match the existing provider interface
- Include error handling and retries
```

### Implementing Memory Strategies

**Claude Prompt:**
```
Implement a conversation memory strategy in domain/memory/ that:
- Stores last N messages
- Summarizes older conversations
- Maintains important context
- Supports different memory types
```

### Adding Evaluation Metrics

**Claude Prompt:**
```
Create an evaluation service in application/evaluation_service/ that:
- Runs test conversations
- Measures response quality
- Tracks tool usage
- Generates reports
```

## 🎨 Code Generation Templates

### Tool Template
```python
# Ask Claude to fill this template
"""
Create a tool that [DESCRIPTION] following this structure:

from typing import [TYPES]
from your_project.domain.exceptions import ToolExecutionError

async def [tool_name]([parameters]) -> [return_type]:
    '''[DOCSTRING]'''
    try:
        # Implementation
        pass
    except Exception as e:
        raise ToolExecutionError(f"[ERROR_MESSAGE]: {str(e)}")

[TOOL_NAME]_SCHEMA = {
    "name": "[tool_name]",
    "description": "[DESCRIPTION]",
    "parameters": {
        # Schema definition
    }
}
"""
```

### Service Template
```python
# Ask Claude to implement following this pattern
"""
Create a service for [FUNCTIONALITY] in application/[service_name]/:

from your_project.domain import [imports]
from your_project.infrastructure import [imports]

class [ServiceName]:
    def __init__(self, config: Settings):
        self.config = config
        # Initialize dependencies
    
    async def [main_method](self, [params]) -> [return_type]:
        '''[DOCSTRING]'''
        # 1. Validate input
        # 2. Retrieve needed data
        # 3. Process/orchestrate
        # 4. Save state
        # 5. Return result
        pass
"""
```

### API Endpoint Template
```python
# Ask Claude to create endpoint following this structure
"""
Add an endpoint for [FUNCTIONALITY]:

@app.post("/[endpoint]")
async def [endpoint_name](request: [RequestModel]):
    '''[DOCSTRING]'''
    try:
        result = await [service_function](request)
        return {"status": "success", "data": result}
    except [SpecificException] as e:
        raise HTTPException(status_code=400, detail=str(e))
    except Exception as e:
        raise HTTPException(status_code=500, detail="Internal server error")
"""
```

## 🧪 Testing with Claude

### Request Test Generation
```
Please create comprehensive tests for [feature] including:
- Unit tests for domain logic
- Integration tests for services
- API endpoint tests
- Mock external dependencies
- Cover edge cases and errors
```

### Test Structure
```python
# tests/test_[feature].py
import pytest
from unittest.mock import Mock, patch

from your_project.domain.tools.search_docs import search_documentation
from your_project.domain.exceptions import ToolExecutionError

@pytest.mark.asyncio
async def test_search_documentation_success():
    """Test successful documentation search"""
    # Arrange
    query = "How to use the API"
    
    # Act
    results = await search_documentation(query)
    
    # Assert
    assert len(results) > 0
    assert "content" in results[0]

@pytest.mark.asyncio
async def test_search_documentation_error():
    """Test error handling in documentation search"""
    with pytest.raises(ToolExecutionError):
        await search_documentation("")
```

## 🔧 Debugging with Claude

### When Something Goes Wrong

**Effective Debug Prompt:**
```
I'm getting this error: [ERROR_MESSAGE]

Here's the relevant code:
[CODE_SNIPPET]

The error occurs when [CONTEXT].

Please help me:
1. Understand what's causing the error
2. Suggest a fix following the template structure
3. Add appropriate error handling
```

### Code Review Request
```
Please review this implementation:
[CODE]

Check for:
- Adherence to template architecture
- Error handling completeness
- Code clarity and documentation
- Potential bugs or edge cases
- Performance considerations
```

## 📚 Reference Patterns

### Dependency Injection
```python
# Good - Dependencies injected
class ChatService:
    def __init__(self, llm_client, memory_store, tools):
        self.llm = llm_client
        self.memory = memory_store
        self.tools = tools

# Ask Claude to follow this pattern
```

### Error Handling
```python
# Good - Specific exceptions with context
try:
    result = await some_operation()
except SpecificError as e:
    logger.error(f"Operation failed: {e}")
    raise DomainException(f"Failed to process: {str(e)}")
```

### Async/Await
```python
# Good - Consistent async usage
async def service_method(self, param: str) -> dict:
    data = await self.repository.fetch(param)
    result = await self.process(data)
    await self.repository.save(result)
    return result
```

## 🚀 Advanced Patterns

### Streaming Responses
```
Implement streaming chat responses that:
- Stream tokens as they arrive
- Handle tool calls mid-stream
- Support cancellation
- Maintain context
```

### Multi-Agent Coordination
```
Create a system where multiple agents:
- Specialize in different tasks
- Share context efficiently
- Coordinate responses
- Handle conflicts
```

### RAG Implementation
```
Implement RAG with:
- Document chunking strategy
- Embedding generation
- Vector search
- Context injection
- Citation tracking
```

## 💡 Pro Tips

1. **Start with Structure**: Ask Claude to explain the layer before coding
2. **Use Examples**: Reference existing template code for patterns
3. **Iterate**: Build incrementally, test frequently
4. **Document**: Request docstrings and comments
5. **Test**: Always ask for tests with implementation
6. **Review**: Have Claude review the generated code
7. **Refactor**: Ask for improvements after initial implementation

## 🎓 Learning Path

### Beginner
1. Understand the three-layer architecture
2. Create simple tools
3. Implement basic chat service
4. Add API endpoints

### Intermediate
5. Implement memory strategies
6. Add multiple LLM providers
7. Create evaluation metrics
8. Implement RAG

### Advanced
9. Multi-agent systems
10. Advanced tool orchestration
11. Production optimization
12. Custom monitoring

## 📖 Additional Resources

- **agents.md**: Detailed architecture and patterns documentation
- **README.md**: Quick start and overview
- **Template Code**: Examples in `{{cookiecutter.package_name}}/`
- **.claude/skills/**: Ready-to-use skill definitions

## 🤝 Working with Claude Skills

This repository includes Claude skills (in `.claude/skills/`) to help initialize projects:
- `init-project.md`: Project initialization workflow
- `generate-prd.md`: PRD generation with requirements gathering
- `create-plan.md`: Development plan creation

Use these skills to streamline project setup:
```
@init-project Help me create a new agent for [use case]
```

---

**Remember:** This template is designed to work seamlessly with AI assistance. The clear separation of concerns and consistent patterns make it easy for Claude to understand and modify the code effectively.

**Happy Coding with Claude! 🎭🤖**
