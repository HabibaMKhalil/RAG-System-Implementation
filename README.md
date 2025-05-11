# RAG-System-Implementation

This repository contains an implementation of a Retrieval-Augmented Generation (RAG) system using open-source tools like LangChain, Sentence Transformers, and FAISS. The system retrieves relevant documents and uses them to generate context-aware responses through a language model (LLM).

## Project Structure

- `main.py`: Main script for executing the RAG system.
- `document_loader.py`: Functions to load documents from PDF, DOCX, and TXT formats.
- `document_processing.py`: Functions for splitting documents into chunks and generating embeddings.
- `embedding.py`: Code for generating embeddings and storing them in FAISS.
- `retrieval.py`: Functions for retrieving documents using similarity search and advanced strategies.
- `rag_pipeline.py`: Integration of retrieval and generation using LangChain.
- `evaluation.py`: Functions to evaluate retrieval and generation performance.
- `config.py`: Configuration for setting up LLM API keys and parameters.
- `queries.py`: Sample queries to test the system's performance.

## Setup Instructions

1. Clone this repository.
2. Install the required dependencies:
pip install -r requirements.txt

markdown
Copy
3. Set up your LLM API keys in `config.py`.
4. Prepare your document corpus in the `documents/` directory.
5. Run the system:
python main.py

markdown
Copy

## Evaluation Metrics

- **Precision**: Measures the proportion of relevant documents retrieved.
- **Recall**: Measures the proportion of relevant documents retrieved from the total relevant documents.
- **F1-score**: Harmonic mean of precision and recall.

## Results

- The system achieves [X]% precision and [Y]% recall with the default configuration.

## Challenges Faced

- Handling different document formats and maintaining metadata.
- Tuning the chunk sizes and overlap for optimal performance.
