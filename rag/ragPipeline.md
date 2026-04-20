# replacing google workspace for internal research using local model
need rag
because host local model, small context window

## architecture
### vector database
store documents
eg chromadb, pgvector

### model
ollama host lightweight model

### logic
orchestration framework, eg langgraph or openclaw
to intercept query, search vector db for right content, hand only that content to local model