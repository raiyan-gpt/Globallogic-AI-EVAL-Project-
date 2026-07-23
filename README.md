# 🧠 Enterprise RAG Evaluation Platform

> An end-to-end **Retrieval-Augmented Generation (RAG)** platform with automated response evaluation using an **LLM-as-a-Judge** framework.

The platform retrieves information from enterprise PDF documents, generates grounded responses using **Google Gemini**, and automatically evaluates answer quality across multiple dimensions — correctness, relevance, completeness, and hallucination detection.

---

## 📌 Overview

This project was developed during my internship to explore enterprise-scale AI evaluation workflows.

Unlike a traditional chatbot, this platform combines **document retrieval**, **grounded answer generation**, **automated evaluation**, and **human feedback** into a single pipeline — designed to demonstrate how enterprise RAG systems can be evaluated beyond simple response generation.

### 🎯 The application enables users to:

- 🔍 Query a collection of enterprise PDF documents
- 📚 Retrieve the most relevant document chunks using semantic search
- 💬 Generate grounded responses using Google Gemini
- 🧪 Automatically evaluate responses using an independent LLM Judge
- 🚨 Detect unsupported or hallucinated statements
- 👤 Capture human feedback for evaluation validation

---

## ✨ Features

- 🏢 Enterprise Retrieval-Augmented Generation (RAG)
- 🔎 Semantic search using **Chroma Vector Database**
- 🤗 **HuggingFace BGE** embeddings
- ⚡ **Google Gemini 2.5 Flash** for answer generation
- ⚖️ Independent **LLM-as-a-Judge** evaluation using **Groq Llama 3.3 70B**
- 📊 Automatic scoring for:
  - ✅ Correctness
  - 🎯 Relevance
  - 📖 Completeness
  - 🚫 Hallucination Detection
- 📂 Retrieved Evidence Viewer
- 🙋 Human-in-the-loop feedback collection
- 📝 Evaluation logging
- 📦 Batch evaluation pipeline

---

## 🏗️ System Architecture

```
User Question
      │
      ▼
Query Classification
      │
      ▼
Chroma Vector Database (Semantic Retrieval using BGE)
      │
      ▼
Retrieved Context Chunks
      │
      ▼
Google Gemini 2.5 Flash (Answer Generation)
      │
      ▼
Groq Llama 3.3 70B Judge (Automatic Evaluation)
      │
      ▼
Correctness • Relevance • Completeness • Hallucination Detection
      │
      ▼
Streamlit Dashboard
      │
      ▼
Human Feedback & Logging
```

---

## 🛠️ Technology Stack

| Component | Technology |
|---|---|
| 🐍 Language | Python |
| 🖥️ Frontend | Streamlit |
| 🔗 Framework | LangChain |
| 🧬 Embeddings | BAAI/bge-small-en-v1.5 |
| 🗄️ Vector Database | ChromaDB |
| ✍️ Generator | Google Gemini 2.5 Flash |
| ⚖️ Judge | Groq Llama-3.3-70B |
| 📄 Document Loader | PyPDF |
| 🧾 Logging | CSV |

---

## 📁 Project Structure

```
AI-Eval-Project/
│
├── app.py
├── requirements.txt
├── .env.example
├── README.md
│
├── data/
│   └── pdfs/
│
├── evaluations/
│   ├── questions.csv
│   ├── results.csv
│   ├── scored_results.csv
│   └── chat_history.csv
│
└── src/
    ├── chatbot.py
    ├── config.py
    ├── create_vectorstore.py
    ├── evaluate.py
    ├── generator.py
    ├── judge.py
    ├── logger.py
    ├── rag_chain.py
    ├── retriever.py
    ├── load_documents.py
    └── chunk_documents.py
```

---

## 🚀 First-Time Setup

Follow these steps when running the project for the first time.

### 1️⃣ Clone the repository
```bash
git clone https://github.com/raiyan-gpt/Globallogic-AI-EVAL-Project-.git
cd Globallogic-AI-EVAL-Project-
```

