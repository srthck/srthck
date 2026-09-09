<div align="center"> <img src="./assets/hero.svg" width="100%" alt="Sarthak Kadam — AI, Backend and Systems Engineer"/> <br/>

<a href="https://github.com/srthck"><img src="https://img.shields.io/badge/GitHub-020617?style=for-the-badge&logo=github&logoColor=white"/></a> <a href="https://www.linkedin.com/in/sarthak-kadam-102134360"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white"/></a> <a href="https://leetcode.com/u/sarthak6001/"><img src="https://img.shields.io/badge/LeetCode-FFA116?style=for-the-badge&logo=leetcode&logoColor=white"/></a> <a href="mailto:sarthakkadam.sk07@gmail.com"><img src="https://img.shields.io/badge/Email-1D4ED8?style=for-the-badge&logo=gmail&logoColor=white"/></a>

</div> <br/>

B.Tech Computer Science & Engineering student at MIT ADT University, Pune. I build systems that have to make a call under uncertainty — is this transaction trustworthy, is this deployment safe, is this payroll run correct — and I try to make every one of those calls explainable after the fact.

<img src="./assets/section.svg" width="100%" alt=""/>
What I build
<table> <tr> <td width="25%" valign="top">

AI / ML

Computer vision, semantic inference, evidence reasoning, ML-assisted classification

</td> <td width="25%" valign="top">

Backend

FastAPI, Node.js/Express, REST APIs, data modeling, auth

</td> <td width="25%" valign="top">

Systems

Offline-first, realtime state, idempotency, audit trails, failure-aware design

</td> <td width="25%" valign="top">

Engineering

Docker, CI/CD, risk analysis, deployment, developer tooling

</td> </tr> </table> <img src="./assets/section.svg" width="100%" alt=""/>
Flagship systems
<table> <tr> <td width="50%" valign="top">
🕸️ TrustMesh

Evidence & trust control plane

Can I trust this before I act on it?

A local-first, pre-transaction evidence system for evaluating transactions, payment destinations, identities, and claims before you act on them — instead of collapsing trust into one binary prediction, it organizes evidence, preserves provenance, and surfaces what to check next.

text
EVIDENCE → EXTRACTION → NORMALIZATION → EVIDENCE GRAPH
   → CONSISTENCY ANALYSIS → RISK / CONFIDENCE / COVERAGE
   → NEXT-BEST EVIDENCE → DETERMINISTIC POLICY
   → PASS · VERIFY · STOP

On-device OCR QR Analysis Claim Extraction Evidence Graph Provenance Contradiction Detection Risk Scoring

Stack: Kotlin · Jetpack Compose · Android · Google ML Kit

<img src="./assets/status.svg" width="100%" alt="TrustMesh: actively building"/> </td> <td width="50%" valign="top">
🛫 PreFlight

Pre-deployment software risk analysis

Before you deploy it — what could break?

A developer-focused system that analyzes the risk a change introduces before it reaches production, reasoning about impact and blast radius rather than just whether the code compiles.

text
CHANGE → IMPACT → DEPENDENCIES → BLAST RADIUS
   → DEPLOYMENT RISK → FAILURE → RECOVERY → DECISION

Git / Diff Code Impact API Impact SQL / Database Docker Blast Radius Rollback Analysis

Stack: Python · Node.js · TypeScript · PostgreSQL · Docker

<img src="./assets/status.svg" width="100%" alt="PreFlight: actively building"/> </td> </tr> </table>

Both come from the same instinct, applied to two different failure modes:

	Problem	Core idea	Decision
🕸️ TrustMesh	Trust under uncertainty	Evidence + reasoning	Pass / verify / stop
🛫 PreFlight	Deployment under uncertainty	Impact + failure analysis	Safe / caution / do not deploy
<img src="./assets/section.svg" width="100%" alt=""/>
Production software
🚛 Shivam Transport — logistics operations platform

Status: 🟢 Production

A full-stack platform built for an actual transport business, running on real field conditions rather than a demo network. It moved my engineering thinking from "can I build it" to "can someone depend on it."

Handles trips, revenue, collections, and field workflows across Unreliable connectivity · Offline queueing · Realtime state · Operational data integrity

Stack: React 19 · TypeScript · Node.js · MUI · Capacitor · Server-Sent Events

FinTech & data integrity
🧾 MSME Payroll & Statutory Compliance

Status: 🟡 In development

A systems-design project treating payroll as a controlled financial process rather than a salary calculator — versioned statutory rules, immutable snapshots, and an append-only ledger so every deduction is explainable and every run is idempotent.

