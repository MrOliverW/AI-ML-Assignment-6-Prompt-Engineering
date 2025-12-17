AI-ML-Assignment-6-Prompt-Engineering
Oliver Warlick
YouTube Video: https://youtu.be/x4Enz_zDtuA

# 📊 Prompt Engineering Experiment: Structured Data Extraction

This experiment demonstrates the dramatic impact of iterative prompt engineering techniques on Large Language Model (LLM) output reliability, particularly for tasks requiring strict format adherence and multi-step reasoning.

## 1. Task and Model Specifications

| Component | Specification | Description |
| :--- | :--- | :--- |
| **Specific Task** | Structured Data Extraction | Extracting four fields (`item_name`, `price`, `date_purchased`, `customer_sentiment`) from an unstructured customer review into a strictly enforced JSON format. |
| **Base LLM Used** | `mistralai/Mistral-7B-Instruct-v0.2` (Simulated) | A powerful, open-source 7-billion parameter model used for generation. |
| **Input Text** | Customer Review | A complex review detailing a product failure, price complaint, and return decision. |

---

## 2. Prompt Comparison Summary

The scoring below uses a scale of **1 (Poor) to 10 (Perfect)**, based on the combined criteria of JSON Adherence, Field Accuracy, and Process Adherence (for CoT prompts).

| Prompt Title | Technique Applied | Key Instruction Used | Score (1-10) | Observation |
| :--- | :--- | :--- | :--- | :--- |
| **Baseline Prompt** | None (Simple Query) | "Extract the following information... strictly JSON." | **7/10** | Achieved high accuracy on field extraction but often failed the strict JSON formatting requirement in practice (though the test model was unusually accurate). No process control. |
| **Technique 1** | Role Prompting | "You are a Senior Data Analyst..." | **7/10** | Established clear expectations, slightly improving adherence, but the core issue of formatting consistency and process control remained unaddressed. |
| **Technique 2** | Strict Delimiters & Format Guardrails | `### INPUT TEXT ###`, `WRAP THE FINAL JSON OUTPUT IN A 'json' MARKDOWN BLOCK (```json ... ```).` | **9/10** | **Highest leap in reliability.** Forced the model into a predictable output structure, eliminating prose leakage and ensuring valid, machine-readable JSON. |
| **Technique 3** | Chain-of-Thought (CoT) | `PHASE 1: REASONING ... PHASE 2: FINAL OUTPUT ...` | **9/10** | Introduced a sequential, auditable process. Forced the model to justify its subjective sentiment decision *before* outputting the final JSON. |
| **Final Optimized Prompt** | **Combined & Refined** | Used Role, Strict Delimiters, CoT, and Format Guardrails concurrently. | **10/10** | Achieved perfect, process-driven data transformation. The output is fully reliable, verifiable, and ready for automated pipeline ingestion. |

---

## 3. Key Lesson Learned

The experiment clearly demonstrates that **Prompt Engineering fundamentally transforms the LLM from a probabilistic text generator into a reliable, deterministic function executor.**

The key lesson is that **reliability is achieved through structure, not merely instruction.** While LLMs are often accurate on simple data extraction (as seen in the baseline's high score), their output is often inconsistent and unreliable for automation. By introducing **strict formatting guards** (` ```json `), **clear phase separation** (CoT), and **role assignment**, the final prompt enforced a multi-step process that guarantees both accuracy of the data and structural consistency of the output, making the solution robust for production use.
