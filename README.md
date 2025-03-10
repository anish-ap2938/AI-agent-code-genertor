# AI-agent-code-genertor
# AI Agents for Code Generation

This project leverages multiple AI agents to generate code based on user prompts. By integrating various components—including document retrieval, natural language understanding, and code generation—the system assists users in producing valid code snippets, along with descriptive explanations and file naming suggestions.

## Project Overview

The project uses a ReAct-style agent architecture to connect different AI components, each specialized in specific tasks:
- **Documentation Retrieval:**  
  A QueryEngineTool reads API documentation from local files and other data sources.
- **Code Reading:**  
  A custom tool reads existing code files to provide context and support code generation.
- **Code Generation:**  
  Two LLMs are integrated:
  - **Mistral:** Serves as the primary language model for general query understanding.
  - **CodeLlama:** Specializes in generating valid code in response to user prompts.

The overall flow is as follows:
1. **Data Ingestion:**  
   The system loads documents (including PDFs) from a data directory using a `SimpleDirectoryReader` and processes them with a parser (LlamaParse). It then builds a vector index using an embedding model.
2. **Tool Setup:**  
   Two main tools are integrated:
   - **API Documentation Tool:** Uses the query engine to provide context from the loaded documents.
   - **Code Reader Tool:** Reads and returns the contents of code files.
3. **Agent Interaction:**  
   A ReActAgent is created using the code generation LLM (CodeLlama) along with the tools. The agent accepts user prompts, generates code along with a description, and outputs a filename suggestion.
4. **Post-Processing:**  
   A QueryPipeline with a PydanticOutputParser processes the generated response into structured JSON (fields include code, description, and filename) which is then printed and saved as a file.

## Technologies Used

- **Python 3.x**  
  The main programming language.
- **Flask**  
  Demonstrated via a sample CRUD API (see `test.py`) to showcase integration with generated code.
- **llama_index and LlamaParse**  
  For document reading, vector indexing, and natural language query processing.
- **ReActAgent (from llama_index)**  
  To orchestrate the interactions between tools and LLMs.
- **Ollama LLM Interface:**  
  - **Mistral:** General language understanding and query processing.
  - **CodeLlama:** Specialized in code generation tasks.
- **Pydantic**  
  For defining and validating structured output (e.g., code, description, filename).
- **dotenv**  
  To manage environment variables.
- **Requests**  
  Used in example scripts (e.g., `create_item_script.py`) for making HTTP requests.
- **Additional Dependencies:**  
  See `requirements.txt` for a complete list, which includes libraries for asynchronous processing, embedding resolution, and more.

## Models Used

- **Mistral:**  
  Utilized via the Ollama API for handling general language processing.
- **CodeLlama:**  
  Employed via the Ollama API for code generation, ensuring the produced code is syntactically valid.
- **BAAI/bge-m3:**  
  A local embedding model (resolved as `local:BAAI/bge-m3`) used for document vectorization and indexing.

## Getting Started

### Prerequisites

- Python 3.x installed on your system.
- Flask (for running the provided CRUD API sample).
- Install required Python packages:
  
  ```bash
  pip install -r requirements.txt
