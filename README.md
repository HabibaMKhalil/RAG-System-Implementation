### 🔍 RAG-Based Document QA System                

This project is a Retrieval-Augmented Generation (RAG) system built using FAISS, HuggingFace Transformers, and LangChain. It enables document ingestion, semantic indexing, diverse search strategies, and free-text answer generation via a local language model.

# 🛠️ Environment Setup
1. Create and activate a virtual environment
bash
Copy
python -m venv rag_env
rag_env\Scripts\activate  # On Windows
or
source rag_env/bin/activate  # On macOS/Linux
2. Install all dependencies
bash
Copy
pip install -r requirements.txt

# Or install individually:
pip install langchain sentence-transformers faiss-cpu PyMuPDF python-docx scikit-learn transformers accelerate
3. (Optional) API Configuration
If you're using any external LLM APIs, set them in config.py. This version supports running fully locally, so no API keys are required.

# 📁 Project Structure
graphql
Copy
rag-assignment/
├── documents/              # Source files (.pdf, .docx, .txt)
├── faiss_store/            # Vector index & metadata
├── main.py                 # Main control script
├── document_loader.py      # PDF, DOCX, TXT loader
├── document_processing.py  # Chunking and cleaning logic
├── embedding.py            # Embedding creation and FAISS indexing
├── retrieval.py            # Semantic and MMR retrieval logic
├── rag_pipeline.py         # Combines retrieval with generation
├── evaluation.py           # Precision, recall, F1 evaluation
├── queries.py              # Sample test queries
├── config.py               # Model/API setup and hyperparams
└── README.md               # Project documentation

# 🧠 System Workflow Overview
Document Ingestion: PDFs, DOCX, and TXT files are parsed using custom loaders.

Text Chunking: Documents are split into overlapping text chunks for better context retention.

Embedding Generation: Sentence embeddings are generated via all-MiniLM-L6-v2.

FAISS Indexing: Embeddings and metadata are stored in a FAISS vector index.

Search Modes:

Mode 2: Standard top-K semantic retrieval.

Mode 3: MMR search to increase diversity of results.

Answer Generation:

Mode 4: Retrieves documents and generates answers using google/flan-t5-base.

# 🧪 Retrieval Strategy Comparison
The system provides three distinct retrieval and generation modes, each designed to address specific information retrieval needs. **Mode 2**, known as *Semantic Search*, performs a standard top-K similarity-based retrieval using sentence embeddings to return the most relevant document chunks based on a user's query. **Mode 3**, called *MMR Search* (Maximal Marginal Relevance), enhances the diversity of retrieved results by balancing relevance and novelty, reducing redundancy in the returned documents. **Mode 4**, referred to as *RAG Answer*, integrates retrieval with language generation, where retrieved documents are fed into a local language model (e.g., Flan-T5) to generate a synthesized, context-aware answer to the user’s question. Each mode offers unique strengths, making the system flexible for various use cases.

# 📊 Evaluation Metrics
Precision: Proportion of retrieved documents that are relevant.

Recall: Proportion of relevant documents retrieved out of all relevant documents.

F1-score: Harmonic mean of precision and recall.

Sample Result (Default Configuration)
Precision: ~X%

Recall: ~Y%

F1-Score: ~Z%

# ✅ Pros
Fully local (no API keys required)

Flexible and modular architecture

Multiple search strategies supported

Easily extendable with LangChain components

# ⚠️ Limitations
Smaller models like flan-t5-base may limit generation detail

No web interface (CLI only)

Evaluation is manual or offline

# 🚧 Challenges Addressed
During development, several key challenges were addressed to improve the system's robustness and usability. One major issue was the limitation of API quotas from services like OpenAI, which was resolved by switching to HuggingFace transformers for fully local model usage. Compatibility concerns with LangChain embeddings were tackled by implementing the appropriate HuggingFace wrappers to ensure smooth integration. To support better tracking of document chunks, metadata was stored alongside vectors in the FAISS index, enabling clearer retrieval and display. Redundancy in search results was reduced by incorporating Maximal Marginal Relevance (MMR), which enhances diversity in retrieved content. The system also handled the variability of document formats—such as PDFs, DOCX, and TXT—by introducing unified loaders. Lastly, chunk size and overlap were carefully tuned to balance between context retention and embedding efficiency, optimizing both retrieval performance and generation quality.

# 📥 Document Corpus Instructions
Place your .pdf, .docx, or .txt files into the documents/ directory. The system automatically loads and processes all supported files.

# 💽 Model + Index Files
File	Purpose
index_miniLM.index	FAISS vector index
index_miniLM_metadata.pkl	Metadata for each chunk

# ▶️ Running the System
bash
Copy
python main.py
Choose one of the following modes:

1: Build FAISS index from documents

2: Semantic search (top-K)

3: MMR search (diverse top-K)

4: RAG-style answer generation

📌 Sample Query
text
Copy
what is the difference between RAG-sequence and RAG-token models
🤝 Contributors
This project was developed for academic purposes using open-source tools and local models. No paid APIs or cloud services are required.
