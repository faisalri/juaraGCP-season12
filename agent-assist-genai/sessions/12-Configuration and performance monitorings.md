# ⚙️ Smart Reply — **Configuration & Performance Monitoring** (Premium Notes)

> Elegant, structured, and GitHub‑ready documentation. Images will be provided by you—placeholders included.

---

## 🧩 Create a **Conversation Profile**
A **Conversation Profile** determines how Smart Reply suggestions are delivered to agents (virtual or human). You must create a profile **before** enabling Smart Reply in any end‑user conversation.

A Conversation Profile includes settings such as:
- **Model ID** → This is the deployed conversation model that you trained.
- **Confidence Threshold** → When the server creates a Smart Reply suggestion, it assigns it with a confidence score. Only when the confidence score is higher than the threshold should the suggestion should be returned to the customer.
- **Max Result Count** → It is recommended that you default the max result count to three. This way, for each request, the server returns three candidate messages that the agent would most likely say.

Once you create a profile in the Agent Assist Console:
- A spinner appears while the profile is being built
- It may take a few minutes before it becomes available
- You can use the built‑in simulator for demos, referencing human eval results or sample scripts


---

## ⚠️ Common Issues & How to Fix Them
### ❗ Lack of suggestions
- Lower the **confidence threshold** in the Conversation Profile
- Re‑test configuration

### ❗ Bad suggestions
- Increase the **confidence threshold** to filter out low‑quality candidates

---

## 📊 Performance Monitoring
Once live traffic flows through your Conversation Profile, you can evaluate how Smart Reply performs using key metrics.

### 🔵 **Request Level Click‑Through Rate (CTR)**
- Percentage of suggestions clicked by agents
- Comparable to offline evaluation *recall*
- Higher CTR = higher adoption & usefulness

### 🟡 **Suggestions Trigger Rate (TR)**
- How frequently Smart Reply returns suggestions
- % of suggestions generated / total agent messages
- Lower confidence threshold → higher trigger rate
- Ideally TR should approach **100%** (agents always receive suggestions)

---

## 🛠️ Troubleshooting Model Performance
If Smart Reply underperforms, the issue typically originates from **training data**. Use this 4‑step workflow:

1. **Compare model evaluation metrics** against your training dataset
2. **Verify integration** configuration
3. **Inspect conversations** from live traffic
4. **Re‑run model evaluation** using live traffic data

---

## 🧪 Example Model Performance Issue
### 🔍 Symptom
Your Smart Reply model’s **CTR is below 10%**.

### 📘 Explanation
Agents may find the suggestions **irrelevant** or **unhelpful**, reducing clicks and adoption.

### ✅ Solution
Start by reviewing your **Allowlist metrics**:
- Aim for Allowlist size: **20,000–100,000 messages**
- Ensure **message coverage >10%** and **recall >15%**

If the issue persists, check:
- Messages in training data follow correct **chronological order**
- Sender **roles are accurate**
- Conversations are not excessively short (ideally >5 sentences)
- Dataset size is **≥30,000** conversations

> Larger, high‑quality datasets produce the strongest model performance.

---

## 🟦 Quick Summary
- A **Conversation Profile** is required to serve Smart Reply suggestions.
- Adjust **confidence threshold** to control suggestion quality vs. volume.
- Monitor **CTR** and **Trigger Rate** to track performance.
- Troubleshoot low CTR by inspecting allowlist quality and dataset integrity.
- Ensure large, clean, chronologically accurate datasets for best results.

---
