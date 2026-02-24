# Module 03 – Large Language Models (LLMs)

## WEEK 3 - DAY 1

## 1. Introduction to LLMs

Large Language Models (LLMs) are AI models trained on massive text data.
They learn language patterns and predict the next most likely word in a sentence.

They are built using **Transformer architecture** and work using **tokens**.

Examples: GPT, LLaMA, Claude, Mistral.

---

## 2. API Keys and Proxy

### API Key
- A secret key used to access AI services.
- Must be stored securely (e.g., `.env` file).
- Never push it to GitHub.

### Proxy
- A middle layer between your app and the AI service.
- Used for:
  - Security
  - Rate limiting
  - Logging
  - Cost tracking

---

## 3. How LLMs Work

1. Text is broken into **tokens**.
2. Tokens are converted into **embeddings (numbers)**.
3. Embeddings pass through **Transformer layers**.
4. The model predicts the next word using probability.

LLMs do not think — they predict based on patterns.

---

## 4. Self-Attention

Self-attention helps the model understand:
- Word relationships
- Context importance

Example:
"The dog chased the cat because it was fast."
→ "it" refers to dog.

---

## 5. Context Limitations

LLMs have token limits (8k, 32k, 128k, etc.).

If the input is too long:
- Earlier content gets removed.

Solutions:
- Split text into chunks
- Use RAG (Retrieval Augmented Generation)

---

## 6. Tokens

- Words are split into smaller pieces.
- Token count affects cost.
- More tokens = higher cost.

---

## 7. Embeddings

Embeddings convert text into numerical vectors.

Similar meaning → similar vectors.

Used for:
- Semantic search
- Similarity matching
- Clustering
- RAG systems

---

## 8. Topic Modeling

Used to find hidden themes in large text datasets.

Methods:
- LDA
- Embedding-based clustering

Applications:
- News grouping
- Research analysis
- Feedback analysis

---

## 9. Vector Databases

Store embeddings for similarity search.

Examples:
- ChromaDB
- LanceDB
- Pinecone
- Weaviate

Used in:
- RAG systems
- Semantic search
- AI chatbots

---

## 10. Retrieval Augmented Generation (RAG)

RAG improves LLM accuracy using external data.

Steps:
1. Convert query into embedding.
2. Search vector database.
3. Retrieve relevant documents.
4. Send documents to LLM.
5. Generate grounded answer.

Benefit:
- Reduces hallucination.
- Improves reliability.

---

## 11. Hybrid RAG

Combines:
- Keyword search
- Vector search

Provides better retrieval results.

---

## 12. Base64 Encoding

Used to encode:
- Images
- Audio
- Files

Converts binary data into text format for API transmission.

---

## 13. Vision Models

AI models that understand images.

They can:
- Describe images
- Extract text (OCR)
- Detect objects

---

## 14. Video Analysis

Video = multiple image frames.

Process:
1. Extract frames.
2. Analyze each frame.
3. Combine results.

---

## 15. Prompt Engineering

Improves LLM output by writing better prompts.

Techniques:
- Clear instructions
- Role-based prompts
- Few-shot examples
- Step-by-step reasoning

Better prompt → Better output.

---

## 16. Sentiment Analysis

Detects emotion in text:
- Positive
- Negative
- Neutral

Used in reviews and social media analysis.

---

## 17. Text Extraction

Extract text from:
- PDFs
- Images
- Scanned documents

---

## 18. Schemas

Schemas define structured output format (e.g., JSON).

Example:
- name
- age
- email

Used for reliable automation.

---

## 19. Function Calling

LLM can select predefined functions and pass structured parameters.

Example:
- get_flights()
- book_hotel()
- check_weather()

Used in automation systems.

---

## 20. SQL Database Interaction

LLM converts natural language into SQL queries.

Example:
"Show users registered this month"
→ Converted into SQL query and executed.

---

## 21. Tools and Agents

Tools:
- APIs
- Databases
- Web search
- Calculators

Agents:
- Decide which tool to use
- Perform multi-step reasoning

---

## 22. LLM Evaluation & Testing

Evaluation methods:
- Accuracy
- Human review
- Regression testing

Testing methods:
- YAML test cases
- Assertions
- Prompt comparisons

---

