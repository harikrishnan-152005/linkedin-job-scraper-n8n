# Setup Guide

## Introduction

This document provides step-by-step instructions to set up and run the LinkedIn Job Scraper and AI-Based Job Matching workflow using n8n.

---

## Prerequisites

Ensure the following tools and services are available:

- n8n (self-hosted or cloud)
- Node.js (if running n8n locally)
- Google account (for Drive and Sheets access)
- Telegram account (for bot notifications)
- API keys:
  - Google Gemini API
  - OpenRouter API (optional)
- Ollama (optional, for local model fallback)

---

## Step 1: Install and Run n8n

### Option 1: Using Docker

```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  n8nio/n8n