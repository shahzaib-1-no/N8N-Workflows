# 🛡️ WooCommerce AI Fraud Detection & Auto-Cancel Workflow

This folder contains an exported n8n workflow that evaluates every new WooCommerce order in real time using an AI Fraud Detection Agent, then automatically cancels high-risk orders, holds suspicious orders for review, and notifies the team via Slack — all without manual intervention.

---

![WooCommerce Fraud Detection Workflow](https://github.com/shahzaib-1-no/N8N-Workflows/blob/81007a9ad96f1390fbfbb8911a0b6736b4e4fa1a/Woocomerece%20Workflows/Fraud%20Detection%20-%20Auto-Cancel%20Automation/Fraud%20Detection%20%20Auto-Cancel%20Workflow%20WooCommerce%20Screenshot%202026-08-09%20184704.png)
---

## 🎯 Key Benefits

* 🧠 **AI-Powered Risk Scoring:** Uses an LLM-based Fraud Detection Agent instead of static rules to catch disposable emails, fake addresses, and suspicious payment patterns.
* ⚡ **Automated Order Actions:** Instantly cancels high-risk orders or places borderline orders on hold — no manual triage needed.
* 🔄 **Dual-Model Reliability:** Runs on Google Gemini with an automatic Mistral Cloud fallback, so scoring never stalls if one model fails.
* 📣 **Instant Slack Alerts:** Sends detailed risk-score breakdowns straight to your risk/ops channel for every flagged order.
* 🛠️ **Built-in Failure Monitoring:** Dedicated error alerts for both agent failures and workflow-level failures, so nothing fails silently.

---

## 📋 Workflow Overview

The automation runs through four core operational phases:

### 1. 🛒 Order Capture & Data Extraction
* **Trigger:** Listens via WooCommerce Webhook for the `order.created` event.
* **Actions:**
  * Extracts key order fields: `order_id`, `billing_email`, `customer_ip`, `order_total`, billing/shipping details, `payment_method`, `customer_id`, and `currency`.

### 2. 🧠 AI Fraud Detection Agent
* **Logic:** Sends the extracted order JSON to an AI Agent that calculates a fraud risk score from 0–100 based on:
  * **Email:** Disposable/temporary domains (e.g. mailinator.com) → +40 to +60 risk.
  * **Name & Address:** Gibberish or keyboard-smash entries (e.g. "qwe", "asdf") → high risk.
  * **Payment & Value:** High order totals combined with Cash on Delivery (COD) → increased risk.
  * **Missing Data:** Assigns a baseline score of 50 to flag the order for manual review.
  * **Unreadable/Invalid Data:** Defaults to a score of 100 to trigger automatic cancellation.
* **Models:** Primary — **Google Gemini** (`gemini-3.5-flash-lite`); Fallback — **Mistral Cloud** (`mistral-medium-latest`) if the primary model fails.
* **Output:** Structured JSON (`risk_score`, `reason`) enforced via an Output Parser.

### 3. 🔀 Tiered Action Routing & Notifications
* **HIGH Priority (score ≥ 75):** Order is automatically set to **Cancelled** in WooCommerce; a Slack alert is sent to the risk team with full order and risk details.
* **MEDIUM Priority (score 40–74):** Order is set to **On-Hold**; a Slack alert requests manual review in WooCommerce Admin.
* **LOW Priority (score < 40):** Order passes through untouched (No Op) and proceeds to normal fulfillment.

### 4. 🚨 Error Handling
* **Agent Failure Alert:** Fires if the Fraud Detection Agent node errors out, notifying the team on Slack immediately.
* **Workflow Failure Alert:** A global Error Trigger catches any node failure across the workflow and posts the failed node, execution ID, and a direct link to the execution log in Slack.

---

## 🛠️ Apps & Integrations Used

* **n8n** (Core Automation Engine)
* **WooCommerce Webhooks & REST API** (Order Trigger & Order Status Updates)
* **Google Gemini** (Primary Fraud Scoring LLM)
* **Mistral Cloud** (Fallback Fraud Scoring LLM)
* **Slack** (Risk Alerts & Failure Notifications)

---

## 🚀 How to Import and Use

1. Download the `.json` workflow file from this repository.
2. Open your **n8n** dashboard and click **Import from File**.
3. Connect your credentials for **WooCommerce**, **Google Gemini**, **Mistral Cloud**, and **Slack**.
4. Set your Slack **channel ID** in the alert nodes.
5. (Optional) Adjust the `risk_score` thresholds in the **Switch - Risk Level** node to fit your store's risk tolerance.
6. Activate the workflow!

---

## ⭐ Support

If you like this Workflow, please **star the repository** on GitHub. It helps others find it and supports the project growth.
---

## 🔹 Author

👨‍💻 Created & maintained by [Shahzaib Ali](https://www.linkedin.com/in/shahzaib-ali-8a2b94247/)
📬 For freelance work: **[sa4715228@gmail.com](mailto:sa4715228@gmail.com)**
