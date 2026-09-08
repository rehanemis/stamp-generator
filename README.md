# Company Stamp Generator

Generate professional company stamps as transparent PNG files.
Input: Company Name, Slogan, Bottom Line, Color, Shape, Logo.
Output: Transparent PNG ready for Word / PDF documents.

---

## Inputs

| Field        | Required | Description                              | Example                          |
|--------------|----------|------------------------------------------|----------------------------------|
| Company Name | ✅       | Appears curved on top of stamp           | SAKIB HASSAN BUILDING MAINTENANCE |
| Slogan       | ❌       | Middle line inside stamp                 | Building Excellence Since 2010   |
| Bottom Line  | ✅       | Appears curved on bottom of stamp        | AJMAN · U.A.E                    |
| Color        | ❌       | Hex color (default navy blue)            | #1a3d8f                          |
| Shape        | ❌       | round / double_round / oval / rectangle / square_round / diamond / hexagon / badge | round |
| Logo         | ❌       | PNG image, placed in stamp center        | company_logo.png                 |

---

## Run Locally

### Backend (Python)
```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
# API: http://localhost:8000
```

### Frontend (React)
```bash
cd frontend
npm install
npm run dev
# App: http://localhost:5173
```

---

## Deploy Free Online

### Step 1 — Push to GitHub
Create a new GitHub repository and push all files.

### Step 2 — Backend → Railway (free)
1. Go to https://railway.app — sign in with GitHub
2. Click "New Project" → "Deploy from GitHub repo"
3. Select your repo → set Root Directory to `backend`
4. Railway auto-runs: `uvicorn main:app --host 0.0.0.0 --port $PORT`
5. Copy your Railway URL e.g. `https://stamp-api-xxxx.up.railway.app`

### Step 3 — Frontend → Vercel (free)
1. Go to https://vercel.com — sign in with GitHub
2. Click "Add New Project" → import your repo
3. Set Root Directory to `frontend`
4. Add Environment Variable:
   - Name:  `VITE_API_URL`
   - Value: your Railway URL from Step 2
5. Click Deploy → get your free live URL

---

## API Endpoints

### POST /generate
```json
{
  "company":     "SAKIB HASSAN BUILDING MAINTENANCE",
  "slogan":      "Building Excellence",
  "bottom_line": "AJMAN · U.A.E",
  "color":       "#1a3d8f",
  "shape":       "double_round"
}
```
Returns: `{ "image": "data:image/png;base64,..." }`

### POST /generate/download
Same body → returns raw PNG file for download.

### POST /generate/with-logo
Same fields as multipart/form-data + `logo` file field.

---

## Shapes Available
- `round` — Single ring circle
- `double_round` — Double ring circle (most official looking)
- `oval` — Oval / ellipse
- `rectangle` — Rectangle with dividers
- `square_round` — Rounded square
- `diamond` — Diamond / rhombus
- `hexagon` — Hexagon
- `badge` — Circle with ribbon banner below
