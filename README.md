# 📚 RAG Document Q&A System

## Overview

A sophisticated **Retrieval-Augmented Generation (RAG)** system that enables intelligent question-answering from PDF documents using state-of-the-art language models and embedding techniques. This application combines the power of **Qwen-2.5-coder** model with **HuggingFace embeddings** to provide accurate, context-aware responses based on document content.

## 🚀 Features

- **📄 PDF Document Processing**: Automatically extracts and processes content from PDF files
- **🔍 Semantic Search**: Uses advanced vector embeddings for relevant document retrieval
- **🤖 AI-Powered Q&A**: Leverages Qwen-2.5-coder model for intelligent response generation
- **🎯 Context-Aware Responses**: Provides answers strictly based on document content
- **📊 Source Attribution**: Shows relevant document sections used for each answer
- **🌐 Web Interface**: Clean, intuitive Streamlit-based user interface
- **⚡ Fast Performance**: Optimized vector search with FAISS indexing

## 🏗️ Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   PDF Documents │───▶│  Text Splitter   │───▶│  HF Embeddings  │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                                         │
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│  User Question  │───▶│   FAISS Vector   │◀───│   Vector Store  │
└─────────────────┘    │     Database     │    └─────────────────┘
         │              └──────────────────┘
         │                       │
         ▼                       ▼
┌─────────────────┐    ┌──────────────────┐
│  Qwen-2.5-coder │◀───│  Retrieved Docs  │
└─────────────────┘    └──────────────────┘
         │
         ▼
┌─────────────────┐
│  Final Answer   │
└─────────────────┘
```

## 🛠️ Technology Stack

- **Frontend**: Streamlit
- **Language Model**: Qwen-2.5-coder
- **Embeddings**: HuggingFace `all-MiniLM-L6-v2`
- **Vector Database**: FAISS
- **Document Processing**: LangChain, PyPDF
- **Text Splitting**: RecursiveCharacterTextSplitter
- **Environment Management**: python-dotenv

## 📋 Prerequisites

- Python 3.8+
- Groq API Key
- HuggingFace Token (for embeddings)

## 🔧 Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd rag-document-qa
   ```

2. **Create virtual environment**
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install streamlit langchain langchain-groq langchain-openai langchain-community langchain-core langchain-huggingface faiss-cpu pypdf python-dotenv openai sentence-transformers
   ```

4. **Set up environment variables**
   
   Create a `.env` file in the project root:
   ```env
   GROQ_API_KEY=your_groq_api_key_here
   HF_TOKEN=your_huggingface_token_here
   OPENAI_API_KEY=optional_openai_key_here
   ```

## 🔑 API Keys Setup

### Groq API Key (Required)
1. Visit [Groq Console](https://console.groq.com/)
2. Sign up/Login to your account
3. Navigate to API Keys section
4. Generate a new API key
5. Copy and paste in `.env` file

### HuggingFace Token (Required)
1. Visit [HuggingFace Settings](https://huggingface.co/settings/tokens)
2. Create a new token with **Read** permissions
3. Copy and paste in `.env` file

### OpenAI API Key (Optional)
- Only required if using `main.py` instead of `app_huggingfaceembedding.py`

## 🚀 Usage

1. **Start the application**
   ```bash
   streamlit run app_huggingfaceembedding.py
   ```

2. **Access the web interface**
   - Open your browser and navigate to `http://localhost:8501`

3. **Initialize document embeddings**
   - Click the **"Document Embedding"** button
   - Wait for "Vector Database is ready" confirmation (2-5 minutes first time)

4. **Ask questions**
   - Enter your question in the text input field
   - Get AI-powered answers based on document content
   - View source documents in the expandable section

## 📁 Project Structure

```
rag-document-qa/
├── app_huggingfaceembedding.py    # Main application (HuggingFace embeddings)
├── main.py                        # Alternative app (OpenAI embeddings)
├── research_papers/               # PDF documents directory
│   ├── Attention.pdf              # Sample research paper
│   └── LLM.pdf                    # Sample research paper
├── .env                          # Environment variables (not in git)
├── .venv/                        # Virtual environment (not in git)
└── README.md                     # Project documentation
```

## 🔄 Application Variants

### 1. `app_huggingfaceembedding.py` (Recommended)
- Uses free HuggingFace embeddings
- Model: `all-MiniLM-L6-v2`
- No OpenAI costs required

### 2. `main.py`
- Uses OpenAI embeddings
- Requires OpenAI API key and credits
- Higher quality embeddings (optional)

## ⚙️ Configuration

### Document Processing Parameters
- **Chunk Size**: 1000 characters
- **Chunk Overlap**: 200 characters
- **Max Documents**: 50 (configurable)

### Model Parameters
- **LLM**: Qwen-2.5-coder
- **Embedding Model**: all-MiniLM-L6-v2
- **Vector Store**: FAISS

## 🎯 Use Cases

- **Research Paper Analysis**: Query academic papers for specific information
- **Document Summarization**: Extract key insights from lengthy documents
- **Knowledge Base**: Create searchable knowledge repositories
- **Educational Tools**: Interactive learning from textbooks and papers
- **Legal Document Review**: Search through contracts and legal documents

## 📊 Performance

- **Initial Setup**: 2-5 minutes (downloads model + processes documents)
- **Query Response**: 3-10 seconds per question
- **Supported Formats**: PDF documents
- **Scalability**: Handles multiple documents efficiently

## 🔒 Security & Privacy

- **Local Processing**: Documents are processed locally
- **API Security**: Secure API key management via environment variables
- **No Data Storage**: No persistent storage of sensitive information

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Create a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## ⚠️ Troubleshooting

### Common Issues

1. **ModuleNotFoundError: sentence_transformers**
   ```bash
   pip install sentence-transformers
   ```

2. **API Key Errors**
   - Verify `.env` file exists and contains valid keys
   - Check API key permissions and quotas

3. **Memory Issues**
   - Reduce chunk size or document count
   - Use smaller embedding models if needed

### Performance Optimization

- **First Run**: Allow extra time for model downloads
- **Large Documents**: Consider increasing chunk overlap
- **Multiple PDFs**: Process in batches for better performance

## 📧 Support

For questions, issues, or contributions, please:
- Open an issue on GitHub
- Check existing documentation
- Review troubleshooting section

## 🙏 Acknowledgments

- **Groq** for fast LLM inference
- **HuggingFace** for open-source embeddings
- **LangChain** for RAG framework
- **Streamlit** for the web interface
- **FAISS** for efficient vector search

---

**Built with ❤️ for intelligent document analysis**
