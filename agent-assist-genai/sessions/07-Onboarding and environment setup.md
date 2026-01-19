# 🧭 Onboarding & Environment Setup — **Smart Reply**

*Premium-style notes for GitHub — concise, visual, and copy‑paste friendly.*

---

## ✅ Smart Reply Prerequisites
- 🗂️ **GCS Bucket + APIs** required for development. The Google Cloud **project must be owned by the customer**.
- 🤝 **Conversational Agent (Dialogflow/CCAIA) APIs** are essential; **enable all required APIs**.
- 👥 **Grant permissions** to PSO members:
  - Project **Owner** *or* **Dialogflow API Admin** *(required)*
  - **Storage Admin** *(optional, for data ops)*

> ℹ️ **Note:** Any resources (e.g., models, allowlist) created under the project are deleted when the project is deleted.

---

## ☁️ Cloud Environment Setup
Follow these steps to select a project, authenticate, configure, and enable APIs.

### Step 1 — Locate GCP Project & Authenticate
Open Cloud Console → choose your project → launch **Cloud Shell**. Authenticate and list accounts:

```bash
# List gcloud authenticated accounts
gcloud auth list

# (Optional) Switch active account
gcloud config set account "ACCOUNT"
```

### Step 2 — Confirm Your Project
```bash
# List projects
gcloud config list project

# Set your target project
gcloud config set project <PROJECT_ID>

# Echo env var for later use
echo $GOOGLE_CLOUD_PROJECT
```

### Step 3 — Set Up the Cloud Environment & Enable APIs
```bash
# Ensure env var is available
echo $GOOGLE_CLOUD_PROJECT

# Enable required services
gcloud services enable dialogflow.googleapis.com
gcloud services enable storage.googleapis.com
gcloud services enable datalabeling.googleapis.com
```

---

## 🧾 Data Formatting Requirements
Upload conversation data to **Google Cloud Storage** (customer-owned project). Accepted formats: **JSON** or **CSV** (zip → upload to GCS).

Each conversation **entry** should include:
- `Transcript ID`, `Role`, `Content`, `user_id`, `Timestamp`
- **Transcript ID** uniquely identifies each conversation (used to name files: `TranscriptID-<n>.json`)
- **Role** ∈ `{AGENT | CUSTOMER}`
- **Messages** stored as **plain text**
- **user_id** uniquely identifies the participant
- **Timestamp** stored in key `start_timestamp_usec`

### Example JSON Snippet
```json
{
  "conversation_info": {
    "categories": [
      { "display_name": "Category 1" }
    ]
  },
  "entries": [
    {
      "start_timestamp_usec": 1000000,
      "text": "Hello, I'm calling in regards to ...",
      "role": "CUSTOMER",
      "user_id": 1
    },
    {
      "start_timestamp_usec": 5000000,
      "text": "Yes, I can answer your question ...",
      "role": "AGENT",
      "user_id": 2
    }
  ]
}
```

---

## 🧼 Data Acceptance Requirements (Pre‑ingest Hygiene)
1. 🔤 **Normalize shared text** (consistent punctuation, casing, spelling).
2. 🛡️ **Remove PII** (names, addresses, phone numbers, IDs, card numbers).
3. 🧹 **Clean bot/system messages**; keep only real agent–customer content.

> Good formatting may not change model *training dynamics*, but it greatly improves **demo quality** and **suggestion readability**.

---

## 📏 Standard Requirements (Quality Gates)
### Step 1 — Verify Dataset Size
- ✅ **Target:** ~**200K transcripts** for best accuracy
- ⚠️ **100K** works but may reduce quality
- 🔽 **Min:** **30K** transcripts (model may underperform)

### Step 2 — Verify Absence of PII
- ≤ **2% PII** across the dataset
- Ensure **no** names, addresses, phone numbers, IDs, card numbers

### Step 3 — Verify Conversation Content
- Every column is a **valid string value**
- In **JSON**, each key has an appropriate **enum** (e.g., `role` ∈ `{Agent, Customer}` only)
- **Only** real contact‑center messages → **exclude** system messages like *“Call is transferring to the Agent.”*

---

## 🟦 Quick Summary (Bullet Points)
- Enable **Dialogflow, Storage, Datalabeling APIs** and set proper **IAM roles**.
- Store data in **GCS**; format as **JSON/CSV** with `Transcript ID`, `Role`, `Content`, `user_id`, `start_timestamp_usec`.
- **Normalize text**, **remove PII**, **exclude bot/system messages**.
- Strive for **~200K transcripts**; 30K minimum; ensure valid enums and strings.
- Use Cloud Shell snippets above to **authenticate**, **select project**, and **enable services** quickly.

---
