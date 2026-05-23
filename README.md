# ai-mentor-portfolio - Surimalli Koteswara Rao
## Day 1 — Setup complete

- ✅ Google AI Studio API key provisioned
- ✅ Groq API key provisioned
- ✅ Hello-Gemini call working — see [Day1_Setup.ipynb](Day1_Setup.ipynb)
- 4-tool comparison matrix from Lab 1A: see screenshot below



<img width="1008" height="383" alt="gemini_first_call png" src="https://github.com/user-attachments/assets/4ec0d799-430c-4597-b56f-364eea2eec96" />

# Day 3 — Lab 3B: Placement-Cell AI Policy 

<img width="1875" height="503" alt="Day-3_Verification__Matrix" src="https://github.com/user-attachments/assets/07c9285f-f832-4326-af95-8ab40bf00caf" />




## Day 4 — Productivity sprint

**Company:** **Deloitte USI**
**Time:** 45 minutes (timeboxed)

1. Gamma generated incorrect hiring statistics; corrected using Perplexity sources.
2. Eligibility slide showed wrong CGPA cutoff; verified and edited.
3. Replaced generic CTA with company-specific preparation advice



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





