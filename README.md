# WikiSearch

WikiSearch is a full-stack web application that delivers concise, clean summaries from Wikipedia based on any search query entered by the user. Instead of navigating through full Wikipedia articles, users get a direct, well-extracted summary in seconds through a simple and responsive interface.

---

## How It Works

The user types any topic into the search bar and either clicks the **Search** button or presses **Enter**. The React frontend sends the query as a POST request to the FastAPI backend. The backend passes the query to LangChain's `WikipediaQueryRun` tool, which internally uses the Wikipedia API to fetch the most relevant article. If the raw result contains a `Summary:` section, it is extracted and cleaned before being returned to the frontend. The result is then displayed on the page in a readable format. While the request is in progress, a loading spinner is shown. If the request fails, an error message is displayed to the user.

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

## Backend

The backend is built with **FastAPI** and served using **Uvicorn**. It exposes a single endpoint:

**`POST /wiki`**

- Accepts a JSON body with a `query` field (string)
- Uses LangChain's `WikipediaQueryRun` with `WikipediaAPIWrapper` configured to fetch the top 1 result
- Strips the `Summary:` label from the raw Wikipedia output if present
- Returns a JSON response with a `result` field containing the cleaned summary
- CORS is fully open (`allow_origins=["*"]`) to support the React frontend during development and in production

**Dependencies (`requirements.txt`):**
- `fastapi`
- `uvicorn`
- `langchain-community`
- `wikipedia`

---

## Frontend

The frontend is a **React 19** single-page application styled with **Material UI (MUI) v7**. It consists of a single component (`App.js`) that manages four pieces of state: the search query, the result, a loading boolean, and an error message.

The UI includes:
- A centered title styled with the *Bowlby One* font in MUI's primary blue (`#1976D2`)
- A subtitle in the *Short Stack* cursive font
- A full-width dark-themed `TextField` (dark background `#222222`, white text) where the user types their query
- A **Search** `Button` that triggers the API call and is disabled while loading
- A `CircularProgress` spinner shown during the fetch
- An error `Typography` element shown in red if the request fails
- The result displayed in a justified, line-height-1.7 `Typography` block in the *Short Stack* font

The frontend currently points to the deployed backend at `https://wikisearch-backend.onrender.com/wiki`. To use a local backend, this URL in `App.js` should be changed to `http://localhost:8000/wiki`.

**Key dependencies (`package.json`):**
- `react` ^19.2.3
- `react-dom` ^19.2.3
- `@mui/material` ^7.3.7
- `@mui/icons-material` ^7.3.7
- `@emotion/react` ^11.14.0
- `@emotion/styled` ^11.14.1

---

## Running the Project

**Backend:**
```bash
cd backend
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --reload
```
Runs at `http://localhost:8000`

**Frontend:**
```bash
cd frontend
npm install
npm start
```
Runs at `http://localhost:3000`

Both servers must be running simultaneously for the app to function locally.