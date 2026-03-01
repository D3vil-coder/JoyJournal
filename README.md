# Local Chatbot with Persistent Memory 🧠

A privacy-focused, local-first chatbot built with **Streamlit**, **Gemma 3**, and **Mem0**. This application features a long-term memory layer that allows the assistant to remember user-specific context across different sessions using a local FAISS vector store.



## 🚀 Features
- **Persistent Memory:** Uses `mem0` to store and retrieve user-specific information.
- **Fully Local:** Powered by **Ollama** (Gemma 3 & Nomic Embeddings)—no data leaves your machine.
- **Multi-User Support:** Personalized memory spaces based on usernames.
- **Hardware Accelerated:** Automatic detection and utilization of FAISS GPU support.
- **Streaming UI:** A smooth, modern chat interface built with Streamlit.

## 🛠️ Tech Stack
- **LLM:** Gemma 3 (via Ollama)
- **Embeddings:** Nomic-Embed-Text (via Ollama)
- **Memory Management:** Mem0
- **Vector Store:** FAISS (Local Index)
- **Frontend:** Streamlit
- **Orchestration:** LiteLLM

## 📋 Prerequisites
1.  **Ollama installed:** [Download here](https://ollama.com/)
2.  **Required Models:**
    ```bash
    ollama pull gemma3:4b
    ollama pull nomic-embed-text:latest
    ```
3.  **FAISS:** - For CPU: `pip install faiss-cpu`
    - For GPU: `pip install faiss-gpu` 

## ⚙️ Configuration
The system is configured to store your memory index locally. Ensure the path in the `config` dictionary exists:
- **Index Path:** `C:\IIT Bombay\AI\Learning Projects\faiss_index\friday_mem.faiss`
- **Embedding Dims:** 768

## 🏃 Getting Started
1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/local-ai-memory.git](https://github.com/your-username/local-ai-memory.git)
    cd local-ai-memory
    ```
2.  **Install dependencies:**
    ```bash
    pip install streamlit mem0 litellm
    ```
3.  **Run the app:**
    ```bash
    streamlit run app.py
    ```

## 🖥️ Usage
1.  **Login:** Enter a unique username in the sidebar. This creates a dedicated memory space.
2.  **Chat:** Talk to the assistant. It will automatically save key facts to its memory.
3.  **View Memory:** Use the **"View My Memory"** button in the sidebar to see what the assistant has learned about you.
