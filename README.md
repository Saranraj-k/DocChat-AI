# DocChat-AI

DocChat-AI is an advanced agentic RAG (Retrieval-Augmented Generation) system designed for interactive conversations with your documents. Unlike traditional RAG applications, DocChat-AI leverages a **multi-agent architecture** to enhance reasoning, context retention, and multi-modal document understanding. You can upload documents in various formats (PDF, DOCX, TXT, etc.) and engage in dynamic, context-aware chat with your content.

---
<img width="900" height="545" alt="image" src="https://github.com/user-attachments/assets/20dbe0ab-912c-4ba1-853a-7727510d70cc" />

## 🚀 What Makes DocChat-AI Unique?

### 1. **Multi-Agent Chat vs. Simple RAG**

- **Simple RAG**: 
  - Usually involves chunking a document, retrieving relevant chunks with a retriever (e.g., vector search), and passing them to an LLM to answer a query.
  - Limited to single-step retrieval and response. Struggles with deep reasoning, document synthesis, and multi-turn context.
  - Often loses track of context in long or multi-document scenarios.

- **DocChat-AI (Multi-Agent RAG)**:
  - Utilizes multiple specialized agents, each focused on a key aspect of the conversation (e.g., retrieval, summarization, reasoning, memory, and format handling).
  - Agents collaborate and communicate to break down complex queries, synthesize information from across a document or multiple documents, and maintain a coherent context over long conversations.
  - Supports multi-format documents (PDF, DOCX, TXT, etc.), and routes parsing to the right tool automatically.
  - The system can ask clarifying questions, chain reasoning steps, and perform advanced workflows that mimic human-like document comprehension.

---

## 🛠️ Tools & Techniques Used

### **Core Technologies**
- **Python**: Backbone of the backend logic and orchestration.
- **LLM (Large Language Models)**: Powering the chat and reasoning agents.
- **Vector Embeddings (e.g., FAISS, ChromaDB)**: For semantic document search and retrieval.
- **Document Parsers**: 
  - `pdfminer`, `PyPDF2` for PDFs,
  - `python-docx` for DOCX,
  - Text parsers for TXT/Markdown.
- **LangChain / LlamaIndex** (or similar frameworks): For agent orchestration, retrieval chaining, and context management.
- **FastAPI/Flask**: For serving the application as an API or Web App.
- **Frontend (optional)**: Streamlit or React-based UI for easy document upload and chat.

### **Multi-Agent Architecture**
- **Retriever Agent**: Finds relevant parts of your documents based on query.
- **Memory Agent**: Tracks conversation history, prior retrievals, and context.
- **Reasoning Agent**: Synthesizes retrieved content, reasons across chunks, and generates coherent answers.
- **Format Handler Agent**: Detects and parses different document formats.
- **Orchestrator**: Coordinates agent interactions and manages workflow for each user query.

---

## 🏗️ High-Level System Structure


<img width="799" height="614" alt="image" src="https://github.com/user-attachments/assets/af7ef232-5f8c-4dcb-86df-bfde74798a05" />


The **DocChat-AI** system is structured as a multi-agentic RAG pipeline, designed for intelligent and interactive document chat. The architecture can be understood in the following key stages, as visualized in the diagram above:

---

### 1. **User Query Intake**
- **User query**: The process starts when a user asks a question about their uploaded documents.
- **Analyze relevance**: The system analyzes the user's question to determine if it is within the scope of the document corpus and the system's capabilities.

### 2. **Query Routing**
- **Route query**: Based on the relevance analysis, the system routes the query:
  - **In scope**: If the query is within scope, it advances to the research/answering phase.
  - **Not in scope**: If out of scope, the system can end the process or provide a direct response indicating the limitation.

### 3. **Document Preprocessing & Vectorization**
- **Docling (Text to Markdown)**: Documents are first converted to a unified markdown format for easier chunking and parsing.
- **LangChain (Chunking & Vector Store Building)**:
  - The system splits the markdown file into logical chunks (often based on headers) using LangChain.
  - Chunks are embedded and stored in a vector database (e.g., ChromaDB) for efficient semantic retrieval.

### 4. **Research Loop (Multi-Agentic Reasoning)**
- **Conduct research**: If the query is in scope, the system launches the research loop—an iterative, agentic process for information synthesis:
    - **Generate queries**: The Reasoning Agent formulates sub-queries to target specific information in the vector store.
    - **Retrieve documents**: The Retriever Agent fetches relevant document chunks from the vector store.
- **Verification finished**: After each cycle, the system checks if the information retrieved is sufficient:
    - If **not sufficient**, the loop continues, generating new sub-queries.
    - If **sufficient**, the loop exits and the system composes the final response.

### 5. **Response Generation**
- **Respond**: Once the research loop verifies enough information has been gathered, the system generates and returns a well-formed answer to the user's query, incorporating all relevant context and reasoning.
- **End**: The process concludes, ready for the next user interaction.

---

### 🧩 **Key Components Explained**

- **Docling**: Ensures all documents, regardless of original format (PDF, DOCX, TXT), are normalized to markdown for consistent chunking and parsing.
- **LangChain**: Powers the document chunking logic and constructs the vector database using ChromaDB, enabling fast and accurate semantic search.
- **Vector Store**: The core retrieval system, storing document embeddings for similarity-based search.
- **Multi-Agent Research Loop**: The heart of the architecture—multiple agents collaborate to decompose, retrieve, verify, and synthesize answers in an iterative process, significantly improving the system's reasoning depth and accuracy compared to traditional single-pass RAG.
- **Verification Step**: Ensures that responses are comprehensive and accurate, looping back to research if more information is needed.

---

### ✨ **How This Architecture Excels**

- **Deep Reasoning with Multi-Agent Loops**: Unlike simple RAG models, DocChat-AI uses a research loop with multiple agent roles, allowing it to tackle complex, multi-step queries over long or multiple documents.
- **Format Agnostic**: By converting all inputs to markdown, the system seamlessly supports a variety of document types.
- **Robust Context Handling**: The iterative research loop and memory tracking allow for coherent, context-aware, multi-turn conversations—even with large or diverse document sets.

---

**In summary:**  
This architecture empowers DocChat-AI to deliver intelligent, context-rich, and reliable answers to complex questions over any set of documents, making it a powerful tool for knowledge work, research, and enterprise document analysis.

---

## 📝 Example Use-Cases

- **Legal Research**: Upload lengthy contracts in PDF/DOCX and ask complex, multi-step questions.
- **Academic Study**: Upload papers or notes and have long-form discussions, summaries, or cross-document Q&A.
- **Enterprise Knowledge Base**: Ingest internal docs and chat with them for onboarding, troubleshooting, or process discovery.

---

## 🌟 Key Features

- **Multi-format Support**: Seamlessly handles PDFs, DOCX, TXT, and more.
- **Multi-agent Reasoning**: Breaks down complex queries and provides deeper, context-aware answers.
- **Long Context Handling**: Maintains memory and context over extended, multi-turn conversations.
- **Extensible**: Easily add new parsers, agents, or integrate with different LLM providers.
- **User-friendly UI**: (If enabled) Simple drag & drop for documents, intuitive chat interface.

---

## 🤔 FAQ

**Q: How is this better than a simple document Q&A bot?**  
*A: DocChat-AI maintains context, chains reasoning across multi-turn chats, and works with multiple document formats. The multi-agent system enables deeper understanding and better answers for complex tasks.*

**Q: Can I add support for a new document type?**  
*A: Yes! Simply implement a new parser agent and register it with the orchestrator.*

**Q: Is it secure for sensitive documents?**  
*A: All processing is local (unless you use a cloud LLM), and document data isn't sent outside your environment.*

---

*Happy chatting with your documents!*
