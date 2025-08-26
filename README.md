## Lead Capture Automation with n8n

Automate your lead intake effortlessly with n8n. This project processes onboarding form submissions, enriches leads with AI, emails both the lead and your team, and updates Google Sheets for centralized tracking.

![Lead Capture Automation Cover](./images/Lead%20Capture%20Automation%20Cover.png)

---

## Table of Contents

- [Overview](#overview)
- [How It Works](#how-it-works)
  - [Workflow Steps](#workflow-steps)
- [Benefits](#benefits)
- [Requirements](#requirements)
- [Setup Instructions](#setup-instructions)
  - [1. Clone or Import Workflow](#1-clone-or-import-workflow)
  - [2. Configure the Form Trigger](#2-configure-the-form-trigger)
  - [3. Connect Gemini AI](#3-connect-gemini-ai)
  - [4. Connect Gmail](#4-connect-gmail)
  - [5. Connect Google Sheets](#5-connect-google-sheets)
  - [6. Test the Workflow](#6-test-the-workflow)
- [Customization](#customization)
  - [Google Sheet Structure](#google-sheet-structure)
  - [Email Message Personalization](#email-message-personalization)
  - [AI Lead Summary Prompt](#ai-lead-summary-prompt)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## Overview

**Lead Capture Automation** is an n8n workflow that streamlines client onboarding and lead management. It:

- Triggers on a form submission using the built-in Form Trigger
- Generates a concise lead summary using Gemini AI
- Sends a personalized welcome email to the lead
- Appends or updates the corresponding row in Google Sheets
- Notifies your internal team by email with the captured details

---

## How It Works

![Lead Capture Workflow](./images/Lead%20Capture%20Automation.png)

### Workflow Steps

1. **Trigger on form submission**
   - Captures `Full Name`, `Email Address`, `Company Name`, `Services Needed`, optional `Additional Onboarding Information`, and `Preferred Contact Method`.

2. **Generate lead summary via Gemini AI**
   - Sends the submitted details to Gemini to produce a 2–3 line summary.

3. **Parse AI output**
   - Uses a structured output parser to ensure valid JSON with a `summary` field.

4. **Email lead a personalized message**
   - Sends a welcome email via Gmail tailored to the lead’s inputs.

5. **Append/update Google Sheets with lead info**
   - Writes lead data and the AI summary into a Google Sheet (matching on `Email Address`).

6. **Notify team via email**
   - Sends an internal notification email to your team with full details and a link to the sheet.

---

## Benefits

- **Automates lead intake & enrichment** with AI summarization
- **Ensures timely lead communication** with immediate emails
- **Centralizes data access** in Google Sheets
- **Simple integrations** using Gmail and Google Sheets

---

## Requirements

- [n8n](https://n8n.io/) installation or cloud account
- Google account with:
  - Access to Gmail (for sending emails)
  - Access to Google Sheets (for storing leads)
- Gemini AI API access (Google Generative AI)

---

## Setup Instructions

### 1. Clone or Import Workflow

- Download or import the attached `Lead Capture Automation.json` workflow into your n8n instance (Desktop or Cloud).

### 2. Configure the Form Trigger

- Open the `On form submission` node and verify the fields:
  - `Full Name`, `Email Address`, `Company Name`, `Services Needed`, `Additional Onboarding Information` (optional), `Preferred Contact Method`.
- Deploy to get the hosted form URL, or use the webhook URL embedded in the node.

![Onboarding Form](./images/Onboarding%20Form.png)

### 3. Connect Gemini AI

- In the `Google Gemini Chat Model` and `Lead Summary` nodes, add your Gemini/PaLM credentials.
- Keep the output format as JSON with a `summary` key to ensure parsing succeeds.

### 4. Connect Gmail

- In the `Send Email to Lead` and `Send Email to Team` nodes, add your Gmail OAuth2 credentials.
- Adjust sender identity if needed.

![Email Sent to Lead](./images/Email%20Sent%20to%20Lead.png)

![Email Sent to Team](./images/Email%20Sent%20to%20Team.png)

### 5. Connect Google Sheets

- In the `Append or update row in sheet` node, add your Google Sheets OAuth2 credentials.
- Set `Document` and `Sheet` references (ID and sheet name).
- Mapping includes: `Email Address` (match), `Full Name`, `Company Name`, `Services Needed`, `Additional Onboarding Information`, `Preferred Contact Method`, `Lead Summary`, `Created At`.

![Leads Data](./images/Leads%20Data.png)

### 6. Test the Workflow

- Submit the form once to generate a test lead.
- Confirm you receive the lead welcome email and your team receives the internal notification.
- Verify the Google Sheet row is appended/updated correctly.

---

## Customization

### Google Sheet Structure

- Required columns: `Email Address` (match key), `Full Name`, `Company Name`, `Services Needed`, `Additional Onboarding Information`, `Preferred Contact Method`, `Lead Summary`, `Created At`.
- You may add additional columns; update the node mappings accordingly.

### Email Message Personalization

Use n8n expressions to tailor content, for example in Gmail nodes:

Subject example:

```
Welcome to Fuzion Tech, {{ $('On form submission').item.json["Full Name"] }}! Let’s Get Started
```

Body snippet example:

```
Hi {{ $('On form submission').item.json['Full Name'] }},

Thank you for choosing us to support {{ $('On form submission').item.json['Company Name'] }} — especially around {{ $('On form submission').item.json['Services Needed'] }}.
```

### AI Lead Summary Prompt

The `Lead Summary` node instructs Gemini to return strictly valid JSON like:

```
{
  "summary": "Your 2-3 line lead summary here"
}
```

You can adjust tone or length, but keep the JSON shape to avoid parser errors.

---

## Troubleshooting

- **Form not triggering**: Redeploy to refresh the webhook; verify the public form URL.
- **Gemini errors or empty `summary`**: Check credentials, rate limits, and ensure the model returns valid JSON.
- **Gmail node failures**: Re-authorize Gmail OAuth2; verify send quotas and from-address permissions.
- **Google Sheets write issues**: Confirm Sheet ID, sheet name, and that `Email Address` exists for matching.

---

## Contributing

Contributions and suggestions are welcome.
Fork the repo, submit issues, or open pull requests for improvements.

---

## License

This project is licensed under the MIT License. See `LICENSE` for details.

---

## Contact

- **Email:** nebeyoumusie@gmail.com
- **LinkedIn:** [LinkedIn](https://www.linkedin.com/in/nebeyou-musie)
- **X(Twitter):** [X](https://x.com/NebeyouMusie)
- **Upwork:** [Upwork](https://www.upwork.com/freelancers/~017ff01729e3cd26e0?mp_source=share)
- **My Agency:** [Fuzion Tech Website](https://fuzion-tech.com/) or [Fuzion Tech on Upwork](https://www.upwork.com/agencies/1948388369189366041/)

---

**Skills & Technologies:**  
`n8n`, `Automation`, `Lead Capture`, `Gemini`, `Gmail`, `Google Sheets Automation`

---

**Enjoy automated lead capture and streamlined onboarding!**

---

