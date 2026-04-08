# 🚀 Multi-Agent Productivity Assistant (GenAI - GCP)

## 📌 Overview

The **Multi-Agent Productivity Assistant** is a cloud-native AI system designed to help users manage tasks, schedules, and notes through intelligent agent coordination.

This project demonstrates how **multiple AI agents collaborate**, interact with tools, and use **Google Cloud Datastore** for persistent storage to execute real-world workflows.

---

## 🎯 Problem Statement

Build a multi-agent AI system that:

* Manages tasks, schedules, and information
* Interacts with multiple tools and data sources
* Executes multi-step workflows
* Deploys as an API-based system

---

## 🧠 Solution Architecture

The system uses a **planner-based multi-agent architecture**:

```
User → API → Planner Agent
                  ↓
        ┌─────────┼─────────┐
        ↓         ↓         ↓
   Task Agent  Calendar   Notes Agent
                  ↓
              Tools Layer
                  ↓
      Google Cloud Datastore
```

---

## 🤖 Agents

### 🔹 Planner Agent

* Interprets user input
* Breaks queries into actionable steps
* Routes tasks to appropriate agents

### 🔹 Task Agent

* Creates and manages tasks

### 🔹 Calendar Agent

* Schedules and manages events

### 🔹 Notes Agent

* Stores and retrieves notes

---

## 🔧 Tools Layer

Acts as an abstraction layer between agents and storage:

* `create_task()`
* `create_event()`
* `add_note()`
* `get_tasks()`
* `get_notes()`

---

## ☁️ Google Cloud Integration

### 🔹 Datastore (Firestore in Datastore mode)

* Stores structured data:

  * Tasks
  * Events
  * Notes
* Provides scalable, serverless storage

### 🔹 Cloud Run (Deployment)

* Hosts FastAPI backend
* Handles API requests

### 🔹 Service Accounts

* Secure authentication for Datastore access

---

## ⚙️ Tech Stack

* **Backend:** Python, FastAPI
* **AI Logic:** Multi-agent architecture (custom / LangChain-ready)
* **Database:** Google Cloud Datastore
* **Cloud Platform:** Google Cloud (Cloud Run, IAM)
* **Environment:** Cloud Shell + CLI

---

## 🔄 Workflow Example

### Input:

```json
"Schedule a meeting tomorrow and create a task for report and save notes"
```

### Execution:

1. Planner analyzes input
2. Breaks into steps:

   * Calendar → schedule meeting
   * Task → create task
   * Notes → save note
3. Agents execute tasks
4. Data stored in Datastore
5. Structured response returned

---

## 📡 API Endpoints

### POST `/query`

Request:

```json
{
  "input": "create a task and add note"
}
```

Response:

```json
{
  "query": "...",
  "plan": ["task", "notes"],
  "results": [...]
}
```

---

## 🗄️ Datastore Schema

### Task

* title
* deadline
* created_at

### Event

* title
* datetime

### Note

* content
* timestamp

---

## 🚀 Setup Instructions

### 1. Clone Repository

```bash
git clone <repo-url>
cd project
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure Environment

Create `.env`:

```
PROJECT_ID=your-gcp-project-id
GOOGLE_APPLICATION_CREDENTIALS=key.json
```

### 4. Authenticate GCP

```bash
gcloud auth application-default login
```

### 5. Run Application

```bash
uvicorn app.main:app --reload
```

---

## ☁️ Deployment (Cloud Run)

```bash
gcloud builds submit --tag IMAGE_URL
gcloud run deploy SERVICE_NAME --image IMAGE_URL --allow-unauthenticated
```

---

## 🔐 Security Notes

* Do not commit `.env` or `key.json`
* Use Google Secret Manager in production
* Use IAM roles for least privilege access

---

## 🌟 Key Features

✔ Multi-agent coordination
✔ Multi-step task execution
✔ Cloud-native architecture
✔ Persistent storage with Datastore
✔ API-first design

---

## 🔮 Future Enhancements

* LLM-based planner (Gemini / GPT)
* Google Calendar API integration
* Vector memory (RAG)
* Async agent execution
* Frontend dashboard

---

## 👨‍💻 Author

**Ayush Maurya**

---

## 📜 License

MIT License
