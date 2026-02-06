# 🧠 Entity & Sentiment Analysis with Google Cloud Natural Language API

> **Goal**: Run end‑to‑end requests for **Entity**, **Sentiment**, **Entity Sentiment**, **Syntax/POS**, and **Multilingual** analysis using REST (`curl`). This guide mirrors your lab flow and fixes common gaps so you can copy‑paste and run.

---

## 📋 What you’ll do

1. Create and export an **API key** (lab shortcut).
2. Prepare `request.json` payloads.
3. Call REST endpoints for each analysis type.
4. Read/interpret responses and scores.
5. Try a multilingual request.

> 🔐 **Note**: For production workloads use **Service Accounts + OAuth 2.0** instead of API keys.

---

## 🧰 Prerequisites

- A Google Cloud project with the **Cloud Natural Language API** enabled.
- `curl` and a terminal (Cloud Shell works great).
- Basic JSON editing.

---

## ✅ Task 1 — Create an API key

1. In **Google Cloud Console**: **Navigation menu → APIs & Services → Credentials**.
2. **Create credentials → API key**. Copy the key.
3. *(Optional but recommended)* **Restrict** the key to the Natural Language API.
4. Export it in your terminal:

```bash
export API_KEY="YOUR_API_KEY_HERE"
```

Windows PowerShell:

```powershell
$env:API_KEY = "YOUR_API_KEY_HERE"
```

---

## 🧩 Request template

Most endpoints accept a **Document** with `type` and `content` (or a `gcsContentUri`). Use `PLAIN_TEXT` unless you need HTML.

```jsonc
{
  "document":{
    "type":"PLAIN_TEXT",
    "content":"Joanne Rowling, who writes under the pen names J. K. Rowling and Robert Galbraith, is a British novelist and screenwriter who wrote the Harry Potter fantasy series."
  },
  "encodingType":"UTF8"
}
```

> ❗ If you see errors about `document`/`type`, check spelling and JSON commas.

---

## 🧷 Task 2 — Entity analysis (people, places, orgs, etc.)

**1) Create `request.json`:**

```json
{
  "document": {
    "type": "PLAIN_TEXT",
    "content": "Joanne Rowling, who writes under the pen names J. K. Rowling and Robert Galbraith, is a British novelist and the best‑selling author of the Harry Potter fantasy series."
  },
  "encodingType": "UTF8"
}
```

---

## 📞 Task 3 — Document sentiment (overall tone)

**1) You can now pass your request body, along with the API key environment variable you saved earlier, to the Natural Language API with the following curl command (all in one single command line):**

**2) Call the API:**

```bash
curl "https://language.googleapis.com/v1/documents:analyzeEntities?key=${API_KEY}" \
  -s -X POST -H "Content-Type: application/json" --data-binary @request.json > result.json
```

**How to read scores**

For each entity in the response, you get the entity type, the associated Wikipedia URL if there is one, the salience, and the indices of where this entity appeared in the text. Salience is a number in the [0,1] range that refers to the centrality of the entity to the text as a whole.

The Natural Language API can also recognize the same entity mentioned in different ways. Take a look at the mentions list in the response: ​the API is able to tell that "Joanne Rowling", "Rowling", "novelist" and "Robert Galbriath" all point to the same thing.​


---

## 🎯 Task 4 — Entity **sentiment** (opinion toward specific things)

**1) Update `request.json`:**

```json
 {
  "document":{
    "type":"PLAIN_TEXT",
    "content":"Harry Potter is the best book. I think everyone should read it."
  },
  "encodingType": "UTF8"
}
```

**2) Call the API:**

```bash
curl "https://language.googleapis.com/v1/documents:analyzeSentiment?key=${API_KEY}" \
  -s -X POST -H "Content-Type: application/json" --data-binary @request.json
```

**How to read scores**

- `documentSentiment.score` ∈ **[-1.0, 1.0]** (negative → positive).
- `documentSentiment.magnitude` ≥ **0.0** (overall emotional **strength**, regardless of polarity).
- Per‑sentence sentiment is available under `sentences[]`.

---

## 🧠 Task 5 — Syntax & Parts‑of‑Speech (POS) / Dependencies

**1) Update `request.json`:**

```json
 {
  "document":{
    "type":"PLAIN_TEXT",
    "content":"I liked the sushi but the service was terrible."
  },
  "encodingType": "UTF8"
}
```

**2) Call the API:**

```bash
curl "https://language.googleapis.com/v1/documents:analyzeEntitySentiment?key=${API_KEY}" \
  -s -X POST -H "Content-Type: application/json" --data-binary @request.json
```

**Reading the response**

- Each `entities[i]` includes its own `sentiment.score` and `sentiment.magnitude`.
- Compare opinions for entities like **“SushiZen”** (likely positive) vs **“service”** (likely negative).

---

## 🌐 Task 6 — Multilingual analysis

You can **auto‑detect** language or set it explicitly.

**1) Japanese sample (`ja`)** — update `request.json`:

```json
{
  "document":{
    "type":"PLAIN_TEXT",
    "content": "Joanne Rowling is a British novelist, screenwriter and film producer."
  },
  "encodingType": "UTF8"
}
```

**2) Call entity analysis (works for other endpoints too):**

```bash
curl "https://language.googleapis.com/v1/documents:analyzeSyntax?key=${API_KEY}" \
  -s -X POST -H "Content-Type: application/json" --data-binary @request.json
```

**What you get**

- Token‑level `partOfSpeech` (NOUN, VERB, ADJ, …), `lemma`, `dependencyEdge` (head token + label such as `NSUBJ`, `DOBJ`).
- Use this for grammar insights, keyword extraction heuristics, or building parse trees.

---

## 🌐 Task 7 — Multilingual natural language processing

The Natural Language API also supports languages other than English (full list can be found in the Language Support Guide)..

**1) Japanese sample (`ja`)** — update `request.json`:

```json
{
  "document":{
    "type":"PLAIN_TEXT",
    "content":"日本のグーグルのオフィスは、東京の六本木ヒルズにあります"
  }
}
```

**2) Call entity analysis (works for other endpoints too):**

```bash
curl "https://language.googleapis.com/v1/documents:analyzeEntities?key=${API_KEY}" \
  -s -X POST -H "Content-Type: application/json" --data-binary @request.json
```

---

## 📚 References

- Cloud Natural Language API (overview & methods): https://cloud.google.com/natural-language/docs
- REST reference (documents methods): https://cloud.google.com/natural-language/docs/reference/rest/v1/documents

---
