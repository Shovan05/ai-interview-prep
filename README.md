# AI Interview Prep

AI-powered interview preparation platform that analyzes your resume and a target job description to generate a personalized match score, technical & behavioral interview questions, skill gap analysis, and a day-wise preparation roadmap. Also generates a tailored, ATS-friendly resume PDF for the job.

## Features

- 🔐 **Authentication** — JWT (cookie-based) auth with register/login/logout and token blacklisting on logout
- 📄 **Resume Parsing** — Upload a PDF resume (parsed with `pdf-parse`) or provide a quick self-description instead
- 🤖 **AI-Generated Interview Report** — Powered by Google Gemini, returns:
  - Match score (0–100) against the job description
  - Technical questions with interviewer intention + model answers
  - Behavioral questions with interviewer intention + model answers
  - Skill gap analysis with severity levels
  - Day-wise preparation roadmap with focus areas and tasks
- 📥 **Tailored Resume PDF** — Generates a job-specific, ATS-friendly resume as a downloadable PDF (via Puppeteer)
- 🗂️ **Report History** — View all previously generated interview reports

## Tech Stack

**Frontend**
- React 19 + Vite
- React Router v7
- Axios
- Sass (SCSS)

**Backend**
- Node.js + Express 5
- MongoDB + Mongoose
- JWT (`jsonwebtoken`) + `bcryptjs` for authentication
- Multer for file uploads
- `pdf-parse` for resume text extraction
- Google Gemini (`@google/genai`) for AI generation
- Zod + `zod-to-json-schema` for structured AI response schemas
- Puppeteer for HTML-to-PDF resume generation

## Project Structure

```
ai_interview_prep/
├── Backend/
│   ├── server.js
│   └── src/
│       ├── app.js
│       ├── config/          # Database connection
│       ├── controllers/     # Auth & interview controllers
│       ├── middlewares/     # Auth guard & file upload
│       ├── models/          # User, InterviewReport, BlacklistToken
│       ├── routes/          # Auth & interview routes
│       └── services/        # Gemini AI integration
└── Frontend/
    └── src/
        ├── app.routes.jsx
        ├── features/
        │   ├── auth/         # Login, Register, auth context/hooks
        │   └── interview/    # Home, Interview report pages, context/hooks
        └── style/
```

## Getting Started

### Prerequisites
- Node.js (v18+ recommended)
- MongoDB instance (local or Atlas)
- Google Gemini API key ([Google AI Studio](https://aistudio.google.com/))

### 1. Clone the repo

```bash
git clone https://github.com/YOUR-USERNAME/ai-interview-prep.git
cd ai-interview-prep
```

### 2. Backend Setup

```bash
cd Backend
npm install
```

Create a `.env` file in `Backend/`:

```env
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
GOOGLE_GENAI_API_KEY=your_gemini_api_key
```

Run the backend:

```bash
npm run dev
```

The server runs on `http://localhost:3000`.

### 3. Frontend Setup

```bash
cd Frontend
npm install
npm run dev
```

The app runs on `http://localhost:5173`.

## API Overview

| Method | Endpoint                                    | Description                          | Access  |
|--------|----------------------------------------------|---------------------------------------|---------|
| POST   | `/api/auth/register`                          | Register a new user                   | Public  |
| POST   | `/api/auth/login`                             | Login user                            | Public  |
| GET    | `/api/auth/logout`                            | Logout & blacklist token              | Public  |
| GET    | `/api/auth/get-me`                            | Get current logged-in user            | Private |
| POST   | `/api/interview/`                              | Generate a new interview report        | Private |
| GET    | `/api/interview/`                              | Get all interview reports              | Private |
| GET    | `/api/interview/report/:interviewId`          | Get a specific interview report        | Private |
| POST   | `/api/interview/resume/pdf/:interviewReportId`| Generate tailored resume PDF           | Private |

## Roadmap / Ideas

- [ ] Add DOCX resume parsing support
- [ ] Add password reset flow
- [ ] Add unit/integration tests
- [ ] Deploy backend + frontend with environment-based config

## License

This project is licensed under the MIT License.

## Contributing

Contributions, issues, and feature requests are welcome. Feel free to open a PR or issue.
