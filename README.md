# 🚀 NL2SQL AI Analytics Agent

An AI-powered Natural Language to SQL analytics assistant built using LangChain and LLMs.  
This system enables users to query relational databases using conversational language instead of writing SQL manually.

---

## 📌 Overview

This project demonstrates how Large Language Models (LLMs) can be integrated with SQL databases to automate query generation and enable conversational analytics.

Users can ask questions like:

- "Show total revenue by restaurant last month"
- "Which campaign had the highest ROI?"
- "Compare week-over-week order growth"
- "Top performing categories by sales"

The system automatically:

1. Understands the natural language query  
2. Generates SQL dynamically  
3. Executes the query  
4. Retrieves results  
5. Formats and returns insights  

---

## 🏗 System Architecture

User Query  
→ Streamlit Chat UI  
→ LangChain SQL Agent  
→ SQLDatabaseToolkit  
→ Database (SQLite / MySQL)  
→ SQL Execution  
→ LLM Response Formatting  
→ Chat Output  

---

## 🛠 Tech Stack

- Python
- Streamlit (UI Layer)
- LangChain (Agent Framework)
- SQLDatabaseToolkit
- SQLAlchemy
- SQLite / MySQL
- Groq LLaMA 3.1 Model
- ReAct Agent (Zero Shot Reasoning)

---

## 🧠 Technical Implementation Highlights

### 1️⃣ LLM Integration

```python
llm = ChatGroq(
    groq_api_key=api_key,
    model_name="llama-3.1-8b-instant",
    streaming=True
)
```

**Details:**

- Uses **LLaMA 3.1 (8B Instant)** model via Groq
- Streaming enabled for real-time response rendering
- Enables conversational AI-based SQL generation
- Supports dynamic query reasoning using LangChain agent framework

---

### 2️⃣ SQL Agent Creation

```python
agent = create_sql_agent(
    llm=llm,
    toolkit=toolkit,
    verbose=True,
    agent_type=AgentType.ZERO_SHOT_REACT_DESCRIPTION
)
```

**Technical Highlights:**

- Implements **ReAct (Reason + Act) reasoning pattern**
- Dynamically decides when to call SQL tools
- Automatically inspects database schema
- Generates SQL queries from natural language
- Executes queries via SQL toolkit
- Returns formatted responses

This architecture reduces hallucination by forcing tool-based execution instead of pure text generation.

---

### 3️⃣ Database Toolkit Integration

```python
toolkit = SQLDatabaseToolkit(db=db, llm=llm)
```

**Enables:**

- Automatic schema awareness
- Table and column inspection
- Query execution through structured tools
- Result retrieval from database
- Structured interaction between LLM and SQL engine

The toolkit bridges LLM reasoning with real database operations.

---

### 4️⃣ Database Configuration & Caching

```python
@st.cache_resource(ttl="2h")
```

- Reuses database connections for improved performance
- Avoids repeated connection initialization
- Enhances application efficiency

Supports:

- Local SQLite database (Read-Only Mode)
- Remote MySQL database (Credential-based connection)

---

### 5️⃣ Session-Based Chat History

```python
st.session_state.messages
```

**Capabilities:**

- Maintains conversation memory
- Supports multi-turn contextual conversations
- Enables interactive analytics experience
- Allows clearing chat history via UI control

This ensures smooth conversational flow and better user experience.

---

## 🔐 Guardrails & Safety Considerations

To ensure safe and controlled execution:

- SQLite opened in **read-only mode**
- Controlled schema exposure via SQLDatabase abstraction
- No direct SQL execution allowed from raw user input
- Agent-based tool invocation instead of raw SQL execution
- Secure credential input via Streamlit sidebar
- Cached database connections for controlled reuse

These measures help minimize risks such as:

- Accidental data modification
- SQL injection
- Unsafe query execution
- Excessive database load

---

## 📈 Business Use Case Inspiration

This solution is inspired by real-world enterprise analytics workflows where non-technical stakeholders frequently require data insights but lack SQL expertise.

It demonstrates how AI agents can:

- Reduce repetitive manual SQL writing
- Improve insight turnaround time
- Enable self-service analytics
- Automate recurring reporting workflows
- Improve accessibility of complex datasets

---

## 🚀 Future Enterprise Implementation

In production environments, this system could be extended with:

- FastAPI backend service
- Role-Based Access Control (RBAC)
- Query cost validation layer
- PII masking mechanisms
- Read-replica database access
- Enterprise LLM hosting (Azure OpenAI / Internal LLM)
- Query logging and monitoring
- Rate limiting
- Governance and compliance controls

These enhancements would make the system enterprise-grade and scalable.

---

## 📊 Potential Impact

Prototype evaluation indicates that automating recurring analytics queries using NL2SQL agents could:

- Reduce ad-hoc query turnaround time by approximately **30–40%**
- Minimize repetitive manual SQL workload
- Improve stakeholder access to insights
- Enable faster decision-making cycles

---

## 🧪 How to Run Locally

### 1️⃣ Clone the Repository

```bash
git clone <your-repo-url>
cd nl2sql-ai-analytics-agent
```

### 2️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

### 3️⃣ Run the Streamlit App

```bash
streamlit run app.py
```

### 4️⃣ Usage Steps

- Enter your Groq API key
- Select database type (SQLite / MySQL)
- Provide credentials if required
- Start asking business questions in natural language

---

## 🎯 Key Learnings

- Schema grounding is critical for accurate SQL generation
- LLM guardrails are essential in enterprise environments
- Tool-based agents reduce hallucination risks
- Read-only database access improves safety
- Conversational analytics enhances user adoption
- Enterprise productionization requires governance planning

---

## 👤 Author

Developed by **Souvik Karmakar**

GenAI | Data Analytics | AI Automation | NL2SQL Systems
