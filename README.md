#IT Chatbot Assistant

A powerful IT support assistant that combines Retrieval-Augmented Generation (RAG) with local LLM capabilities. This system helps IT support teams with automated troubleshooting, knowledge base retrieval, and ticket triage, reducing response times and improving customer satisfaction.

##  Features

- **Document Processing**
  - Automatic document ingestion and indexing
  - Support for various document formats (PDF, TXT, DOCX)
  - Efficient document chunking and embedding generation

- **Vector Storage**
  - ChromaDB integration for fast and efficient vector search
  - Persistent storage of document embeddings
  - Scalable vector database architecture

- **Local LLM Integration**
  - Ollama integration for local LLM inference
  - GPU acceleration support
  - Customizable model selection

- **Modern Web Interface**
  - OpenWebUI for intuitive user interaction
  - Real-time chat interface
  - Document management dashboard

- **Containerized Architecture**
  - Docker-based deployment
  - Microservices architecture
  - Easy scaling and maintenance

##  Prerequisites

- Docker and Docker Compose
- NVIDIA GPU (recommended for Ollama)
- Git
- At least 8GB RAM
- 20GB free disk space

##  Installation

1. Clone the repository:
```bash
git clone <your-repo-url>
cd <repo-name>
```

2. Configure environment variables (optional):
Create a `.env` file in the root directory:
```bash
CHROMA_HOST=chroma
CHROMA_PORT=8000
OLLAMA_HOST=ollama
OLLAMA_PORT=11434
```

3. Start the services:
```bash
docker-compose up -d
```

##  Service Architecture

The system consists of four main services:

1. **ChromaDB** (Port 8000)
   - Vector database for document embeddings
   - Persistent storage
   - Fast similarity search

2. **Ollama** (Port 11434)
   - Local LLM service
   - GPU-accelerated inference
   - Model management

3. **OpenWebUI** (Port 3000)
   - Web interface
   - Chat functionality
   - Document management

4. **Main Application** (Port 8001)
   - FastAPI backend
   - Document processing
   - Query handling

## Usage:

### 1. Accessing the Web Interface

Open your browser and navigate to:
```
http://localhost:3000
```

### 2. Uploading Documents

Using curl:
```bash
curl -X POST -F "file=@your_document.pdf" http://localhost:8001/upload
```

Using Python:
```python
import requests

files = {'file': open('your_document.pdf', 'rb')}
response = requests.post('http://localhost:8001/upload', files=files)
print(response.json())
```

### 3. Querying the Knowledge Base

Using curl:
```bash
curl -X POST -H "Content-Type: application/json" \
     -d '{"text":"How do I reset my password?"}' \
     http://localhost:8001/query
```

Using Python:
```python
import requests

query = {"text": "How do I reset my password?"}
response = requests.post('http://localhost:8001/query', json=query)
print(response.json())
```

## 🔧 Configuration

### Ollama Model Selection

To use a different model with Ollama:

1. Access the OpenWebUI interface
2. Go to Settings > Models
3. Select your preferred model (e.g., llama2, mistral, etc.)

### ChromaDB Settings

ChromaDB configuration can be modified in `docker-compose.yml`:
```yaml
chroma:
  environment:
    - ALLOW_RESET=true
    - ANONYMIZED_TELEMETRY=false
```

##  Testing

Run the test suite:
```bash
docker-compose exec app python -m pytest
```

##  Troubleshooting

Common issues and solutions:

1. **ChromaDB Connection Issues**
   - Check if ChromaDB is running: `docker-compose ps`
   - Verify port 8000 is not in use
   - Check ChromaDB logs: `docker-compose logs chroma`

2. **Ollama GPU Issues**
   - Verify NVIDIA drivers are installed
   - Check GPU availability: `nvidia-smi`
   - Review Ollama logs: `docker-compose logs ollama`

3. **Document Upload Failures**
   - Check file permissions
   - Verify file format is supported
   - Review application logs: `docker-compose logs app`

##  Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Commit your changes: `git commit -m 'Add feature'`
4. Push to the branch: `git push origin feature-name`
5. Create a Pull Request


## Acknowledgments

- [LlamaIndex](https://github.com/run-llama/llama_index) for the RAG framework
- [ChromaDB](https://github.com/chroma-core/chroma) for vector storage
- [Ollama](https://github.com/ollama/ollama) for local LLM support
- [OpenWebUI](https://github.com/open-webui/open-webui) for the web interface 
