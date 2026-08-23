# 🚀 B2B Lead Capture & CRM Qualification Automation

This repository contains an exported **n8n workflow** designed to automate B2B lead capture, CRM management, lead qualification, prioritization, and internal sales notifications.

The workflow integrates **n8n Forms, HubSpot, Gmail, and Slack** to capture new leads, prevent duplicate contacts, calculate lead scores, assign priority levels, update HubSpot, and send targeted communications based on lead quality.

---

![B2B Lead Capture & CRM Qualification Automation](Lead-to-CRM%20Qualification%20%26%20Outreach%20Automation%202026-08-23%20152634.png)

---

## 🎯 Key Benefits

* ⚡ **Automated Lead Capture:** Captures new B2B leads directly through an n8n form.
* 🔄 **CRM Contact Management:** Automatically checks HubSpot for existing contacts and creates or updates records.
* 📊 **Smart Lead Scoring:** Scores leads based on budget, company size, and required service.
* 🎯 **Priority-Based Routing:** Automatically categorizes leads as High, Medium, or Low priority.
* 📧 **Personalized Email Outreach:** Sends different client emails based on lead priority.
* 💬 **Instant Slack Alerts:** Notifies the internal team with lead details and recommended actions.
* 🧹 **Reduced Manual Work:** Automates repetitive lead qualification and CRM updates.

---

## 📋 Workflow Overview

The automation runs through four core operational phases:

### 1. 📝 Lead Capture & CRM Management

* **Trigger:** Starts when a prospect submits the n8n lead capture form.
* **Actions:**
  * Captures lead information such as name, email, phone, company, service, company size, and budget.
  * Normalizes the submitted data into a consistent structure.
  * Searches HubSpot using the lead's email address.
  * Creates a new contact or updates the existing HubSpot contact.

### 2. 📊 Lead Qualification & Scoring

* **Actions:**
  * Prepares the required lead information for qualification.
  * Calculates a lead score based on:
    * 💰 Budget range
    * 🏢 Company size
    * 🛠️ Service required
  * Assigns individual scores for each qualification factor.
  * Calculates the final `lead_score`.

### 3. 🔀 Priority Routing & CRM Update

The workflow automatically routes leads into three priority levels:

* 🔴 **High Priority:** Lead score of 80+
* 🟠 **Medium Priority:** Lead score of 50–79
* 🟢 **Low Priority:** Lead score of 0–49

The assigned priority and final lead score are then updated back into the HubSpot contact record.

### 4. 📧 Client Outreach & Team Notifications

Each priority level follows its own communication path:

* **High Priority**
  * Sends a direct client email focused on scheduling a consultation.
  * Sends an urgent Slack notification to the internal team.

* **Medium Priority**
  * Sends a professional consultation email.
  * Sends a Slack notification for standard follow-up.

* **Low Priority**
  * Sends a low-pressure acknowledgement email.
  * Sends a Slack notification to place the lead into the nurture/follow-up queue.

---

## 🛠️ Apps & Integrations Used

* **n8n** – Core automation engine and workflow orchestration
* **HubSpot** – CRM, contact management, lead scoring, and qualification tracking
* **Gmail** – Automated client email communication
* **Slack** – Internal sales team notifications

---

## 🔄 Workflow Architecture

```text
n8n Form Submission
        ↓
Normalize Lead Data
        ↓
HubSpot Search Contact
        ↓
Create or Update Contact
        ↓
Prepare Lead Data
        ↓
Calculate Lead Score
        ↓
Route Lead by Score
     ↙    ↓    ↘
   High  Medium  Low
     ↓    ↓      ↓
Set Lead Priority
        ↓
     Merge Leads
        ↓
Update Lead Qualification
        ↓
Route Follow-Up
     ↙    ↓    ↘
   High  Medium  Low
    ↓      ↓      ↓
 Gmail + Slack Notifications
```

---

## ⭐ Support

If you like this Workflow, please **star the repository** on GitHub. It helps others find it and supports the project growth.

---

## 🔹 Author

👨‍💻 Created & maintained by [Shahzaib Ali](https://www.linkedin.com/in/shahzaib-ali-8a2b94247/)

📬 For freelance work: **[sa4715228@gmail.com](mailto:sa4715228@gmail.com)**
