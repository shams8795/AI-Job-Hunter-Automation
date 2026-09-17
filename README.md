# AI Job Hunter Agent

An AI-powered job search automation workflow built with n8n, Google Gemini, RemoteOK, and Gmail.

The workflow analyzes a candidate's CV, extracts relevant skills and experience, searches for available remote jobs, identifies the closest matching opportunity, customizes the CV for that position, generates a professional cover letter, and sends the generated application package through Gmail.

---

## Overview

The AI Job Hunter Agent is designed to automate repetitive parts of the job search process.

Instead of manually reviewing job listings and preparing application content for every position, the workflow combines AI, job search APIs, matching logic, and email automation into a single n8n pipeline.

The workflow starts when a CV is uploaded and continues automatically through job discovery, matching, CV customization, cover letter generation, and email delivery.

---

## Workflow Preview

![AI Job Hunter Agent n8n Workflow](n8n-job-hunter-workflow.png)

---

## How It Works

### 1. CV Upload

The workflow starts with an n8n Webhook that receives the candidate's CV.

The uploaded document is passed directly to the AI analysis step.

### 2. CV Analysis

Google Gemini 2.5 Flash analyzes the CV and extracts structured information such as:

- Job titles
- Skills
- Tools and technologies
- Years of experience

The AI response is returned as JSON so it can be reused throughout the workflow.

### 3. Structured Data Parsing

A JavaScript node cleans the Gemini response and converts it into structured JSON data.

This makes the extracted candidate information available to the following workflow steps.

### 4. Job Search

The workflow connects to the RemoteOK API to retrieve current remote job opportunities.

The returned job listings include information such as:

- Job position
- Company
- Job description
- Job requirements

### 5. Job Matching

The candidate's extracted skills are compared with each available job description.

A match percentage is calculated based on the number of relevant skills found in the job description.

The jobs are then ranked by match percentage, and the closest matching job is selected.

### 6. CV Customization

The selected job description is sent to Google Gemini.

Gemini generates a customized version of the CV that emphasizes:

- Relevant skills
- Relevant experience
- Job-specific qualifications
- Clear professional language

### 7. Cover Letter Generation

A professional cover letter is automatically generated based on:

- The selected job
- Company information
- Job description
- Customized CV content

The generated letter is designed to be concise and relevant to the selected position.

### 8. Email Automation

The workflow uses Gmail integration to send the generated application content to a configured email address.

The email includes the generated cover letter and information about the selected position.

### 9. Confirmation Email

After the workflow completes, a confirmation email is sent containing:

- Company name
- Position
- Submission status

---

## Workflow Flow

```text
Upload CV
    ↓
Analyze CV with Gemini
    ↓
Parse Gemini Output
    ↓
Search Jobs using RemoteOK
    ↓
Calculate Job Match
    ↓
Select Best Matching Job
    ↓
Customize CV
    ↓
Generate Cover Letter
    ↓
Send Application Content via Gmail
    ↓
Send Confirmation Email
```

---

## Technologies Used

### n8n

Used to design, connect, and automate the complete workflow.

### Google Gemini 2.5 Flash

Used for:

- CV analysis
- Information extraction
- CV customization
- Cover letter generation

### RemoteOK API

Used to retrieve real remote job listings.

### JavaScript

Used to process the AI output and calculate skill-based job matching scores.

### Gmail

Used for automated email delivery and workflow confirmation.

---

## Job Matching Logic

The workflow extracts the candidate's skills from the CV and compares them against each job description.

A match score is calculated using:

```text
Matched Skills
────────────── × 100
Total CV Skills
```

Jobs are ranked from highest to lowest match percentage.

The current workflow selects the highest matching job for the next stages.

---

## Project Files

```text
AI-Job-Hunter-Agent/
│
├── README.md
├── job-hunter-workflow.json
└── n8n-job-hunter-workflow.png
```

`job-hunter-workflow.json` contains the exported n8n workflow.

`n8n-job-hunter-workflow.png` shows the visual workflow structure inside n8n.

---

## Setup

### 1. Install or Open n8n

Use an existing n8n instance or create a new one.

### 2. Import the Workflow

Download:

```text
job-hunter-workflow.json
```

Then import it into n8n.

### 3. Configure Google Gemini

Connect your own Google Gemini API credentials to the Gemini nodes.

### 4. Configure Gmail

Connect your Gmail account using OAuth credentials.

### 5. Configure the Email Address

Update the Gmail nodes with the email address that should receive the generated application content and confirmation messages.

### 6. Test the Workflow

Upload a CV through the configured webhook and execute the workflow.

---

## Security

API credentials and authentication secrets should not be stored directly in the public repository.

When importing the workflow, configure your own:

- Google Gemini credentials
- Gmail OAuth credentials
- Email address
- n8n environment settings

---

## Current Capabilities

The current workflow can:

- Receive a CV
- Analyze CV content with AI
- Extract candidate skills and experience
- Retrieve remote job listings
- Calculate job matching scores
- Select the closest job match
- Customize CV content for the selected job
- Generate a professional cover letter
- Send generated application content through Gmail
- Send a confirmation email

---

## Future Improvements

Future versions could include:

- Support for multiple job platforms
- Multiple best-match job recommendations
- Direct application integrations
- Applicant tracking dashboard
- Application history
- More advanced job ranking
- Location and salary filtering
- Scheduled automatic job searches
- Notifications for newly matched opportunities

---

## About the Project

This project was designed and developed as an AI automation workflow that combines job search, document understanding, AI-generated application content, API integration, and email automation.

It demonstrates how n8n and generative AI can be combined to automate a multi-step real-world workflow.

