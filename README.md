# 📄 RAG Document Chatbot — LLaMA 3.1-8B + FAISS + LangChain

A Retrieval-Augmented Generation (RAG) chatbot that lets you upload any PDF or Word document and ask questions about it using a locally running LLaMA 3.1-8B model (4-bit quantized via Unsloth).

---

## 🚀 How It Works

1. You upload a PDF or `.docx` file at runtime (inside Google Colab)
2. The document is split into chunks and embedded using `BAAI/bge-base-en`
3. Embeddings are stored in a FAISS vector database
4. When you ask a question, the top 3 relevant chunks are retrieved
5. LLaMA 3.1-8B generates an answer grounded in those chunks

---

## ⚙️ Requirements

### Platform
- **Google Colab** with a **GPU runtime** (T4 or better recommended)

### HuggingFace Setup
- A [HuggingFace](https://huggingface.co/) account
- Accept the license for [meta-llama/Meta-Llama-3.1-8B](https://huggingface.co/meta-llama/Meta-Llama-3.1-8B)
- Generate an access token at https://huggingface.co/settings/tokens
- In Colab, go to **Secrets** (🔑 icon in the left sidebar) and add:
  - **Name:** `HF_TOKEN`
  - **Value:** your HuggingFace token

### Python Dependencies (auto-installed by the notebook)
```
unsloth
sentence-transformers
faiss-cpu
langchain
langchain-community
pypdf
python-docx
torch==2.9.0
torchaudio==2.9.0
```

---

## 📂 Repository Contents

```
RAG_Document_LLM.ipynb   ← The main notebook (upload this to Colab and run)
README.md                ← This file
```

> ⚠️ **No input document is included in this repository.** You supply your own PDF or Word file at runtime — see instructions below.

---

## ▶️ How to Run

1. Open [Google Colab](https://colab.research.google.com/) and upload `RAG_Document_LLM.ipynb`
2. Set the runtime to **GPU**: `Runtime → Change runtime type → T4 GPU`
3. Add your `HF_TOKEN` to Colab Secrets
4. Run all cells in order
5. When prompted by the **Upload** cell, click the upload button and select your PDF or `.docx` file
6. Once the model loads, type your questions in the interactive prompt at the bottom

---

## 📎 Supported Input File Types

| Format | Loader Used |
|--------|-------------|
| `.pdf` | `PyPDFLoader` (LangChain) |
| `.docx` | `Docx2txtLoader` (LangChain) |

Multiple files can be uploaded at once — all will be merged into a single knowledge base.

---

## 💬 Example Usage

```
❓ Ask a question: How many FMLA leave days can be taken in a year?

🤖 Answer:
12 workweeks of FMLA leave in a 12-month period for the birth,
adoption or foster placement of a child, a serious health condition,
or qualifying military reasons...
```

---

## 🔒 Privacy Note

Your uploaded documents are processed entirely within your Colab session. They are not stored anywhere permanently and are lost when the session ends. Do not commit sensitive documents to this repository.

---

## 🛠️ Model Details

| Component | Details |
|-----------|---------|
| LLM | `unsloth/Meta-Llama-3.1-8B` (4-bit quantized) |
| Embedding Model | `BAAI/bge-base-en` |
| Vector Store | FAISS (CPU) |
| Framework | LangChain + Unsloth |
| Prompt Style | Alpaca instruction format |

---

## 📝 License

This project is for educational and personal use. Model usage is subject to Meta's [LLaMA 3.1 Community License](https://llama.meta.com/llama3_1/license/).
