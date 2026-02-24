
## WEEK 3 - DAY 1

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

### Week 3 – Day 3
- Made OpenAI API calls using HTTPX
- Sent structured JSON requests
- Configured API keys via environment variables
- Updated .bashrc for persistent setup
- Built chatbot with message roles
- Implemented system prompt behavior control
- Maintained conversation history manually
- Generated embeddings for text inputs
- Calculated cosine similarity using NumPy
- Ranked most similar text chunks
- Compared model outputs (nano vs larger model)
- Tested structured JSON output format
- Implemented basic function calling
- Handled API response parsing
- Debugged request and authentication errors


### Week 3 – Day 4
- Implemented full RAG pipeline
- Split large documents into chunks
- Stored chunks with embeddings in JSON
- Generated query embeddings
- Calculated cosine similarity using NumPy
- Ranked chunks by similarity score
- Retrieved Top-K most relevant chunks
- Sent retrieved context to chat completion API
- Compared responses with and without RAG
- Tested different Top-K values
- Implemented hybrid retrieval approach
- Used async API calls
- Added timeout handling
- Ensured JSON-safe outputs

