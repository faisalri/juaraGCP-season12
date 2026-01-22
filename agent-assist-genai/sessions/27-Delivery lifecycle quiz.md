
# 📦 Delivery Lifecycle Quiz (Updated)
Passing Score: **80%**

---

## 📝 Quiz Items

### **1. During the implementation and testing phase, what is the best way to ensure the UI integration with the Agent Desktop and Chat Backend is working correctly?**

Options:
1. Checking the accuracy of individual features, such as Smart Reply or Summarization.
2. Evaluating the system's performance metrics, such as speed and latency.
3. Conducting a survey of users to gather their subjective feedback on the UI.
4. **Simulating several rounds of conversation to perform end‑to‑end testing of all functionalities.** ✅

**Correct Answer:** Option 4

---

### **2. When evaluating the accuracy of a Smart Reply model, which method is the most reliable?**

Options:
1. Measuring the time it takes for a suggestion to be generated.
2. Evaluating the length of the suggested response.
3. Guessing what the customer might have wanted to hear and checking for a match.
4. **Comparing suggested replies to a dataset of high‑quality, historical agent responses.** ✅

**Correct Answer:** Option 4

---

### **3. What are the four key steps of the Discovery phase?**

Options:
1. Set up the Agent Assist backend, configure UI modules, integrate with Salesforce, and provide training.
2. **Identify and assess business goals & constraints, review historical data, understand the current Google Cloud setup, and determine implementation expertise & scope.** ✅
3. Define business needs, plan data integration, design the UI, and deploy the solution.
4. Assess channels and features, create a knowledge base, perform a load test, and launch to production.

**Why:** #1 and #4 include implementation/launch tasks, while #3 mixes discovery with deployment. Discovery focuses on **requirements & current‑state assessment** (goals, data, platforms, skills) to shape the implementation plan.

**Correct Answer:** Option 2

---

### **4. What is the role of the analyzeContent API in the Agent Assist data flow?**

Options:
1. **It is called by the Chat Backend to process messages in real time from both the customer and the agent.** ✅
2. It is called by the Agent Desktop Client to receive suggestions from Agent Assist.
3. It is used to export conversation data from Agent Assist to Google Cloud Storage (GCS).
4. It is used by the Chat Client to initiate conversations with the Chat Backend.

**Correct Answer:** Option 1

---

# ⭐ Quick Summary
- The Delivery Lifecycle validates UI flows, Smart Reply accuracy, and feature completeness.
- End‑to‑end simulations are the strongest form of integration testing.
- Smart Reply should always be evaluated against historical agent responses.
- **Discovery** = clarify goals, assess data, understand current GCP setup, confirm skills/scope.
- The analyzeContent API enables real‑time message processing.
