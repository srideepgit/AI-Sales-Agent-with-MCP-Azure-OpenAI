---
page_type: sample
languages:
  - python
products:
  - azure-openai
  - azure-container-apps
  - azure
  - langchain
  - pgvector
urlFragment: langchain-agent-python
name: LangChain Sales Agent with MCP and Azure OpenAI (Python)
description: A multi-step LangChain v1 sales-conversation agent that uses the Azure OpenAI Responses API, an MCP server with Postgres + pgvector for catalog and CRM tools, and ships with one command via azd up.
---

<div align="center">

# 🤖 AI-Sales-Agent-with-MCP-Azure-OpenAI

### Multi-Step AI Sales Agent with Azure OpenAI Responses API + MCP

<p>
  <img src="https://img.shields.io/badge/Python-3.11%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/LangChain-v1-1C3C3C?style=for-the-badge&logo=chainlink&logoColor=white" />
  <img src="https://img.shields.io/badge/Azure%20OpenAI-Responses%20API-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white" />
</p>

<p>
  <img src="https://img.shields.io/badge/MCP-FastMCP-6B4FBB?style=for-the-badge" />
  <img src="https://img.shields.io/badge/PostgreSQL-pgvector-336791?style=for-the-badge&logo=postgresql&logoColor=white" />
  <img src="https://img.shields.io/badge/Azure-Container%20Apps-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white" />
</p>

<p>
  <img src="https://img.shields.io/badge/Authentication-Entra%20ID-5E5E5E?style=for-the-badge&logo=microsoft&logoColor=white" />
  <img src="https://img.shields.io/github/license/Azure-Samples/langchain-agent-python?style=for-the-badge" />
</p>

<br>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=20&pause=1000&color=0078D4&center=true&vCenter=true&width=800&lines=Multi-Step+AI+Sales+Agent;LangChain+v1+%2B+Azure+OpenAI;Model+Context+Protocol+%2B+PostgreSQL;RAG+%2B+pgvector+Semantic+Search;Enterprise+Authentication+with+Entra+ID" />

<br><br>

**Build → Ground → Qualify → Educate → Handle Objections → Book → Handoff**

<br>

<a href="#-quick-start">
<img src="https://img.shields.io/badge/🚀%20Quick%20Start-0078D4?style=for-the-badge" />
</a>
&nbsp;
<a href="#-architecture">
<img src="https://img.shields.io/badge/🏗️%20Architecture-24292F?style=for-the-badge" />
</a>
&nbsp;
<a href="#-how-it-works">
<img src="https://img.shields.io/badge/🧠%20How%20It%20Works-6B4FBB?style=for-the-badge" />
</a>

</div>

---

# 📑 Table of Contents

