# 🧠 Lab Session (Premium)

**Classify Text into Categories with the Natural Language API**

> Google Cloud Self‑Paced Lab (GSP063)
> Level: Intermediate | Duration: ~1 hour

---

## 🎯 Objectives

- Enable the Cloud Natural Language API
- Classify text documents into content categories
- Process long text inputs
- Store and analyze results in BigQuery

---

## ✅ Prerequisites

- Active Google Cloud Skills Boost lab
- Cloud Shell access

---

## 🔹 Task 0 – Start the Lab & Open Cloud Shell

```bash
gcloud config get-value project
```

---

## 🔹 Task 1 – Enable Cloud Natural Language API

APIs & Services → Library → Cloud Natural Language API → Enable

---

## 🔹 Task 2 – Create an API Key

```bash
export API_KEY=YOUR_API_KEY
```

---

## 🔹 Task 3 – Classify Text

```bash
cat > request.json <<EOF
{
  "document": {
    "type": "PLAIN_TEXT",
    "content": "Google Cloud enables AI and scalable analytics platforms."
  }
}
EOF
```

```bash
curl -s -X POST   -H "Content-Type: application/json"   "https://language.googleapis.com/v1/documents:classifyText?key=$API_KEY"   --data-binary @request.json
```

---

## 🔹 Task 4 – Store Result in BigQuery

```bash
bq mk news_dataset
bq mk --table news_dataset.results text:STRING,category:STRING,confidence:FLOAT
```

---

✅ Lab Completed