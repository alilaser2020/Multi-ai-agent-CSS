# Multi-Agent Intelligent Customer Support System

## 📋 Project Overview
This project implements an **intelligent multi-agent customer support system** using LangChain and LangGraph frameworks. The system efficiently manages customer support requests across three main categories: **Billing**, **Technical**, and **General** inquiries.

## 🏗 System Architecture

### 🤖 Intelligent Agents

#### 1. **Triage Agent**
- **Function**: Initial classification of user requests
- **Output**: One of three categories - BILLING, TECHNICAL, or GENERAL
- **Behavior**: Directly responds to GENERAL queries, routes specialized requests to appropriate agents

#### 2. **Billing Specialist**
- **Function**: Handles financial and subscription-related issues
- **Tools**:
  - `check_subscription_status`: Checks user subscription details
  - `process_refund`: Processes refund requests with payment gateway simulation
- **Database**: *Integrated_user* database with subscription info and transaction history

#### 3. **Technical Support**
- **Function**: Answers technical questions using RAG (Retrieval-Augmented Generation)
- **Tools**:
  - `search_knowledge_base`: Semantic search in technical documentation
- **Features**: Persian language embeddings using ParsBERT for accurate semantic search

#### 4. **Sentiment Guardrail**
- **Function**: Analyzes user sentiment and triggers human intervention when needed
- **Capability**: Interrupts normal flow and connects to senior manager for negative sentiments

## 📚 Technical Knowledge Base

### `tech_doc.txt` - Technical Documentation File

The `tech_doc.txt` file serves as the **primary knowledge source** for the Technical Support agent. This comprehensive Persian-language document contains structured technical information covering:

#### 📖 Document Structure
tech_doc.txt
├── 🛠️ Authentication & Security
├── 🌐 Technical Issues & Troubleshooting
├── 👤 Account Management
├── 💳 Subscription (Non-Financial)
├── 📞 Support Contact Information
├── ❓ Complex/Combined Issues
├── 🧪 Out-of-Scope Questions
└── ⚠️ General Guidelines

#### 🔍 Key Sections

1. **Authentication & Security**
   - Password reset procedures
   - Login troubleshooting
   - Reset page URLs and link validity

2. **Technical Issues**
   - Page display problems
   - Error 500 (Internal Server Error) handling
   - Browser recommendations and versions

3. **Account Management**
   - Profile editing procedures
   - Email change process with two-step verification
   - Security settings

4. **Subscription (Non-Financial)**
   - Technical aspects of subscription renewal
   - Clear separation from financial queries
   - Redirection to billing team for payment issues

5. **Support Channels**
   - Phone numbers and extensions
   - Email addresses for different purposes
   - Live chat availability and hours

6. **Complex Issues**
   - Combined problem troubleshooting (e.g., 404 error + login issues)
   - Priority-based problem solving
   - Post-password-reset troubleshooting

7. **Out-of-Scope Handling**
   - Graceful handling of questions outside knowledge base
   - Suggestions for finding information
   - Escalation paths

#### 🎯 Purpose in the System

The `tech_doc.txt` file is:
- **Loaded** by the TextLoader in the technical support node
- **Split** into chunks using RecursiveCharacterTextSplitter
- **Embedded** using ParsBERT (HooshvareLab/bert-base-parsbert-uncased)
- **Stored** in FAISS vector database
- **Retrieved** for semantic search when users ask technical questions

## 🛠 Technologies Used

### Core Frameworks
- **Python 3.13+**
- **LangChain**: Creating processing chains
- **LangGraph**: Managing multi-agent workflow
- **LangGraph Checkpoint**: Saving conversation state

### Language Models
- **GPT-4o**: Primary model for analysis and responses
- **GPT-4-turbo-preview**: Sentiment analysis

### Search & Embeddings
- **FAISS**: Vector database for similarity search
- **HuggingFace Embeddings**: ParsBERT model for Persian language
- **RecursiveCharacterTextSplitter**: Intelligent text chunking

### Supporting Libraries
- **Pydantic**: Data validation and schema definition
- **python-dotenv**: Environment variable management
- **unittest.mock**: Payment gateway simulation

## 📁 Project Structure
📦 Multi-Agent Customer Support System
├── 📓 Multi-agent_CSS.ipynb # Main project notebook
├── 📄 tech_doc.txt # Technical knowledge base (Persian)
├── 📄 requirements.txt # Project dependencies
├── 📄 .gitignore # Git ignore rules
└── 📄 README.md # Project documentation

## 🚀 Installation & Setup

### 1. Create Virtual Environment
```bash
python -m venv aienv
source aienv/bin/activate  # Linux/Mac
# or
aienv\Scripts\activate     # Windows
```
##    Install Dependencies

pip install -r requirements.txt

##  Configure API Key
```bash
import os
import getpass

os.environ["METISAI_API_KEY"] = getpass.getpass("Enter your API key: ")
```

##  Run the Notebook
jupyter notebook Multi-agent_CSS.ipynb

##💡  Key Features
### Intelligent Conversation Flow
1. Receive user message

2. Triage agent analyzes and categorizes

3. Route to specialized agent

4. Use domain-specific tools

5. Sentiment analysis with human intervention if needed

### 🛡️ Human-in-the-Loop
1. Automatic negative sentiment detection

2. Workflow interruption for manager intervention

3. Direct manager response capability

### 🗄 Integrated Database System
1. User information management

2. ubscription status tracking

3. Transaction history

4. Refund processing logic

### 🔍 Semantic Technical Search (RAG)
1. Persian language embeddings using ParsBERT

2. Technical knowledge base (tech_doc.txt) search

3. Documented and accurate responses

4. Chunk size: 1000 characters with 102 overlap

## 📊 Sample Queries

```bash
[
    "How can I reset my password?",
    "You stole my money! I want to speak with a manager.",
    "What's my subscription status? My ID is 08642",
    "I want a refund for transaction TRX-10020001",
    "Hello, how are you?"
]
```

## 🔧 Customization & Development
### Adding New Agent
```bash
graph.add_node("new_agent", new_agent_function)
graph.add_edge("triage_agent", "new_agent")
```

### Defining New Tool
```bash
new_tool = StructuredTool.from_function(
    func=new_function,
    name="tool_name",
    description="Tool description"
)
```

### Updating Technical Knowledge Base
Simply edit tech_doc.txt to add, modify, or remove technical documentation. 
The RAG system will automatically use the updated content in future queries.

## 📝 Important Notes
- Default Language: Persian (with English support)

- State Management: MemorySaver for conversation history

- Error Handling: Comprehensive try-except in all functions

- Logging: Status printing at each stage for debugging

- Technical Documentation: tech_doc.txt is the sole knowledge source for technical queries


## 📚 Technical Documentation: 
The tech_doc.txt file is specifically designed for the Technical Support agent and contains comprehensive Persian-language technical documentation for troubleshooting common user issues.
