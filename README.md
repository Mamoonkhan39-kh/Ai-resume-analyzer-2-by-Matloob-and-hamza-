# Resume ATS & Interview Coach

A Streamlit app that uses Google's Gemini API to review an uploaded resume and provide an estimated ATS-readiness score, role-specific improvements, keyword suggestions, improved bullet examples, interview questions, STAR-story prompts, and a learning plan.

> **Important:** The score is an AI-generated estimate, not a real employer ATS score and not a prediction of whether you will get an interview. Different ATS products and employers use different rules.

## Features

- Upload a text-based PDF, DOCX, or TXT resume (maximum 10 MB)
- Enter a target role and experience level
- Optionally paste the job description for more targeted recommendations
- View score breakdown, strengths, priority fixes, keywords, and section feedback
- Get professional-summary and experience-bullet examples
- Practice likely interview questions and STAR-format stories
- Download the report as JSON or TXT
- API key is read from Streamlit secrets or the `GEMINI_API_KEY` environment variable

## Files

- `app.py` — Streamlit application
- `requirements.txt` — Python dependencies
- `README.md` — setup and deployment guide

## Run locally

You need Python 3.10 or newer and a Gemini API key from Google AI Studio.

1. Download or clone this repository and open a terminal in its folder.
2. Create a virtual environment (recommended):

   **Windows**
   ```powershell
   py -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

   If `py` is unavailable, try `python -m venv .venv`.

3. Install packages:
   ```bash
   python -m pip install -r requirements.txt
   ```
4. Set your API key for the current terminal session. Do not paste the key into `app.py` or commit it to GitHub.

   **Windows PowerShell**
   ```powershell
   $env:GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
   ```

   **macOS/Linux**
   ```bash
   export GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
   ```

5. Start the app:
   ```bash
   python -m streamlit run app.py
   ```
6. Open the local URL shown in the terminal, usually `http://localhost:8501`.

The default model is `gemini-2.5-flash`. If that model is unavailable to your Google AI account, change the model field in the sidebar to a model name currently available to your account.

## Push to GitHub using the website UI (no Git commands)

1. Sign in at [GitHub](https://github.com/) and click **+** → **New repository**.
2. Give it a name such as `resume-ats-interview-coach`. Choose Public or Private, then click **Create repository**. You can skip adding a README because this project already has one.
3. On the new repository page, choose **Add file** → **Upload files**.
4. Upload these three files: `app.py`, `requirements.txt`, and `README.md`. Make sure they are at the repository root, not inside an extra folder.
5. Enter a commit message such as `Add Resume ATS and Interview Coach app` and click **Commit changes**.
6. Check that all three filenames appear on the repository's main page.

**Security:** Never upload your API key, a `.env` file containing the key, or a real resume. If a key is accidentally committed, revoke it and create a new one.

## Deploy on Streamlit Community Cloud

1. Push the three files to GitHub using the steps above.
2. Open [Streamlit Community Cloud](https://share.streamlit.io/) and sign in with GitHub.
3. Click **Create app** (or **New app**), select the repository, branch (usually `main`), and main file path `app.py`.
4. Open **Advanced settings** / **Secrets** before or after deployment (the label may vary by interface).
5. Add the following in the Secrets box, replacing the placeholder with your real key:

   ```toml
   GEMINI_API_KEY = "YOUR_GEMINI_API_KEY"
   ```

6. Click **Deploy**. Wait for the build to finish, then open the app URL.
7. If you change code on GitHub, Streamlit Cloud normally detects the commit and redeploys. If it does not, use the app's **Manage app** controls to reboot or redeploy.

Do not add quotes around the entire TOML line; only the key value should be quoted. Keep secrets out of your GitHub repository.

## Troubleshooting

- **Gemini API key not found:** Check the spelling `GEMINI_API_KEY`, save Secrets, then reboot the app.
- **Invalid API key / permission error:** Create or verify a key in Google AI Studio and confirm that the Gemini API is enabled for the project.
- **Quota or rate-limit error:** Check the API project's quota and billing/usage settings; wait and retry if the limit is temporary.
- **Model not found:** Use a model name available to your account; update the model field in the sidebar.
- **PDF has no readable text:** The PDF may be scanned. Use a text-based PDF or DOCX, or OCR it before upload.
- **Deployment dependency error:** Confirm `requirements.txt` is at the repository root and check the Streamlit build logs for the package that failed.
- **Large resume:** The app accepts files up to 10 MB and sends up to 45,000 extracted characters to Gemini.

## Privacy and responsible use

The app sends extracted resume text and any pasted job description to Google's Gemini API. Do not upload documents unless you are comfortable sharing their contents with that service. The app does not intentionally save resumes to a database, but hosting and API providers may process data under their own policies. Review applicable privacy requirements before using this with customers. AI suggestions can be wrong; candidates should verify every claim and never add invented achievements or qualifications.

## Testing

Basic static validation was performed with Python's syntax compiler. A live Gemini API request and Streamlit Cloud deployment require your API key and account, so those cannot be verified from this project bundle. Test locally with a non-sensitive sample resume before sharing the app publicly.
