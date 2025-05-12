# 🔍 RAG-Based Document QA System

This project is a Retrieval-Augmented Generation (RAG) system implemented entirely in a single Python file, `main.py`, using open-source tools like FAISS, HuggingFace Transformers, and LangChain. It allows users to search a local document corpus and generate context-aware answers using a lightweight local language model.

---

## 🛠️ Environment Setup

1. Create and activate a virtual environment
```bash
python -m venv rag_env
rag_env\Scripts\activate  # On Windows
```
or
source rag_env/bin/activate  # On macOS/Linux
2. Install all dependencies
```bash
Copy
pip install -r requirements.txt
```

Or install manually:
pip install langchain sentence-transformers faiss-cpu PyMuPDF python-docx scikit-learn transformers accelerate


## 📁 Project Structure
rag-system/                        
├── documents/              # Place your source files here (.pdf, .docx, .txt)              
├── faiss_store/            # Automatically created to store vector index & metadata                 
├── main.py                 # Full system logic (loading, embedding, search, and generation)                
└── README.md               # Documentation                    

## 🧠 System Workflow
The system begins by loading and parsing .pdf, .docx, and .txt files placed in the documents/ directory. These documents are split into chunks to preserve context, and sentence embeddings are generated using the all-MiniLM-L6-v2 model. The embeddings are stored in a FAISS vector index for efficient similarity search. Users can perform either standard top-K semantic retrieval or apply MMR (Maximal Marginal Relevance) to increase diversity in results. Finally, a local language model (such as google/flan-t5-base) can be used to generate an answer from the retrieved context.

## 🧪 Retrieval and Generation Modes
The system offers three key modes:
Mode 2: Semantic Search, retrieves the top-K most relevant chunks.
Mode 3: MMR Search, improves result diversity by reducing redundancy.
Mode 4: RAG Answer, synthesizes an answer using retrieved documents and a local LLM.

## 📊 Evaluation Metrics
The system can be qualitatively evaluated using:
Precision: Measures how many retrieved chunks are relevant.
Recall: Measures how many relevant chunks were successfully retrieved.
F1-score: Balances both precision and recall.
With default configuration, it achieves reasonable accuracy for document QA tasks using local models.

## ✅ Advantages
Fully functional in a single file (main.py)
No need for API keys or external services
Supports various document formats
Efficient search via FAISS
Context-aware generation using HuggingFace models

## ⚠️ Limitations
Limited generation detail due to small LLMs
No GUI (CLI only)
Manual evaluation unless extended

## 🚧 Challenges Solved
Several development challenges were tackled, including replacing API-based models with open-source alternatives to avoid rate limits, adapting LangChain components for embedding and generation, and storing metadata in FAISS for better traceability. The system also handles multiple document formats through unified logic and optimizes chunk sizing for improved results.

## 📥 Preparing Your Corpus
Simply place your .pdf, .docx, or .txt files into the documents/ folder. They will be automatically processed during indexing.

## 💽 Index Files
File	Description
index_miniLM.index	Stores FAISS vector embeddings
index_miniLM_metadata.pkl	Stores corresponding chunk metadata

## ▶️ Running the System
```bash
Copy
python main.py
```
Choose from:
1: Build or rebuild the FAISS index
2: Perform semantic search
3: Perform MMR search
4: Generate an answer using retrieved documents

## 📌 Sample Query
text
Copy
What are the advantages of using MMR in document retrieval?

## 🤝 Authors
This single-file implementation was developed for educational purposes using only free and open-source tools. No paid APIs or services are required.
---

## 📂 Document Corpus
Place your `.pdf`, `.docx`, or `.txt` files inside the `documents/` folder. If you do not have documents yet, you can:
- Use any public domain content such as AI-related articles, whitepapers, or legal documents
- Download example files from course materials or project repositories

---

## 💾 Saved Model States and Indexes
The FAISS index and metadata are saved under the `faiss_store/` directory:
- `index_miniLM.index`
- `index_miniLM_metadata.pkl`
- `index_paraLM.index`
- `index_paraLM_metadata.pkl`

You can re-create them by choosing option `1` (Build Index) or option `5` (Compare Models) in the CLI.  
**Tip**: Add a `.gitignore` file to exclude large index files from GitHub uploads if needed.

---

## 📈 Results & Evaluation
The system supports evaluation using Precision, Recall, and F1-score. These metrics help analyze retrieval quality across different configurations.

### 🔍 Model Comparison (MiniLM vs Paraphrase-MiniLM)
Use CLI option `5` to compare retrieval effectiveness between the two models. Example test queries include:
- "What is LangChain used for?"
- "Explain semantic similarity search"
- "What is FAISS used for?"

The system evaluates how well retrieved chunks match expected keywords and prints the evaluation results.

---

## 🔁 Mode 5: Compare Models
This mode automatically:
- Embeds documents using both MiniLM and Paraphrase-MiniLM models
- Stores separate FAISS indexes
- Runs evaluation tests for each model using sample queries
- Reports Precision, Recall, and F1-Score

To run:
```bash
python main.py
```
Then choose:
```
5: Compare Models
```

This provides a quick performance insight and supports informed model selection.