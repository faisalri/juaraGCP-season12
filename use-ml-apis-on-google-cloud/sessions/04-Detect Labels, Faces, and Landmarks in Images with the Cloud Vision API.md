# 🧠 Lab Session (Premium)

**Detect Labels, Faces, and Landmarks in Images with the Cloud Vision API**

> Google Cloud Skills Boost – Self‑Paced Lab  
> Level: Intermediate | Duration: ~1 hour

---

## 🎯 Learning Objectives

By completing this session, you will be able to:

- Enable and authenticate access to the **Cloud Vision API**
- Upload images to **Cloud Storage**
- Build Vision API request payloads
- Perform **label detection** on images
- Perform **web detection** on images
- Perform **face detection** using Vision API features
- Perform **landmark annotation** on images
- Perform **object localization** on images
- Interpret and validate Vision API JSON responses

---

## ✅ Prerequisites

- Active Google Cloud Skills Boost lab project
- Access to **Google Cloud Console**
- Cloud Shell enabled
- Basic understanding of REST APIs and JSON

---

## 🔹 Task 0 – Activate Cloud Shell

1. Click **Open Google Cloud Console** from the lab page
2. Click the **Cloud Shell** icon in the top‑right corner
3. Authenticate when prompted
4. Verify your project:

```bash
gcloud config get-value project
```

✅ Checkpoint: Cloud Shell ready

---

## 🔹 Task 1 – Create an API Key

1. In the Console, navigate to **APIs & Services → Credentials**
2. Click **Create Credentials → API key**
3. Copy the generated API key

Set the API key as an environment variable:

```bash
export API_KEY="YOUR_API_KEY"
```

✅ Checkpoint: API key created

---

## 🔹 Task 2 – Upload an Image to a Cloud Storage Bucket

### 1️⃣ Create a Cloud Storage bucket

```bash
export BUCKET_NAME="vision-lab-$RANDOM"

gsutil mb gs://$BUCKET_NAME
```

### 2️⃣ Upload an image

```bash
gsutil cp image.jpg gs://$BUCKET_NAME
```

### 3️⃣ Make the image publicly accessible (lab requirement)

```bash
gsutil acl ch -u AllUsers:R gs://$BUCKET_NAME/image.jpg
```

✅ Checkpoint: Image uploaded and accessible

---

## 🔹 Task 3 – Create the Vision API Request

Create a request file that references the image in Cloud Storage:

```bash
cat > request.json <<EOF
{
  "requests": [
    {
      "image": {
        "source": {
          "gcsImageUri": "gs://$BUCKET_NAME/image.jpg"
        }
      },
      "features": [
        { "type": "LABEL_DETECTION", "maxResults": 10 }
      ]
    }
  ]
}
EOF
```

✅ Checkpoint: Request file created

---

## 🔹 Task 4 – Perform Label Detection

Send the request to the Vision API:

```bash
curl -s -X POST   -H "Content-Type: application/json"   "https://vision.googleapis.com/v1/images:annotate?key=$API_KEY"   --data-binary @request.json > label-response.json
```

Inspect the labels:

```bash
cat label-response.json | jq '.responses[0].labelAnnotations'
```

✅ Checkpoint: Labels successfully detected

---

## 🔹 Task 5 – Perform Web Detection

Update the request file:

```bash
cat > request.json <<EOF
{
  "requests": [
    {
      "image": {
        "source": {
          "gcsImageUri": "gs://$BUCKET_NAME/image.jpg"
        }
      },
      "features": [
        { "type": "WEB_DETECTION" }
      ]
    }
  ]
}
EOF
```

Call the API again:

```bash
curl -s -X POST   -H "Content-Type: application/json"   "https://vision.googleapis.com/v1/images:annotate?key=$API_KEY"   --data-binary @request.json > web-response.json
```

✅ Checkpoint: Web detection completed

---

## 🔹 Task 6 – Perform Face Detection

Update the request file to use face detection:

```bash
cat > request.json <<EOF
{
  "requests": [
    {
      "image": {
        "source": {
          "gcsImageUri": "gs://$BUCKET_NAME/image.jpg"
        }
      },
      "features": [
        { "type": "FACE_DETECTION", "maxResults": 5 }
      ]
    }
  ]
}
EOF
```

Send the request:

```bash
curl -s -X POST   -H "Content-Type: application/json"   "https://vision.googleapis.com/v1/images:annotate?key=$API_KEY"   --data-binary @request.json > face-response.json
```

✅ Checkpoint: Face detection response received

---

## 🔹 Task 7 – Perform Landmark Annotation

Upload a second image that contains a recognizable structure:

```bash
gsutil cp landmark.jpg gs://$BUCKET_NAME
```

Update the request file:

```bash
cat > request.json <<EOF
{
  "requests": [
    {
      "image": {
        "source": {
          "gcsImageUri": "gs://$BUCKET_NAME/landmark.jpg"
        }
      },
      "features": [
        { "type": "LANDMARK_DETECTION" }
      ]
    }
  ]
}
EOF
```

Call the API:

```bash
curl -s -X POST   -H "Content-Type: application/json"   "https://vision.googleapis.com/v1/images:annotate?key=$API_KEY"   --data-binary @request.json > landmark-response.json
```

✅ Checkpoint: Landmark detected

---

## 🔹 Task 8 – Perform Object Localization

Update the request to use object localization:

```bash
cat > request.json <<EOF
{
  "requests": [
    {
      "image": {
        "source": {
          "gcsImageUri": "gs://$BUCKET_NAME/image.jpg"
        }
      },
      "features": [
        { "type": "OBJECT_LOCALIZATION" }
      ]
    }
  ]
}
EOF
```

Call the API:

```bash
curl -s -X POST   -H "Content-Type: application/json"   "https://vision.googleapis.com/v1/images:annotate?key=$API_KEY"   --data-binary @request.json > object-response.json
```

✅ Checkpoint: Objects localized successfully

---

## 🧪 Final Validation Checklist

- [x] API key created
- [x] Images uploaded to Cloud Storage
- [x] Label detection completed
- [x] Web detection completed
- [x] Face detection completed
- [x] Landmark annotation completed
- [x] Object localization completed

---

🎉 **Congratulations! You have successfully completed the Cloud Vision API image analysis session.**

---

📌 *This session is optimized for GitHub documentation and Skills Portfolio tracking.*