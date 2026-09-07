# APEX Corp Enterprise Multi-Department Voice Receptionist

An enterprise voice receptionist named **Ava** that answers incoming calls, understands caller intent, handles common requests, and routes callers to the appropriate APEX Corp department.

Built with **Vapi** for the voice assistant and **n8n** for backend tool orchestration and mock integrations.

## Project Overview

Ava is designed to act as a professional front-desk voice receptionist for APEX Corp. The assistant supports six department intents:

- **HR** — Check available job openings or route callers to HR
- **Finance** — Check invoice/payment status or route callers to Finance
- **Sales** — Capture sales leads or route callers to Sales
- **IT** — Collect employee/ticket information or route callers to IT
- **Support** — Collect ticket information or route callers to Support
- **Reception** — Handle general requests and direct callers appropriately

## Architecture

```text
Caller
  ↓
Vapi Voice Assistant — Ava
  ↓
Intent Detection & Department Routing
  ↓
n8n Backend Webhook
  ↓
Tool Router
  ├── check_job_openings
  ├── check_invoice_status
  ├── capture_sales_lead
  ├── send_confirmation
  └── route_call
```

## Technology Stack

- **Vapi** — Voice AI assistant and telephony interface
- **n8n** — Workflow automation and backend tool routing
- **GPT-4.1** — Language model
- **Soniox** — Speech transcription
- **SIP** — Intended mechanism for department transfer/handoff

## Backend Webhook

The n8n backend exposes a single webhook that routes requests based on the `tool` field:

```text
https://shaik-mohammad-shaheed.app.n8n.cloud/webhook/apex-receptionist-tools
```

The current backend uses mock responses for assessment and testing purposes.

## Available Tools

| Tool | Purpose | Mock Response |
|---|---|---|
| `route_call` | Route caller to a department | Transferring → `sip:sales@voice.apex.com`, extension `x4081` |
| `check_job_openings` | Retrieve open positions | Software Engineer - Austin; HR Manager - Remote |
| `check_invoice_status` | Check invoice/payment status | Paid; `$4500.00`; due `2026-07-20` |
| `capture_sales_lead` | Log a sales lead | Lead Logged; `DEAL-8821` |
| `send_confirmation` | Send confirmation to caller | Sent via email |

## Example Test Flows

### HR

**Caller:**

> Hi, I'm calling to see what engineering jobs you have open right now.

**Expected behavior:**

Ava invokes `check_job_openings` and reads the available engineering-related openings.

### Finance

**Caller:**

> Hi, I need to check the payment status on invoice INV-9912. My email is john@acme.com.

**Expected behavior:**

Ava invokes `check_invoice_status`, provides the payment status and invoice details, then can use `send_confirmation` to email the caller.

### Sales

**Caller:**

> Hi, I want to talk to a Sales representative immediately.

**Expected behavior:**

Ava invokes `route_call`, announces the transfer, and initiates the configured Sales handoff flow.

## Current Implementation Status

### Completed

- Vapi assistant **Ava - APEX Corp Receptionist** created and published
- GPT-4.1 model configured
- Soniox transcription configured
- Six department routing instructions configured
- Five backend tools connected to n8n
- n8n mock backend workflow published
- HR, Finance, and Sales test scenarios prepared
- Configuration documentation prepared

### Production Enhancements

The current project uses mock integrations for assessment and demonstration. A production deployment could replace these with:

- **Greenhouse** for real-time job openings
- **Stripe** for invoice/payment status
- **HubSpot** for sales lead creation
- **Twilio/SIP** for live department transfer
- SIP user-to-user metadata containing caller name, initial intent, and conversation summary

## Repository Structure

```text
apex-enterprise-voice-receptionist/
├── README.md
├── docs/
│   ├── project-documentation.pdf
│   ├── system-prompt.md
│   └── test-scenarios.md
├── config/
│   ├── vapi-assistant-config.md
│   └── tool-definitions.json
├── n8n/
│   └── mock-tools-workflow.json
└── demo/
    └── loom-link.md
```

## Demo

Loom demonstration:

https://www.loom.com/share/e63835aa4b42430484aa358715bb180f

## Assessment Context

This project was developed as an enterprise voice receptionist assessment demonstrating:

- Multi-intent voice routing
- Tool calling
- Backend automation with n8n
- Mock API responses
- Department transfer handling
- Confirmation dispatch
- Production-readiness planning

## Author

**Shaik Mohammad Shaheed**

GitHub: https://github.com/shaikshahid777

LinkedIn: https://linkedin.com/in/shaikshaheed777

## Note

This repository intentionally documents the current assessment implementation separately from future production integrations. Mock SIP and backend behavior should not be interpreted as a live production telephony integration until the corresponding SIP/Twilio configuration is deployed and end-to-end verified.
