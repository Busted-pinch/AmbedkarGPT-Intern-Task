
# AI Speech Summarizer 🗣️➡️🤖➡️📄  
An intelligent speech summarization system built using **Ollama**, **Mistral LLM**, **ChromaDB**, and **Docker**.  
It automatically reads your `speech.txt`, creates embeddings, stores them in a vector database, retrieves the most relevant chunks, and generates a concise summary using an LLM.

---

## 📌 Features

- 🔥 **Mistral LLM via Ollama** for fast and accurate summarization  
- 🧠 **Chroma Vector Database** for document chunking & retrieval  
- 📂 Fully **Dockerized** (no local Python setup needed!)  
- 📝 Automatic text chunking + retrieval-based summarization  
- 🎯 Clean architecture and easily extendable  

---

## 🚀 Prerequisites

Before running the project, ensure the following are installed:

### **1. Docker**
Install Docker:  
https://docs.docker.com/get-docker/

### **2. Docker Compose**
Install Docker Compose:  
https://docs.docker.com/compose/install/

### **3. Git (optional, for cloning)**
https://git-scm.com/downloads

---

## 📦 Installation & Setup

### **1. Clone the repository**

```bash
git clone https://github.com/Busted-pinch/AmbedkarGPT-Intern-Task.git
cd AmbedkarGPT-Intern-Task
```

---

### **2. Build the Docker containers**

```bash
sudo docker compose up --build
```

This will:

- Build the Python container  
- Install requirements  
- Start the Ollama LLM server  
- Start the app container  

---

### **3. Pull the Mistral model (one-time setup)**

```bash
sudo docker compose exec ollama ollama pull mistral
```

This downloads the Mistral LLM (~4.4GB).

---

## ▶️ Running the Application

### **Summarize the speech**

```bash
sudo docker compose exec app python main.py -q "Summarize the speech"
```

The system will:

1. Read `speech.txt`
2. Chunk into embeddings
3. Save document embeddings in Chroma
4. Retrieve the top relevant chunks
5. Generate a summary using **Mistral** via Ollama

---

## 📁 Project Structure

```
📦 AmbedkarGPT-Intern-Task
 ┣ 📜 Dockerfile
 ┣ 📜 docker-compose.yml
 ┣ 📜 main.py
 ┣ 📜 requirements.txt
 ┣ 📜 speech.txt
 ┗ 📜 README.md  (this file)
```

---

## 🛠 Troubleshooting

### ❗ *App container exits immediately*

Make sure you're running:

```bash
sudo docker compose up --build
```

The app is **not** a long-running service — it runs, prints results, and exits.  
That is normal.

To manually attach & debug:

```bash
sudo docker compose run --rm app bash
```

---

### ❗ Chroma errors: *InvalidDimensionException* or *DB not reading*

Fix by removing Chroma volume:

```bash
sudo docker compose down -v
sudo docker compose up --build
```

This wipes the old vector DB and rebuilds it.

---

### ❗ Ollama unreachable / fallback triggered

Make sure Ollama container is running:

```bash
sudo docker compose ps
```

And test manually:

```bash
sudo docker compose exec ollama ollama run mistral "hello"
```

---

## 📘 Example Output

```
=== LLM ANSWER ===
The speaker argues that caste cannot be removed until the unquestioned
authority of the shastras is rejected. Social reform alone cannot solve the issue;
the root cause is the belief in the infallibility of scripture.
=== END ANSWER ===
```

---

## 📄 License

This project is licensed under the **MIT License**.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!  
Feel free to fork the repo and submit improvements.

---

## 🙏 Acknowledgements

- **Ollama** for local LLM serving  
- **Mistral AI** for high-quality language modeling  
- **ChromaDB** for vector search  
- **Docker** for portable, reproducible builds  

---

### 🎉 Enjoy your AI Speech Summarizer!
A clean, fast, and production-ready RAG pipeline powered by open-source LLMs.
