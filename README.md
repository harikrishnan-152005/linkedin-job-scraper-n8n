# LinkedIn Job Scraper and AI-Based Job Matching System

## Overview

This project is an automated job discovery and evaluation pipeline built using n8n. It scrapes job listings from LinkedIn, evaluates job relevance against a candidate's resume using multiple AI models, and generates structured outputs including match scores and tailored cover letters. The system stores results in Google Sheets and sends real-time notifications via Telegram.

---

## Features

- Automated LinkedIn job scraping with recent job filtering
- Resume-based job relevance scoring using AI models
- Multi-model fallback mechanism for reliability
- Automated cover letter generation for relevant jobs
- Google Sheets integration for job tracking
- Telegram notifications for real-time alerts
- Deduplication and structured data extraction
- Error handling and fallback logic

---

## Workflow Summary

The system follows a structured pipeline:

1. Scheduled trigger initiates the workflow
2. Resume is downloaded from Google Drive
3. Resume text is extracted from the file
4. Job search parameters are read from Google Sheets
5. LinkedIn search URL is dynamically generated
6. Job listings are fetched via HTTP request
7. Job links are extracted and deduplicated
8. Each job is processed iteratively
9. Job details are scraped and structured
10. AI models evaluate job relevance:
    - Primary: Gemini
    - Secondary: OpenRouter
    - Fallback: Ollama
11. Scores are validated and normalized
12. Cover letters are generated for qualified jobs
13. Results are stored in Google Sheets
14. Notifications are sent via Telegram

---

## Technology Stack

- Automation: n8n
- Programming: JavaScript (n8n Code Nodes)
- AI Models:
  - Google Gemini
  - OpenRouter
  - Ollama
- Data Storage: Google Sheets
- File Handling: Google Drive
- Notifications: Telegram Bot API
- Web Scraping: HTTP Requests and HTML parsing

---

## Project Structure
```text
linkedin-job-scraper/
│
├── workflows/
│   └── linkedin-job-scraper.json
│
├── docs/
│   ├── setup.md
│   ├── architecture.md
│   └── screenshots/
│       ├── workflow.png
│       ├── google-sheet-output.png
│       └── telegram-output.png
│
├── assets/
│   └── preview.png
│
├── .gitignore
└── README.md
```


---

## Setup Instructions

### Import Workflow

- Open n8n
- Navigate to Import Workflow
- Upload the workflow JSON file
- Save the workflow

### Configure Credentials

Set up the following credentials in n8n:

- Google Drive API
- Google Sheets API
- Telegram Bot API
- Google Gemini API
- OpenRouter API (optional)
- Ollama (optional)

### Configure Input Data

Prepare a Google Sheet with the following fields:

- Keyword
- Location
- Experience Level
- Job Type
- Remote
- Start

### Run Workflow

- Execute manually for testing
- Enable scheduled trigger for automation

---

## Output

### Google Sheets

- Job Title
- Company
- Location
- Job Description
- Relevance Score
- Generated Cover Letter

### Telegram

- Real-time job alerts with job details and application links

---

## Design Considerations

- Modular workflow design for scalability
- Multi-model fallback ensures reliability
- Input-driven configuration for flexibility
- Controlled request flow to prevent blocking
- Validation of AI outputs for consistency

---

## Limitations

- LinkedIn scraping depends on page structure
- May be affected by anti-scraping mechanisms
- AI output depends on API availability and limits

---

## Future Enhancements

- Integration with vector databases for semantic matching
- Dashboard for analytics and visualization
- Deployment as a web-based application
- Advanced filtering using embeddings
- Resume personalization and versioning

---

## Author

Harikrishnan  
Bachelor of Technology in Artificial Intelligence and Data Science  

---

## License

This project is intended for educational and personal use. Ensure compliance with third-party platform policies before production use.
