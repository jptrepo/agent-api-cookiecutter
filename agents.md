# 🤖 Building Agents with agent-api-cookiecutter

This document is designed to help you get started quickly with building powerful AI Agent APIs using this cookiecutter template.

## 📋 What is agent-api-cookiecutter?

The `agent-api-cookiecutter` is a production-ready template for creating structured, scalable AI Agent API projects in Python. It solves one of the most common questions in AI development: **"How should I structure my Agent projects?"**

This cookiecutter provides:
- ✅ **Battle-tested project structure** that scales from prototype to production
- ✅ **Three-layer architecture** for clean separation of concerns
- ✅ **DevOps ready** with Docker, docker-compose, and Makefiles
- ✅ **Modern Python tooling** with FastAPI, Pydantic, and more
- ✅ **Testing infrastructure** included out of the box

## 🏗️ Architecture Overview

The generated projects follow a **three-layer architecture pattern**:

### 1. Infrastructure Layer (`infrastructure/`)
This layer handles all external interactions and technical implementations:
- **API** (`api/`): FastAPI endpoints and request/response models
- **Database** (`db/`): Database connections and repositories
- **LLM Providers** (`llm_providers/`): Integrations with OpenAI, Anthropic, etc.
- **MCP Clients** (`mcp_clients/`): Model Context Protocol clients
- **Monitoring** (`monitoring/`): Logging, metrics, and observability

### 2. Application Layer (`application/`)
This layer contains business logic and service orchestration:
- **Chat Service** (`chat_service/`): Main conversational logic
- **Evaluation Service** (`evaluation_service/`): Testing and evaluation
- **Ingest Documents Service** (`ingest_documents_service/`): Document processing
- **Reset Memory Service** (`reset_memory_service/`): Memory management

### 3. Domain Layer (`domain/`)
This layer defines core business logic and models:
- **Memory** (`memory/`): Conversation history and state management
- **Prompts** (`prompts/`): LLM prompts and templates
- **Tools** (`tools/`): Agent tools and capabilities
- **Exceptions** (`exceptions.py`): Custom error types
- **Utils** (`utils.py`): Helper functions

## 🚀 Getting Started

### Prerequisites

Install Cookiecutter:
```bash
pip install -U cookiecutter
```

### Creating a New Project

Generate a new agent project:
```bash
cookiecutter https://github.com/neural-maze/agent-api-cookiecutter.git
```

You'll be prompted for:
- **full_name**: Your name (default: "Miguel Otero Pedrido")
- **package_name**: Package name (default: "agent-api")
- **project_name**: Human-readable project name (default: "Agent API")
- **project_short_description**: Brief description
- **first_version**: Initial version (default: "0.1.0")

### Project Structure

After generation, you'll have:

```
your-agent-api/
├── Dockerfile              # Container definition
├── Makefile               # Common commands
├── README.md              # Project documentation
├── docker-compose.yaml    # Multi-container setup
├── pyproject.toml         # Python project config
├── data/                  # Data files and datasets
├── notebooks/             # Jupyter notebooks for experimentation
├── static/                # Static assets
├── src/
│   └── your_project/
│       ├── config.py              # Configuration management
│       ├── application/           # Business logic services
│       ├── domain/                # Core domain models
│       └── infrastructure/        # Technical implementations
└── tests/                 # Test suite
    ├── conftest.py        # Pytest configuration
    └── test_*.py          # Test files
```

## 🛠️ Development Workflow

### 1. Initial Setup

After creating your project:

```bash
cd your-agent-api

# Install dependencies using uv (recommended)
pip install uv
uv sync

# Or use pip
pip install -e ".[dev]"

# Set up pre-commit hooks
pre-commit install
```

### 2. Configure Your Agent

Edit `src/your_project/config.py` to add your settings:

```python
from pydantic_settings import BaseSettings, SettingsConfigDict

class Settings(BaseSettings):
    model_config = SettingsConfigDict(
        env_file=".env", 
        extra="ignore", 
        env_file_encoding="utf-8"
    )
    
    # Add your configuration
    openai_api_key: str = ""
    model_name: str = "gpt-4"
    temperature: float = 0.7
    # ... more settings

settings = Settings()
```

### 3. Implement Your Services

Start with the application layer services:

**Chat Service Example:**
```python
# src/your_project/application/chat_service/__init__.py

from your_project.domain.tools import get_tools
from your_project.infrastructure.llm_providers import get_llm_client

async def chat(message: str, conversation_id: str):
    """Main chat logic"""
    # 1. Get conversation history from memory
    # 2. Prepare prompt with context
    # 3. Call LLM with tools
    # 4. Process response
    # 5. Update memory
    return response
```

### 4. Add Domain Logic

Define your tools and prompts:

```python
# src/your_project/domain/tools/__init__.py

def get_tools():
    """Define agent tools/capabilities"""
    return [
        {
            "name": "search_documents",
            "description": "Search through ingested documents",
            "parameters": {...}
        },
        # ... more tools
    ]
```

### 5. Set Up Infrastructure

