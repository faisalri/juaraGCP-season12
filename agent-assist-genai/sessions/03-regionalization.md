
# Regionalization with Agent Assist

> ### 🟦 Module: Regionalization & Data Residency

---

## 📘 What Is Regionalization?

**Regionalization** ensures customer **data‑at‑rest** is stored physically within a specified **geographical region**.

This means:

- When a region is chosen, data‑at‑rest stays **inside that region**  
- Data is **not stored** outside the selected region  

Agent Assist uses regionalization to support:

- **Compliance requirements**
- **Performance improvements** (reduced latency when customer + data are close)

*Pricing is the same for all regions.*

---

## 📌 When Is Regionalization Helpful?

### 1️⃣ Compliance Requirements  
Some systems require all customer data to stay within a defined geographical area for legal or regulatory compliance.

### 2️⃣ Improved Performance  
Placing data closer to your customers may reduce latency and improve user experience.

> ⚠️ **Important:** Regionalization applies only to **data‑at‑rest**,  
> not **data‑in‑use** or **data‑in‑transit**.

---

## 🚫 Regionalization Limitations in Agent Assist

### • Model Training  
Model training **does not** support regionalization.  
Your data might be routed outside your selected region during model training.

### • Transcription  
Transcription supports multi‑region **data‑in-use** and **data‑at-rest** only in:

- EU  
- US  
- North America (Canada)  

(When Speech Adaptation is *not* used.)

---

## 📚 Additional Resources (Provided by Module)

🔗 **Regionalization and Data Residency Documentation**  
https://docs.cloud.google.com/agent-assist/docs/regionalization

---

## ⚡ Quick Summary (TL;DR)

- Regionalization keeps **data‑at‑rest** in the specified region.  
- Useful for **compliance** and **latency improvements**.  
- Does **not** apply to data‑in‑use or data‑in‑transit.  
- **Limitations:**  
  - Model training is not regionalized  
  - Transcription multi‑region support limited to EU, US, Canada  
- Pricing is equal across all regions.

---

