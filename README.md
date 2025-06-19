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

pip install elasticsearch>=8.0.0,<9.0.0 sentence-transformers PyPDF2


### 🚀 Installation & Configuration

This section will guide you from setting up ElasticSearch with Docker, to installing dependencies, to indexing your first PDF for hybrid semantic search.


### 1. Run ElasticSearch Server with Docker

ElasticSearch 8.x requires at least 2GB RAM. We recommend using Docker for a quick, isolated setup.

#### **Step 1: Ensure Docker is Installed**

- Download & install [Docker Desktop](https://www.docker.com/products/docker-desktop) for your OS (Mac/Windows/Linux).
- Start Docker Desktop and ensure it is running.

#### **Step 2: Allocate Sufficient Memory**

- In Docker Desktop, go to **Settings > Resources > Memory** and set at least **2GB** (3–4GB recommended).

#### **Step 3: Start ElasticSearch Container**

```bash
docker run -d --name elasticsearch \
  -e "discovery.type=single-node" \
  -e "ES_JAVA_OPTS=-Xms2g -Xmx2g" \
  -p 9200:9200 \
  docker.elastic.co/elasticsearch/elasticsearch:8.13.4

Step 4: Set the Elastic Password (if prompted)

If you need to set or reset the password:

docker exec -it elasticsearch bin/elasticsearch-reset-password -u elastic

Copy the generated password for use in the Python code.

Step 5: Test ElasticSearch

Visit https://localhost:9200 in your browser.
	•	If you see a JSON response or a login prompt, ElasticSearch is running!

⸻

2. Install Python Dependencies

It’s recommended to use a virtual environment (e.g., venv or conda):

pip install "elasticsearch>=8.0.0,<9.0.0" sentence-transformers PyPDF2


⸻

3. Project Configuration

Update your code or environment variables with the correct ElasticSearch URL and credentials.
For local development, you can use:

from elasticsearch import Elasticsearch

es = Elasticsearch(
    "https://localhost:9200",
    basic_auth=("elastic", "YOUR_ELASTIC_PASSWORD"),
    verify_certs=False   # Use only for local/dev
)


⸻

4. Index Your PDF Files

Use the provided class (e.g., HybridPDFSearch) to index your PDF:

from hybrid_pdf_search import HybridPDFSearch  # Update import as needed

searcher = HybridPDFSearch(
    es_url="https://localhost:9200",
    index_name="hybrid_pdf",
    embedding_model="all-MiniLM-L6-v2",    # or any compatible SentenceTransformer
    # basic_auth=("elastic", "YOUR_ELASTIC_PASSWORD"),
    # verify_certs=False  # For local/dev only
)

searcher.index_pdf("yourfile.pdf")


⸻

5. Search Your Indexed Content

Run a hybrid search with both keywords and semantic similarity:

results = searcher.search("What is semantic search?", top_k=3)
for idx, res in enumerate(results, 1):
    print(f"{idx}. [Score: {res['score']:.2f}]\n{res['content']}\n")


⸻

✅ You’re Ready!

You can now perform hybrid semantic search across your PDF content using ElasticSearch + Python.

⸻

Troubleshooting Tips
	•	If you can’t access https://localhost:9200, ensure Docker is running and the container is healthy (docker ps -a).
	•	Make sure the correct password is used for the elastic user.
	•	For SSL certificate errors during development, use verify_certs=False in the Python client (never in production!).

