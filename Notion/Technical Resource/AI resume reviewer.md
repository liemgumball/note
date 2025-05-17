
Created by: liemgumball
Created time: March 8, 2025 5:54 PM
Tags: Product
URL: https://github.com/liemgumball/ai-resume-reviewer

# Goals

Create an AI-powered resume analysis tool that helps job seekers improve their resumes and match job descriptions more effectively.

## Non-goals

- Practicing technical
- Back-End with NestJS
- PostgreSQL
- Docker and AWS for CI/CD

# Features

- Upload **PDF/DOC** resumes
- AI-powered resume analysis (format, grammar, skills)
- **Job Match Score** – AI compares resume with job description
- Smart **resume improvement suggestions**
- **API for resume analysis** (for future integrations)
- **Dashboard** to track past resume analyses

## **🛠 Tech Stack**

- **Front-end**: `Next.js`, `TypeScript`, `TailwindCSS`
- **Back-end**: `NestJS`, `OpenAI API`, `PostgreSQL`
- **Infrastructure**: `Docker`, `AWS`

# Feature plan

## **🛠 Core Features (MVP - 3-4 weeks)**

🔹 **1. User Authentication**

- Sign up & login (NextAuth.js with JWT)
- Google/GitHub login
- Profile settings (basic user info)
- Authorization (basic user & recruiter)

🔹 **2. Resume Upload & Parsing**

- Upload PDF/DOCX resumes
- Extract text using **pdf-parse / mammoth.js**
- Store parsed content in **MongoDB/PostgreSQL**

🔹 **3. AI-Powered Resume Analysis**

- Integrate **OpenAI API** (GPT-4-turbo)
- AI feedback on:
✅ Formatting
✅ Grammar & readability
✅ Skills & experience match
✅ Missing keywords
- Generate structured feedback

🔹 **4. Job Match Score**

- Users input job descriptions
- AI compares resume & job description
- Calculates **"Job Match Score" (0-100%)**
- Highlights missing skills & improvements

🔹 **5. AI-Generated Resume Suggestions**

- AI suggests better **wording & structure**
- Option to **download improved resume**

🔹 **6. API for Resume Analysis**

- REST API for future integration (e.g., recruiters)

🔹 **7. Basic Dashboard**

- View uploaded resumes
- See past analyses & scores