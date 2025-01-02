# Vector Database with Ollama and Milvus

A Docker-based setup for running a vector database system using Milvus, Ollama, and Miniconda. This project enables semantic search capabilities using large language models and efficient vector storage.

## Components

- **Milvus**: Vector database for storing and searching embeddings
- **Ollama**: Local LLM server for generating embeddings
- **Attu**: Web UI for Milvus management
- **Miniconda**: Python environment with Jupyter support

## Prerequisites

- Docker
- Docker Compose
- Make

## Quick Start

1. Build all containers:
```bash
make build
```

2. Start the services:
```bash
make run
```

This will:
- Start all containers
- Pull the required models (llama3.2:3b and mxbai-embed-large)
- Display container logs

3. Access the services:
- Milvus: `localhost:19530`
- Attu UI: `localhost:8080`
- Ollama: `localhost:11434`
- Miniconda: VSCode server

## Project Structure

```
.
├── llama/
│   ├── Dockerfile
│   └── Makefile
├── milvus/
│   ├── Dockerfile
│   └── Makefile
├── miniconda/
│   ├── Dockerfile
│   ├── environment.yml
│   └── Makefile
├── docker-compose.yml
└── Makefile
```

## Configuration

- **Milvus**: Configured for standalone mode with embedded etcd
- **Ollama**: Serves LLM models locally
- **Miniconda**: Python 3.9 environment with basic data science packages
- **Network**: All services communicate through `vectorDB-net` bridge network

## Data Persistence

The setup includes three Docker volumes:
- `milvus_data`: Stores Milvus database files
- `ollama_data`: Stores downloaded LLM models
- `conda_data`: Stores Conda environment data

## Commands

```bash
# Build all images
make build

# Start services
make run

# Clean up containers and volumes
make clean
```

## Development

The Miniconda container includes VSCode server for development. You can access it using Dev Container Extension in VS Code.