text
PAYROLL INPUT → RULE VERSIONING → STATUTORY CALCULATION
   → IMMUTABLE SNAPSHOT → FINANCIAL LEDGER → AUDIT TRAIL

Stack: FastAPI · PostgreSQL · React · TypeScript · Docker

<img src="./assets/section.svg" width="100%" alt=""/>
Selected builds
<details> <summary><b>🧩 SchemaSense AI — semantic JSON inference platform</b></summary> <br/>

Hybrid JSON intelligence combining deterministic validation with ML-assisted semantic type inference: malformed JSON detection and repair, context-aware TypeScript generation, ML-assisted prediction.

Stack: React · TypeScript · Node.js · Express · FastAPI · scikit-learn Repo: srthck/schemasense-ai

</details> <details> <summary><b>🚑 AmbuFlow — emergency ambulance coordination</b></summary> <br/>

Emergency coordination platform with authentication, role-based workflows, dashboards, and live tracking.

Stack: Node.js · Express · MongoDB · Firebase · Google Maps Repo: srthck/AmbuFlow

</details> <details> <summary><b>👁️ YOLOv8 Acne Analysis — computer vision</b></summary> <br/>

Detection and classification pipeline for acne using YOLOv8 and image-processing techniques.

Stack: Python · YOLOv8 · OpenCV Repo: srthck/yolov8-acne-analysis

</details> <details> <summary><b>🖼️ VisionCaption AI — deep learning</b></summary> <br/>

Computer-vision and deep-learning application that generates natural-language descriptions from images.

Stack: Python · TensorFlow · OpenCV

</details> <img src="./assets/section.svg" width="100%" alt=""/>
Technical arsenal
Layer	Stack
Languages	Python · Java · C++ · TypeScript · JavaScript · SQL · Kotlin
Backend	FastAPI · Node.js · Express · REST APIs
Frontend	React · Next.js · TypeScript · Tailwind CSS
Mobile	Android · Kotlin · Jetpack Compose · React Native · Capacitor
Data	PostgreSQL · MongoDB · MySQL · SQLite · Firebase
AI / ML	scikit-learn · TensorFlow · YOLOv8 · OpenCV · MediaPipe · Hugging Face
Infrastructure	Docker · Git · GitHub Actions · Linux
Engineering	System design · API design · Idempotency · Audit trails · Offline-first · Realtime · Risk analysis
Experience

Full-Stack Web Development Intern — Prodigy InfoTech JWT auth, employee management systems, React/Node.js/MongoDB apps, realtime communication, financial-management workflows. Recognition: Letter of Recommendation. React Node.js JavaScript MongoDB

Full-Stack Development Intern — CodeAlpha One-month internship delivering application assignments across modern web technologies. Recognition: Certificate of Completion + Letter of Recommendation. React Node.js JavaScript APIs

<img src="./assets/section.svg" width="100%" alt=""/>
Engineering principles
	
Data	Model state before UI
Failure	Design beyond the happy path
Trust	Preserve evidence and provenance
Risk	Make uncertainty explicit
Integrity	Protect system state
Audit	Make decisions reconstructable
Idempotency	Make repetition safe
Deploy	Production is part of engineering
How I build
Understand the real problem
Model the system and data
Define boundaries and invariants
Design APIs and core architecture
Build the backend
Integrate AI where it adds real value
Test failure cases
Deploy
Observe
Iterate
<img src="./assets/section.svg" width="100%" alt=""/>
GitHub activity

<sub>Rendered by <a href="./scripts/generate_stats.py"><code>scripts/generate_stats.py</code></a> and committed by <a href="./.github/workflows/refresh-stats.yml">a scheduled GitHub Action</a> — self-hosted, so nothing here depends on a third-party card that can rate-limit or go down.</sub>

<div align="center"> <img src="./stats.svg" width="49%" alt="Contribution activity, last 365 days"/> <img src="./streak.svg" width="49%" alt="Current and longest contribution streak"/> <br/> <img src="./langs.svg" width="49%" alt="Top languages by bytes across public repositories"/> <img src="./year.svg" width="49%" alt="Contributions per day over the last year"/> </div> <img src="./assets/section.svg" width="100%" alt=""/> <div align="center"> <img src="./assets/status.svg" width="320" alt="Status: actively building"/>

<br/><br/>

<a href="https://github.com/srthck">GitHub</a> · <a href="https://www.linkedin.com/in/sarthak-kadam-102134360">LinkedIn</a> · <a href="https://leetcode.com/u/sarthak6001/">LeetCode</a> · <a href="mailto:sarthakkadam.sk07@gmail.com">Email</a>

</div>
