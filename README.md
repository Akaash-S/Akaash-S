<!-- Profile repo: github.com/Akaash-S/Akaash-S (must be public).
     The banner, divider, footer and section icons are local SVG files in assets/ (commit that folder together with this README).
     To recolour the icons, change stroke="#38BDF8" inside assets/icons/*.svg. -->

<!-- ============================ BANNER ============================ -->
<div align="center">

<img width="100%" src="assets/banner.svg" alt="Akaash S: Backend and Cloud Engineer" />

<a href="https://github.com/Akaash-S">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&duration=3000&pause=900&color=38BDF8&center=true&vCenter=true&width=760&height=40&lines=Event-driven+backends+that+stay+up;Least-privilege+IAM+with+AWS+%2B+LLM+guardrails;Java+%7C+Python+%7C+TypeScript;Redis+Streams%2C+SQS%2C+PostgreSQL%2C+Docker" alt="Typing animation" />
</a>

<br/>

<a href="#about"><img src="https://img.shields.io/badge/About-0F172A?style=for-the-badge&logo=readme&logoColor=38BDF8" alt="About" /></a>
<a href="#projects"><img src="https://img.shields.io/badge/Projects-0F172A?style=for-the-badge&logo=github&logoColor=38BDF8" alt="Projects" /></a>
<a href="#stack"><img src="https://img.shields.io/badge/Stack-0F172A?style=for-the-badge&logo=stackshare&logoColor=38BDF8" alt="Stack" /></a>
<a href="#journey"><img src="https://img.shields.io/badge/Journey-0F172A?style=for-the-badge&logo=timescale&logoColor=38BDF8" alt="Journey" /></a>
<a href="#stats"><img src="https://img.shields.io/badge/Stats-0F172A?style=for-the-badge&logo=chartdotjs&logoColor=38BDF8" alt="Stats" /></a>
<a href="#contact"><img src="https://img.shields.io/badge/Contact-0F172A?style=for-the-badge&logo=gmail&logoColor=38BDF8" alt="Contact" /></a>

<br/><br/>

<img src="https://img.shields.io/badge/B.Tech_IT-Class_of_2027-38BDF8?style=flat-square" alt="B.Tech IT, class of 2027" />
<img src="https://img.shields.io/badge/CGPA-8.52%2F10-8B5CF6?style=flat-square" alt="CGPA 8.52/10" />
<img src="https://img.shields.io/badge/Based_in-Chengalpattu%2C_India-22C55E?style=flat-square&logo=googlemaps&logoColor=white" alt="Chengalpattu, India" />
<img src="https://img.shields.io/badge/Open_to-2027_internships-F59E0B?style=flat-square" alt="Open to 2027 internships" />

</div>

<img width="100%" src="assets/divider.svg" alt="" />

<!-- ============================ ABOUT ============================ -->
<a id="about"></a>

<h2><img src="assets/icons/user.svg" width="30" height="30" align="absmiddle" alt="" />&nbsp; About</h2>

I build **backend systems that handle failure well**: event-driven pipelines, retries and dead-letter queues, race-condition-safe writes, and cloud tooling with security guardrails built in.

I'm a B.Tech Information Technology student (graduating 2027) and my primary language is **Java**, with most of my recent work in **Python** and **TypeScript**. I like projects where I own the full path from design to tests to deployment, and where I can explain every number I put on the page.

<div align="center">

| <img src="assets/icons/graduation-cap.svg" width="18" align="absmiddle" alt="" /> Education | <img src="assets/icons/braces.svg" width="18" align="absmiddle" alt="" /> Core languages | <img src="assets/icons/target.svg" width="18" align="absmiddle" alt="" /> Problem solving | <img src="assets/icons/trophy.svg" width="18" align="absmiddle" alt="" /> Recognition |
|:---:|:---:|:---:|:---:|
| B.Tech IT, MSEC<br/>Class of 2027 | Java · Python<br/>SQL · TypeScript · Bash | 140+ LeetCode problems<br/>(Java, SQL) | Winner, Hackintym'25<br/>(college level) |

</div>

<!-- ============================ PROJECTS ============================ -->
<a id="projects"></a>

<h2><img src="assets/icons/rocket.svg" width="30" height="30" align="absmiddle" alt="" />&nbsp; Featured Projects</h2>

<h3><img src="assets/icons/shield-check.svg" width="26" height="26" align="absmiddle" alt="" />&nbsp; Cedar-Sentinel: IAM Least-Privilege Policy Tightener</h3>

*Solo project · Sep 2026 · AWS, Python, Terraform*

An event-driven AWS pipeline that reads what a role actually did in CloudTrail and proposes a tighter IAM policy. An LLM drafts the policy, and **five independent guard layers** check it before a human approves anything. The Lambda role itself has **zero IAM write permissions**.

<div align="center">

[![Cedar-Sentinel](https://github-readme-stats.vercel.app/api/pin/?username=Akaash-S&repo=cedar-sentinel&theme=tokyonight&hide_border=true&border_radius=12)](https://github.com/Akaash-S/cedar-sentinel)

[![Live demo](https://img.shields.io/badge/Live_demo-Replay_of_10_sanitized_runs-FF9900?style=for-the-badge&logo=awsamplify&logoColor=white)](https://main.d3i4xcsmv7sca9.amplifyapp.com)

</div>

| Result | Detail |
|---|---|
| <img src="assets/icons/trending-down.svg" width="18" align="absmiddle" alt="" /> **4 → 1** statements | A test role with service-wide wildcards (`s3:*`, `dynamodb:*`, `ec2:*`, `logs:*`) became 1 statement of 6 observed S3 actions |
| <img src="assets/icons/badge-check.svg" width="18" align="absmiddle" alt="" /> **No new access** | Confirmed with IAM Access Analyzer `CheckNoNewAccess` |
| <img src="assets/icons/layers.svg" width="18" align="absmiddle" alt="" /> **5-layer guard** | AST sanitizer, coverage/lockout check, CloudTrail-to-IAM action map, Cedar (Verified Permissions) validation, Access Analyzer |
| <img src="assets/icons/flask.svg" width="18" align="absmiddle" alt="" /> **38 tests** | Unit and integration, including live Access Analyzer checks |
| <img src="assets/icons/dollar.svg" width="18" align="absmiddle" alt="" /> **~$0.0001** | Approximate Bedrock cost per analysis |

<details>
<summary><img src="assets/icons/network.svg" width="16" align="absmiddle" alt="" /> <b>Architecture</b></summary>

```mermaid
flowchart LR
    CT[(CloudTrail activity)] --> EB[EventBridge]
    EB --> SQS[SQS queue]
    SQS --> L[Lambda]
    L -->|observed actions| CW[CloudWatch Logs Insights]
    L -->|draft policy| BR[Amazon Bedrock]
    BR --> G{5-layer guard}
    G -->|AST sanitizer + coverage check + action map| V[Cedar / Verified Permissions]
    V --> AA[IAM Access Analyzer]
    AA --> DB[(DynamoDB: proposal + rollback snapshot)]
    DB --> H([Human approval])
```

</details>

<details>
<summary><img src="assets/icons/clipboard-check.svg" width="16" align="absmiddle" alt="" /> <b>What I owned</b></summary>

- Designed the whole pipeline and deployed it with **AWS SAM**.
- Designed the guard layers so a bad LLM draft can't lock a role out of what it actually uses.
- Wrote the tests, including live Access Analyzer checks.
- Kept the blast radius small: the Lambda role cannot write IAM, and applying a change needs a human `y/N`, with a DynamoDB rollback snapshot.

<img src="assets/icons/arrow-right.svg" width="14" align="absmiddle" alt="" /> **Next:** run it against a larger set of real CloudTrail history (tested on a dozen real events so far).

</details>

<p align="center"><img src="https://skillicons.dev/icons?i=py,aws,terraform,dynamodb,lambda&theme=dark" alt="Cedar-Sentinel stack" /></p>

---

<h3><img src="assets/icons/radio-tower.svg" width="26" height="26" align="absmiddle" alt="" />&nbsp; NexOps: Incident Intelligence Platform</h3>

*Solo project · Apr 2026 – present · Python, FastAPI, Redis Streams, PostgreSQL*

A distributed backend that ingests **GitHub and PagerDuty webhooks**, correlates related incidents, and scores the **blast radius** of a deployment across a dependency graph. It has a REST API, a WebSocket feed and a Next.js dashboard.

<div align="center">

<a href="https://github.com/Akaash-S/NexOpsBackend"><img src="https://github-readme-stats.vercel.app/api/pin/?username=Akaash-S&repo=NexOpsBackend&theme=tokyonight&hide_border=true&border_radius=12" alt="NexOpsBackend" /></a>
<a href="https://github.com/Akaash-S/NexOpsFrontend"><img src="https://github-readme-stats.vercel.app/api/pin/?username=Akaash-S&repo=NexOpsFrontend&theme=tokyonight&hide_border=true&border_radius=12" alt="NexOpsFrontend" /></a>

</div>

| Result | Detail |
|---|---|
| <img src="assets/icons/database.svg" width="18" align="absmiddle" alt="" /> **13 tables** | PostgreSQL schema managed with Alembic |
| <img src="assets/icons/repeat.svg" width="18" align="absmiddle" alt="" /> **Retries + dead-letter** | Redis Streams worker with consumer groups, retry counters and graceful shutdown |
| <img src="assets/icons/lock.svg" width="18" align="absmiddle" alt="" /> **10 replays → 1 incident** | PostgreSQL advisory locks stop duplicate incidents under concurrent events |
| <img src="assets/icons/heart-pulse.svg" width="18" align="absmiddle" alt="" /> **Deep health check** | Protected endpoint checks DB, Redis, worker heartbeat and external reachability, and returns HTTP 503 on failure |
| <img src="assets/icons/flask.svg" width="18" align="absmiddle" alt="" /> **60+ pytest tests** | Race-condition, replay and scoring tests |

<details>
<summary><img src="assets/icons/network.svg" width="16" align="absmiddle" alt="" /> <b>Architecture</b></summary>

```mermaid
flowchart LR
    GH[GitHub webhooks] --> API[FastAPI]
    PD[PagerDuty webhooks] --> API
    API -->|publish| RS[(Redis Streams)]
    RS --> W[Worker: consumer group]
    W -->|retry, then dead-letter| DLQ[(Dead-letter stream)]
    W -->|advisory lock per workspace + repo| PG[(PostgreSQL)]
    PG --> C[Correlation + blast-radius scoring]
    C --> WS[WebSocket feed]
    WS --> UI[Next.js dashboard]
    W -.->|heartbeat| H[/Deep health endpoint/]
```

</details>

<details>
<summary><img src="assets/icons/clipboard-check.svg" width="16" align="absmiddle" alt="" /> <b>What I owned</b></summary>

- Designed the service end to end: API, schema, worker, scoring and dashboard.
- Solved the duplicate-incident race with advisory locks, and proved it with concurrent replay tests.
- Added bounded, feedback-driven recalibration of the scoring weights.
- Added Sentry error tracking, a post-deploy smoke script and Docker/Render deployment configs.

<img src="assets/icons/arrow-right.svg" width="14" align="absmiddle" alt="" /> **Next:** load-test on production-like infrastructure (my load tests so far ran locally).

</details>

<p align="center"><img src="https://skillicons.dev/icons?i=py,fastapi,postgres,redis,docker,nextjs,firebase,sentry&theme=dark" alt="NexOps stack" /></p>

---

<h3><img src="assets/icons/inbox.svg" width="26" height="26" align="absmiddle" alt="" />&nbsp; Signal: AI Communication Triage Platform</h3>

*Team project · Jul 2026 · Java 21, Spring Boot 3, AWS SQS, Angular*

A microservice platform that pulls in Gmail and Google Calendar, scores urgency with an LLM, and triages what needs attention first. I was the **primary contributor (81 of 87 commits)**.

<div align="center">

<a href="https://github.com/DhivyaSivakumar123/signal_backend"><img src="https://github-readme-stats.vercel.app/api/pin/?username=DhivyaSivakumar123&repo=signal_backend&theme=tokyonight&hide_border=true&border_radius=12" alt="signal_backend" /></a>
<a href="https://github.com/DhivyaSivakumar123/signal"><img src="https://github-readme-stats.vercel.app/api/pin/?username=DhivyaSivakumar123&repo=signal&theme=tokyonight&hide_border=true&border_radius=12" alt="signal" /></a>

</div>

| Result | Detail |
|---|---|
| <img src="assets/icons/blocks.svg" width="18" align="absmiddle" alt="" /> **Gateway + 5 services** | 7 Maven modules, 27 endpoints |
| <img src="assets/icons/container.svg" width="18" align="absmiddle" alt="" /> **8-container setup** | Docker Compose with AWS SQS (LocalStack), multi-schema PostgreSQL and Redis |
| <img src="assets/icons/mail.svg" width="18" align="absmiddle" alt="" /> **Live ingestion** | Real Gmail and Google Calendar polling with OAuth2 refresh-token recovery |
| <img src="assets/icons/refresh.svg" width="18" align="absmiddle" alt="" /> **LLM migration** | Moved urgency scoring from OpenAI to Groq Llama 3.1 with strict JSON output |
| <img src="assets/icons/flask.svg" width="18" align="absmiddle" alt="" /> **11 unit tests** | Scorer parsing and token refresh |

<details>
<summary><img src="assets/icons/network.svg" width="16" align="absmiddle" alt="" /> <b>Architecture</b></summary>

```mermaid
flowchart LR
    UI[Angular 17 + NgRx] --> GW[Spring Cloud Gateway: JWT]
    GW --> AU[Auth]
    GW --> IN[Integration]
    GW --> TR[Triage]
    GW --> AN[Analytics]
    IN -->|poll| GM[Gmail + Google Calendar]
    IN -->|SQS| SC[Scoring: Groq Llama 3.1]
    SC -->|SQS| TR
    TR --> PG[(PostgreSQL)]
    AN --> PG
    IN -.-> RD[(Redis)]
```

</details>

<details>
<summary><img src="assets/icons/clipboard-check.svg" width="16" align="absmiddle" alt="" /> <b>What I owned</b></summary>

- Replaced mock data with live Gmail and Google Calendar ingestion.
- Handled OAuth2 refresh-token recovery: a revoked token marks the integration as expired instead of failing silently.
- Added an on-demand sync endpoint that runs the pollers in parallel.
- Migrated scoring to Groq, with explicit exceptions on API failure instead of silent fallbacks.
- Owned the Docker Compose orchestration and the Angular dashboard with Chart.js analytics.

<img src="assets/icons/arrow-right.svg" width="14" align="absmiddle" alt="" /> **Next:** encrypt stored OAuth refresh tokens at rest, and replace the Slack and Outlook stubs with real integrations.

</details>

<p align="center"><img src="https://skillicons.dev/icons?i=java,spring,postgres,redis,docker,angular,aws&theme=dark" alt="Signal stack" /></p>

---

<h3><img src="assets/icons/route.svg" width="26" height="26" align="absmiddle" alt="" />&nbsp; SkillBridge: Career Learning Platform</h3>

*Solo project · 2025 – 2026 · React, TypeScript, Flask, Firestore, GCP*

A career-development platform that tracks skills, analyzes skill gaps against job roles, and generates personalized learning roadmaps with AI.

<div align="center">

<a href="https://github.com/Akaash-S/skillbridgeBackend"><img src="https://github-readme-stats.vercel.app/api/pin/?username=Akaash-S&repo=skillbridgeBackend&theme=tokyonight&hide_border=true&border_radius=12" alt="skillbridgeBackend" /></a>
<a href="https://github.com/Akaash-S/skillbridge"><img src="https://github-readme-stats.vercel.app/api/pin/?username=Akaash-S&repo=skillbridge&theme=tokyonight&hide_border=true&border_radius=12" alt="skillbridge" /></a>

</div>

| Scope | Detail |
|---|---|
| <img src="assets/icons/globe.svg" width="18" align="absmiddle" alt="" /> **133 endpoints** | 19 Flask blueprints and 21 backend services |
| <img src="assets/icons/database.svg" width="18" align="absmiddle" alt="" /> **28 Firestore collections** | Skills, roadmaps, progress, assessments and more |
| <img src="assets/icons/sparkles.svg" width="18" align="absmiddle" alt="" /> **AI roadmaps** | Gemini and Groq with validation against a master skill catalog |
| <img src="assets/icons/server.svg" width="18" align="absmiddle" alt="" /> **Deployment** | Docker, Gunicorn and Nginx on a GCP VM, with scheduled Firestore backups |

<details>
<summary><img src="assets/icons/clipboard-check.svg" width="16" align="absmiddle" alt="" /> <b>What I owned</b></summary>

- Designed the skill-gap and readiness-scoring logic and the roadmap generator.
- Moved authentication from localStorage tokens to httpOnly cookies.
- Wrote the VM setup and deployment scripts and the scheduled backup job.

<img src="assets/icons/arrow-right.svg" width="14" align="absmiddle" alt="" /> **Next:** split the 2 MB single JavaScript bundle with code-splitting (Lighthouse flagged it).

</details>

<p align="center"><img src="https://skillicons.dev/icons?i=react,ts,flask,firebase,gcp,docker,nginx&theme=dark" alt="SkillBridge stack" /></p>

<details>
<summary><img src="assets/icons/folder-open.svg" width="16" align="absmiddle" alt="" /> <b>More projects</b></summary>

<br/>

- <img src="assets/icons/graduation-cap.svg" width="16" align="absmiddle" alt="" /> **[AI Classroom Assistant](https://github.com/Akaash-S/classroomAssistant)** *(Individual)*: lecture audio to transcript, then Gemini summaries, exam notes and teacher-approved assignment tasks. Next.js and Flask with Firebase.
- <img src="assets/icons/mic.svg" width="16" align="absmiddle" alt="" /> **Dynamic Meeting Assistant** *(Individual)*: speech processing, summaries and task extraction for meetings.
- <img src="assets/icons/stethoscope.svg" width="16" align="absmiddle" alt="" /> **MediMind AI** *(Contributed)*: AI-assisted healthcare-oriented platform.

</details>

<!-- ============================ STACK ============================ -->
<a id="stack"></a>

<h2><img src="assets/icons/layers.svg" width="30" height="30" align="absmiddle" alt="" />&nbsp; Tech Stack</h2>

<div align="center">

| | |
|:---|:---|
| **Languages** | <img src="https://skillicons.dev/icons?i=java,py,ts,bash&theme=dark" alt="Languages" /> |
| **Backend** | <img src="https://skillicons.dev/icons?i=spring,fastapi,flask,firebase&theme=dark" alt="Backend" /> |
| **Data & messaging** | <img src="https://skillicons.dev/icons?i=postgres,redis,dynamodb&theme=dark" alt="Data and messaging" /> |
| **Cloud & DevOps** | <img src="https://skillicons.dev/icons?i=aws,gcp,docker,terraform,nginx,githubactions,linux,git&theme=dark" alt="Cloud and DevOps" /> |
| **Frontend** | <img src="https://skillicons.dev/icons?i=react,nextjs,angular,tailwind&theme=dark" alt="Frontend" /> |
| **Tools** | <img src="https://skillicons.dev/icons?i=vscode,postman,sentry&theme=dark" alt="Tools" /> |

</div>

<!-- ============================ JOURNEY ============================ -->
<a id="journey"></a>

<h2><img src="assets/icons/route.svg" width="30" height="30" align="absmiddle" alt="" />&nbsp; Journey</h2>

| When | What |
|---|---|
| **Sep 2023** | Started B.Tech Information Technology at Meenakshi Sundararajan Engineering College |
| **2025** | Won **Hackintym'25** (college level) with an AI-assisted classroom assistant; started SkillBridge |
| **Apr 2026 – now** | Building and owning **NexOps** |
| **Jul 2026** | Led development of **Signal**, a Java 21 / Spring Boot microservice platform |
| **Sep 2026** | Designed and shipped **Cedar-Sentinel** on AWS |
| **Now** | Working through the **AWS Developer** learning path on Skill Builder, and practicing DSA |

<div align="center">

<h3><img src="assets/icons/compass.svg" width="24" height="24" align="absmiddle" alt="" />&nbsp; Currently</h3>

<img src="assets/icons/cloud.svg" width="16" align="absmiddle" alt="" /> Deepening AWS &nbsp;·&nbsp;
<img src="assets/icons/flask.svg" width="16" align="absmiddle" alt="" /> Making NexOps tests and CI more robust &nbsp;·&nbsp;
<img src="assets/icons/target.svg" width="16" align="absmiddle" alt="" /> Practicing data structures and algorithms

</div>

<!-- ============================ STATS ============================ -->
<a id="stats"></a>

<h2><img src="assets/icons/activity.svg" width="30" height="30" align="absmiddle" alt="" />&nbsp; Stats</h2>

<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github-readme-stats.vercel.app/api?username=Akaash-S&show_icons=true&theme=tokyonight&hide_border=true&include_all_commits=true&count_private=true&border_radius=12" />
  <img width="49%" alt="GitHub stats" src="https://github-readme-stats.vercel.app/api?username=Akaash-S&show_icons=true&theme=default&hide_border=true&include_all_commits=true&count_private=true&border_radius=12" />
</picture>
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github-readme-stats.vercel.app/api/top-langs/?username=Akaash-S&layout=compact&theme=tokyonight&hide_border=true&border_radius=12" />
  <img width="37%" alt="Top languages" src="https://github-readme-stats.vercel.app/api/top-langs/?username=Akaash-S&layout=compact&theme=default&hide_border=true&border_radius=12" />
</picture>

<br/>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://streak-stats.demolab.com?user=Akaash-S&theme=tokyonight&hide_border=true&border_radius=12" />
  <img alt="Streak" src="https://streak-stats.demolab.com?user=Akaash-S&theme=default&hide_border=true&border_radius=12" />
</picture>

<br/>

<a href="https://leetcode.com/u/Akaash_S">
  <img height="170" alt="LeetCode stats" src="https://leetcard.jacoblin.cool/Akaash_S?theme=dark&font=Fira%20Code&ext=heatmap" />
</a>

<br/><br/>

[![Activity graph](https://github-readme-activity-graph.vercel.app/graph?username=Akaash-S&theme=tokyo-night&hide_border=true&radius=16)](https://github.com/Akaash-S)

<img src="https://raw.githubusercontent.com/Akaash-S/Akaash-S/output/github-contribution-grid-snake-dark.svg" alt="Contribution snake" />

</div>

<!-- ============================ CONTACT ============================ -->
<a id="contact"></a>

<h2><img src="assets/icons/chat.svg" width="30" height="30" align="absmiddle" alt="" />&nbsp; Let's connect</h2>

<div align="center">

<a href="https://linkedin.com/in/akaashs"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
<a href="mailto:akaashofficial21@gmail.com"><img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Gmail" /></a>
<a href="https://leetcode.com/u/Akaash_S"><img src="https://img.shields.io/badge/LeetCode-FFA116?style=for-the-badge&logo=leetcode&logoColor=black" alt="LeetCode" /></a>
<!-- Add a resume badge here once the PDF has a public link:
<a href="RESUME_URL"><img src="https://img.shields.io/badge/Resume-PDF-38BDF8?style=for-the-badge&logo=adobeacrobatreader&logoColor=white" alt="Resume" /></a> -->

<br/>

*"Building scalable systems engineered for real-world impact."*

<img width="100%" src="assets/footer.svg" alt="" />

</div>