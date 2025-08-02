# Graphiti with Enhanced Gemini Support 🧠⚡

> **Enhanced fork with production-ready Gemini API integration and Docker MCP server**

Build Real-Time Knowledge Graphs for AI Agents with seamless Google Gemini support.

## 🚀 Quick Start with Gemini API

**Get up and running in under 5 minutes:**

### 1. Clone and Setup
```bash
git clone https://github.com/your-username/graphiti.git
cd graphiti/mcp_server
```

### 2. Configure Environment
```bash
cp .env.example .env
# Edit .env with your Gemini API key:
```

```bash
# Neo4j Database Configuration
NEO4J_URI=bolt://neo4j:7687
NEO4J_USER=neo4j
NEO4J_PASSWORD=your_secure_password

# Gemini API Configuration
OPENAI_API_KEY=your_gemini_api_key_here
OPENAI_BASE_URL=https://generativelanguage.googleapis.com/v1beta/openai/
MODEL_NAME=gemini-2.0-flash
EMBEDDER_MODEL_NAME=gemini-embedding-001
SEMAPHORE_LIMIT=3
```

### 3. Start with Docker
```bash
docker-compose up -d
```

**That's it!** Your Graphiti MCP server with Gemini support is running on `http://localhost:8081/sse`

## ✨ What's New in This Fork

### 🔥 Production-Ready Gemini Integration
- **Full Gemini API Support**: LLM inference + embeddings via OpenAI-compatible endpoints
- **Automatic Provider Detection**: Smart switching between OpenAI and Gemini based on configuration
- **Background Task Processing**: Fixed asyncio garbage collection issues for reliable episode processing

### 🐳 Enhanced Docker Setup
- **One-Command Deployment**: Complete setup with `docker-compose up`
- **Secure Configuration**: No hardcoded secrets, all via `.env` files
- **Custom Networking**: Isolated container communication with health checks
- **Remote MCP Access**: SSE transport for seamless AI assistant integration

### 🧠 MCP Server Improvements
- **Multi-Provider Support**: OpenAI, Gemini, and Azure OpenAI ready
- **Robust Background Processing**: Fixed episode queue processing with proper task management
- **Rate Limiting**: Configurable API call limits to prevent throttling
- **Claude Code Integration**: Pre-configured for all Claude Code projects

## 📋 MCP Integration

### For Claude Desktop
Add to your `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "graphiti-memory": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "http://127.0.0.1:8081/sse"
      ]
    }
  }
}
```

### For Claude Code
Add to your `~/.claude.json` (or use our pre-configured setup):
```json
{
  "mcpServers": {
    "graphiti-memory": {
      "command": "npx",
      "args": [
        "-y", 
        "mcp-remote",
        "http://127.0.0.1:8081/sse"
      ]
    }
  }
}
```

## 🔧 Configuration Options

### Gemini API Setup
1. Get your API key from [Google AI Studio](https://aistudio.google.com/)
2. Use the OpenAI-compatible endpoint for seamless integration
3. Choose from available models:
   - **LLM**: `gemini-2.0-flash`, `gemini-1.5-pro`, `gemini-1.5-flash`
   - **Embeddings**: `gemini-embedding-001`, `text-embedding-004`

### Alternative Providers
The enhanced setup also supports:
- **OpenAI**: Direct API integration
- **Azure OpenAI**: Enterprise deployments
- **Local Models**: Via Ollama integration

### Ollama Local Models Setup
For completely local AI operations without cloud dependencies:

1. **Install Ollama** on your host machine: [ollama.ai](https://ollama.ai/)

2. **Pull required models**:
   ```bash
   ollama pull qwen2.5-coder:7b
   ollama pull nomic-embed-text:latest
   ```

3. **Configure .env for Ollama**:
   ```bash
   # Ollama Configuration
   OPENAI_API_KEY=ollama
   MODEL_NAME=qwen2.5-coder:7b
   SMALL_MODEL_NAME=qwen2.5-coder:7b
   EMBEDDER_MODEL_NAME=nomic-embed-text:latest
   OPENAI_BASE_URL=http://host.docker.internal:11434/v1
   SEMAPHORE_LIMIT=1
   ```

4. **Start with Docker**: `docker-compose up -d`

The Docker container automatically connects to your host Ollama instance.

## 🛠 Development Commands

### From Project Root
```bash
# Install dependencies
uv sync --extra dev

# Format code
make format

# Run tests
make test

# Lint code
make lint
```

### MCP Server Development
```bash
cd mcp_server/

# Install dependencies
uv sync

# Run development server
uvicorn graphiti_mcp_server:app --reload --port 8000

# Check logs
docker-compose logs graphiti-mcp -f
```

## 📊 Key Improvements

### Background Task Processing
- **Fixed Garbage Collection**: Proper asyncio task reference management
- **Reliable Episode Processing**: Episodes now process consistently into the knowledge graph
- **Task Lifecycle Management**: Automatic cleanup with error handling

### Security & Configuration
- **Environment-Only Secrets**: No hardcoded credentials in Docker files
- **Comprehensive Documentation**: Updated `.env.example` with all options
- **Docker Best Practices**: Health checks, custom networks, and proper dependency management

### Performance Optimizations
- **Rate Limiting**: Configurable `SEMAPHORE_LIMIT` for API throttling
- **Efficient Networking**: Custom Docker bridge for optimized container communication
- **Background Processing**: Non-blocking episode ingestion with queue management

## 🎯 Use Cases

Perfect for:
- **AI Agent Memory**: Persistent knowledge graphs for conversational AI
- **Real-time RAG**: Dynamic retrieval-augmented generation
- **Enterprise Knowledge Management**: Temporal data with relationship tracking
- **Research & Analysis**: Graph-based information discovery

## 📚 Original Graphiti Features

This fork maintains all original Graphiti capabilities:

- **Real-Time Incremental Updates**: No batch recomputation needed
- **Bi-Temporal Data Model**: Track both event and ingestion times
- **Hybrid Retrieval**: Semantic + keyword + graph traversal search
- **Custom Entity Types**: Flexible Pydantic-based schemas
- **Scalability**: Optimized for large datasets with parallel processing

## 🤝 Contributing

This enhanced fork welcomes contributions! Focus areas:
- Additional LLM provider integrations
- MCP server feature enhancements
- Docker deployment optimizations
- Documentation improvements

## 📖 Documentation

- [Original Graphiti Docs](https://help.getzep.com/graphiti)
- [MCP Server Setup](./mcp_server/README.md)
- [Configuration Guide](./mcp_server/.env.example)

## 🆘 Support

- **Issues**: [GitHub Issues](https://github.com/your-username/graphiti/issues)
- **Discord**: [Zep Community #Graphiti](https://discord.com/invite/W8Kw6bsgXQ)
- **Discussions**: Share your Gemini + Graphiti setups!

---

**⭐ If this enhanced Gemini integration helps your project, please star the repo!**

Built on the foundation of [Zep's Graphiti](https://github.com/getzep/graphiti) with production-ready enhancements for modern AI development.