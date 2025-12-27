# Agentic LinkedIn Outreach Automation (n8n)

## Overview
This project demonstrates the design and implementation of an **agentic automation workflow** using **n8n** to streamline LinkedIn-based job outreach.

The workflow converts a job description into:
- Targeted LinkedIn profile leads
- Structured candidate context
- Personalized cold email drafts
- A reviewable output stored in Google Sheets

This is a **design-first system-thinking project**. While the workflow was tested in an editing environment, full production execution depends on paid APIs.

---

## Problem Statement
Outbound job searching is inefficient due to:
- Manual LinkedIn searches
- Repetitive, low-quality outreach
- Difficulty scaling personalization

The goal was to design a system that automates **lead discovery + personalization** while keeping a **human-in-the-loop**.

---

## Why This Is Complex
Unlike simple automations, this system:
- Uses AI as a **decision-making agent**, not just text generation
- Orchestrates multiple tools (Search, AI, Enrichment, Email)
- Separates reasoning from execution
- Preserves human review for ethical outreach

---

## High-Level Architecture

**Input**
- Job Description

**Processing**
1. AI-driven Boolean search generation
2. Google Search-based LinkedIn discovery
3. Profile context extraction
4. Email enrichment
5. Personalized cold email generation

**Output**
- Google Sheet with enriched leads
- Optional Gmail draft emails

---

## Tools Used
- n8n – Workflow orchestration
- OpenAI – Reasoning, extraction, personalization
- Google Search – Profile discovery
- Hunter.io – Email enrichment
- Google Sheets – Data persistence
- Gmail – Draft creation

---

## Workflow Walkthrough

### 1. Job Description Trigger
The workflow starts when a job description is submitted via a chat trigger node.  
This serves as the single source of truth for targeting and personalization.

### 2. Boolean Search Generation (AI)
An OpenAI node converts the job description into a recruiter-style Google Boolean search string optimized for LinkedIn profile discovery.

### 3. LinkedIn Profile Discovery
A Google search is executed using authenticated headers (cookie-based session auth).  
LinkedIn profile URLs and contextual snippets are extracted.

### 4. Profile Context Structuring
AI extracts structured data:
- Name
- Role
- Company
- Company domain
- Relevance context

### 5. Email Enrichment
Hunter.io is used to find professional emails using the company domain.  
If no email is found, the lead is preserved for LinkedIn-only outreach.

### 6. Personalized Cold Email Generation
AI generates context-aware cold emails using:
- Job description
- Candidate background
- Company context

Emails are saved as **drafts**, not auto-sent.

### 7. Data Persistence
All outputs are stored in Google Sheets for review, scoring, and follow-ups.

---

## Implementation Notes
- Google search required cookie-based authentication.
- Cookies had to be added both to HTTP Header Auth credentials and Header parameters.
- Workflow was tested in n8n’s editing environment.

---

## AI Usage Disclosure
AI was used as a **reasoning and decision agent** for:
- Search strategy generation
- Context extraction
- Personalization logic
- Workflow branching decisions

---

## Constraints & Trade-offs
- Paid APIs (OpenAI, Hunter.io) limited full execution
- Design-first approach reflects real-world PM trade-offs

---

## Future Enhancements
- Lead scoring and prioritization
- CRM integration
- Compliance guardrails
- Open-source enrichment alternatives

---

## Author
**Chanderprakash Sharma**  
Aspiring Associate Product Manager
