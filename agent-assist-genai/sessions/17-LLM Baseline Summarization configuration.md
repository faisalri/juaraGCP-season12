# 🔧 LLM Baseline Summarization Configuration — Premium Notes

---

## ⚙️ Configuring LLM Summarization
To configure **LLM Baseline Summarization** in a Jupyter notebook running on Google Cloud, you must define key parameters that inform the pipeline where to pull data, where to save outputs, and which conversation profile to use.

### Required Parameters

#### **1. PROJECT_NAME**
The Google Cloud project where your notebook will run.

#### **2. GCS_BUCKET_URI**
The root GCS bucket path in the format:
```
gs://<bucket-name>
```
All transcript input and summarization outputs will be stored here.

#### **3. TRANSCRIPTS_INPUT_FOLDER_PREFIX**
Name of the folder (inside the bucket) where **transcripts are uploaded**.
Example:
```
transcripts_input/
```

#### **4. SUMMARIZATION_OUTPUT_FOLDER_PREFIX**
Folder where **summary outputs** will be written.
Example:
```
summaries_output/
```

#### **5. CONV_PROFILE_ID**
A unique Conversation Profile ID generated when you configure summarization in Agent Assist Console.
Format:
```
projects/<project>/locations/<location>/conversationProfiles/<id>
```

It ensures output summaries map correctly to the profile’s settings (language, sections, and model version).

---

## 🛡️ Optional: Fine‑Tune Data Loss Prevention (DLP) Redaction
By default, the summarization notebook uses a predefined list of **INFO_TYPES** (patterns that match sensitive entities such as person names, emails, phone numbers, credit cards, and more).

However, business domains often need **additional or customized patterns**.

You can:
- Add domain‑specific INFO_TYPES
- Remove patterns irrelevant to your environment
- Improve quality of redaction for your use case

👉 Official INFO_TYPES Reference:  
<https://docs.cloud.google.com/sensitive-data-protection/docs/infotypes-reference>


After configuring the parameters and fine‑tuning INFO_TYPES, run the notebook cells. Summaries will populate inside the **SUMMARIZATION_OUTPUT_FOLDER_PREFIX** within your storage bucket.

---

## 📚 Additional Resources (Expanded)
For more detailed implementation information:
- **Cloud Data Loss Prevention (DLP)** — identify & redact sensitive information  
  <https://cloud.google.com/security/products/dlp>
- **Vertex AI Search & Conversation (Agent Builder)**  
  <https://cloud.google.com/products/agent-builder>
- **Cloud Storage IAM Permissions**  
  <https://cloud.google.com/storage/docs/access-control/iam-permissions>
- **Dialogflow ES Quick Setup**  
  <https://cloud.google.com/dialogflow/es/docs/quick/setup>
- **Python Client for Cloud Storage**  
  <https://cloud.google.com/python/docs/reference/storage/latest>

---

## 🟦 Quick Summary
- Configure project, bucket, input/output folders, and Conversation Profile ID.
- Use DLP INFO_TYPES to customize redaction for your business domain.
- Summaries are written to GCS along your specified output prefix.
- Use provided official resources for in‑depth API and IAM understanding.

---
