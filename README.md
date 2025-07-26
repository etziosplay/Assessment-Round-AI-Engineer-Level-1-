# 📚 Bengali-English RAG Question Answering System

This project implements a **Retrieval-Augmented Generation (RAG)** pipeline that allows users to ask questions in **Bangla or English** and get accurate answers from a given textbook (e.g., NCTB Literature books) using **LangChain**, **FAISS**, and **Hugging Face Transformers**.

---

## 🔍 Features

- 🔄 Preprocessing and OCR support for scanned textbooks (if needed)
- 🧼 Intelligent text cleaning and chunking
- 🌐 Multilingual support: Bengali (বাংলা) and English questions
- 🤖 Uses state-of-the-art models for both:
  - **Embedding** (e.g., `intfloat/multilingual-e5-small`)
  - **Question Answering** (e.g., `csebuetnlp/bangla-bert-base`)
- ⚡ Fast retrieval via **FAISS vector store**
- 💬 Can be used as a backend for a QA chatbot or a learning assistant

---

## 🛠️ Setup

### 🔗 Requirements

Install dependencies:

```bash
pip install -r requirements.txt
```

Or manually:

```bash
pip install langchain faiss-cpu sentence-transformers transformers
```

---

## 🧠 How It Works

1. **Text Extraction & Cleaning**  
   Loads PDF → Extracts text → Applies regex-based formatting → Saves clean text

2. **Chunking & Embedding**  
   Splits cleaned text into overlapping chunks → Embeds chunks using multilingual model → Stores in FAISS

3. **QA System**  
   Retrieves top relevant chunks based on the question → Feeds context to QA model → Returns final answer

---

## 🚀 Usage

```python
from transformers import pipeline

# Ask a question (Bangla or English)
query = "অন্নদামের ভাষায় সুকুমার কাকে বলা হয়েছে?"

# Retrieve top relevant context
docs = retriever.get_relevant_documents(query)
context = "\n".join([doc.page_content for doc in docs])

# Use Hugging Face QA pipeline directly
qa_pipeline = pipeline("question-answering", model="csebuetnlp/bangla-bert-base")
response = qa_pipeline(question=query, context=context)

print("Answer:", response["answer"])
```

---

## 📂 Dataset

- 📘 NCTB Literature PDF (11-12th grade textbook)
- OCR not required if PDF is text-based

---

## 📈 Results

| Example Question | Answer |
|------------------|--------|
| অন্নদামের ভাষায় সুকুমার কাকে বলা হয়েছে? | অতনুকে |

---

## 📌 TODO

- [ ] UI with Streamlit or Gradio
- [ ] Add OCR support for scanned textbooks
- [ ] Expand to other subjects
- [ ] Deploy via HuggingFace Spaces / Colab

---

## 🤝 Contributing

Contributions, issue reports, or suggestions are very welcome! Feel free to fork and improve the project.

---

## 📜 License

MIT License

---

## ✍️ Author

**Niamul Hassan Samin**  
Final Year CSE Student, AI & NLP Enthusiast  
🇧🇩 Bangladesh
