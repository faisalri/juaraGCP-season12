# 🧠 LLM Baseline Summarization — Quiz (Unique MD Style)

> **Module:** LLM Baseline Summarization  
> **Format:** Multiple‑choice with all options listed, correct answers marked, explanations included.  
> **Author:** Faisal Riyadi  
> **Status:** ✔ Updated (Q3 corrected)

---

## 1) Correct procedure for uploading chat transcripts
- **A.** Upload the transcripts directly to a Google Drive folder and link it to the Cloud project.
- **B.** Upload the transcripts directly to the Agent Assist console.
- **C. ✅ Correct.** Upload the transcripts directly to a **Cloud Storage** bucket as **JSON or CSV** files.
- **D.** Create a separate Cloud Storage bucket for each chat transcript.

**Why C?** Summarization pipelines expect batch files in **GCS**; JSON/CSV are the supported interchange formats for ingestion.

---

## 2) Purpose of `CONV_PROFILE_ID`
- **A.** To fine‑tune the data loss prevention (DLP) redaction.
- **B.** To name the Google Cloud project where the notebook will run.
- **C.** To define the path in the Cloud Storage bucket for transcript files.
- **D. ✅ Correct.** To **correlate audio/transcripts with the correct conversation profile**.

**Why D?** The conversation profile ID binds transcripts/audio to the right configuration and context for processing.

---

## 3) Content metric used to assess the summary
- **A. ✅ Correct.** **Resolution** — evaluates whether the summary addresses the core request with sufficient, coherent detail.
- **B.** Fairness — a socio‑linguistic property, not a content quality metric for summaries in this context.
- **C.** Repetition — **compliance/fluency signal**, not a content metric (used to detect duplicate phrases).
- **D.** Grammar and spelling — a surface‑form fluency metric, not content.

**Why A?** In content evaluation frameworks, *resolution* focuses on how well the summary captures and resolves the salient information from the conversation.

---

## 4) Primary purpose of the **LLM Baseline Summarization** model
- **A.** To provide a single platform for all custom and pre‑trained models.
- **B.** To provide suggestions for customer answers in a live conversation.
- **C. ✅ Correct.** To **automatically summarize conversations** using a **pre‑trained** model.
- **D.** To provide a summary of an entire contact center's conversational history.

**Why C?** The baseline model ships pre‑configured to generate concise summaries automatically without custom fine‑tuning.

---

### ✅ Score Key
- Each question: 1 point  
- Passing score: 80%  
- Correct options are marked with **✅** and include a brief rationale.

---