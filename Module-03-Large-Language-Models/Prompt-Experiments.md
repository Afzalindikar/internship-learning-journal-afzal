# Prompt Engineering Experiments

## WEEK 3 -DAY 1

## Experiment 1 – Basic Prompt
Prompt:
"Explain machine learning."

Observation:
Response was generic.

---

## Experiment 2 – Role Prompting
Prompt:
"You are a university professor. Explain machine learning in simple terms."

Observation:
More structured and educational response.

---

## Experiment 3 – Few-Shot Prompting
Provided 2 examples before asking question.

Observation:
Model followed desired format consistently.

---

## Experiment 4 – Chain of Thought
Prompt:
"Explain step by step..."

Observation:
Improved reasoning clarity.

---

## Experiment 5 – Structured Output
Used JSON schema.

Observation:
Reliable structured responses for automation.


## WEEK 3 - DAY 2

# Week 3 – Day 2 Prompt Experiments

## Experiment 1 – Direct Question Without Retrieval

Prompt:
"What is vector similarity?"

Observation:
- Answer was generic.
- Not grounded in project data.
- Risk of hallucination.

---

## Experiment 2 – Using Retrieved Top-5 Chunks (RAG)

Prompt Structure:
"Answer the question using only the provided context."

Context:
Top-5 most similar chunks from chunks.json.

Observation:
- Answer was more accurate.
- Based on stored project notes.
- Reduced hallucination.

Conclusion:
RAG improves reliability.

---

## Experiment 3 – Clear Instruction Prompt

Prompt:
"Explain cosine similarity in simple terms with formula."

Observation:
- Response became structured.
- Included formula and explanation.
- Clearer output.

Lesson:
Specific instructions improve clarity.

---

## Experiment 4 – Step-by-Step Prompt

Prompt:
"Explain step-by-step how similarity is calculated."

Observation:
- Model explained:
  1. Dot product
  2. Norm
  3. Final cosine formula
- Easier to understand.

Lesson:
Step-by-step prompting improves reasoning quality.

---

## Experiment 5 – JSON Structured Output

Prompt:
"Return the result in JSON format with fields: answer, similarity_score."

Observation:
- Output became structured.
- Easy to parse programmatically.
- Useful for automation.

