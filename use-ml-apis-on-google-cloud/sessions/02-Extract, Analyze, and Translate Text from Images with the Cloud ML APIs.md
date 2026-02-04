## 🧠 Lab Session (Premium)

**Extract, Analyze, and Translate Text from Images with the Cloud ML APIs**

> Google Cloud Skills Boost – Self‑Paced Lab  
> Level: Intermediate | Duration: ~1 hour

---

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Enable and use **Cloud Vision API** for OCR (text detection)
- Store and access images from **Cloud Storage**
- Analyze extracted text using **Natural Language API**
- Translate detected text using **Translation API**
- Chain multiple Cloud ML APIs into a simple pipeline

---

## 🧩 Architecture Overview

```
Image (GCS)
   │
   ▼
Cloud Vision API (OCR)
   │
   ├──► Natural Language API (sentiment & syntax)
   │
   └──► Translation API (target language)
```

---

## ✅ Prerequisites

- Active Google Cloud project (provided by lab)
- Cloud Shell access
- Basic understanding of REST & JSON

---

## 🔹 Task 0 – Activate Cloud Shell

1. Open **Cloud Shell** from the Google Cloud Console
2. Authorize when prompted
3. Verify project:
  
  ```bash
  gcloud config get-value project
  ```
  

---

## 🔹 Task 1 – Create an API Key

Cloud ML APIs in this lab use **API Key authentication**.

### Steps

1. Go to **APIs & Services → Credentials**
2. Click **Create Credentials → API key**
3. Copy the generated key

### Set API key as environment variable

```bash
export API_KEY="YOUR_API_KEY"
```

✅ **Checkpoint:** API key created

---

## 🔹 Task 2 – Upload an Image to Cloud Storage

### 1️⃣ Create a bucket

```bash
export BUCKET_NAME="ml-vision-$RANDOM"

gsutil mb gs://$BUCKET_NAME
```

### 2️⃣ Upload the sample image

```bash
gsutil cp sign.jpg gs://$BUCKET_NAME
```

✅ **Checkpoint:** Image uploaded to GCS

---

## 🔹 Task 3 – Create a Cloud Vision API Request

### 1️⃣ Create request JSON

```bash
cat > vision-request.json <<EOF
{
  "requests": [
    {
      "image": {
        "source": {
          "gcsImageUri": "gs://$BUCKET_NAME/sign.jpg"
        }
      },
      "features": [
        { "type": "TEXT_DETECTION" }
      ]
    }
  ]
}
EOF
```

### 2️⃣ Call Vision API

```bash
curl -s -X POST   -H "Content-Type: application/json"   "https://vision.googleapis.com/v1/images:annotate?key=$API_KEY"   --data-binary @vision-request.json > vision-response.json
```

---

## 🔹 Task 4 – Extract Detected Text

```bash
cat vision-response.json | jq '.responses[0].fullTextAnnotation.text'
```

---

## 🔹 Task 5 – Translate Text with Translation API

```bash
cat > translate-request.json <<EOF
{
  "q": "LE BIEN PUBLIC Pour Obama, la moutarde",
  "target": "en"
}
EOF
```

```bash
curl -s -X POST   -H "Content-Type: application/json"   "https://translation.googleapis.com/language/translate/v2?key=$API_KEY"   --data-binary @translate-request.json > translate-response.json
```

---

## 🔹 Task 6 – Analyze Text with Natural Language API

```bash
cat > nl-request.json <<EOF
{
  "document": {
    "type": "PLAIN_TEXT",
    "content": "LE BIEN PUBLIC Pour Obama, la moutarde"
  },
  "encodingType": "UTF8"
}
EOF
```

```bash
curl -s -X POST   -H "Content-Type: application/json"   "https://language.googleapis.com/v1/documents:analyzeSentiment?key=$API_KEY"   --data-binary @nl-request.json > nl-response.json
```

---

## 🧪 Final Assignment

Build an OCR → Translation → NLP pipeline using a new image.

---

> 📌 Optimized for GitHub / Skills Portfolio