# Session 04 — Prompt Design in Vertex AI: Challenge Lab (GSP519)

> **Timebox:** 1 hour 30 minutes • **Level:** Introductory (Skill Badge Challenge Lab)  
> **Mode:** Self‑paced Lab • **Platform:** Google Cloud Skills Boost

---

## 📝 Overview

This challenge lab tests your ability to apply **prompt engineering best practices** within **Vertex AI Studio** and **Vertex AI Workbench**.  
You’ll help *Cymbal Direct*, an outdoor gear retailer, create a set of generative AI tools for:

- **Evocative Product Descriptions**  
- **Catchy Marketing Taglines**

You will design, refine, evaluate, and implement prompts using Gemini models, then extend your work into executable Python code within a Jupyter notebook.

This lab requires you to perform tasks **without step-by-step guidance**, using your skills from previous sessions.

---

## 🎯 Objectives

After completing this challenge lab, you will:

- Build an **image‑based product analysis prompt** using the Gemini model  
- Create a **tagline generator prompt** with parameters & examples  
- Evaluate and iterate prompts for clarity, creativity, and control  
- Run **image analysis Python code** inside Vertex AI Workbench  
- Run **tagline generation Python code** inside Vertex AI Workbench  
- Validate your results using the challenge checkpoints

---

## 🧰 Setup & Requirements

Before starting the lab:

- Use **Incognito** mode to avoid conflicts with your main Google account  
- Use the **student credentials** provided by the lab  
- Do not enable:  
  - 2FA  
  - Recovery email  
  - Google Cloud free trial  
- The timer **cannot be paused** once the lab starts

---

# 🚀 Task-by-Task Guide

---

## **Task 1 — Build a Gemini Image Analysis Tool**

You will create a prompt in Vertex AI Studio using the `model_1_name` Gemini model to analyze product images and generate descriptive text.

### Steps:
1. Open **Vertex AI Studio** → create **New Prompt**  
2. Load the provided product image (from Google Cloud Storage path)  
3. Experiment with prompts that generate:  
   - Short descriptive captions  
   - Catchy phrases for advertisements  
   - Poetic, nature-inspired descriptions  
4. Evaluate and refine your outputs  
5. Save the prompt as:  
   **Cymbal Product Analysis**

---

## **Task 2 — Build a Gemini Tagline Generator**

You will create a customizable tagline generator using the `model_1_name` Gemini model.

### Requirements:
- Add **System Instructions** describing the marketing scenario  
- Add **2 Examples** (input → output) for in-context few-shot prompting  
- Design a prompt that supports parameterized tagline styles:  
  - Product attributes (durable, lightweight, etc.)  
  - Target audience (adventurers, families, etc.)  
  - Emotional resonance (empowered, inspired, connected)

Save the prompt as:  
**Cymbal Tagline Generator Template**

---

## **Task 3 — Experiment with Image Analysis Code (Notebook)**

Switch to **Vertex AI Workbench**, open the notebook:

```
image-analysis.ipynb
```

Set kernel → **Python 3**.

### Do the following:
- Copy the code snippet from Vertex AI Studio  
- Paste into the designated notebook cell  
- Replace authentication block with `PROJECT_ID` and `LOCATION`  
- Run all cells  
- Modify the prompt inside the code to generate more creative descriptions

---

## **Task 4 — Experiment with Tagline Generation Code**

Open the notebook:

```
tagline-generator.ipynb
```

Set kernel → **Python 3**.

### Actions:
- Copy tagline generator code from Vertex AI Studio  
- Paste into notebook  
- Replace `PROJECT_ID` and `LOCATION`  
- Modify the prompt to include a **specific keyword** (as requested)  
- Run the updated code and verify new tagline quality

---

# 📝 Session Summary

In this challenge lab, you demonstrated your ability to design and deploy generative AI prompts in Vertex AI Studio and implement them inside Python notebooks. You successfully created:

- A **Gemini-powered product description tool**  
- A **customizable tagline generator**  
- Enhanced and refined both prompts using prompt engineering techniques  
- Executed and modified Gemini API code in Workbench notebooks  

Completing this lab validates your understanding of prompt design and multimodal generative AI integration using Vertex AI.

---

## 📎 Reference Files

- [📄 Cymbal_Tagline_Generator_Template.ipynb](../ref/Cymbal_Tagline_Generator_Template.ipynb)
- [📄 Cymbal_Product_Analysis.ipynb](../ref/Cymbal_Product_Analysis.ipynb)
- [📄 image-analysis.ipynb](../ref/image-analysis.ipynb)
- [📄 notebook_template4.ipynb](../ref/notebook_template4.ipynb)
- [📄 tagline-generator.ipynb](../ref/tagline-generator.ipynb)