Configure your API endpoints:

```python
# src/your_project/infrastructure/api/main.py

@app.post("/chat")
async def chat(request: ChatRequest):
    """Chat endpoint"""
    from your_project.application.chat_service import chat
    response = await chat(request.message, request.conversation_id)
    return {"response": response}
```

### 6. Run Locally

```bash
# Using Docker (recommended)
make start-project

# Or directly with FastAPI
fastapi dev src/your_project/infrastructure/api/main.py

# Or with uvicorn
uvicorn your_project.infrastructure.api.main:app --reload
```

Visit `http://localhost:8000/docs` for interactive API documentation.

### 7. Test Your Agent

```bash
# Run tests
pytest

# Run with coverage
pytest --cov=src

# Run specific test
pytest tests/test_your_project.py::test_chat
```

## 💡 Best Practices

### Separation of Concerns
- **Infrastructure**: Keep external dependencies here (APIs, databases)
- **Application**: Business logic and orchestration only
- **Domain**: Pure business rules, no external dependencies

### Configuration Management
- Use `.env` files for secrets (never commit these!)
- Use `config.py` for application settings
- Environment-specific configs in `docker-compose.yaml`

### Tool Development
1. Define tool schema in `domain/tools/`
2. Implement tool logic as pure functions
3. Register tools in your LLM client
4. Test tools independently

### Memory Management
- Store conversation history efficiently
- Implement memory summarization for long conversations
- Consider different memory types (short-term, long-term, episodic)

### Testing Strategy
- Unit tests for domain logic
- Integration tests for services
- API tests for endpoints
- Use fixtures in `conftest.py`

## 🔧 Common Patterns

### Adding a New Endpoint

1. Define the model in `infrastructure/api/models.py`:
```python
class NewFeatureRequest(BaseModel):
    param: str
```

2. Add the endpoint in `infrastructure/api/main.py`:
```python
@app.post("/new-feature")
async def new_feature(request: NewFeatureRequest):
    from your_project.application.new_service import process
    return await process(request.param)
```

3. Create the service in `application/new_service/`:
```python
# application/new_service/__init__.py
async def process(param: str):
    # Implementation
    pass
```

### Adding a New Tool

1. Define the tool in `domain/tools/your_tool.py`:
```python
def your_tool(param: str) -> dict:
    """Tool description for the LLM"""
    # Tool implementation
    return result
```

2. Register it in `domain/tools/__init__.py`:
```python
TOOLS = [
    {
        "name": "your_tool",
        "function": your_tool,
        "description": "What this tool does",
        "parameters": {...}
    }
]
```

### Integrating a New LLM Provider

1. Create a provider module in `infrastructure/llm_providers/`:
```python
# infrastructure/llm_providers/new_provider.py
class NewProviderClient:
    def __init__(self, api_key: str):
        self.client = SomeSDK(api_key=api_key)
    
    async def chat(self, messages, tools=None):
        # Implementation
        pass
```

2. Update the factory in `infrastructure/llm_providers/__init__.py`

## 📚 Resources

- **Main Repository**: [neural-maze/agent-api-cookiecutter](https://github.com/neural-maze/agent-api-cookiecutter)
- **The Neural Maze Newsletter**: [theneuralmaze.substack.com](https://theneuralmaze.substack.com/)
- **YouTube Channel**: [The Neural Maze](https://www.youtube.com/@TheNeuralMaze)

## 🤝 Contributing

This template is open source (MIT License). Contributions, feedback, and suggestions are welcome!

## 🎯 Example Use Cases

This cookiecutter is perfect for:
- 🤖 **Conversational AI agents** with memory and tools
- 📚 **RAG (Retrieval-Augmented Generation)** systems
- 🔧 **Function-calling agents** that interact with external APIs
- 📊 **Data analysis agents** that process and visualize information
- 🎓 **Educational chatbots** with specialized knowledge
- 💼 **Customer support automation** with context awareness

## ⚡ Quick Tips

1. **Start Small**: Begin with a simple chat endpoint, then add complexity
2. **Use Notebooks**: The `notebooks/` folder is perfect for experimenting with prompts and tools
3. **Environment Variables**: Always use `.env` for API keys and secrets
4. **Docker First**: Use Docker for consistent environments across dev/prod
5. **Test Early**: Write tests as you build to catch issues quickly
6. **Monitor**: Add logging and metrics from the start
7. **Iterate**: The structure supports refactoring as your agent evolves

## 🐛 Troubleshooting

### Common Issues

**Import errors after generation:**
```bash
pip install -e ".[dev]"
```

**Docker build fails:**
```bash
docker compose build --no-cache
```

**Tests not finding modules:**
```bash
export PYTHONPATH="${PYTHONPATH}:${PWD}/src"
```

**Pre-commit hooks failing:**
```bash
pre-commit run --all-files
```

---

**Happy Agent Building! 🚀**

For questions or issues, visit the [GitHub repository](https://github.com/neural-maze/agent-api-cookiecutter) or join the discussion on [The Neural Maze](https://theneuralmaze.substack.com/).
