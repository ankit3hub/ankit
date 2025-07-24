# 🧹 Clean Out Unwanted Emails from Gmail (n8n Workflow)

This n8n workflow helps you automatically clean up your Gmail inbox by deleting unwanted emails based on specific filters like `unsubscribe`, promotional content, and spam-like messages.

## 🚀 Features

- Fetch all Gmail messages excluding chats and important keywords like `license`, `key`, and `password`
- Filter out promotional/unwanted emails using the search query
- Automatically deletes them in batches (up to 100 emails at a time)
- Triggered manually via n8n's **Execute Node** or via Webhook

## 🔧 How It Works

1. **Trigger:**
   - Manually via the `Execute Workflow` button
   - Optionally triggered via a Webhook

2. **Gmail Node (`getAll`):**
   - Retrieves all emails matching the custom search query:  
     ```
     -in:chats unsubscribe -license -key -password
     ```

3. **Split In Batches:**
   - Splits emails into batches of 100 for processing

4. **Delete Operation:**
   - Each email ID in the batch is deleted using Gmail’s `delete` operation

5. **Webhook (optional):**
   - You can also integrate this workflow with an external trigger via webhook (e.g. button click on a custom app)

## 🛡️ Safety Notes

- **Be careful** with the search query – once deleted, emails can’t be recovered.
- Review the query string and test the filter before enabling deletion in production.

## 🧠 Prerequisites

- n8n instance (self-hosted or cloud)
- Gmail OAuth2 credentials setup in n8n
- Proper scopes enabled (e.g., `https://www.googleapis.com/auth/gmail.modify`)

## 🗃️ Node Overview

| Node Name           | Type            | Function                                      |
|---------------------|------------------|-----------------------------------------------|
| Manual Trigger       | Trigger         | Starts the workflow manually                  |
| Gmail (getAll)       | Gmail           | Fetches filtered emails                       |
| SplitInBatches       | Utility         | Batches emails (100 at a time)                |
| Gmail (delete)       | Gmail           | Deletes each email using its ID               |
| Webhook (optional)   | Webhook         | Optional webhook entry                        |
| Merge                | Utility         | Merges webhook inputs                         |

## 🔗 Webhook URLs

If using webhook-based triggering:
- **Trigger Webhook:** `/webhook/eb49f632-c190-41a7-81a7-c777dcb1f773`
- **Intermediate Webhook:** `/webhook/c9aa01ee-2c91-4069-bf63-ce904a932e9f`

## 📂 File Structure

This repo includes:

- `Clean out unwanted emails from Gmail.json` – the exported workflow
- `README.md` – this documentation

## 📘 Usage

1. Import the JSON workflow into n8n.
2. Connect your Gmail OAuth2 credentials.
3. Test run manually or via webhook.
4. Watch your inbox clean itself up!

---

👨‍💻 Created with 💡 by Ankit Yadav  
🔗 GitHub: [ankit3hub](https://github.com/ankit3hub)

