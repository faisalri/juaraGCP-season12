# 🔍 Discovery Phase — Agent Assist Delivery Lifecycle (Premium MD Session)

## 📘 Module Introduction: Delivery Lifecycle
The delivery lifecycle for Agent Assist implementations (POC or full deployment) typically includes four phases:
1. **Discovery**
2. **Design**
3. **Implementation & Testing**
4. **Deploy / Post‑Launch**

This session covers the **Discovery Phase**, where we identify customer requirements, assess feasibility, and plan the integration approach.

---

## 🥇 Step 1: Identify and Assess
The Discovery Phase begins with gathering customer requirements. Three primary assessment areas are:

### 🟦 **CHANNEL**
- Does the customer need Agent Assist features for **Chat**, **Voice**, or **both**?
- Are different channels using different workflows or CRMs?

### 🟩 **FEATURES**
Which Agent Assist features must be enabled per channel?
- LLM Summarization
- Generative Knowledge Assist (GKA)
- Smart Reply
- Live Translation
- (Optional) Custom model development requirements

### 🟨 **ECOSYSTEM**
Identify the customer's existing environment:
- What **Agent Desktop / CRM** do they use? (e.g., Salesforce, Zendesk, custom UI)
- Do they want **direct integration** with their existing Agent Desktop?
- Assess integration feasibility.

---

## 🥈 Step 2: Assess Historical Data
Historical data helps train, tune, and validate features such as Summarization and Agent Assist Recommendations.

Key considerations:
- What formats does the customer store historical data in?
- Voice recordings must be transcribed via STT or converted to JSON text.
- Data must match **Cloud Speech‑to‑Text** response structures.
- Quality of historical data affects AI accuracy.

---

## 🥉 Step 3: Understand the Current Google Cloud Setup
Determine whether the customer has the necessary GCP setup:
- Cloud Storage
- STT
- Conversational Agents (DFCX)
- Agent Assist
- Pub/Sub

CES components may live across multiple projects. Conversations and documents may be in different environments.

For UI integration:
- Agent Assist **Backend Module** must be deployed in the customer's project.
- This requires a UI connector + Pub/Sub interceptor.

---

## 🏅 Step 4: Determine Implementation Expertise
Evaluate whether the customer's engineering team can configure the required modules.

### 🖥️ **Agent Assist UI Modules**
**Customer Capability:**
- Can the customer configure the Agent Assist UI modules in their current CRM or desktop UI?

**Service Provider Support:**
- If not, the service provider assists with integration (e.g., Salesforce UI integration) to deliver a functional end‑to‑end experience.

### 🗂️ **Agent Assist Backend Modules**
**Customer Capability:**
- Can the customer deploy the Backend modules in their GCP environment?

**Service Provider Support:**
- If not feasible, the service provider deploys a **default backend module** to enable demo‑ready functionality.

---

# 📝 Summary
During Discovery, you:
- Identify channels, features, and ecosystem requirements
- Evaluate historical data readiness
- Assess Google Cloud setup
- Determine implementation skills and support needs

This ensures the solution design aligns perfectly with customer reality.

---
