# Functional Requirements

## Project

AI-Powered Meeting Intelligence & Workflow Automation

## Purpose

This document defines the functional requirements for the prototype workflow that converts unstructured meeting notes into structured business actions and automates post-meeting administrative activities.

## Functional Requirements

| ID | Requirement |
|---|---|
| FR-01 | The workflow shall capture submitted meeting notes. |
| FR-02 | The workflow shall send meeting notes to Google Gemini for processing. |
| FR-03 | Gemini shall extract structured meeting information in JSON format. |
| FR-04 | The workflow shall process the generated JSON so individual fields can be used by downstream actions. |
| FR-05 | The workflow shall create a Google Calendar event using the extracted meeting information. |
| FR-06 | The workflow shall create a Microsoft To Do task using the extracted action item. |
| FR-07 | The workflow shall generate a stakeholder email as a Gmail draft. |
| FR-08 | The stakeholder email shall remain in draft status for human review before sending. |
| FR-09 | The complete workflow shall be tested through a successful end-to-end Zapier test run. |

## Key Data Fields

The AI output includes:

- Meeting title
- Meeting date
- Meeting time
- Duration
- Action item
- Priority
- Email draft
