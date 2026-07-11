<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:030014,35:1e1b4b,70:0e7490,100:06b6d4&height=170&section=header&text=Arnav%20Mahajan&fontSize=50&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=Math%20%26%20Computing%20%C2%B7%20AI%2FML%20Engineer%20%C2%B7%20Builder&descSize=17&descAlignY=58&descColor=94d8e8" width="100%"/>

</div>

<div align="center">

[![Typing SVG](https://readme-typing-svg.demolab.com?font=JetBrains+Mono&size=16&pause=1200&color=06b6d4&center=true&vCenter=true&width=640&lines=B.Tech+Mathematics+%26+Computing+%40+MITS+Gwalior;Building+things+that+actually+work;DSA+grinder+%7C+ML+explorer+%7C+Full-stack+builder;Semester+4+%E2%86%92+shipping+real+projects)](https://git.io/typing-svg)

</div>

<br/>

<div align="center">

![Degree](https://img.shields.io/badge/🎓%20B.Tech-Mathematics%20%26%20Computing-1e1b4b?style=for-the-badge)
![College](https://img.shields.io/badge/🏫-MITS%20Gwalior-0e7490?style=for-the-badge)
![Semester](https://img.shields.io/badge/📚-Semester%204%20%C2%B7%20Batch%2012-4338ca?style=for-the-badge)
![Location](https://img.shields.io/badge/📍-India-334155?style=for-the-badge)

</div>

<div align="center">

[![Projects](https://img.shields.io/badge/🚀_Projects-06b6d4?style=for-the-badge&logoColor=white)](#-ls-projects)
[![LinkedIn](https://img.shields.io/badge/Connect-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/arnav-mahajan-61b7b2301/)
[![Email](https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:toarnavmahajan@gmail.com)
[![LeetCode](https://img.shields.io/badge/LeetCode-FFA116?style=for-the-badge&logo=leetcode&logoColor=black)](https://leetcode.com/u/VXBBbYkQpraqs/)
[![X](https://img.shields.io/badge/Follow-000000?style=for-the-badge&logo=X&logoColor=white)](https://x.com/ArnavMahaj44081)

</div>

<div align="center">

![Profile Views](https://komarev.com/ghpvc/?username=Code99701&color=06b6d4&style=for-the-badge&label=VISITORS)

</div>

<br/>

<div align="center">

<img src="https://skillicons.dev/icons?i=py,cpp,cs,js,html,css,react,tailwind,nodejs,flask,fastapi,mysql,mongodb,sqlite,git,github,vscode,tensorflow,pytorch&theme=dark&perline=10" alt="Skill Icons"/>

</div>

<br/>

## About

I'm a Mathematics & Computing undergraduate at MITS Gwalior (Semester 4), focused on data structures, applied mathematics, and full-stack engineering. I'd rather ship something that runs than talk about something that might.

My project work spans the full stack — from training a Random Forest classifier that predicts live IPL match outcomes, to building an async FastAPI + MongoDB platform that fingerprints documents and verifies ownership with a blockchain-backed audit trail. I care about the engineering underneath the demo: clean data pipelines, sensible APIs, and systems that hold up under real use, not just a happy path.

I pair that with daily DSA practice on LeetCode and ML/DL fundamentals built from scratch — strong problem-solving instincts make the rest of the stack easier to reason about.

---

## `> ls ./projects`

| # | Project | What it does | Stack | Status |
|---|---------|---------------|-------|--------|
| 01 | [**IPL Win Predictor**](https://github.com/Code99701/macro-project) | Predicts live match win-probability from a Random Forest model trained on 2008–2020 IPL data | `Python` `Flask` `scikit-learn` | 🟢 Live |
| 02 | [**DataDNA AI**](https://github.com/Code99701/DataDNA-AI) | Document ownership tracking & verification platform with blockchain-backed proofs | `FastAPI` `MongoDB` `Sentence-Transformers` | 🔄 Active dev |
| 03 | [**Currency Converter**](https://github.com/Code99701/currency-converter-using-api-data) | Real-time currency conversion via a pluggable exchange-rate API adapter | `JavaScript` `HTML` `CSS` | ✅ Done |

<sub>Dropped the old DSA Vault entry — that repo no longer exists on GitHub.</sub>

---

## `> cat ./featured-projects.md`

<details>
<summary><b>🏏 IPL Win Predictor</b> — real-time match win-probability engine</summary>
<br/>

**Overview**
A Flask web app that predicts a live IPL match's win probability from the current match state — target, current score, overs bowled, wickets lost, teams, and venue.

**Problem Statement**
Static pre-match predictions ignore how win probability shifts ball-by-ball as a chase unfolds. This models that in-game uncertainty from historical outcomes instead of commentary gut-feel.

**Key Features**
- Live win/loss probability from partial match state
- Ground-aware predictions — venue-specific boundary size is engineered in as a feature
- Every prediction is logged to a database for later analysis
- Legacy Streamlit variant included alongside the primary Flask app

**Architecture**
```
Match state (form) → Flask route → sklearn Pipeline
  (OneHotEncoder + RandomForestClassifier) → win probability → SQLite log
```

**Tech Stack**
`Python` · `Flask` · `scikit-learn` · `Pandas` · `NumPy` · `SQLAlchemy` · `SQLite`

**Engineering Challenges**
- Normalizing inconsistent venue names across seasons (e.g. Bangalore vs. Bengaluru) before merging in ground-size data
- Balancing the classifier against a skewed win/loss distribution in the historical dataset
- Keeping the trained pipeline out of version control — `pipe.pkl` is pulled from Google Drive at runtime via `gdown` instead of being committed

**Performance**
A 500-tree Random Forest with class-balanced weighting, evaluated with an 80/20 train-test split and reported via `classification_report`.

**Scalability**
The inference path is stateless per request; the SQLite log is the only shared state, which makes it straightforward to move to a managed database as traffic grows.

**Future Improvements**
- Move match-history storage into a normalized relational schema
- Live ball-by-ball data feed instead of manual match-state entry
- Model versioning with accuracy tracking across retrains

**Repository:** [Code99701/macro-project](https://github.com/Code99701/macro-project)

</details>

<details>
<summary><b>🧬 DataDNA AI</b> — document ownership tracking & verification platform</summary>
<br/>

**Overview**
An async FastAPI platform that registers documents (PDF / DOCX / TXT), fingerprints their content, and later verifies new uploads against everything already registered — with blockchain-backed proof of ownership.

**Problem Statement**
Once a file is shared, proving who created it first is hard. Visible watermarks are easy to strip and metadata is easy to fake, so this focuses on the document's actual content instead of a fragile external marker.

**Key Features**
- Tiered verification pipeline: exact file hash → page hash → embedding similarity → chunk-level analysis
- Multi-owner attribution with contribution percentages when a document overlaps several sources
- JWT authentication with bcrypt password hashing and Google OAuth login
- Rate-limited API (`slowapi`) plus an admin dashboard for oversight
- Blockchain-backed ownership recording via dedicated blockchain routes

**Architecture**
```
Upload → hash + text extraction → per-page sentence embedding
   → similarity check against MongoDB → register (+ blockchain record)
     or return a similarity report if significant overlap is found
```

**Tech Stack**
`FastAPI` · `MongoDB (Motor, async)` · `Sentence-Transformers` · `scikit-learn` · `PyJWT` · `bcrypt` · `slowapi`

**Engineering Challenges**
- Tuning a similarity threshold that catches real overlap without flagging unrelated documents
- Keeping page-level embedding comparisons fast as the registered-document collection grows
- Coordinating hash-based exact matches with fuzzier embedding-based matches in a single pipeline

**Performance**
The tiered design short-circuits on exact hash matches, so most repeat-verification requests never reach the more expensive embedding-comparison step.

**Scalability**
Motor's async MongoDB driver keeps I/O non-blocking under FastAPI; the embedding-similarity step is the natural place to introduce a vector index as the document corpus grows.

**Future Improvements**
- Autoencoder-based watermarking layered on top of the current pipeline
- Video and image ownership support
- Public-facing verification API for third parties

**Repository:** [Code99701/DataDNA-AI](https://github.com/Code99701/DataDNA-AI)

</details>

<details>
<summary><b>💱 Currency Converter</b> — real-time FX conversion micro-project</summary>
<br/>

**Overview**
A lightweight, framework-free currency converter that fetches live exchange rates and converts between currencies in real time.

**Problem Statement**
A focused, dependency-light tool for practicing third-party API integration, error handling, and a clean adapter pattern without the overhead of a full framework.

**Key Features**
- Real-time conversion via a live exchange-rate API
- Responsive UI with currency search
- Graceful handling of network/API failures and invalid input
- Adapter layer so the underlying rate provider can be swapped without touching the UI

**Architecture**
```
UI (vanilla JS) → adapter layer → exchange-rate API → parsed response → rendered conversion
```

**Tech Stack**
`JavaScript` · `HTML5` · `CSS3`

**Engineering Challenges**
- Handling rate-limited or failed API responses without breaking the UI
- Keeping the provider swap genuinely painless via the adapter layer

**Performance**
Minimal footprint by design — no build step, no framework overhead.

**Scalability**
The adapter layer is the intentional extension point: a caching layer or a second rate provider can be added without touching UI code.

**Future Improvements**
- Response caching to cut down on repeated API calls
- Historical rate charting

**Repository:** [Code99701/currency-converter-using-api-data](https://github.com/Code99701/currency-converter-using-api-data)

</details>

---

## `> cat ./stack.txt`

**Languages**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=c%2B%2B&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?style=flat-square&logo=c-sharp&logoColor=white)
![MATLAB](https://img.shields.io/badge/MATLAB-0076A8?style=flat-square&logo=mathworks&logoColor=white)

**Frontend**

![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-06B6D4?style=flat-square&logo=tailwind-css&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-563D7C?style=flat-square&logo=bootstrap&logoColor=white)

**Backend**

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=flat-square&logo=flask&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Express](https://img.shields.io/badge/Express-404D59?style=flat-square&logo=express&logoColor=white)

**Databases**

![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=flat-square&logo=supabase&logoColor=white)

**AI / ML**

![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat-square&logo=tensorflow&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white)

**Cloud**

![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonaws&logoColor=white)

**Tools**

![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![VS Code](https://img.shields.io/badge/VS%20Code-007ACC?style=flat-square&logo=visual-studio-code&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)

---

## `> cat ./ai-ml-expertise.md`

| Domain | Proficiency | Tools | Experience |
|---|---|---|---|
| Machine Learning | Applied | scikit-learn, RandomForest | Trained a 500-tree Random Forest classifier for real-time win-probability prediction, with custom feature engineering (venue boundary size, team/city encoding) |
| NLP & Embeddings | Learning | Sentence-Transformers | Semantic similarity search over document embeddings as part of a tiered ownership-verification pipeline |
| Data Analysis | Applied | Pandas, NumPy | Cleaned and engineered features from multi-season historical match and ball-by-ball datasets |
| API Engineering | Applied | FastAPI, Flask | Shipped async, JWT-secured, rate-limited REST APIs and a lightweight ML inference service |
| Model Deployment | Applied | Flask, Pickle, gdown | Serves a trained model in a live Flask app, pulling versioned weights at runtime |
| Data Visualization | Familiar | Pandas, Jupyter | Exploratory analysis and notebooks for model experimentation |

---

## `> git log --engineering-experience`

**Academic Foundation**
- B.Tech in Mathematics & Computing, MITS Gwalior — Semester 4, Batch 12
- Coursework: Number Theory & Cryptography, Applied Mathematics (Transforms & Calculus), DBMS (Normalization, Transactions, SQL)

**Personal Products**
- **IPL Win Predictor** — Flask + Random Forest classifier, model served via `gdown`, predictions logged through SQLAlchemy
- **DataDNA AI** — FastAPI + MongoDB ownership/verification platform with a blockchain-backed proof-of-ownership layer
- **Currency Converter** — vanilla JS real-time FX tool with a pluggable provider adapter

**Practice & Research**
- Implementing core ML/DL algorithms from scratch for hands-on fundamentals
- Daily DSA problem-solving on LeetCode

**Open Source**
- Actively looking to make first contributions — reach out if you know a good first issue

---

## `> ls ./certifications`

**Currently Pursuing**

No formal certifications yet — currently building proof-of-work through shipped projects instead of badges. Actively exploring Machine Learning specializations and AWS cloud fundamentals.

---

## `> ls ./coding-profiles`

<div align="center">

[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Code99701)
[![LeetCode](https://img.shields.io/badge/LeetCode-FFA116?style=for-the-badge&logo=leetcode&logoColor=black)](https://leetcode.com/u/VXBBbYkQpraqs/)

</div>

---

## `> git log --stats`

<div align="center">

<table>
  <tr>
    <td>
      <img src="https://github-readme-stats.vercel.app/api?username=Code99701&show_icons=true&theme=aura&include_all_commits=true&count_private=true&hide_border=true&rank_icon=github&custom_title=Arnav's+GitHub+Stats" alt="GitHub Stats"/>
    </td>
    <td>
      <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Code99701&layout=compact&langs_count=8&theme=aura&hide_border=true" alt="Top Languages"/>
    </td>
  </tr>
</table>

[![GitHub Streak](https://streak-stats.demolab.com?user=Code99701&theme=aura&hide_border=true&date_format=j%20M%5B%20Y%5D)](https://git.io/streak-stats)

<br/>

<img src="https://github-readme-activity-graph.vercel.app/graph?username=Code99701&theme=react-dark&hide_border=true&color=06b6d4&line=06b6d4&point=ffffff&area=true&area_color=06b6d420" width="100%" alt="Contribution Graph"/>

<br/><br/>

<img src="https://github-profile-trophy.vercel.app/?username=Code99701&theme=tokyonight&column=4&no-frame=true&margin-w=10&margin-h=10" alt="Trophies"/>

<br/>

<img src="https://raw.githubusercontent.com/Code99701/Code99701/output/github-snake-dark.svg" width="100%" alt="Contribution Snake"/>

</div>

<sub>The contribution snake needs a one-time setup — see <code>snake-workflow.yml</code> below.</sub>

---

## `> cat ./currently-learning.md`

```yaml
current_focus:
  learning:
    - Data Structures & Algorithms (daily practice)
    - Machine Learning theory → applied projects
    - Number Theory & Applied Mathematics (semester coursework)
  building:
    - DataDNA AI — extending ownership verification with blockchain-backed proofs
    - IPL Win Predictor — refining feature engineering & model accuracy
  exploring:
    - Semantic embeddings & similarity search (Sentence-Transformers)
    - Async API design with FastAPI
  practicing:
    - LeetCode, daily problem solving
    - ML/DL fundamentals from scratch
  open_to:
    - Open-source collaboration
    - Internship / SDE & AI-ML opportunities
```

---

## `> cat ./contact.md`

<div align="center">

[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Code99701)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/arnav-mahajan-61b7b2301/)
[![Email](https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:toarnavmahajan@gmail.com)
[![X](https://img.shields.io/badge/X-000000?style=for-the-badge&logo=X&logoColor=white)](https://x.com/ArnavMahaj44081)

</div>

---

<div align="center">

*"Ship it, learn from it, repeat."*

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:06b6d4,50:1e1b4b,100:030014&height=90&section=footer" width="100%"/>

</div>