* [🎯 Overview](#-overview)
* [🎥 Application Preview](#-application-preview)
* [✨ Key Features](#-key-features)
* [🧠 What You'll Learn](#-what-youll-learn)
* [🏗️ Architecture](#️-architecture)
* [🛒 Six-Step Sales Funnel](#-six-step-sales-funnel)
* [⚙️ How It Works](#️-how-it-works)
* [🔌 MCP Server](#-mcp-server)
* [🔎 Retrieval with PostgreSQL + pgvector](#-retrieval-with-postgresql--pgvector)
* [🔐 Authentication & Security](#-authentication--security)
* [📁 Repository Structure](#-repository-structure)
* [🚀 Quick Start](#-quick-start)
* [💻 Local Development](#-local-development)
* [🛠️ Customise the Agent](#️-customise-the-agent)
* [📊 Monitoring](#-monitoring)
* [🔮 Future Work](#-future-work)
* [🧹 Clean Up](#-clean-up)
* [📚 Resources](#-resources)
* [🤝 Contributing](#-contributing)
* [📄 License](#-license)

---

# 🎯 Overview

This project demonstrates how to build a **multi-step AI sales-conversation agent** using **LangChain v1**, the **Azure OpenAI Responses API**, **Model Context Protocol (MCP)**, and **PostgreSQL + pgvector**.

The agent guides customers through a structured **six-step sales funnel**, while grounding its responses in real product, pricing, case-study, and knowledge-base data.

The application uses an MCP server to expose database and CRM-style capabilities to the agent, allowing the AI to retrieve relevant information without tightly coupling the agent to the underlying database implementation.

### Core Technology Stack

| Layer               | Technology                           |
| ------------------- | ------------------------------------ |
| Agent orchestration | LangChain v1                         |
| LLM                 | Azure OpenAI                         |
| API                 | Azure OpenAI Responses API           |
| Agent middleware    | LangChain Middleware                 |
| Tool protocol       | Model Context Protocol               |
| MCP framework       | FastMCP                              |
| Database            | PostgreSQL                           |
| Vector search       | pgvector                             |
| Vector index        | HNSW                                 |
| Embeddings          | `text-embedding-3-small`             |
| Authentication      | Microsoft Entra ID                   |
| Identity            | Managed Identity                     |
| Deployment          | Azure Container Apps                 |
| Infrastructure      | Bicep + Azure Developer CLI          |
| Observability       | Application Insights + Log Analytics |

---

# 🎥 Application Preview

The application includes a web-based sales chat interface together with a debugging / observability panel.

<p align="center">
  <img src="images/app-image.png" width="95%" alt="LangChain Sales Agent application interface" />
</p>

<p align="center">
  <em>AI-powered sales conversation interface</em>
</p>

<br>

<p align="center">
  <img src="images/debug-image.png" width="95%" alt="LangChain Sales Agent debug panel" />
</p>

<p align="center">
  <em>Agent execution and debugging panel</em>
</p>

---

# ✨ Key Features

<table>
<tr>
<td width="50%">

### 🤖 Multi-Step AI Agent

* Six-stage sales funnel
* Stateful conversations
* Lead qualification
* Customer education
* Objection handling
* Meeting workflow
* AE escalation

</td>

<td width="50%">

### 🔌 MCP Integration

* Product search
* Pricing lookup
* Plan comparison
* Case-study retrieval
* Knowledge-base search
* Analytics tools

</td>
</tr>

<tr>
<td>

### 🔎 RAG + Vector Search

* PostgreSQL
* pgvector
* HNSW indexes
* Semantic retrieval
* Product embeddings
* Sales knowledge embeddings

</td>

<td>

### 🔐 Enterprise Security

* Entra ID
* Managed Identity
* Azure RBAC
* Keyless authentication
* Private MCP communication
* Read-only database access

</td>
</tr>

<tr>
<td>

### ☁️ Azure-Native

* Azure OpenAI
* Azure Container Apps
* PostgreSQL Flexible Server
* Application Insights
* Log Analytics
* Bicep infrastructure

</td>

<td>

### ⚡ Developer Experience

* One-command deployment
* `azd up`
* Docker support
* GitHub Codespaces
* Local development
* Automated database seeding

</td>
</tr>
</table>

---

# 🧠 What You'll Learn

This sample demonstrates several important patterns for building modern agentic AI systems.

### 1. LangChain Handoff Pattern

Build a multi-stage workflow where the agent transitions between specialized sales stages.

### 2. Middleware-Based Control

Use middleware to:

* Refine user queries
* Manage conversation context
* Control the current sales step
* Filter available tools
* Validate response groundedness
* Summarize long conversations

### 3. MCP-Based Tool Architecture

Expose database and CRM capabilities through an independent MCP server.

### 4. Retrieval-Augmented Generation

Use PostgreSQL + pgvector to ground responses in:

* Product catalogue data
* Pricing plans
* Customer case studies
* Knowledge-base articles

### 5. Keyless Azure Authentication

Use Managed Identity and Microsoft Entra ID instead of storing API keys or database credentials.

---

# 🏗️ Architecture

The core LangChain agent and PostgreSQL MCP server are deployed independently as two Azure Container Apps.

<p align="center">
  <img src="images/architecture.png" width="100%" alt="Zava Sales Agent architecture" />
</p>

### Architecture Principles

The architecture follows a few important design principles:

**Separation of concerns**

The agent and MCP server are independently deployable.

**Controlled tool access**

The agent only receives tools permitted for the current sales stage.

**Grounded responses**

Sales answers can be validated against retrieved documentation.

**Private backend**

The MCP server is not exposed directly to the public internet.

**Keyless authentication**

Azure resources communicate through Managed Identity and RBAC.

---

# 🛒 Six-Step Sales Funnel

The sales workflow consists of six stages.

<p align="center">
  <img src="images/sales-funnel.svg" width="100%" alt="Zava Sales Agent six-step sales funnel" />
</p>

### Funnel Stages

| Stage             | Purpose                                    |
| ----------------- | ------------------------------------------ |
| **Greet**         | Start the conversation                     |
| **Qualify**       | Understand customer needs                  |
| **Educate**       | Explain relevant products and capabilities |
| **Objection**     | Handle concerns and comparisons            |
| **Book**          | Propose meeting times                      |
| **Handoff to AE** | Escalate to a human account executive      |

Each step contains:

* A dedicated system prompt
* A filtered tool subset
* State transitions
* Business logic

The state machine lives in:

```text
agent/app/middleware/steps.py
```

The individual prompts are maintained under:

```text
agent/app/prompts/
```

---

# ⚙️ How It Works

## 1. The Agent — Middleware Chain

`agent/app/agent.py` builds the agent during application startup.

The MCP connection, credentials, and middleware closures are reused across requests.

```python
main = ChatOpenAI(
    model="gpt-5.4-mini",
    use_responses_api=True,
)

nano = ChatOpenAI(
    model="gpt-5-nano",
    use_responses_api=True,
    tags=["nano-utility"],
)

refine_query = make_refine_query(nano)
validate_response = make_validate_response(nano)
summariser = SummarizationMiddleware(
    model=nano,
    max_tokens_before_summary=4000,
)

agent = create_agent(
    model=main,
    tools=LOCAL_TOOLS + mcp_tools,
    state_schema=SalesState,
    middleware=[
        refine_query,
        apply_step_config,
        validate_response,
        summariser,
    ],
    checkpointer=InMemorySaver(),
)
```

---

## 2. Two-Tier Model Architecture

The application uses different models for different responsibilities.

| Model                    | Responsibility             |
| ------------------------ | -------------------------- |
| `gpt-5.4-mini`           | Main user-facing agent     |
| `gpt-5-nano`             | Query refinement           |
| `gpt-5-nano`             | Groundedness validation    |
| `gpt-5-nano`             | Conversation summarization |
| `text-embedding-3-small` | Vector embeddings          |

This keeps lightweight middleware operations separate from the primary user-facing reasoning model.

---

## 3. Step-Aware Tool Filtering

`apply_step_config` reads:

```python
state["current_step"]
```

It then:

1. Determines the current sales stage
2. Loads the stage-specific system prompt
3. Filters the available tools
4. Sends only the permitted tools to the model

This prevents the model from accessing tools that are irrelevant to the current stage.

---

## 4. Groundedness Validation

The `validate_response` middleware operates during the:

* `educate`
* `objection`

stages.

It checks whether answers containing sales claims are grounded in retrieved documentation.

If the answer cannot be sufficiently grounded, the system can redirect the customer toward human AE escalation rather than silently generating unsupported pricing or case-study claims.

---

# 🔌 MCP Server

The MCP server is implemented with **FastMCP**.

It exposes nine read-only tools over the `streamable_http` transport.

| Tool                       | Step                | Purpose                        |
| -------------------------- | ------------------- | ------------------------------ |
| `get_current_utc_date`     | Any                 | Resolve relative dates         |
| `get_table_schemas`        | Analytics           | Retrieve schema definitions    |
| `execute_sales_query`      | Analytics           | Read-only ad-hoc SQL           |
| `semantic_search_products` | Educate             | Search product catalogue       |
| `get_product_details`      | Educate             | Retrieve product details       |
| `search_case_studies`      | Educate / Objection | Find relevant customer stories |
| `search_kb_articles`       | Educate / Objection | Search knowledge articles      |
| `get_pricing`              | Educate / Objection | Retrieve pricing               |
| `compare_plans`            | Objection           | Compare plans                  |

The MCP server provides a clean abstraction between the AI agent and the underlying data services.

---

# 🔎 Retrieval with PostgreSQL + pgvector

The application uses PostgreSQL as both the relational data store and vector retrieval layer.

The database contains:

* Product catalogue
* Pricing plans
* Case studies
* Knowledge-base articles
* Sales data

Embeddings are generated using:

```text
text-embedding-3-small
```

Vector search is performed using:

```text
pgvector
+
HNSW indexes
```

### Retrieval Pipeline

```text
Customer Question
        │
        ▼
Embedding Generation
        │
        ▼
Vector Search
        │
        ▼
Relevant Products / Documents
        │
        ▼
Azure OpenAI
        │
        ▼
Grounded Sales Response
```

---

## ⚡ Embedding Cache

Embedding lookups use an in-process **LRU cache**.

The cache key contains:

```text
(deployment_name, query_text)
```

This means repeated queries can reuse existing embeddings without unnecessarily repeating the embedding request.

Including the deployment name also ensures that switching embedding models naturally invalidates the previous cache namespace.

---

# 🔐 Authentication & Security

The application uses **Microsoft Entra ID and Managed Identity** for Azure resource authentication.

### Agent → Azure OpenAI

The agent's user-assigned identity is granted:

```text
Cognitive Services User
```

on the Azure OpenAI resource.

### MCP → PostgreSQL

The MCP server authenticates to Azure Database for PostgreSQL using the configured identity.

### MCP → Azure OpenAI

The MCP server also uses Managed Identity for embedding requests.

---

## Security Model

```text
                    PUBLIC
                      │
                      ▼
             ┌────────────────┐
             │  Agent App     │
             │ Container App  │
             └───────┬────────┘
                     │
                Private MCP
                     │
                     ▼
             ┌────────────────┐
             │  MCP Server    │
             │ Container App  │
             └───────┬────────┘
                     │
              Managed Identity
                     │
            ┌────────┴────────┐
            ▼                 ▼
       PostgreSQL        Azure OpenAI
```

### Security Characteristics

* No API keys committed to the repository
* No client secrets
* No database passwords stored in application code
* MCP server is internally accessible
* Azure RBAC controls resource access
* Analytics queries use read-only access
* Managed Identity handles Azure authentication

---

# ☁️ Infrastructure

Infrastructure is provisioned using:

```text
Bicep
+
Azure Developer CLI
```

The main infrastructure definition is:

```text
infra/main.bicep
```

It provisions:

* Azure OpenAI
* Model deployments
* PostgreSQL Flexible Server
* pgvector
* Container Apps environment
* Agent Container App
* MCP Container App
* Log Analytics
* Application Insights

The deployment configuration is defined through:

```text
azure.yaml
```

---

# 📁 Repository Structure

```text
.
├── agent/
│   ├── app/
│   │   ├── agent.py
│   │   ├── main.py
│   │   ├── streaming.py
│   │   ├── state.py
│   │   │
│   │   ├── middleware/
│   │   │   ├── refine.py
│   │   │   ├── steps.py
│   │   │   └── validate.py
│   │   │
│   │   ├── tools/
│   │   │   └── workflow.py
│   │   │
│   │   └── prompts/
│   │       ├── greet.txt
│   │       ├── qualify.txt
│   │       ├── educate.txt
│   │       ├── objection.txt
│   │       ├── book.txt
│   │       └── handoff_to_ae.txt
│   │
│   └── static/
│
├── mcp/
│   └── app.py
│
├── data/
│   ├── generate_database.py
│   ├── generate_sales_kb.py
│   └── regenerate_embeddings.py
│
├── infra/
│   ├── main.bicep
│   └── main.parameters.json
│
├── azure.yaml
├── docker-compose.yml
├── .env.example
├── LICENSE
├── SUPPORT.md
└── README.md
```

---

# 🚀 Quick Start

## Prerequisites

You need:

* An Azure subscription
* Azure Developer CLI (`azd`)
* Azure CLI
* Python 3.11+
* Docker for full local development

The fastest setup is through **GitHub Codespaces**, where the required developer tools are preinstalled.

---

## ☁️ Deploy to Azure

Authenticate with Azure:

```bash
az login
azd auth login
```

Deploy the complete application:

```bash
azd up
```

The deployment provisions:

```text
Azure OpenAI
       │
       ├── gpt-5.4-mini
       ├── gpt-5-nano
       └── text-embedding-3-small
                    │
                    ▼
       PostgreSQL + pgvector
                    │
                    ▼
          Azure Container Apps
              ┌─────┴─────┐
              ▼           ▼
            Agent        MCP
              │           │
              └─────┬─────┘
                    ▼
          Application Insights
```

---

## ⏱️ Deployment Time

Estimated end-to-end deployment time:

**~10–15 minutes**

PostgreSQL Flexible Server creation is generally the slowest individual step.

---

## 🌎 Deployment Region

The default region is:

```text
eastus2
```

Override it with:

```bash
azd env set AZURE_LOCATION <region>
azd up
```

The selected region needs to support the required Azure OpenAI model deployments.

---

# 💬 Try the Application

After deployment, `azd up` displays the application URLs.

Example:

```text
🚀 Your LangChain Agent is Ready!

🌐 Web chat:
https://ca-agent-<id>.<region>.azurecontainerapps.io/

Health:
https://ca-agent-<id>.<region>.azurecontainerapps.io/api/health

MCP Server:
https://ca-mcp-<id>.<region>.azurecontainerapps.io/mcp
```

Try prompts such as:

```text
Hi, I run a 25-person property management company —
do you work with teams like mine?
```

```text
We're already on Big-Box Pro — why switch?
```

```text
Can you show me your pricing tiers?
```

---

# 💻 Local Development

There are two supported development approaches.

---

## Option 1 — Cloud PostgreSQL + Local Services

This is the recommended development workflow.

First retrieve the deployed environment variables:

```bash
azd env get-values > .env.local
```

Then configure the local MCP endpoint:

```bash
echo "MCP_SERVER_URL=http://localhost:8000" >> .env.local
```

### Terminal 1 — MCP Server

```bash
cd mcp
source ../.env.local
python app.py
```

### Terminal 2 — Agent

```bash
cd agent
source ../.env.local
PORT=8001 python app.py
```

Open:

```text
http://localhost:8001
```

---

# 🐳 Option 2 — Full Local Stack

Start PostgreSQL + pgvector:

```bash
docker compose up -d
```

Create the local environment file:

```bash
cp .env.example .env.local
```

Add your Azure OpenAI configuration.

Then initialize the database:

```bash
cd data

source ../.env.local

python generate_database.py
python generate_sales_kb.py
python regenerate_embeddings.py
```

Start the MCP server and agent using the same commands shown in Option 1.

---

# 🧰 VS Code Tasks

The repository also provides VS Code tasks for common operations.

Open:

```text
Cmd/Ctrl + Shift + P
```

Then select:

```text
Tasks: Run Task
```

Available tasks include:

* Start MCP Server
* Start Agent
* Start PostgreSQL
* Initialize Database

---

# 🛠️ Customise the Agent

## Add a New MCP Tool

Add a function to:

```text
mcp/app.py
```

Example:

```python
@mcp.tool(
    annotations={
        "title": "Top Categories",
        "readOnlyHint": True
    }
)
async def top_categories(
    limit: int = 5,
    ctx: Context = None
) -> str:
    """Return the top-selling product categories."""
    ...
```

Then expose the tool to the required sales stage:

```python
STEP_CONFIG["educate"]["tools"].add(
    "top_categories"
)
```

The tool will only be available to stages that explicitly whitelist it.

---

# 🧠 Change Agent Behaviour

Sales prompts are stored separately under:

```text
agent/app/prompts/
```

For example:

```text
greet.txt
qualify.txt
educate.txt
objection.txt
book.txt
handoff_to_ae.txt
```

To modify qualification behaviour, update:

```text
qualify.txt
```

To modify which tools are available during that step, update:

```text
agent/app/middleware/steps.py
```

Redeploy the agent:

```bash
azd deploy agent
```

---

# 🤖 Change the Model

Modify:

```text
infra/main.parameters.json
```

Example:

```json
{
  "openAiModelName": {
    "value": "gpt-5-mini"
  }
}
```

Use a model that supports the required Responses API capabilities and hosted tools.

---

# 📊 Monitoring

The application integrates with:

* Application Insights
* Log Analytics
* Azure Container Apps logging

Open monitoring:

```bash
azd monitor
```

Tail the agent logs:

```bash
az containerapp logs show \
  -n <agent-name> \
  -g <resource-group> \
  --follow
```

Application Insights captures:

```text
HTTP Requests
     │
     ├── Agent execution
     │
     ├── MCP tool calls
     │
     └── Azure OpenAI requests
```

This enables end-to-end tracing across the application.

---

# 🔮 Future Work

## Microsoft WorkIQ MCP Integration

The current `book` step uses:

```text
propose_meeting_times
```

and hands the actual calendar booking to the human AE during escalation.

A natural future extension is integrating Microsoft WorkIQ MCP servers such as:

```text
mcp_CalendarServer
mcp_TeamsServer
mcp_MailTools
```

This could enable the agent to:

* 📅 Book meetings
* 📧 Retrieve recent lead emails
* 💬 Check Teams discussions
* 🗓️ Inspect calendar availability

Potential future architecture:

```text
                 Sales Agent
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
     Sales MCP                WorkIQ MCP
          │                       │
          ▼                ┌──────┼──────┐
     PostgreSQL             ▼      ▼      ▼
                         Calendar Teams  Mail
```

WorkIQ uses delegated OAuth and Microsoft 365 authentication, so the deployment would require an appropriate user sign-in flow and per-request authorization.

---

# 🧹 Clean Up

To remove the resources provisioned by `azd up`:

```bash
azd down
```

This removes the Azure resources created for the deployment.

---

# 📚 Resources

* [Azure OpenAI Responses API](https://learn.microsoft.com/azure/ai-services/openai/how-to/responses)
* [LangChain](https://python.langchain.com/)
* [LangChain MCP Adapters](https://github.com/langchain-ai/langchain-mcp-adapters)
* [Model Context Protocol](https://modelcontextprotocol.io/)
* [FastMCP](https://github.com/jlowin/fastmcp)
* [Azure Developer CLI](https://learn.microsoft.com/azure/developer/azure-developer-cli/)
* [pgvector](https://github.com/pgvector/pgvector)
* [Microsoft WorkIQ MCP Servers](https://learn.microsoft.com/en-us/microsoft-agent-365/tooling-servers-overview)

This sample is inspired by the Microsoft AI Tour WRK540 workshop and reuses its product catalogue.

---

# 🤝 Contributing

Contributions are welcome.

For significant changes, open an issue first to discuss the proposed modification.

Most contributions require agreement to a Contributor License Agreement.

---

# 📄 License

MIT — see [`LICENSE`](LICENSE).

---

<div align="center">

## ⭐ If this project helped you, consider giving it a star!

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&height=120&section=footer&text=LangChain%20%2B%20Azure%20OpenAI%20%2B%20MCP&fontSize=24&fontAlignY=65" />

<br>

### Built with

<img src="https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=chainlink&logoColor=white" />
<img src="https://img.shields.io/badge/Azure%20OpenAI-0078D4?style=flat-square&logo=microsoftazure&logoColor=white" />
<img src="https://img.shields.io/badge/MCP-6B4FBB?style=flat-square" />
<img src="https://img.shields.io/badge/PostgreSQL-336791?style=flat-square&logo=postgresql&logoColor=white" />
<img src="https://img.shields.io/badge/pgvector-336791?style=flat-square" />

<br><br>

**Agentic AI · RAG · MCP · Azure · PostgreSQL**

</div>
