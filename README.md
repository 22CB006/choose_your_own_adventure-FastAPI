# 🧭 Choose Your Own Adventure Game API (Backend)


**Description:** API to generate cool interactive stories using AI ✨  

This backend application, built with **FastAPI**, uses **LangChain** and **OpenAI** to generate branching “choose your own adventure” stories based on a theme (e.g., *pirates*, *spring*, *space travel*).  
Users can test and explore all endpoints directly in **FastAPI’s Swagger UI** (`/docs`).

---

## 🚀 Features

- 🤖 **AI Story Generation:** Creates branching, multi-ending stories using LangChain + OpenAI.  
- 🧩 **Async Processing:** Story generation handled as background jobs.  
- 💾 **Database:** SQLite via SQLAlchemy ORM (local storage).  
- ⚡ **API Testing:** Fully interactive via FastAPI `/docs` or Postman.  
- 🧠 **Schema-Driven:** Follows OpenAPI 3.1 spec with typed Pydantic models.

---

## 🧰 Tech Stack

- **Framework:** FastAPI  
- **Language:** Python  
- **Database:** SQLite  
- **ORM:** SQLAlchemy  
- **AI Integration:** LangChain + OpenAI API  
- **Server:** Uvicorn  
- **Environment Management:** `.env` via Pydantic Settings  

**Libraries Used:**
```
fastapi[all]
langchain
langchain-openai
sqlalchemy
pydantic
psycopg2-binary
```

---

## ⚙️ API Overview

### 🧠 Base URL
```
http://localhost:8000
```

---

### 🔹 1. Create Story  
**POST** `/api/stories/create`  
**Description:** Starts a new AI story generation job.  

**Request Body:**
```json
{
  "theme": "spring"
}
```

**Response Example (200):**
```json
{
  "job_id": "55629d1c-b2df-49c4-889c-fc8cc5311711",
  "status": "pending",
  "created_at": "2025-10-23T10:29:08",
  "story_id": null,
  "completed_at": null,
  "error": null
}
```

**Curl Example:**
```bash
curl -X 'POST' \
  'http://localhost:8000/api/stories/create' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "theme": "spring"
}'
```

---

### 🔹 2. Get Job Status  
**GET** `/api/jobs/{job_id}`  
**Description:** Returns current status of a story generation task.

**Example Request:**
```
/api/jobs/55629d1c-b2df-49c4-889c-fc8cc5311711
```

**Response Example (200):**
```json
{
  "job_id": "55629d1c-b2df-49c4-889c-fc8cc5311711",
  "status": "failed",
  "created_at": "2025-10-23T10:29:08",
  "story_id": null,
  "completed_at": "2025-10-23T15:59:16.103718",
  "error": "Error code: 429 - {'error': {'message': 'You exceeded your current quota, please check your plan and billing details...'}}"
}
```

---

### 🔹 3. Get Complete Story  
**GET** `/api/stories/{story_id}/complete`  
**Description:** Retrieves the fully generated story once the job is completed.

**Response Example:**
```json
{
  "id": 1,
  "title": "The Spring Adventure",
  "content": "You step into a blooming meadow...",
  "is_ending": false,
  "options": [
    { "choice": "Follow the butterfly", "next_node": 2 },
    { "choice": "Rest under the tree", "next_node": 3 }
  ]
}
```

---

## 🧩 Schemas

**StoryJobResponse:**  
`job_id`, `status`, `created_at`, `story_id`, `completed_at`, `error`  

**CompleteStoryNodeResponse:**  
`id`, `content`, `is_ending`, `is_winning_ending`, `options`  

**CreateStoryRequest:**  
`theme: string`

---

## 🧪 Local Setup

**1️⃣ Clone Repository**
```bash
git clone https://github.com/aryalakshmisece/adventure-ai-backend.git
cd adventure-ai-backend
```

**2️⃣ Create Virtual Environment**
```bash
python -m venv venv
source venv/bin/activate  # Mac/Linux
venv\Scripts\activate     # Windows
```

**3️⃣ Install Dependencies**
```bash
pip install -r requirements.txt
```

**4️⃣ Add Environment Variables**

Create a `.env` file in the root folder:
```
OPENAI_API_KEY=your_openai_api_key_here
```

**5️⃣ Run the Server**
```bash
uvicorn main:app --reload
```

App will run at:  
🔗 Base URL → http://127.0.0.1:8000  
📘 Docs → http://127.0.0.1:8000/docs  
📄 OpenAPI Spec → http://127.0.0.1:8000/openapi.json  

---

## ⚠️ Common Error Example

**Error:**
```json
{
  "error": {
    "message": "You exceeded your current quota, please check your plan and billing details.",
    "type": "insufficient_quota"
  }
}
```

**Fix:**  
Make sure your OpenAI API key has valid credits or a paid plan.

---

## 💡 Future Enhancements

- Add React-based frontend for interactive story play  
- Use PostgreSQL for production  
- Deploy on Coro with secrets management  
- Enable story sharing via unique URLs  

---

## 👩‍💻 Author

**Arya Lakshmi**  
AI Engineer
🌐 [GitHub](https://github.com/aryalakshmisece)
