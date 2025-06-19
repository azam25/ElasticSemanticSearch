# 🧠 Elastic Semantic Hybrid Search on PDFs with Python

Leverage the power of **Elastic Search** and **AI-based semantic search** to perform hybrid (keyword + meaning-based) search on your PDF documents — all in Python.

---

## 🚀 Features

- **PDF Text Extraction**: Reads and splits PDFs into pages/chunks for granular search.
- **Semantic Embedding**: Uses state-of-the-art sentence transformers to generate dense vector representations.
- **Hybrid Search**: Combines classic keyword search and vector-based (cosine similarity) semantic search.
- **Scalable & Fast**: Indexes and searches large document collections efficiently with Elastic Search.
- **Production-Ready Class**: Clean, reusable Python class for indexing and querying.

---

## 📦 Dependencies

- Python 3.7+
- [Elasticsearch](https://www.elastic.co/) 8.x server (Docker recommended)
- `elasticsearch` Python library (version 8.x)
- `sentence-transformers`
- `PyPDF2`

### Install Python dependencies:
```bash
pip install elasticsearch>=8.0.0,<9.0.0 sentence-transformers PyPDF2
