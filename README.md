
# AI-Powered Workflow Automation for Meeting Intelligence & Business Productivity

> **Using Generative AI and no-code automation to transform unstructured meeting information into structured business actions.**

---

## Executive Summary

### Project Overview
Modern organizations conduct numerous meetings every day, generating action items, follow-up meetings, and stakeholder communications. Managing these activities manually is repetitive, time-consuming, and increases the risk of missed tasks or inconsistent communication.

This project demonstrates how Generative AI and workflow automation can streamline post-meeting activities by converting unstructured meeting notes into structured business outputs. Using **Google Gemini AI** and **Zapier**, the workflow automatically extracts key information from meeting notes, creates calendar events, generates tasks in **Microsoft To Do**, and drafts professional follow-up emails for user review.

The solution is designed to support knowledge workers across business functions (Business Analysts, Project Coordinators, Operations Teams, Executive EAs) by reducing repetitive administrative effort while maintaining human oversight.

### Business Problem
After meetings, employees often need to:
1. Review meeting notes
2. Identify action items & priorities
3. Schedule follow-up meetings
4. Update task management systems
5. Draft stakeholder emails

These activities are typically completed across multiple applications, requiring repetitive manual effort and increasing the possibility of delays or missed actions.

### Project Objectives
- Automate post-meeting administrative workflows.
- Convert unstructured meeting notes into structured business information.
- Generate calendar events automatically.
- Create action-item tasks in Microsoft To Do.
- Draft professional follow-up emails in Gmail.
- Enforce human review before stakeholder emails are sent.

---

## Tools & Technologies

| Category | Tool / Technology |
| :--- | :--- |
| **Input Interface** | Zapier Forms |
| **AI Processing Layer** | Google Gemini AI |
| **Orchestration & Automation** | Zapier |
| **Calendar Automation** | Google Calendar |
| **Task Management** | Microsoft To Do |
| **Communication** | Gmail |
| **Data Format & Parsing** | JSON, JavaScript (`Code by Zapier`) |
| **Process Diagramming** | Draw.io |

---

## Business Analysis & Stakeholder Impact

### Business Stakeholders Matrix

| Stakeholder | Primary Responsibility | Business Benefit |
| :--- | :--- | :--- |
| **Executive Assistant (EA)** | Manage C-suite schedules and communications | Reduced manual effort; accelerated meeting follow-up |
| **Executive Manager** | Review commitments and approve outputs | Improved visibility of commitments and decisions |
| **Business Analyst (BA)** | Capture meeting outcomes and user stories | Structured, standardized information extraction |
| **Project Coordinator** | Track project deliverables and deadlines | Faster action tracking; zero unlogged tasks |
| **Operations Team** | Maintain workflow efficiency and standards | Standardized documentation and handoff processes |

---

## Process Redesign (As-Is vs. To-Be)

### Current State — As-Is (Manual Administration)
`Meeting Ends` ➔ `Review Notes` ➔ `Manual Calendar Update` ➔ `Manual Task Creation` ➔ `Manual Email Draft` ➔ `Send`

