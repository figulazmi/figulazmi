# 👋 Hi there, I'm Figur Ulul Azmi!

**Fullstack .NET Engineer · AI-Augmented Developer**

Building enterprise systems by day, homelab AI infrastructure by night.

> 💡 I ship production .NET systems *and* build the AI tooling that accelerates the work — RAG-first knowledge bases, local LLM setups, and custom Claude Code integrations are part of my daily development workflow.

## 💫 About Me

- **Enterprise backend & fullstack** — 3+ years shipping production .NET 9 systems in a software house, specializing in Clean Architecture, CQRS/MediatR, Blazor WASM, and REST APIs
- **Shipped at scale** — led development of an e-procurement platform for an Oil & Gas company serving hundreds of employees and vendors; features include AD auth, dual-login flows, complex procurement workflows, and Hangfire job scheduling
- **Homelab AI practitioner** — self-hosted Qdrant (vector DB), Ollama (local LLM), n8n (workflow automation), and a .NET RAG Gateway on a Linux VM, all wired together with Docker and Tailscale
- **Developer tooling builder** — created RTK (a custom CLI reducing Claude Code token usage 60–99%) and a RAG Capture Pipeline that turns coding sessions into a queryable knowledge base via Qdrant MCP
- Deploying on: IIS · Linux Nginx · Docker · CentOS

## 🚀 Featured Projects

### 🏗️ Enterprise E-Procurement System *(Oil & Gas)*
> `.NET 9` · `Blazor WASM` · `MudBlazor` · `CQRS/MediatR` · `EF Core` · `SQL Server` · `JWT + Active Directory` · `Hangfire` · `Docker`

Full-cycle procurement platform serving hundreds of internal employees and external vendors. Covers Tender, Pra-Qualifikasi (PQ), and Cancel/Fail workflows with B2B activity routing. Implements dual authentication (Employee via Active Directory, Vendor via numeric ID), single-device login enforcement, and background job scheduling via Hangfire.

---

### 🤖 Homelab AI Stack
> `Qdrant` · `Ollama` · `n8n` · `.NET RAG Gateway` · `Docker Compose` · `Tailscale`

Self-hosted AI infrastructure on a Linux VM, accessible via Tailscale VPN. Qdrant runs hybrid dense+sparse vector search for knowledge retrieval. n8n orchestrates ingestion workflows (chunking → embedding → upsert). Ollama serves local LLMs. A custom .NET API (rag-gateway-mini) exposes the full stack through a single endpoint.

---

### 🛠️ AI Developer Tooling — RTK + RAG Capture Pipeline
> `Python` · `Bash` · `Claude Code Hooks` · `Qdrant MCP`

Two tools built to eliminate AI development friction:
- **RTK** — intercepts and rewrites Claude Code Bash commands, yielding 60–99% token savings on builds, tests, git ops, and Docker
- **RAG Capture Pipeline** — structured knowledge capture from coding sessions; chunks by problem/solution type and pushes to Qdrant, queryable in future sessions via MCP server

## 🌐 Socials

[![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white)](https://linkedin.com/in/figulazmi)
[![Email](https://img.shields.io/badge/Email-D14836?logo=gmail&logoColor=white)](mailto:azmi.codes@gmail.com)
[![GitHub](https://img.shields.io/badge/github-%23121011.svg?logo=github&logoColor=white)](https://github.com/figulazmi)

## 💻 Tech Stack

| Category | Technologies |
|----------|-------------|
| **Backend** | ![C#](https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=csharp&logoColor=white) ![ASP.NET Core](https://img.shields.io/badge/ASP.NET_Core-512BD4?style=for-the-badge&logo=.net&logoColor=white) ![EF Core](https://img.shields.io/badge/EF_Core-512BD4?style=for-the-badge&logo=.net&logoColor=white) ![MediatR](https://img.shields.io/badge/CQRS%2FMediatR-512BD4?style=for-the-badge&logo=.net&logoColor=white) ![Hangfire](https://img.shields.io/badge/Hangfire-1F1F1F?style=for-the-badge&logo=nuget&logoColor=white) ![REST API](https://img.shields.io/badge/REST_API-02569B?style=for-the-badge&logo=Swagger&logoColor=white) |
| **Frontend** | ![Blazor](https://img.shields.io/badge/Blazor-512BD4?style=for-the-badge&logo=blazor&logoColor=white) ![MudBlazor](https://img.shields.io/badge/MudBlazor-1E88E5?style=for-the-badge&logo=blazor&logoColor=white) ![jQuery](https://img.shields.io/badge/jQuery-0769AD?style=for-the-badge&logo=jquery&logoColor=white) ![HTML](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white) ![CSS](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white) |
| **Database** | ![SQL Server](https://img.shields.io/badge/SQL_Server-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white) ![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white) ![Postgres](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white) ![Qdrant](https://img.shields.io/badge/Qdrant-FF4F64?style=for-the-badge&logoColor=white) |
| **AI / Automation** | ![Ollama](https://img.shields.io/badge/Ollama-1A1A1A?style=for-the-badge&logoColor=white) ![n8n](https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white) ![Python](https://img.shields.io/badge/Python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) |
| **DevOps** | ![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white) ![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white) ![IIS](https://img.shields.io/badge/IIS-0078D6?style=for-the-badge&logo=microsoft&logoColor=white) ![CentOS](https://img.shields.io/badge/CentOS-262577?style=for-the-badge&logo=centos&logoColor=white) ![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white) ![Tailscale](https://img.shields.io/badge/Tailscale-242424?style=for-the-badge&logo=tailscale&logoColor=white) |
| **Tools** | ![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white) ![Swagger](https://img.shields.io/badge/Swagger-85EA2D?style=for-the-badge&logo=swagger&logoColor=black) ![Scalar](https://img.shields.io/badge/Scalar-1A1A1A?style=for-the-badge&logoColor=white) ![Figma](https://img.shields.io/badge/Figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white) ![GitHub](https://img.shields.io/badge/GitHub-121011?style=for-the-badge&logo=github&logoColor=white) ![Notion](https://img.shields.io/badge/Notion-000000?style=for-the-badge&logo=notion&logoColor=white) |

## 📊 GitHub Stats

![](https://github-readme-stats.vercel.app/api?username=figulazmi&theme=outrun&hide_border=false&include_all_commits=true&count_private=true)
![](https://github-readme-stats.vercel.app/api/top-langs/?username=figulazmi&theme=outrun&hide_border=false&include_all_commits=true&count_private=true&layout=compact)
![](https://nirzak-streak-stats.vercel.app/?user=figulazmi&theme=outrun&hide_border=false)

[![](https://visitcount.itsvg.in/api?id=figulazmi&icon=0&color=0)](https://visitcount.itsvg.in)