## 23. Cost Optimization

Ways to reduce cost:
- Reduce token usage
- Use smaller models
- Cache responses
- Use RAG instead of long prompts

---

## 24. Commercial Applications

- AI chatbots
- Customer support automation
- Document summarization
- Coding assistants
- Resume screening

## WEEK 3 - DAY 2

# Project 1 – Embeddings, Vector DBs & RAG

## 1. Introduction

This project focuses on:
- Embeddings
- Vector Databases
- Hybrid RAG
- Function Calling
- Cost-effective similarity search
- Multimodal embeddings (text + image)

Goal:
Build a system that stores embeddings and answers questions using similarity search.

---

# 2. Embeddings

Embeddings convert text (or image) into numerical vectors.

Example:
"dog" → [0.23, -0.91, 0.11, ...]

Similar meaning → Similar vectors.

Used for:
- Text similarity
- Image similarity
- Search systems
- RAG

---

## Similarity Methods

To compare vectors:

### 1. Cosine Similarity
Measures angle between vectors.
Most commonly used.

Formula:
cos(A,B) = (A · B) / (||A|| ||B||)

### 2. Dot Product
Measures alignment between vectors.

### 3. Norm
Length (magnitude) of vector.

Libraries:
- NumPy
- Sentence Transformers

---

# 3. Sentence Transformers

Sentence Transformers generate embeddings for full sentences.

Used when:
- You need semantic search
- You want better sentence-level similarity

More cost-effective compared to large LLM embeddings.

---

# 4. OpenAI + HTTPX

Used for:
- Calling embedding APIs
- Making async requests

Why HTTPX?
- Supports async
- Supports timeout handling
- Better control over requests

---

# 5. Environment Variables

Store API keys securely.

Example:
export OPENAI_API_KEY="your_key_here"

Can be stored in:
- .bashrc
- .env file

Never commit API keys to GitHub.

---

# 6. AI Pipe

AI Pipe is a middleware system that:
- Manages API requests
- Handles authentication
- Controls rate limits
- Tracks cost

Acts as a central AI gateway.

---

# 7. Multimodal Embeddings

Multimodal = Text + Image embeddings.

Example:
- Nomic AI models
- OpenAI vision models

Use cases:
- Search images using text
- Match image to description

Data sent via:
- JSON
- Base64 (for images)

---

# 8. Vector Databases

Vector DB stores embeddings for similarity search.

Common options:
- ChromaDB
- LanceDB
- Pinecone

They allow:
- Fast nearest-neighbor search
- Efficient similarity retrieval

---

# 9. Chunking

Large documents must be split into smaller parts.

Why?
Because LLMs have token limits.

Process:
1. Break text into chunks
2. Generate embedding for each chunk
3. Store in chunks.json

Example structure:

chunks.json

[
  {
    "id": 1,
    "source": "document1.pdf",
    "text": "Chunk content...",
    "embedding": [0.12, 0.44, -0.91]
  }
]

---

# 10. Tokens

- Text is split into tokens.
- Token count affects cost.
- More tokens = more API cost.

Keep chunks small and optimized.

---

# 11. Asking Questions (ask_question.py)

Steps:

1. Convert user question → embedding
2. Load embeddings from chunks.json
3. Compute cosine similarity
4. Select top-5 most similar chunks
5. Send top chunks to LLM
6. Generate answer

Implementation tools:
- HTTPX (API calls)
- NumPy (similarity calculation)
- Async requests
- Timeout handling
- JSON-safe formatting



# WEEK 3 – DAY 3 

## 1. API Key Issues & Troubleshooting

- API keys can expire or become invalid.
- Always check:
  - Expiry
  - Correct environment variable
  - Correct header format
- Common mistake: Using wrong key in OpenAPI vs AI Pipe.

Key Learning:
Always verify environment variables before debugging code.

---

## 2. AI Pipe vs AI Proxy

AI Proxy:
- Simple middle layer.
- For forwarding API requests.

AI Pipe:
- More advanced system.
- Handles:
  - Token tracking
  - Authentication
  - Rate limiting
  - Cost control

Understanding difference helps avoid token misuse.

---

## 3. Google Authentication (GA2) Issues

Problems faced:
- Key mismatch
- Invalid credentials
- Image compression issues

