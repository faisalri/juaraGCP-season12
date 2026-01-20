# 🧠 Smart Reply & Smart Compose — **Quiz (with Answers)**

> Passing score minimum: **80%**

---

## ✅ Correct Answers (Quick View)
1) **Recall**  
2) **Provides a concise summary of the current conversation to save agents time on post‑call work.**  
3) **Smart Compose auto‑completes the next word/phrase; Smart Reply suggests an entire sentence.**  
4) **Text**  
5) **Unreviewed**

---

## 📋 Full Quiz

### 1) Which of the following metrics is generated during the training and evaluation of a machine learning model?
- ☐ Click‑Through Rate (CTR)  
- ☐ Message Coverage  
- ☑ **Recall**  
- ☐ L‑Rougu  

**Why:** Offline model evaluation commonly reports **recall** (and related metrics). **CTR** is a live, post‑deployment metric in the agent desktop.

---

### 2) What is the primary benefit of the Agent Assist **Summarization** feature?
- ☐ It summarizes every sentence the customer speaks into a few words to speed up interactions.  
- ☑ **It provides a concise summary of the current conversation to save agents time on post‑call work.**  
- ☐ It summarizes previous similar conversations to help the agent find a resolution faster.  
- ☐ It sends a summary report to the end user as a record of the interaction.  

**Why:** Summarization targets **agent efficiency** by producing a concise recap of the **ongoing** conversation for after‑call notes/work.

---

### 3) What is the key difference between **Smart Compose** and **Smart Reply**?
- ☐ Smart Compose suggests an entire sentence, whereas Smart Reply auto‑completes the next word or phrase.  
- ☐ Smart Compose has different prerequisites than Smart Reply.  
- ☑ **Smart Compose auto‑completes the next word or phrase, whereas Smart Reply suggests an entire sentence.**  
- ☐ Smart Compose does not require a conversation dataset for training.  

**Why:** Smart Compose is **token/phrase completion**; Smart Reply serves **full‑sentence suggestions**.

---

### 4) Which of the following is a **required field** for each entry in the conversation data used to train Smart Reply?
- ☐ Conversation_info  
- ☑ **Text**  
- ☐ Categories  
- ☐ User_id  

**Why:** Each entry must include message **text** (along with role/user/timestamps in the schema). Without **text**, the sample is unusable for language modeling.

---

### 5) When a new **allowlist** is generated, what is the **default state** of the topics/messages?
- ☐ Allowed  
- ☐ Reviewed  
- ☑ **Unreviewed**  
- ☐ Blocked  

**Why:** Candidates start as **Unreviewed** and require human moderation to move to **Allowed** (or **Blocked**).

---

## 🟦 Quick Summary
- **Recall** is an offline training/evaluation metric; **CTR** is a live metric.  
- **Summarization** saves agent time by condensing the **current conversation**.  
- **Smart Compose** = next‑word/phrase; **Smart Reply** = full sentence.  
- Training entries require **text** content.  
- Newly generated allowlist items start **Unreviewed**.

---
