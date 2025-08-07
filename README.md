# 🚀 AI-Powered Insurance Claims Evaluation – HackRx 6.0 Submission

This project presents an innovative, AI-powered solution for automating the evaluation of insurance claims using a **Retrieval-Augmented Generation (RAG)** pipeline. Built for **HackRx 6.0**, this self-contained system provides **transparent**, **data-driven**, and **privacy-preserving** decision-making based on private policy documents — all on your local machine.

---

## 🧠 Architecture Overview

The system is built on a modular RAG architecture, integrating:

| Component        | Description |
|------------------|-------------|
| **LLM**          | [`Gemma 3`](https://ollama.com/library/gemma) (via Ollama) for natural language understanding and reasoning. |
| **RAG Backend**  | Fork of `localGPT` customized for insurance use-cases. |
| **Embedding Model** | [`Qwen3-Embedding-0.6B`](https://huggingface.co/Qwen/Qwen3-Embedding-0.6B) for vectorizing documents and queries. |
| **Vector Store** | [`LanceDB`](https://lancedb.github.io/lancedb/) for high-performance local vector storage. |
| **API Server**   | Python-based REST API (`rag_system/api_server.py`) to handle interactions. |
| **Backend Services** | Local Python scripts for session, document, and database management. |

---

## ✅ Key Features

- **⚖️ Transparent Decisions**  
  Returns relevant clauses and document names used in decision-making.

- **🔒 100% Private**  
  All data stays on your machine. No third-party APIs or cloud services.

- **🧾 Structured Output**  
  JSON-based responses make integration with other platforms easy.

- **💸 Scalable & Cost-Effective**  
  Built on open-source models; no ongoing API usage fees.

---

## ⚙️ API Endpoints

Base URL: `http://localhost:8001`

### 🔍 1. POST `/chat` – Evaluate a Claim

Submit a query about an insurance scenario and get an automated decision.

#### ✅ Request Body:
```json
{
  "query": "A 55-year-old female had a successful angioplasty. Her policy has been active for 2 years. Is this covered?",
  "session_id": "your_unique_test_session_id"
}
🔁 Response:
json
Copy
Edit
{
  "Decision": "approved",
  "Amount": "₹80,000",
  "Justification": [
    {
      "clause": "Coverage includes angioplasty if policy duration exceeds 1 year.",
      "source_document": "Policy_Document_v1.pdf"
    }
  ]
}
📄 2. POST /index – Index New Documents
Use this to ingest new policy PDFs into the vector database.

✅ Request Body:
json
Copy
Edit
{
  "file_paths": [
    "D:\\HackRx_Project\\localGPT\\rag_system\\documents\\Policy_Document_v1.pdf"
  ],
  "session_id": "your_unique_test_session_id"
}
🛠️ Local Setup Guide
1. 📦 Clone the Repository
bash
Copy
Edit
git clone https://github.com/your-username/insurance-claims-evaluator
cd insurance-claims-evaluator
2. 🐍 Setup Python Virtual Environment
bash
Copy
Edit
python -m venv venv
source venv/bin/activate  # or .\venv\Scripts\activate (Windows)
3. 🔧 Install Dependencies
bash
Copy
Edit
pip install -r requirements.txt
4. 🧠 Install Ollama & Models
Install Ollama: https://ollama.com/download

Then pull the required models:

bash
Copy
Edit
ollama pull gemma3
ollama pull qwen3:0.6b
5. 📁 Prepare Policy Documents
Place your .pdf files inside:

bash
Copy
Edit
rag_system/documents/
6. 📚 Index the Documents
bash
Copy
Edit
python create_index_script.py
Follow the on-screen prompts to ingest your files.

7. 🚀 Start the API Server
bash
Copy
Edit
python -m rag_system.api_server
Keep this terminal running.

8. 💬 Start Chat Client
In a new terminal:

bash
Copy
Edit
python chat_client.py
Type your query and get a real-time decision.

🎯 Sample Query
“A 46-year-old male had knee surgery in Pune. His insurance started 3 months ago. Is this covered?”

Expected output (example):

json
Copy
Edit
{
  "Decision": "rejected",
  "Amount": "N/A",
  "Justification": [
    {
      "clause": "Surgeries are only covered after a 6-month waiting period.",
      "source_document": "Policy_Document_v2.pdf"
    }
  ]
}
💡 Why This Matters
✅ Removes human bias & manual effort
✅ Ensures consistent & transparent claim evaluations
✅ Designed with real-world constraints like data privacy
✅ 100% open-source & offline-ready solution

👨‍💻 Contributors
Kshitiz Naik – AI/ML Engineer
📄 License
This project is licensed under the MIT License.

📄 License
This project is licensed under the MIT License.
