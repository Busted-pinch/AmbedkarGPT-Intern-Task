# 🚀 AI Text File Based Query Processing Agent
### *RAG-Based · Fully Local · Powered by Ollama + Mistral + ChromaDB*

This project is a **production-grade AI Speech processing Agent** that reads long text, chunks it, embeds it, performs semantic retrieval using ChromaDB, and generates accurate query response using **Mistral LLM through Ollama** — all running **locally** and fully containerized with Docker Compose.

---

# 🧱 Project Structure

AmbedkarGPT-Intern-Task/  
├── main.py              → Main RAG pipeline  
├── requirements.txt     → Python dependencies  
├── speech.txt           → Input file for summarization  
├── docker-compose.yml   → Multi-container setup (App + ChromaDB)  
├── Dockerfile           → Python app image  
├── .dockerignore  
└── README.md

---

# 🧠 Key Features

- Reads any `.txt` document or speech  
- Splits text into overlapping semantic chunks  
- Embeds chunks using Sentence-Transformers  
- Stores embeddings in **ChromaDB**  
- Retrieves relevant chunks via vector similarity  
- Processes queries using **Mistral LLM** via Ollama  
- Fully containerized with Docker Compose  
- Works fully offline — full privacy  
- Reproducible setup and single-command runs

---

# 🛠 Tech Stack

- Python  
- LangChain  
- Sentence-Transformers  
- ChromaDB  
- Ollama (Mistral LLM)  
- Docker & Docker Compose  
- Git

---

# ⚠️ Prerequisites

Install the following before running the project:

- Docker: https://www.docker.com/products/docker-desktop/  
- Git: https://git-scm.com/downloads  
- Ollama (must be installed on the host machine): https://ollama.com/download

Pull the Mistral model (host):
    ollama pull mistral

---

# 📥 Clone the Repository

    git clone https://github.com/Busted-pinch/AmbedkarGPT-Intern-Task.git
    cd AmbedkarGPT-Intern-Task

---

# ✍️ Prepare Your Input File

Edit or replace the file named `speech.txt` in the repo root.

- Must be plain `.txt`  
- Can be long or short  
- This is the file the agent will generate a response for the query

---

# ▶️ Execution

## 1️⃣ Start Ollama (REQUIRED — run on HOST, outside Docker)

    ollama serve

You should see:
    Listening on 127.0.0.1:11434

Keep this terminal open.

## 2️⃣ Start Docker Compose (new terminal)

    sudo docker compose up --build

What this does:
- Builds the Python app image  
- Installs Python dependencies inside the container  
- Starts ChromaDB (persisted in a Docker volume)  
- Connects the app to ChromaDB and Ollama  
- Runs the pipeline

---

# 🔍 Internal Workflow (what runs automatically)

1. Loads `speech.txt`  
2. Splits into chunks (default chunk size: 1000, overlap: 100)  
3. Generates embeddings with Sentence-Transformers  
4. Persists embeddings to ChromaDB  
5. Performs semantic search for the query  
6. Retrieves the top relevant chunks  
7. Sends retrieved text to **Mistral** via **Ollama**  
8. Prints the final response to stdout/logs

Sample output format:
    --- SUMMARY ---
    <your generated summary here>

---

# 🧹 Troubleshooting

### Ollama not reachable
Ensure Ollama is serving on host:
    ollama serve

### Mistral model missing
Pull the model on host:
    ollama pull mistral

### ChromaDB index problems (e.g., dimension mismatch, corrupted DB)
Reset the Chroma volume and rebuild:
    sudo docker volume rm ambedkargpt-intern-task_chroma_data
    sudo docker compose up --build

### App container exits quickly
The app is designed to run the pipeline and exit. For interactive debugging, you can start a shell in the app container:
    sudo docker compose run --rm app bash

---

# 🎯 Expected Output

- A concise, context-aware summary printed in the logs  
- RAG-driven results produced using local LLM inference and vector search  
- Reproducible results on any machine with the prerequisites installed

---

# 🔗 Repository

https://github.com/Busted-pinch/AmbedkarGPT-Intern-Task
