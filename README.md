# AI-Powered SQL Database Query Assistant

## 📌 Project Overview

The AI-Powered SQL Database Query Assistant enables users to interact with a SQL database using natural language instead of writing SQL queries manually.

Using LangChain and Groq's Llama 3.1 model, the system converts user questions into SQL queries, executes them against a database, and returns meaningful results.

This project demonstrates the integration of Large Language Models (LLMs) with relational databases for intelligent data retrieval.

---

## 🚀 Features

* Natural Language to SQL Conversion
* Automatic SQL Query Generation
* SQL Server Database Connectivity
* Fast Query Execution
* Groq LLM Integration
* LangChain SQL Query Chain
* Dynamic Data Retrieval
* Easy-to-Use Interface for Database Queries

---

## 🛠️ Tech Stack

| Technology    | Purpose                         |
| ------------- | ------------------------------- |
| Python        | Programming Language            |
| LangChain     | LLM Orchestration Framework     |
| Groq API      | Large Language Model Provider   |
| Llama 3.1     | Language Model                  |
| SQLAlchemy    | Database ORM and Connectivity   |
| PyODBC        | SQL Server Driver               |
| SQL Server    | Relational Database             |
| Python-dotenv | Environment Variable Management |
| Pandas        | Data Processing                 |

---

## 📂 Project Structure

```text
project/
│
├── README.md
├── requirements.txt
├── .env
├── company.db
└── SQL_Query_Assistant.ipynb
```

---

## ⚙️ Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd project
```

### 2. Create Virtual Environment

```bash
python -m venv venv
```

### Activate Virtual Environment

#### Windows

```bash
venv\Scripts\activate
```

#### Linux / macOS

```bash
source venv/bin/activate
```

---

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 📦 Requirements

```txt
langchain
langchain-community
langchain-groq
sqlalchemy
pyodbc
python-dotenv
pandas
```

---

## 🔐 Environment Variables

Create a `.env` file inside the project root directory.

```env
GROQ_API_KEY=YOUR_API_KEY
```

Replace `YOUR_API_KEY` with your Groq API key.

---

## 🗄️ Database Configuration

Configure SQL Server connection details:

```python
SERVER = "RANI\\RAMYASERVER"
DATABASE = "project_file"
USERNAME = "sa"
PASSWORD = "Password123"
```

---

## 🔗 Database Connection String

```python
DATABASE_URI = (
    f"mssql+pyodbc://{USERNAME}:{PASSWORD}"
    f"@{SERVER}/{DATABASE}"
    "?driver=ODBC+Driver+17+for+SQL+Server"
)
```

---

## 📥 Load Environment Variables

```python
from dotenv import load_dotenv

load_dotenv()
```

---

## 🤖 Initialize Groq LLM

```python
from langchain_groq import ChatGroq
import os

llm = ChatGroq(
    groq_api_key=os.getenv("GROQ_API_KEY"),
    model_name="llama-3.1-8b-instant",
    temperature=0
)
```

### Parameter Description

| Parameter    | Description                  |
| ------------ | ---------------------------- |
| groq_api_key | Authentication Key           |
| model_name   | LLM Model                    |
| temperature  | Controls Response Randomness |

---

## 🏗️ Create Database Engine

```python
from sqlalchemy import create_engine

engine = create_engine(DATABASE_URI)
```

---

## 📊 Create SQL Database Object

```python
from langchain_community.utilities import SQLDatabase

db = SQLDatabase(engine)
```

This object allows LangChain to access database tables and metadata.

---

## 📋 Display Available Tables

```python
print(db.get_usable_table_names())
```

Purpose:

* Verify database connection.
* Display accessible tables.
* Validate schema availability.

---

## 🔄 Create SQL Query Chain

```python
from langchain.chains import create_sql_query_chain

chain = create_sql_query_chain(llm, db)
```

The query chain converts natural language questions into SQL statements.

---

## 🧠 Workflow

```text
User Question
      │
      ▼
Groq LLM (Llama 3.1)
      │
      ▼
LangChain SQL Query Chain
      │
      ▼
Generate SQL Query
      │
      ▼
SQL Server Database
      │
      ▼
Execute Query
      │
      ▼
Return Results
      │
      ▼
Display Output
```

---

## 💻 Query Function

```python
def ask_question(question):

    sql_query = chain.invoke({
        "question": question
    })

    print("Generated SQL Query:")
    print(sql_query)

    result = db.run(sql_query)

    return result
```

---

## 📝 Example Usage

### User Question

```text
Show all employees earning more than 50000
```

### Generated SQL

```sql
SELECT *
FROM Employees
WHERE Salary > 50000;
```

### Execute Query

```python
result = ask_question(
    "Show all employees earning more than 50000"
)

print(result)
```

---

## ✅ Advantages

* Eliminates manual SQL writing.
* Faster database querying.
* User-friendly interface.
* Supports business users with no SQL knowledge.
* Reduces development effort.
* Enhances productivity.

---

## 🔮 Future Enhancements

* Streamlit Web Application
* Chat Interface
* Query History Tracking
* User Authentication
* Multi-Database Support
* Data Visualization Dashboard
* Export Results to CSV/Excel
* Role-Based Access Control

---

## 👨‍💻 Author

**Ramya Priya**

Data Science & AI Project

---

## 📄 License

This project is developed for educational and learning purposes.
