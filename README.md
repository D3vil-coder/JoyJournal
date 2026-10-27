# JoyJournal

JoyJournal is an experimental Streamlit chat application that combines local Ollama models with a persistent memory layer. It uses Mem0 to store user-specific memories in a FAISS vector store and LiteLLM to stream responses from Gemma 3. The repository is a prototype: its environment is not pinned and the setup below has not been reproduced end to end.

## How it works

1. A user enters a username in the Streamlit sidebar. Changing it clears the displayed session history.
2. For each message, the app asks Mem0 to store the user's input and retrieves saved memories for that username with `get_all`.
3. The retrieved memories and current message are sent to `gemma3:4b` through LiteLLM and a local Ollama endpoint. The assistant response is streamed to the interface and added to memory.
4. The sidebar can display saved memories for the entered username.

This implementation retrieves the user's saved memories with `get_all` rather than selecting a measured top-k semantic search result. The displayed chat history is held in Streamlit session state; it is the extracted memories, not necessarily the complete conversation transcript, that are intended to persist. Although the UI title mentions Llama 3.1, the configured response model is Gemma 3.

## Components

- `Main.py`: Streamlit interface, memory configuration and chat flow.
- [Ollama](https://ollama.com/): serves `gemma3:4b` for generation and `nomic-embed-text:latest` for embeddings at `http://localhost:11434`.
- [Mem0](https://docs.mem0.ai/): memory extraction and storage, configured with a FAISS vector store and 768-dimensional embeddings.
- [LiteLLM](https://docs.litellm.ai/): connects the chat response to Ollama's model endpoint.

## Setup

The repository does not include a dependency lock file, and package/API compatibility can change. These are the intended steps from the published code, not a verified one-command installation.

1. Install Python and Ollama, and make sure the Ollama service is running locally.
2. Download the configured models:

   ```bash
   ollama pull gemma3:4b
   ollama pull nomic-embed-text:latest
   ```

3. Clone the repository and install the imported libraries in a virtual environment:

   ```bash
   git clone https://github.com/D3vil-coder/JoyJournal.git
   cd JoyJournal
   python -m pip install streamlit mem0ai litellm faiss-cpu
   ```

4. **Edit `Main.py` before running it.** The FAISS `path` in the memory configuration is hardcoded to the original author's Windows machine. Change it to a suitable local path for your environment and check the installed Mem0 version's FAISS configuration requirements. The Ollama endpoint is also configured as `http://localhost:11434`.
5. Start the app:

   ```bash
   streamlit run Main.py
   ```

Model downloads, dependency installation, the memory store and a complete chat have not been verified as part of this README update. Depending on package versions or platform, additional changes may be required.

## Limitations and privacy

- The username is a label, **not authentication**. Anyone with access to the app who knows or guesses a username can request that user's stored memories. Do not expose this prototype to untrusted users or networks.
- The code configures local Ollama endpoints and a local FAISS path, but that alone does not establish a comprehensive privacy or security guarantee. Review the installed dependencies, logs, storage permissions and network configuration before using sensitive information.
- The program checks whether FAISS reports a GPU, but this is not evidence that its memory index actually runs on a GPU. CPU or GPU performance has not been benchmarked here.
- There is no dependency lock file, automated setup, reproducible evaluation, or demonstrated latency or retrieval-quality benchmark in this repository. `get_all` can also grow the prompt as the number of saved memories increases.
- Exceptions during model streaming are displayed, but memory initialization and storage calls are not covered by that error handler. Check the Streamlit and Ollama logs when troubleshooting.

## Status

This is a personal prototype for exploring persistent conversational memory, not a production-ready or clinical application. See `Main.py` for the implementation and model configuration.

