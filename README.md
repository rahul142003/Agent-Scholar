# AgentScholar

Agent Scholar is a multi agent research automation platform built with LangGraph and Google Gemini. It automatically conducts deep research across multiple trusted sources and generates well structured research papers of more than 2000 words, complete with properly cited references.

## 🌟 Features

- **Multi-Agent Workflow**: Planner → Concurrent Researchers → Final Compiler pipeline
- **Depth-Oriented Research**: Automatically creates 6–10 targeted sub-questions and handles them in parallel
- **Extended Report Generation**: Produces detailed 2000+ word research documents with inline reference markers like [S1], [S2]
- **Live Execution Tracking**: Real-time status updates streamed via Server-Sent Events (SSE)
- **Modern Technology Stack**: FastAPI + LangGraph + Gemini LLM + React + TypeScript
- **Memory-Based Data Handling**: Operates entirely in memory without the need for a database


## 🏗️ Architecture

```
User Question
      ↓
┌────────────────┐
│    Planner     │  → Expands the query into 6–10 focused sub-topics
└────────────────┘
      ↓
┌────────────────┐
│   Researchers  │  → Executes parallel investigation for each sub-topic
│   (Concurrent) │  → Collects sources, key findings, and citation data
└────────────────┘
      ↓
┌────────────────┐
│   Aggregator   │  → Combines and organizes all results into a coherent document
└────────────────┘
      ↓
Final Research Output (2000+ words including inline citations)

```

## 📋 Prerequisites

- Python 3.10 or higher
- Node.js 18+ and npm
- Google Gemini API key ([Get one here](https://makersuite.google.com/app/apikey))

## 🚀 Quick Start

### Backend Setup

1. Navigate to the backend directory:
```bash
cd backend
```

2. Create a virtual environment:
```bash
python -m venv venv

# On Windows:
venv\Scripts\activate

# On macOS/Linux:
source venv/bin/activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Create a `.env` file with your Gemini API key:
```bash
copy .env.example .env
# Edit .env and add your GEMINI_API_KEY
```

5. Start the backend server:
```bash
python main.py
```

The backend will run at `http://localhost:8000`

### Frontend Setup

1. Navigate to the frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

The frontend will run at `http://localhost:3000`

## 📡 API Endpoints

### `POST /api/report`
Create a new research task
```json
{
  "query": "What are the latest advances in quantum computing?"
}
```

### `GET /api/report/{task_id}/status`
Get task status and progress

### `GET /api/report/{task_id}`
Get complete task state including final report

### `GET /api/report/{task_id}/stream`
Server-Sent Events stream for real-time progress updates

### `GET /api/reports`
List all active research tasks

### `DELETE /api/report/{task_id}`
Delete a research task

## 🧪 Example Queries

- "How does blockchain technology affect the environment and sustainability efforts?"
- "In what ways is CRISPR being applied in modern cancer therapeutics?"
- "What recent breakthroughs have occurred in quantum computing and how might they impact cryptography?"
- "What ethical challenges arise from the use of AI in self-driving vehicles?"

## 🔧 Project Structure

```
AgentScholar/
├── backend/
│   ├── agents/
│   │   ├── planner.py      # Sub-question generation
│   │   ├── executor.py     # Parallel research execution
│   │   └── publisher.py    # Report synthesis
│   ├── llm/
│   │   ├── gemini_client.py # Gemini API wrapper
│   │   └── prompts.py       # System prompts
│   ├── main.py              # FastAPI application
│   ├── graph.py             # LangGraph workflow
│   ├── models.py            # Pydantic models
│   ├── memory.py            # In-memory storage
│   └── requirements.txt
│
└── frontend/
    ├── src/
    │   ├── api/
    │   │   ├── client.ts    # API client
    │   │   └── hooks.ts     # React Query hooks
    │   ├── components/
    │   │   ├── ProgressTracker.tsx
    │   │   └── ReportDisplay.tsx
    │   ├── pages/
    │   │   └── QueryPage.tsx
    │   ├── App.tsx
    │   └── main.tsx
    ├── package.json
    └── vite.config.ts
```

## 🎯 Workflow Details

### 1. Planner Agent
- Analyzes user query
- Generates 6-10 focused sub-questions
- Covers: background, current state, findings, methodologies, controversies, limitations, future directions

### 2. Executor Agents (Parallel)
- Each sub-question is researched independently
- Simulates web search and retrieval
- Extracts facts, summaries, and citations
- Returns structured data with sources

### 3. Publisher Agent
- Synthesizes all research into cohesive narrative
- Creates structured report with sections:
  - Introduction
  - Background & Fundamentals
  - Current Evidence & Findings
  - Methodologies & Approaches
  - Controversies & Limitations
  - Future Directions & Implications
  - Conclusion
  - References
- Uses inline citations [S1], [S2], etc.
- Ensures 2000+ word count

## ⚙️ Configuration

### Backend Environment Variables
Create a `.env` file in the `backend/` directory:
```env
GEMINI_API_KEY=your_api_key_here
```

### Frontend Environment Variables (Optional)
Create a `.env` file in the `frontend/` directory:
```env
VITE_API_URL=http://localhost:8000
```

## 🔒 Important Notes

- **In-Memory Only**: All data is stored in memory and will be lost on server restart
- **No Persistence**: This is by design - no database or file storage
- **Demo Purposes**: The executor currently simulates web search. For production, integrate real search APIs
- **API Costs**: Be aware of Gemini API usage and rate limits

## 🛠️ Development

### Backend Development
```bash
cd backend
uvicorn main:app --reload
```

### Frontend Development
```bash
cd frontend
npm run dev
```

### Build Frontend for Production
```bash
cd frontend
npm run build
```

## 📝 License

MIT License - feel free to use this project for learning and development.

## 🤝 Contributing

Contributions are welcome! This is a demonstration project showcasing multi-agent research workflows.

## 🐛 Troubleshooting

### Backend won't start
- Ensure Python 3.10+ is installed
- Check that all dependencies are installed: `pip install -r requirements.txt`
- Verify GEMINI_API_KEY is set in `.env`

### Frontend compilation errors
- Run `npm install` to ensure all dependencies are installed
- Clear node_modules and reinstall: `rm -rf node_modules && npm install`

### CORS errors
- Ensure backend is running on port 8000
- Check frontend proxy configuration in `vite.config.ts`

## 📚 Learn More

- [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)
- [Google Gemini API](https://ai.google.dev/)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [React Documentation](https://react.dev/)

---

Built with ❤️ using LangGraph, Gemini, FastAPI, and React ❤️.
