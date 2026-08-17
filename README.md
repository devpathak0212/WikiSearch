# WikiSearch

WikiSearch is a full-stack web application that delivers concise, clean summaries from Wikipedia based on any search query entered by the user. Instead of navigating through full Wikipedia articles, users get a direct, well-extracted summary in seconds through a simple and responsive interface.

**Live:** https://searchwikipedia.vercel.app

---

## How It Works

The user types a topic into the search bar and either clicks **Search** or presses **Enter**. The React frontend sends the query to the FastAPI backend, which uses LangChain's Wikipedia tool to fetch and clean the relevant summary, then returns it to be displayed on the page. A loading spinner shows while the request is in progress, and an error message is shown if it fails.

---

## Project Structure

```
WikiSearch/
├── backend/
│   ├── main.py            # FastAPI application with the /wiki POST endpoint
│   └── requirements.txt   # Python dependencies
│
└── frontend/
    ├── public/            # Static HTML and assets
    └── src/
        ├── App.js         # Main React component with all UI logic
        └── index.js       # React entry point
```

---

## Tech Stack

- **Backend:** FastAPI, Uvicorn, LangChain (Wikipedia tool)
- **Frontend:** React 19, Material UI (MUI) v7

---

## Running Locally

**Backend:**
\`\`\`bash
cd backend
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --reload
\`\`\`
Runs at \`http://localhost:8000\`

**Frontend:**
\`\`\`bash
cd frontend
npm install
npm start
\`\`\`
Runs at \`http://localhost:3000\`

Both servers must be running simultaneously for the app to function locally.

---

## Deployment

- **Backend:** hosted on Render
- **Frontend:** hosted on Vercel

Both auto-deploy on every push to \`main\`.
