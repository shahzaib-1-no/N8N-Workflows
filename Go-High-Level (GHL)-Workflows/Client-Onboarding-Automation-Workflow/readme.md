# 🚀 Client Onboarding Automation Workflow

This folder contains an exported n8n workflow designed to completely automate the client onboarding process. It integrates **GoHighLevel (GHL)**, **Google Sheets**, **Gmail**, and **Slack** to ensure a seamless transition from a closed-won deal to project kickoff.

---

## 📋 Workflow Overview

The automation is divided into three core phases:

### 1. 📌 Deal Closed & Client Logging
* **Trigger:** Listens for a GoHighLevel webhook when a deal is updated.
* **Logic:** Filters exclusively for deals with a **`Won`** status.
* **Actions:** 
  * Instantly sends a `Contract Sent Alert` to the team via Slack.
  * Appends the new client's details into a Google Sheets tracking database.

### 2. ⏱️ Automated Contract Follow-up Loop
* **Trigger:** Runs on a scheduled timer (Cron/Interval).
* **Logic:** Reads the Google Sheet to find pending contracts and calculates the hours passed since the contract was sent.
* **Actions:**
  * **24 Hours:** Sends a friendly check-in email to the client.
  * **48 Hours:** Sends a follow-up email and notifies the team via Slack that the contract is still unsigned.
  * **Stalled Queue:** Routes overdue/unresponsive items to a Slack channel for manual review.

### 3. ✅ Contract Signed & Project Handoff
* **Trigger:** Receives a webhook as soon as the client signs the contract.
* **Actions:** 
  * Updates the respective Google Sheets row status to `Completed`.
  * Automatically sends a Welcome Email to the client.
  * Posts a Slack notification telling the team to start the project work.

---

## 🛠️ Apps & Integrations Used
* **n8n** (Core Automation Engine)
* **GoHighLevel** (CRM / Webhook Triggers)
* **Google Sheets** (Database & Status Tracking)
* **Gmail** (Client Email Communication)
* **Slack** (Internal Team Notifications)

---

## 🚀 How to Import and Use

1. Download the `.json` workflow file from this repository.
2. Open your n8n workspace and create a new workflow.
3. Click on the three dots (options menu) in the top right corner and select **Import from File**.
4. Upload the downloaded `.json` file.
5. **Setup Credentials:** Authenticate your Google Sheets, Slack, and Gmail nodes.
6. **Update Webhooks:** Copy the Production Webhook URLs from the n8n trigger nodes and paste them into your GoHighLevel workflows.
7. Click **Activate** to make the workflow live!
