# 🤖 Agentic RAG — Multi-Agent Retrieval-Augmented Generation

**An AI-powered system combining semantic search, Retrieval-Augmented Generation (RAG), and specialized LLM agents for code assistance, mathematical explanations, and HR-related queries.**

[![Hugging Face](https://img.shields.io/badge/LLM-SmolLM2-orange)](https://huggingface.co/HuggingFaceTB/SmolLM2-360M-Instruct)

## 📌 Overview

Agentic RAG is a Python-based AI project that explores the combination of retrieval-augmented generation and specialized language-model agents.

The system uses semantic embeddings and FAISS to retrieve relevant information from a knowledge source. The retrieved context can then be incorporated into prompts for a language model to generate context-aware responses.

The project also includes specialized agents for code assistance, mathematics, and HR-related questions, demonstrating how LLMs can be adapted to different tasks using role-specific prompts and knowledge.

## ✨ Key Features

- **Retrieval-Augmented Generation:** Retrieves relevant information to provide contextual grounding for generated responses.
- **Semantic Search:** Uses Sentence Transformers to convert text and queries into vector embeddings.
- **FAISS Vector Search:** Performs efficient similarity search over document embeddings.
- **Specialized AI Agents:** Includes Code, Math, and HR agents with task-specific instructions.
- **Local LLM Inference:** Uses Hugging Face Transformers with the SmolLM2-360M-Instruct model.
- **Document Processing:** Supports loading text documents and splitting them into smaller chunks for retrieval.
- **Modular Architecture:** Separates retrieval, document loading, and agent logic into reusable Python modules.

## 🏗️ System Architecture

```text
             User Query
                  |
                  v
        +--------------------+
        | Specialized Agent  |
        +--------------------+
                  |
          +-------+--------+
          |                |
          v                v
    Load Knowledge    User Question
          |                |
          v                |
    Text Chunking           |
          |                |
          v                |
    Text Embeddings         |
          |                |
          v                |
     FAISS Index <----------+
          |
          v
   Retrieve Top-K Chunks
          |
          v
    Context Construction
          |
          v
    Prompt Construction
          |
          v
   SmolLM2-360M-Instruct
          |
          v
    Generated Response
```

*The Code Agent follows the retrieval-based workflow. The Math and HR agents use task-specific prompts, with the HR agent also incorporating predefined HR knowledge.*

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Hugging Face Transformers | LLM inference |
| SmolLM2-360M-Instruct | Text generation |
| Sentence Transformers | Text and query embeddings |
| all-MiniLM-L6-v2 | Embedding model |
| FAISS | Vector indexing and similarity search |
| NumPy | Numerical operations and embedding arrays |
| scikit-learn | Cosine similarity experimentation |

## 📂 Project Structure

```text
agentic_RAG/
│
├── agentic_rag/
│   ├── agents/
│   │   ├── code_agent.py
│   │   ├── math_agent.py
│   │   └── hr_agent.py
│   │
│   ├── rag/
│   │   ├── loader.py
│   │   ├── retriever.py
│   │   ├── embeddings.py
│   │   └── vector_store.py
│   │
│   ├── data/
│   │   └── python.txt
│   │
│   ├── rag_app.py
│   ├── basic_llm.py
│   ├── test_agents.py
│   ├── test_code_agent.py
│   └── test_retriever.py
│
└── README.md
```

*This tree illustrates the intended module organization; adjust folder names to match the actual repository layout.*

## ⚙️ How It Works

### 1. Document Loading and Chunking

The document loader reads text files and splits the content into smaller chunks to make retrieval more manageable.

### 2. Embedding Generation

The `all-MiniLM-L6-v2` model converts document chunks into numerical vector representations.

### 3. Vector Indexing

FAISS creates a vector index using `IndexFlatL2`, enabling nearest-neighbor search over the stored embeddings.

### 4. Context Retrieval

When a query is received, the retriever embeds it and searches for the top three most relevant document chunks.

### 5. Agent-Specific Processing

The system provides different agents for different tasks:

- **Code Agent:** Retrieves relevant programming knowledge and generates software-related responses.
- **Math Agent:** Answers mathematical questions with instructions to explain the reasoning clearly.
- **HR Agent:** Answers HR-related questions using predefined HR knowledge and task-specific prompting.

### 6. Response Generation

The Hugging Face Transformers pipeline runs `SmolLM2-360M-Instruct` to generate a response based on the supplied prompt and context.

## 🚀 Getting Started

### Prerequisites

- Python 3.x
- pip
- Internet access for downloading model files on the first run
- Sufficient RAM and storage for the embedding and language models

### 1. Clone the Repository

```bash
git clone https://github.com/prasanthrenamgi/agentic_RAG.git
cd agentic_RAG
```

### 2. Create a Virtual Environment

**Windows:**

```bash
python -m venv .venv
.venv\Scripts\activate
```

**Linux/macOS:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install Dependencies

Install the libraries used by the project:

```bash
pip install numpy scikit-learn sentence-transformers transformers faiss-cpu torch
```

*Note: Use a compatible Python version and PyTorch build for your operating system. A `requirements.txt` file can be added to pin tested dependency versions.*

### 4. Run the RAG Application

From the directory containing `rag_app.py`, run:

```bash
python rag_app.py
```

The application demonstrates retrieving relevant text about Python and binary search, constructing a context-aware prompt, and generating a response with SmolLM2.

### 5. Test the Agents

Run the available test scripts from the project root:

```bash
python test_agents.py
```

To interact with the Code Agent:

```bash
python test_code_agent.py
```

Run the retriever demonstration:

```bash
python test_retriever.py
```

*These commands assume the files are organized into importable `agents` and `rag` packages and that the test scripts are located at the project root. Update paths if your repository differs.*

## 💻 Example Use Cases

**Code Agent**

Example query: `Write a Python function to reverse a list.`

The Code Agent retrieves relevant programming context and generates a response using the language model.

**Math Agent**

Example query: `What is the time complexity of binary search?`

The Math Agent generates a response with instructions to explain the reasoning.

**HR Agent**

Example query: `What happens during employee onboarding?`

The HR Agent uses its predefined HR knowledge to generate a relevant answer.

## 🔬 Additional Experiments

The project also includes experiments involving:

- Generating embeddings for individual text samples.
- Comparing semantic similarity using cosine similarity.
- Building a standalone FAISS vector index.
- Exploring text generation independently of the RAG pipeline.

## 🔮 Future Enhancements

- Implement dynamic agent selection based on query intent.
- Add conversation memory for multi-turn interactions.
- Support PDF, DOCX, and other document formats.
- Integrate a persistent vector database for larger knowledge collections.
- Add source attribution and retrieval-quality evaluation.
- Build a Streamlit or FastAPI interface.
- Add automated tests and dependency version management.

## 👨‍💻 Author

**Prasanth Renamgi**

GitHub: [@prasanthrenamgi](https://github.com/prasanthrenamgi)

Repository: [Agentic RAG](https://github.com/prasanthrenamgi/agentic_RAG)

---

⭐ If you find this project interesting, consider starring the repository!
