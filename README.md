# 🚀 AI Speech Summarizer Agent  
### *RAG-Based · Fully Local · Powered by Ollama + Mistral + ChromaDB*

This project is a **production-style AI Speech Summarization Agent** capable of reading long text files, chunking them into meaningful segments, retrieving relevant context via semantic vector search, and generating clean, context-aware summaries using **Mistral LLM served locally through Ollama**.

Everything runs inside **Docker Compose**, making the system fully reproducible, portable, and free from Python environment conflicts.

---

# 🧱 Project Structure (Flat Layout)

```
AmbedkarGPT-Intern-Task/
│
├── main.py              # Main application logic (RAG pipeline)
├── requirements.txt     # Python dependencies
├── speech.txt           # Input file for summarization
├── docker-compose.yml   # Multi-container setup (App + Chroma)
├── Dockerfile           # Image build for Python app
├── .dockerignore
└── README.md
```

---

# 🧠 Key Features

- Reads any `.txt` based document or long speech  
- Splits text into meaningful semantic chunks  
- Generates embeddings using Sentence-Transformers  
- Stores vectors in **ChromaDB** for similarity search  
- Retrieves the most relevant chunks using vector similarity  
- Summarizes using **Mistral LLM** running locally via Ollama  
- Entire pipeline runs through Docker Compose  
- Zero cloud dependency → full privacy → local execution  

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

# ⚠️ Prerequisites (IMPORTANT)

Before running the project, make sure you have:

### ✔ Docker Installed  
https://www.docker.com/products/docker-desktop/

### ✔ Git Installed  
https://git-scm.com/downloads

### ✔ Ollama Installed (Runs on host machine, NOT in Docker)  
https://ollama.com/download

Install Mistral model:

```
ollama pull mistral
```

---

# 📥 Clone the Repository

```
git clone https://github.com/Busted-pinch/AmbedkarGPT-Intern-Task.git
cd AmbedkarGPT-Intern-Task
```

---

# ✍️ Preparing Input File

Replace or edit:

```
speech.txt
```

- Must be `.txt`  
- Can be extremely long  
- Add any text you want the agent to summarize  

---

# ▶️ Execution Steps (Super Descriptive — Follow Carefully)

## **1️⃣ Start Ollama**

Before touching Docker, run:

```
ollama serve
```

You should see:

```
Listening on 127.0.0.1:11434
```

Leave it running.

---

## **2️⃣ Start Docker Compose**

Inside the project folder:

```
sudo docker compose up --build
```

This performs:

- Builds the Python app image  
- Installs dependencies inside container  
- Starts ChromaDB  
- Connects Python app → ChromaDB  
- Connects Python app → Ollama (host)  
- Runs the full RAG summarization pipeline  

---

## **3️⃣ Behind the Scenes Workflow**

- Reads `speech.txt`  
- Chunks text  
- Generates embeddings  
- Stores vectors in ChromaDB  
- Performs similarity search  
- Sends prompt to Mistral through Ollama  
- Prints final summary in logs  

You will see:

```
--- SUMMARY ---
<your final summary here>
```

---

## **4️⃣ Stop Containers**

```
CTRL + C
sudo docker compose down
```

---

# 🧹 Troubleshooting

### 🔸 Ollama not responding  
Run:
```
ollama serve
```

### 🔸 Model not found  
Run:
```
ollama pull mistral
```

### 🔸 Chroma issues  
Rebuild:
```
sudo docker compose down
sudo docker compose up --build
```

---

# 🎯 Expected Output

A clean, readable, context-aware summary of your input text powered by:

- Retrieval-Augmented Generation  
- Local Vector Search  
- Local LLM Inference  

Everything happens entirely offline.

---

# 🔗 Repository

https://github.com/Busted-pinch/AmbedkarGPT-Intern-Task