### Future State — To-Be (AI & Automated Workflow)
```text
[ Meeting Notes Input (Zapier Form) ]
                  │
                  ▼
      [ Google Gemini AI Layer ]
                  │
                  ▼
       [ Structured JSON Output ]
                  │
                  ▼
      [ JavaScript Parser (Zapier) ]
                  │
                  ▼
        [ Zapier Orchestrator ]
      ┌───────────┼───────────┐
      ▼           ▼           ▼
   [ Google    [ MS      [ Gmail
   Calendar ]  To Do ]   Draft ]
                             │
                             ▼
                    [ Human Review Gate ]
                             │
                             ▼
                   [ Send to Stakeholders ]

Solution Architecture & Workflow Steps
Step 1 — Submit Meeting Notes: The user submits unstructured meeting notes through a Zapier Form.
Step 2 — AI Processing: Google Gemini analyzes the text and extracts structured information including title, date, time, duration, action items, priority, and draft email body.
Step 3 — JSON Processing: A JavaScript step in Zapier parses the JSON response and validates data types for downstream tools.
Step 4 — Automated Output Execution:
Follow-up event generated in Google Calendar.
Action item task added to Microsoft To Do.
Professional follow-up email saved in Gmail Drafts.
Step 5 — Human Review Gate: The generated Gmail draft remains safely in the Drafts folder until a human reviews, edits, and sends it.

Implementation Details & System Prompt
Gemini AI System Prompt
JSON
{ 
  "role": "system", 
  "content": "You are an AI productivity assistant. Parse the provided raw meeting notes or audio transcript and extract structured parameters. You MUST return ONLY valid JSON matching this exact schema:\n{\n  \"meeting_title\": \"Short, professional calendar event title\",\n  \"meeting_date\": \"YYYY-MM-DD format based on context\",\n  \"meeting_time\": \"HH:MM AM/PM format\",\n  \"duration_minutes\": 30,\n  \"action_item\": \"Primary actionable task extracted\",\n  \"priority\": \"High | Medium | Low\",\n  \"email_draft\": \"Concise, professional summary email to stakeholders outlining key decisions and next steps.\"\n}\n\nRules:\n1. Use professional business language.\n2. Calculate relative dates (e.g., 'next Tuesday') into a strict ISO date format (YYYY-MM-DD).\n3. If meeting duration is missing, default to 30.\n4. If meeting time is unclear, set meeting_time to 'TBD - Confirmation Required'.\n5. Return valid JSON only with no conversational prose." 
} 
Sample Input & Validated Output
Sample Input Text:

"Met with Sarah regarding the Q3 strategy review. Schedule a follow-up meeting next Tuesday at 11 AM for 45 minutes. Finalize financial metrics before Friday and send stakeholders a summary."

Validated JSON Response:

JSON
{ 
  "meeting_title": "Q3 Strategy Review Follow-Up", 
  "meeting_date": "2026-08-11", 
  "meeting_time": "11:00 AM", 
  "duration_minutes": 45, 
  "action_item": "Finalize Q3 financial metrics", 
  "priority": "High", 
  "email_draft": "Hello Sarah,\n\nThank you for today's meeting regarding the Q3 strategy review. As agreed, our follow-up meeting is scheduled for next Tuesday at 11:00 AM (45 mins).\n\nKey Action Item:\n- Finalize financial metrics prior to Friday.\n\nPlease let me know if any updates are needed.\n\nBest regards," 
}
Testing, UAT Matrix & Governance
User Acceptance Testing (UAT)
Test Case	Description	Expected Result	Actual Result	Status
UAT-01	Meeting Notes Parsing	ISO JSON payload generated	Structured JSON successfully generated with required fields	✅ Pass
UAT-02	Calendar Event Creation	Event queued with correct duration	Google Calendar event created with correct time & 45-min duration	✅ Pass
UAT-03	Task Creation	Action item card created	Microsoft To Do task created with 'High' priority	✅ Pass
UAT-04	Email Generation	Draft created in Gmail	Draft saved in Gmail Drafts folder	✅ Pass
UAT-05	Human Approval Gate	Email unsent until manual action	Email held in Drafts; zero automated distribution	✅ Pass

Risk Mitigation Matrix
Identified Risk	Severity	Mitigation Strategy
Ambiguous Notes	Medium	System prompts for clarification when dates/times are missing
Hallucinated Email Body	Medium	Mandatory Human Review Gate before any email is dispatched
Data Privacy Concerns	High	Non-sensitive test data used during prototyping; strict policy enforcement for production
API / Integration Failure	Low	Zapier error logging and fallback alert system

Prototype Limitations & Future Enhancements
Limitations
Microsoft To Do vs. Planner: Microsoft To Do was utilized because Microsoft Planner native connectors were restricted in the free testing environment.
Performance depends directly on the clarity of submitted notes.

Future Enhancements
Integration with Microsoft Outlook Calendar for enterprise environments.
Slack / Microsoft Teams channel notifications for automated post-meeting summary alerts.
Jira / Asana direct sync for engineering and product teams.

Repository Structure
Plaintext
ai-meeting-workflow-automation/
│
├── documentation/
│   ├── business-requirements.md
│   ├── functional-requirements.md
│   └── uat-test-cases.md
│
├── screenshots/
│   ├── 01-zapier-workflow.png
│   ├── 02-gemini-json-output.png
│   ├── 03-calendar-todo-verification.png
│   └── 04-gmail-draft-review.png
│
├── as-is-to-be-process.png
└── README.md

Author & Contact
Mansi Singh

Business & Operations Analyst

Mumbai, India

https://www.linkedin.com/in/mansisingh836/ 
