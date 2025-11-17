# 🚀 AgentScholar Setup Guide

Follow these steps to get AgentScholar running on your machine.

## Prerequisites Check

Before starting, ensure you have:

- ✅ Python 3.10 or higher (`python --version`)
- ✅ Node.js 18+ and npm (`node --version`)
- ✅ Google Gemini API key ([Get one here](https://makersuite.google.com/app/apikey))

## Step-by-Step Setup

### 1️⃣ Backend Setup (5 minutes)

Open a terminal in the project root:

```cmd
d backend
```

Create and activate a virtual environment:

```cmd
python -m venv venv
venv\Scripts\activate
```

Install Python dependencies:

```cmd
pip install -r requirements.txt
```

Create your `.env` file:

```cmd
copy .env.example .env
```

Edit `.env` and add your Gemini API key:

```env
GEMINI_API_KEY=your_actual_api_key_here
```

Start the backend server:

```cmd
python main.py
```

✅ **Backend should now be running at http://localhost:8000**

Test it by visiting: http://localhost:8000 (you should see a JSON response)

---

### 2️⃣ Frontend Setup (3 minutes)

Open a **NEW terminal** (keep backend running) and navigate to frontend:

```cmd
cd frontend
```

Install Node.js dependencies:

```cmd
npm install
```

Start the development server:

```cmd
npm run dev
```

✅ **Frontend should now be running at http://localhost:3000**

---

### 3️⃣ Test the Application

1. Open your browser to **http://localhost:3000**
2. You should see the AgentScholar interface
3. Try an example query:
   - "What are the latest advances in quantum computing?"
4. Click "Generate Research Report"
5. Watch the progress as agents work:
   - Planner generates sub-questions
   - Executors research in parallel
   - Publisher creates final report
6. View your comprehensive 2000+ word report!

---

## 🎯 Quick Start Commands

### Backend

```cmd
cd backend
venv\Scripts\activate
python main.py
```

### Frontend

```cmd
cd frontend
npm run dev
```

---

## 🔍 Verifying Installation

### Check Backend

Visit http://localhost:8000/docs to see the interactive API documentation

### Check Frontend

Visit http://localhost:3000 to see the React application

### Test the Full Workflow

1. Submit a query from the frontend
2. Watch real-time progress updates
3. Download the final report as Markdown

---

## 🐛 Troubleshooting

### Backend Issues

**"ModuleNotFoundError"**

```cmd
# Make sure virtual environment is activated
venv\Scripts\activate
pip install -r requirements.txt
```

**"GEMINI_API_KEY not found"**

- Check that `.env` file exists in `backend/` directory
- Verify the API key is correctly set (no spaces, quotes)

**"Port 8000 already in use"**

- Kill the existing process or change port in `main.py`

### Frontend Issues

**"Cannot find module"**

```cmd
# Delete node_modules and reinstall
rmdir /s node_modules
npm install
```

**"CORS errors"**

- Ensure backend is running on port 8000
- Check `vite.config.ts` proxy settings

**TypeScript errors during development**

- These are expected before installing dependencies
- Run `npm install` to resolve

---

## 📊 Expected Behavior

### Timeline for a Research Query

1. **Planning (20%)**: ~5-10 seconds - Generates sub-questions
2. **Executing (60%)**: ~30-60 seconds - Researches each question
3. **Publishing (100%)**: ~10-20 seconds - Synthesizes report

**Total**: ~1-2 minutes for a complete report

### What You'll See

- Progress bar moving through stages
- Sub-questions appearing one by one
- Status updates in real-time
- Final report with:
  - 2000+ words
  - Multiple sections (Introduction, Evidence, Analysis, etc.)
  - Inline citations [S1], [S2], etc.
  - Full bibliography

---

## 🎨 Example Queries to Try

Start with these to test the system:

1. **Technology**: "What are the environmental impacts of blockchain technology?"
2. **Science**: "How is CRISPR gene editing being used in cancer treatment?"
3. **AI Ethics**: "What are the ethical implications of AI in autonomous vehicles?"
4. **Climate**: "What are the most promising carbon capture technologies?"
5. **Health**: "What is the current state of mRNA vaccine research beyond COVID-19?"

---

## 📝 Next Steps

Once everything is working:

1. **Explore the API**: Visit http://localhost:8000/docs
2. **Customize Prompts**: Edit `backend/llm/prompts.py`
3. **Adjust Agent Logic**: Modify files in `backend/agents/`
4. **Style the Frontend**: Update Tailwind classes in React components
5. **Add Real Search**: Integrate actual web search APIs in `executor.py`

---

## 🎓 Understanding the Architecture

```
Frontend (React)                Backend (FastAPI)
─────────────────              ──────────────────
                             
QueryPage.tsx                   main.py (REST API)
     │                               │
     ├─> POST /api/report           │
     │                          graph.py (LangGraph)
     │                               │
     ├─> GET /status           ┌─────┴─────┐
     │   (polling)             │           │
     │                    planner    executor (×6-10)
     ├─> GET /stream          │           │
     │   (SSE)                └─────┬─────┘
     │                              │
     └─> GET /report            publisher
                                    │
                              Final Report
```

---

## 💡 Tips for Success

1. **First Run**: Use a simple query to verify everything works
2. **API Key**: Keep your Gemini API key secure, don't commit it
3. **Memory**: Remember all data is in-memory - restarting clears everything
4. **Development**: Use `--reload` flag with uvicorn for auto-restart

---

## ✅ Checklist

Before considering setup complete:

- [ ] Backend starts without errors at http://localhost:8000
- [ ] Frontend loads at http://localhost:3000
- [ ] Can submit a research query
- [ ] Progress updates appear in real-time
- [ ] Final report generates successfully
- [ ] Can download report as Markdown

---

## 🆘 Getting Help

If you encounter issues:

1. Check the console output for both backend and frontend
2. Verify all environment variables are set correctly
3. Ensure both servers are running simultaneously
4. Review the troubleshooting section above

---

**Happy Researching! 🎉**

Your AgentScholar system is now ready to generate comprehensive AI-powered research reports!
