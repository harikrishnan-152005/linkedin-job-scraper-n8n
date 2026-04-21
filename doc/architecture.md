
---

# 📄 architecture.md

```md
# Architecture Documentation

## Overview

This system is a workflow-driven automation pipeline built using n8n. It integrates web scraping, AI-based evaluation, and real-time notification systems to provide an end-to-end job matching solution.

---

## High-Level Architecture

The system consists of the following major components:

1. Input Layer
2. Data Acquisition Layer
3. Processing Layer
4. AI Evaluation Layer
5. Output Layer

---

## Component Breakdown

### 1. Input Layer

- Source: Google Sheets
- Purpose: Define job search parameters
- Fields:
  - Keyword
  - Location
  - Experience Level
  - Job Type
  - Remote preference
  - Pagination offset

---

### 2. Data Acquisition Layer

#### LinkedIn Job Scraping

- Dynamic URL generation based on input parameters
- HTTP request node fetches job listings
- HTML parsing extracts job links

#### Link Processing

- Deduplication logic removes repeated links
- Normalization ensures consistent URL structure

---

### 3. Processing Layer

#### Job Detail Extraction

- Individual job pages are fetched
- HTML parsing extracts:
  - Title
  - Company
  - Location
  - Description
  - Job ID

#### Data Cleaning

- Text normalization
- Whitespace cleanup
- Field standardization

---

### 4. AI Evaluation Layer

#### Resume Processing

- Resume is downloaded from Google Drive
- Text is extracted from PDF

#### Multi-Model Scoring System

Primary Model:
- Google Gemini

Secondary Model:
- OpenRouter

Fallback Model:
- Ollama (local)

#### Scoring Logic

- Input: Resume + Job Description
- Output: Score between 0 and 100
- Validation ensures numeric and bounded output

#### Cover Letter Generation

- Triggered when score exceeds threshold
- Uses same multi-model fallback strategy
- Enforces structured output format

---

### 5. Output Layer

#### Data Storage

- Google Sheets stores:
  - Job details
  - Scores
  - Cover letters

#### Notifications

- Telegram bot sends job alerts
- Includes:
  - Title
  - Company
  - Location
  - Score
  - Application link

---

## Workflow Control

### Looping Mechanism

- Batch processing using SplitInBatches node
- Controlled iteration over job links

### Rate Limiting

- Wait nodes prevent excessive requests
- Helps avoid blocking and throttling

---

## Error Handling Strategy

- Fallback between AI models
- Default values when parsing fails
- Conditional branching using IF nodes
- Logging of invalid outputs

---

## Data Flow Summary

1. Read job parameters from Google Sheets
2. Generate LinkedIn search URL
3. Fetch job listings
4. Extract and deduplicate links
5. Loop through job links
6. Extract job details
7. Evaluate using AI models
8. Generate cover letter if applicable
9. Store results in Google Sheets
10. Send Telegram notifications

---

## Scalability Considerations

- Modular node-based architecture
- Easy integration of additional AI models
- Can extend to multiple job platforms
- Supports parallel execution with batching

---

## Security Considerations

- API keys stored securely in n8n credentials
- OAuth used for Google integrations
- Avoid exposing sensitive data in logs

---

## Limitations

- Dependent on LinkedIn HTML structure
- Susceptible to anti-scraping measures
- AI output variability based on model behavior

---

## Future Architecture Improvements

- Introduce message queue for large-scale processing
- Add database layer instead of Google Sheets
- Implement caching for repeated queries
- Add monitoring and alerting system
- Deploy as distributed microservices

---