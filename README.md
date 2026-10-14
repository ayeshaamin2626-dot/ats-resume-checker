# 📄 ATS Resume Checker

A Streamlit app that scores a resume for ATS (Applicant Tracking System) friendliness and suggests concrete improvements, powered by Google's Gemini Flash model.

## Features

- Upload a resume as **PDF, DOCX or TXT**
- Optional **job description** for a targeted keyword-match score
- Overall **ATS score (0-100)** plus a breakdown (formatting, keywords, experience impact, education, clarity)
- **Strengths, weaknesses and missing keywords**
- **Prioritized improvements** with specific fixes
- Download the report as JSON

## Project structure

```
.
├── app.py
├── requirements.txt
└── README.md
```

## Run locally

1. Get a free API key from [Google AI Studio](https://aistudio.google.com/app/apikey).
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Provide your key (pick one):
   - Create `.streamlit/secrets.toml`:
     ```toml
     GEMINI_API_KEY = "your-key-here"
     ```
   - or set an environment variable:
     ```bash
     export GEMINI_API_KEY="your-key-here"      # macOS/Linux
     set GEMINI_API_KEY=your-key-here           # Windows (cmd)
     ```
4. Start the app:
   ```bash
   streamlit run app.py
   ```

> Never commit `.streamlit/secrets.toml` or your key to GitHub. Add `.streamlit/secrets.toml` to `.gitignore`.

## Configuration

| Setting | Where | Default |
|---|---|---|
| `GEMINI_API_KEY` | Streamlit secrets or env var | required |
| `GEMINI_MODEL` | Streamlit secrets or env var | `gemini-2.5-flash` |

If Google retires or renames the model, set `GEMINI_MODEL` to a current Flash model name without editing code.

## Deploy on Streamlit Community Cloud

1. Push this repo to GitHub.
2. Go to [share.streamlit.io](https://share.streamlit.io) and sign in with GitHub.
3. Click **Create app**, choose the repo, branch `main`, and main file `app.py`.
4. Open **Advanced settings → Secrets** and paste:
   ```toml
   GEMINI_API_KEY = "your-key-here"
   ```
5. Click **Deploy**.

## Notes

- Scanned/image-only PDFs can't be read (ATS systems can't read them either). Use a text-based PDF.
- The resume text is sent to the Gemini API for analysis. The app does not store it.
- Scores are AI estimates, not the output of a real ATS. Use them as guidance.