### 2️⃣ Create and activate a virtual environment

**Windows**
```bash
python -m venv venv
venv\Scripts\activate
```

**macOS / Linux**
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3️⃣ Install dependencies
```bash
pip install -r requirements.txt
```

### 4️⃣ Configure environment variables

Create a `.env` file in the project root:

```env
GOOGLE_API_KEY=your_google_api_key
GROQ_API_KEY=your_groq_api_key
```

### 5️⃣ Prepare the knowledge base

Ensure the PDF documents are available inside:
```
data/pdfs/
```

### 6️⃣ Build the Vector Database
```bash
python src/create_vectorstore.py
```

This step:
- 📥 Loads all PDF documents
- ✂️ Splits the documents into chunks
- 🧬 Generates embeddings
- 🗄️ Creates the local Chroma Vector Database

> ⚠️ **Important:** This step must be completed before running the application for the first time.

### 7️⃣ (Optional) Verify the retrieval pipeline

You can test whether the vector database was created successfully:
```bash
python src/test_retrieval.py
```

### 8️⃣ (Optional) Verify Gemini connectivity
```bash
python src/test_gemini.py
```
This checks whether your Gemini API key is configured correctly.

### 9️⃣ Launch the application
```bash
streamlit run app.py
```

🌐 The application will be available at:
```
http://localhost:8501
```

---

## 🔁 Running the Project After Initial Setup

After the initial setup is complete, future runs only require:
```bash
streamlit run app.py
```

If you add, remove, or modify any PDF documents, rebuild the vector database by running:
```bash
python src/create_vectorstore.py
```
before launching the application again.

---

## 🔄 Evaluation Pipeline

For every user query, the platform performs the following sequence:

1. 🔍 Retrieve relevant document chunks
2. 💬 Generate an answer using Gemini
3. ⚖️ Evaluate the generated answer using an independent LLM Judge
4. 📊 Compute evaluation metrics
5. 📂 Display retrieved evidence
6. 🙋 Allow human validation
7. 📝 Save evaluation logs

---

## 📊 Evaluation Metrics

| Metric | Description |
|---|---|
| ✅ **Correctness** | Whether the answer is factually supported by the retrieved context |
| 🎯 **Relevance** | Whether the response answers the user's question |
| 📖 **Completeness** | Whether important retrieved information is covered |
| 🚫 **Hallucination Detection** | Detects unsupported or fabricated statements |

---

## 💡 Example Questions

- "What are the benefits of microservices?"
- "Summarize the CSR policy."
- "Compare healthcare and gaming solutions."
- "How can GlobalLogic help utility companies?"
- "What digital transformation services are offered?"

---

## 📦 Batch Evaluation

To evaluate the complete benchmark dataset:

```bash
python src/evaluate.py
```

Results are automatically written to:
```
evaluations/scored_results.csv
```

---

## 🧯 Troubleshooting

**🔑 Missing API Keys**
> Ensure the `.env` file exists and contains valid API keys.

**📭 Empty Retrieval Results**
> Rebuild the vector database:
> ```bash
> python src/create_vectorstore.py
> ```

**🐢 Slow Responses**
> The Groq Judge model may be rate limited depending on API usage.

---

## 🔮 Future Improvements

- 🔀 Hybrid Retrieval (BM25 + Vector Search)
- 🎯 Cross-Encoder Reranking
- 🔌 Support for Multiple LLM Providers
- 📈 Evaluation Dashboard
- 📏 Additional Evaluation Metrics
- 🆚 Multi-document comparison
- 🐳 Docker deployment
- 🔁 CI/CD integration

---

## 🙏 Acknowledgements

This project was developed during my internship as part of an **AI Evaluation initiative** focused on enterprise Retrieval-Augmented Generation (RAG) systems. The implementation demonstrates document retrieval, grounded answer generation, automated evaluation, and human-in-the-loop validation for enterprise knowledge bases.