Solution:
- Check credentials.json
- Verify OAuth setup
- Use Chrome Dev Tools to inspect errors

---

## 4. FastAPI Deployment Issues (Vercel)

Common issues:
- Incorrect configuration
- Missing requirements.txt
- Environment variables not set
- Wrong file structure

Deployment requires:
- FastAPI app
- Proper routing
- API key setup

---

## 5. Project 1 Requirements

Deadline: June 14

Project must include:
- FastAPI backend
- Web scraping
- Discourse API integration
- Deployment (public link)
- Proper evaluation handling

Evaluation:
- Based on 2x2 scoring model
- Functionality + Correctness

---

## 6. Scraping Discourse Data

- Use Discourse API
- Extract posts
- Clean text
- Store for processing

Important:
Handle rate limits properly.

---

## 7. Prompt Engineering (GA3 Q11)

- Clear prompts give better results.
- Specify format.
- Avoid vague instructions.
- Structured prompts reduce ambiguity.

---

## 8. OpenAPI vs AI Pipe Token Usage

- Tokens consumed differ based on service.
- Track usage carefully.
- Improper configuration can double token usage.

---

## 9. Course Structure Insights

- TDS focuses on tools + implementation.
- Requires basic coding background.
- Encouraged asking questions on Discourse.
- GitHub portfolio is important.

---

## 10. Resume & Career Advice

- Showcase projects on GitHub.
- Deploy working APIs.
- Highlight:
  - FastAPI
  - RAG
  - Embeddings
  - Deployment skills


# WEEK 3 – DAY 4 

## 1. Word Embeddings & Semantic Meaning

- Words are converted into vectors.
- Similar meaning → similar vectors.
- Used cosine similarity to compare vectors.
- Learned distance calculation using NumPy.

Key idea:
Embeddings capture meaning, not just keywords.

---

## 2. OpenAI API Calls

- Used HTTPX for making API requests.
- Learned how to send:
  - POST request
  - Headers (Authorization)
  - JSON body
  - API URL

Understood:
- Different endpoints
- Chat completion API
- Model selection (e.g., GPT-4.1 nano)
- API pricing depends on token usage

---

## 3. Environment Setup

- Stored API key in .bashrc
- Used environment variables
- Tested API using curl commands

Important:
Never hardcode API keys in source code.

---

## 4. Chat Completion API

Chat structure includes roles:
- system → instructions
- user → question
- assistant → response

Example:
System: "You are a helpful assistant."
User: "Explain embeddings."

This helps maintain conversation structure.

---

## 5. Chatbot with History

- Maintained previous messages.
- Sent full conversation to API.
- LLM uses history as memory (within token limit).

Important:
LLMs don’t have permanent memory.

---

## 6. Base64 Encoding

- Used to convert image → text format.
- Required when sending images to API.
- Learned encoding and decoding process.

Used for:
- Image understanding
- Multimodal models

---

## 7. Vector Databases & Similarity

- Stored embedding vectors.
- Calculated cosine similarity.
- Retrieved most similar text.
- Used NumPy for vector operations.

Steps:
1. Convert query to embedding.
2. Compare with stored embeddings.
3. Return most similar chunk.

---

## 8. Multimodal Embeddings

- Embeddings for text + image.
- Can search images using text.
- Used models supporting multimodal input.

Example:
Upload product image → Extract details.

---

## 9. Function Calling

LLM can call predefined functions.

Process:
1. Define function schema.
2. Pass tools to model.
3. Model selects function.
4. Returns structured JSON arguments.

Used for:
- Extracting manufacturing date
- Extracting expiry date
- Structured data extraction

---

## 10. Tools & Function Schema

- Defined schema using JSON format.
- Specified required fields.
- Model returned structured output.

Benefits:
- Reliable automation
- Easy parsing
- Reduced ambiguity

---

## 11. Image to Text Conversion

- Convert image → Base64
- Send to multimodal model
- Extract structured information

---

## 12. Key Takeaways

- Understood embeddings deeply.
- Implemented cosine similarity.
- Made API calls using HTTPX.
- Built chatbot with conversation history.
- Implemented function calling with schema.
- Worked with multimodal embeddings.
- Improved debugging and troubleshooting skills.
