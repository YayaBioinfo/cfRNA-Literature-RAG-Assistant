# 🧬 cfRNA-Literature-RAG-Assistant

A Retrieval-Augmented Generation (RAG) system for querying scientific literature on **cell-free RNA (cfRNA)** biology and liquid biopsy research. Built for Google Colab with free-tier LLM access via OpenRouter.

---

## 🔍 What This Does

Instead of asking an LLM from general knowledge, this system:

1. **Reads your PDF papers** — extracts and indexes the full text
2. **Finds relevant excerpts** — uses semantic search to locate the most relevant passages for your question
3. **Answers from your literature** — sends those excerpts to an LLM, grounded to your specific papers

```
Your Question
      ↓
SciBERT Embedding (sentence-transformers)
      ↓
FAISS Vector Search → Top 5 relevant chunks
      ↓
LLM (Llama 3.3 70B via OpenRouter) → Grounded Answer
```

---

## 🛠️ Tech Stack

| Component | Tool |
|---|---|
| PDF extraction | PyMuPDF (fitz) |
| Text embedding | `sentence-transformers/all-MiniLM-L6-v2` |
| Vector search | FAISS (IndexFlatIP, cosine similarity) |
| LLM | `meta-llama/llama-3.3-70b-instruct:free` via OpenRouter |
| Environment | Google Colab |

---

## 🚀 Quick Start

### 1. Open in Google Colab
Upload `cfRNA_RAG_OpenRouter_Colab.ipynb` to [colab.research.google.com](https://colab.research.google.com)

### 2. Get a free OpenRouter API key
1. Go to [openrouter.ai](https://openrouter.ai)
2. Sign up (free)
3. Go to **Keys** → **Create Key**
4. Copy your key — starts with `sk-or-...`

> OpenRouter provides free access to several LLMs including Llama 3.3 70B — no credit card required for free models.

### 3. Run the notebook step by step

| Step | What it does |
|---|---|
| Step 1 | Install dependencies |
| Step 2 | Import libraries |
| Step 3 | Upload your PDF papers |
| Step 4 | Extract text from PDFs |
| Step 5 | Chunk text into 1000-character segments |
| Step 6 | Embed chunks + build FAISS index |
| Step 7 | Setup OpenRouter API |
| Step 8 | Define RAG query function |
| Step 9 | Run a test question |
| Step 10 | Interactive chat loop |

---

## 📄 Supported Topics

This assistant is specialized for **cfRNA research**, including:

- Human-derived cfRNA biomarkers (cancer, organ-of-origin)
- Microbe-derived cfRNA in blood plasma
- Liquid biopsy sequencing pipelines
- Misincorporation analysis
- Longitudinal study design
- Differential abundance analysis

---

## 💬 Example Questions

```
What biomarkers are associated with lung cancer in cfRNA studies?
How is organ-of-origin inferred from plasma cfRNA?
What is the role of misincorporation in cfRNA damage analysis?
How do human and microbe-derived cfRNA differ in plasma?
What sequencing depth is recommended for cfRNA studies?
```

---

## ⚙️ Configuration

**Chunk size** — default 1000 characters with 200 overlap. Increase for longer context, decrease for more precise retrieval:
```python
chunks = chunk_text(doc["text"], chunk_size=1000, overlap=200)
```

**Number of retrieved chunks** — default 5. Increase for broader context:
```python
answer = query_rag(question, n_results=5)
```

**Verbose mode** — shows which papers were retrieved per query:
```python
answer = query_rag(question, verbose=True)
```

**Model** — swap to any free model on OpenRouter:
```python
model="meta-llama/llama-3.3-70b-instruct:free"
# Other free options:
# "mistralai/mistral-7b-instruct:free"
# "google/gemma-3-27b-it:free"
```

---

## 📁 Repository Structure

```
cfRNA-RAG/
├── cfRNA_RAG_OpenRouter_Colab.ipynb    # Main notebook
└── README.md                           # This file
```

---


## 👤 Author

**Yaya Idayanti**
Brawijaya University — Biology, Microbiology
[github.com/YayaBioinfo](https://github.com/YayaBioinfo)
