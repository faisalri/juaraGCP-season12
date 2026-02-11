
# 04 — Where Does the Data Come From? Where Does it Go?

> ⏱️ *Estimated time:* 30 minutes (quizzes ~1 hour)  
> 🎯 *Goal:* Capture key ideas and practical takeaways.

---

▶️ Video: Where Does the Data Come From? Where Does It Go?

Click below to watch the full walkthrough:

[![Video](https://img.youtube.com/vi/UFNMeQRMXEs/0.jpg)](https://www.youtube.com/watch?v=UFNMeQRMXEs)

> 📺 *YouTube Video:* Data Flow & AI — Introduction to Security in the World of AI

---

## 🧠 At a Glance

- Training data fuels AI models; its quality determines output quality.
- Poor or unsafe training data can cause harmful, biased, or incorrect outputs.
- AI applications evolve by retraining models using new user‑provided data.
- User input may or may not be collected, depending on the application.
- Data collection practices differ between enterprise and consumer products.

---

## 🔐 Key Concepts

### ⭐ The importance of good training data

- Bad training data → bad outputs.
- Sensitive information in training data may leak via model responses.
- Real‑world data is messy; processing it can introduce unintended behavior.
- Example: Training a recipe generator with bad recipes → bad results.

### ⭐ How AI applications evolve

- AI apps improve using updated models.
- New training data may include user interactions → introduces security concerns.

### ⭐ User input & data collection

- Providing data to an AI app is similar to filling out a form: you are *sharing* data.
- Whether data is collected depends on how the app/API was built.
- Always evaluate data‑handling practices before using an AI application.

### ⭐ Enterprise vs. Consumer Data Practices

- Enterprise software often provides stronger privacy guarantees.
- Consumer apps may store interactions to improve models.
- Always review data policies before using any AI tool.

---

## 📝 Quiz — What should you ask? (Choose two)

**Scenario:** You're about to input medical personal data into a generative AI model. You do **not** want this data to be stored or linked to you.

### Correct Answers

- **✔️ Does the AI application store inputs/outputs?**
- **✔️ Does the AI application obfuscate or anonymize personal identifying information (PII) before storing or processing data?**

### Incorrect Options

- Can the model be fine‑tuned for specific medical domains?
- Does the AI application have a user‑friendly interface?
- What is the underlying architecture of the AI model?

---

## ✅ Action Items

- Evaluate the source and quality of training data for any AI system you use.
- Review how apps store or process user input.
- Distinguish between enterprise‑grade vs. consumer‑grade data policies.