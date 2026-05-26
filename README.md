# ai-mentor-portfolio - Surimalli Koteswara Rao
## Day 1 — Setup complete

- ✅ Google AI Studio API key provisioned
- ✅ Groq API key provisioned
- ✅ Hello-Gemini call working — see [Day1_Setup.ipynb](Day1_Setup.ipynb)
- 4-tool comparison matrix from Lab 1A: see screenshot below



<img width="1008" height="383" alt="gemini_first_call png" src="https://github.com/user-attachments/assets/4ec0d799-430c-4597-b56f-364eea2eec96" />

---------------------------------------------------------

# Day 3 — Lab 3B: Placement-Cell AI Policy 

<img width="1875" height="503" alt="Day-3_Verification__Matrix" src="https://github.com/user-attachments/assets/07c9285f-f832-4326-af95-8ab40bf00caf" />


---------------------------------------------------------


## Day 4 — Productivity sprint

**Company:** **Deloitte USI**
**Time:** 45 minutes (timeboxed)

1. Gamma generated incorrect hiring statistics; corrected using Perplexity sources.
2. Eligibility slide showed wrong CGPA cutoff; verified and edited.
3. Replaced generic CTA with company-specific preparation advice


---------------------------------------------------------


# Day 5 — Résumé Scorer Streamlit Application

## Live Application
Official App Link: https://resume-scorer-5m5zts9ysniuvappiitnhad.streamlit.app/

## Project Overview
This project was developed as part of **Day 5 Lab 5A**.

The application compares a résumé with a job description and generates an AI-powered fit score using Gemini 2.5 Flash.

## Features
- Résumé vs Job Description scoring
- AI-generated rationale
- Missing skills detection
- Suggestions for improvement
- Technical and soft skill breakdown
- Learning resources for missing skills
- Streamlit interactive UI

## Technologies Used
- Python
- Streamlit
- Gemini 2.5 Flash
- Continue.dev
- GitHub
- Streamlit Community Cloud

## Project Status
✅ Completed Day 5 Task  
✅ Successfully deployed on Streamlit Cloud  
✅ Public application link working

## Reflection
This project helped in understanding:
- AI-assisted application development
- Streamlit deployment workflow
- GitHub integration
- API key security using Streamlit secrets
- Prompt engineering with Gemini


---------------------------------------------------------

# Day 5 Lab 5B — Hugging Face Pulls

## Models tested

- facebook/bart-large-mnli
- distilbert-base-uncased-finetuned-sst-2-english

## Timing comparison

| Mode | Min | Avg | Notes |
|---|---|---|---|
| HF API | 0.8s | 1.2s | Cold start around 20s |
| Local Colab | 2.1s | 3.4s | Initial download around 60s |

## Reflection

1. HF API is useful for quick experiments without downloading models.
2. Local inference is better for batch processing after the model is cached.
3. API is easier for small projects; local hosting helps at scale.


---------------------------------------------------------


# Day 6 – Lab 6A: Hello-Gemini Structured Output

## Objective
Extract structured résumé data from unstructured text using :contentReference[oaicite:0]{index=0} Gemini and validate it with Pydantic.

## Tech Used
- Python
- :contentReference[oaicite:1]{index=1} Gemini API
- Pydantic
- Google Colab

## Workflow
- Install libraries
- Configure Gemini API key
- Define résumé schema using Pydantic
- Extract JSON from résumé text
- Validate output against schema
- Process multiple sample résumés

## Errors Handled

### 1. Markdown Fence Wrapping
Gemini sometimes returns JSON inside ```json blocks.  
Handled by retrying with prompt: **Return only JSON, no markdown.**

### 2. Missing Phone Number
Some résumés have no phone number.  
Handled using:

```python
phone: Optional[str] = None

## Day 6 — Capstone Sprint 1: PlacementDataProcessor

### Engineer Answer

### 1. PROBLEM
Job descriptions from company career sites are unstructured HTML pages. Placement teams need structured data such as company name, role, required skills, location, CGPA, and package so students can search and filter opportunities easily. Manual extraction does not scale across many JDs.

---

### 2. ARCHITECTURE
Pipeline built:

JD URL  
→ BeautifulSoup scraper  
→ Clean extracted text  
→ Gemini structured-output call using `response_schema=JD.model_json_schema()`  
→ Pydantic validation  
→ save output into `data/jds.jsonl`

This converts raw web job postings into clean machine-readable JSON.

---

### 3. TRADE-OFFS

- **Cost:** Used :contentReference[oaicite:0]{index=0} Gemini free-tier API, so cost was zero.
- **Latency:** ~2–5 seconds per JD depending on page size and API response.
- **Accuracy:** Pydantic validated schema successfully, but some fields like Netflix role title came back incomplete due to weak page text extraction.
- **Complexity:** Scraping is fragile.  
  - :contentReference[oaicite:1]{index=1} returned compressed `zstd` response and scrape failed.
  - :contentReference[oaicite:2]{index=2} returned `503 high demand` from Gemini.
  These required retry / fallback handling.

---

### 4. SCALE

- **10 JDs/day** → easy on free tier
- **100 JDs/day** → possible with batching + retries
- **1000+ JDs/day** → requires queueing + better scraping strategy
- **10K/day** → move to paid API or open-source hosted model

Output JSONL can later be indexed into vector DB for retrieval.

---

### 5. INTERVIEW ANSWER

“I built a structured-output data pipeline that converts job-description URLs into validated JSON using BeautifulSoup, Gemini structured generation, and Pydantic. The output is stored as JSONL and will be used as the input dataset for the Day 7 RAG pipeline.”

---

## Results

Successfully processed 3 JDs:

- :contentReference[oaicite:3]{index=3}
- :contentReference[oaicite:4]{index=4} — Software Engineer, Android/Chrome, Security Infrastructure
- :contentReference[oaicite:5]{index=5} — AS400 (RPG/400)

Saved output file:

`data/jds.jsonl`

---

## Files

- `Day6_PlacementProcessor.ipynb`
- `data/jds.jsonl`

---

### Pair:
Mentor 1 :Surimalli Koteswara Rao
Mentor 2 : M Sudheer

## Day 7 — PlacementKnowledgeRAG

Built a citation-based RAG chatbot for placement preparation using:

- **MiniLM (all-MiniLM-L6-v2)** for embeddings
- **ChromaDB** for vector storage
- **LangChain RetrievalQA** for retrieval pipeline
- **Gemini 2.5 Flash** for answer generation

### Features
- Indexed **50+ documents** (Job Descriptions + syllabus chunks)
- Retrieves **top-4 relevant chunks**
- Answers only from retrieved context
- Includes source references for answers
- Returns **“I do not know”** for out-of-context questions

### Sample Queries
- Which companies want Java + DSA + CGPA 7+?
- Which JDs require Python?
- What are Sem 5 OS topics?
- Companies hiring in Hyderabad?

### Interview Summary
Built a placement-focused RAG chatbot using MiniLM embeddings, ChromaDB, LangChain, and Gemini that answers from private placement data with citations while avoiding hallucinated answers.
