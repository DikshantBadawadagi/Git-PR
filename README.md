# Autonomous Code Review Agent System

An AI-powered system designed to autonomously analyze GitHub pull requests. The agent reviews code, identifies potential issues, and provides structured feedback through a robust API. The project leverages asynchronous task processing and a goal-oriented AI agent to streamline code reviews.

---

## 🚀 Features

- **Asynchronous Task Processing**: Code reviews handled asynchronously using Celery.
- **AI Code Review Agent**: Analyzes code for:
  - Code style and formatting issues.
  - Potential bugs or errors.
  - Performance improvements.
  - Adherence to best practices.
- **API Endpoints**:
  - **POST** `/analyze-pr`: Submit a pull request for analysis.
  - **GET** `/status/<task_id>`: Check the status of an analysis task.
  - **GET** `/results/<task_id>`: Retrieve the results of an analysis.
- **Storage Options**: Results stored in Redis or PostgreSQL for persistence.
- **Extensible Framework**: Supports AI frameworks like LangChain, Crewai, LiteLLM, or Autogen.

---

## 📋 Core Requirements

### 1. **API Endpoints (FastAPI)**

#### POST `/analyze-pr`

Accepts GitHub PR details for analysis:
```json
{
  "repo_url": "https://github.com/user/repo",
  "pr_number": 123,
  "github_token": "optional_token"
}
GET /status/<task_id>
Retrieve the current status of a submitted task.

GET /results/<task_id>
Fetch detailed analysis results.

2. Asynchronous Task Processing
Celery for asynchronous task execution.
Task statuses: pending, processing, completed, failed.
Graceful error handling and fallback mechanisms.
3. AI Agent Implementation
The agent analyzes:

Code style and formatting.
Bugs and potential errors.
Performance improvements.
Adherence to best practices.
Example Output:

json
Copy code
{
  "task_id": "abc123",
  "status": "completed",
  "results": {
    "files": [
      {
        "name": "main.py",
        "issues": [
          {
            "type": "style",
            "line": 15,
            "description": "Line too long",
            "suggestion": "Break line into multiple lines"
          },
          {
            "type": "bug",
            "line": 23,
            "description": "Potential null pointer",
            "suggestion": "Add null check"
          }
        ]
      }
    ],
    "summary": {
      "total_files": 1,
      "total_issues": 2,
      "critical_issues": 1
    }
  }
}
💡 Bonus Points
Live Deployment: Host the service on platforms like Railway, Render, etc.
Docker Configuration: Simplify deployment and management with Docker.
Caching: Cache API results for improved performance.
Structured Logging: Enhance debugging and traceability with detailed logs.
Multi-Language Support: Support diverse codebases with multiple programming languages.
GitHub Webhook Integration: Seamlessly integrate with GitHub for automatic PR analysis.
🛠️ Technical Stack
Python: 3.8+
FastAPI: For API development.
Celery: Asynchronous task processing.
Redis/PostgreSQL: Task status and result storage.
AI Frameworks: LangChain, Crewai, LiteLLM, or Autogen.
Testing: pytest for unit and integration tests.
Ollama (Optional): Run language models locally for AI analysis.
📦 Setup Instructions
Clone the repository:

bash
Copy code
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
Install dependencies:

bash
Copy code
pip install -r requirements.txt
Set up environment variables:

Create a .env file based on .env.example.
Add your GitHub token and database credentials.
Start services:

Run Redis/PostgreSQL server.
Start Celery worker:
bash
Copy code
celery -A app.celery_app worker --loglevel=info
Launch the application:

bash
Copy code
uvicorn app.main:app --reload
🚀 Deployment
Docker
Build and run the container:

bash
Copy code
docker-compose up --build
Live Deployment: Deploy to platforms like Render or Railway for real-time testing.

🔍 Testing
Run unit and integration tests:
bash
Copy code
pytest
