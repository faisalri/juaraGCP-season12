
# 05 — Understanding Your AI System

> ⏱️ *Estimated time:* 30 minutes
> 🎯 *Goal:* Capture key ideas and practical takeaways.

---

🧠 At a Glance

- An AI system typically includes **four components** working in concert: **Application (or API)**, **Model**, **Data**, and **Infrastructure**.
- Securing AI means assessing and reinforcing **each** component, not just the model.

---

## 🔐 Key Components

### 1) Application (or API)

The interface users or other systems interact with. It collects inputs, invokes the model, and presents outputs.

**Security focus:** authN/authZ, input validation, content filtering, rate limiting, logging, and privacy controls for submitted data.

---

### 2) The AI Model

The “brain” that generates predictions or content based on its training.

**Security focus:** model versioning, evaluation & red‑teaming, alignment/safety policies, prompt injection defenses, abuse monitoring.

---

### 3) Data

The fuel that trains the model and the information it uses at inference.

**Security focus:** data classification, minimization, provenance tracking, PII handling (mask/anonymize), encryption in transit/at rest, retention & deletion.

---

### 4) Infrastructure

The hardware & software the model runs on — compute, storage, networking, CI/CD.

**Security focus:** hardened images, patching, IAM least privilege, network segmentation, KMS‑backed secrets, monitoring, backup/DR.

---

## 🧩 How They Work Together

Inputs flow from **Application → Model**, which uses **Data** and runs on **Infrastructure**. Weakness in any layer can compromise the whole system. Effective AI security requires **end‑to‑end** controls and clear ownership per component.

---

## 📝 Quick Check

Match the component to its primary responsibility:

- **Application (or API):** User/system interface for inputs & outputs. **✅**
- **Model:** Generates outputs from learned patterns. **✅**
- **Data:** Provides training and contextual information. **✅**
- **Infrastructure:** Provides compute, storage, and platform services. **✅**

---

## 🖼️ Screenshots

../screenshots/05-01.png

---

## 🔗 References

See ../ref/links.md

---

## ✅ Action Items

- Draw your AI system diagram: app/API, model, data, infra.
- Assign security ownership and controls per component.
- Implement regular reviews for data flows, model changes, and infra hardening.