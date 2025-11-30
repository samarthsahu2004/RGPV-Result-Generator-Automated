# RGPV-Result-Generator-Automated
RGPV RESULT GENERATOR AUTOMATED
=================================

Project overview
----------------
An automated tool to fetch RGPV student results in bulk. The system uses Selenium to navigate the RGPV results page, solves the CAPTCHA via Google Gemini (Generative AI) OCR, extracts student result data (name, enrollment number, subject grades, SGPA, CGPA), and stores results in CSV files. A Streamlit front-end provides a simple UI for users to submit batches and retrieve results via a Flask webhook.

This project includes:
- Automation.py  — main Selenium script that scrapes results and handles captcha solving
- app.py         — Streamlit web UI for users to submit batches and request a generated file
- webhook.py     — Flask webhook that triggers Automation.py in a background thread
- requirements.txt
- .devcontainer  — devcontainer configuration for development environment
- files/         — directory where CSV output files are stored

Key features
------------
- Bulk result extraction for a range of roll numbers (supports lateral students)
- CAPTCHA solving via Google Generative AI (Gemini) image-to-text
- Headless Chrome browser automation (Selenium)
- Background processing using Python threading (Flask webhook launches Automation)
- Streamlit front-end to submit jobs and download generated CSV via token
- Output: CSV files containing Name, Enrollment No, Subject Grades, Result, SGPA, CGPA

Tech stack
----------
- Python 3.11+
- Selenium
- Google Generative AI (Gemini) Python SDK
- Flask
- Streamlit
- Google Chrome / ChromeDriver

Prerequisites
-------------
1. Python 3.8+ (recommended 3.11)
2. Google Chrome installed
3. Matching ChromeDriver for your Chrome version (on PATH or in working dir)
4. An API key for Google Generative AI (Gemini) and configured in Automation.py
5. Install Python packages: `pip install -r requirements.txt` and `pip install streamlit streamlit-lottie`

Configuration
-------------
1. Set up Gemini API key:
   - Replace the placeholder in `Automation.py`:
     `genai.configure(api_key="your api key")`
   - Alternatively, change the script to read the key from an environment variable for security.

2. ChromeDriver:
   - Ensure `chromedriver` binary is available and compatible with installed Google Chrome.
   - Place chromedriver in PATH or in project root.

3. Files directory:
   - Ensure a directory `files/` exists in project root. Output CSVs will be written to `files/{token}.csv` or `files/{file_name}.csv`.

Installation
------------
1. Clone or copy the project to your local machine.
2. Create and activate a virtual environment (recommended):
   - `python -m venv venv`
   - `source venv/bin/activate` (Linux/macOS) or `venv\Scripts\activate` (Windows)
3. Install dependencies:
   - `pip install -r requirements.txt`
   - `pip install streamlit streamlit-lottie`

Running locally (development)
-----------------------------
1. Start the Flask webhook (optional; app will call Automation through webhook):
   - `python webhook.py`
   - The webhook listens on port 80 by default (change in code if port conflict).

2. Start the Streamlit UI:
   - `streamlit run app.py`
   - Use the sidebar to provide inputs and submit jobs.

Direct usage (run automation script)
-----------------------------------
You can run the automation script directly with command-line args:

