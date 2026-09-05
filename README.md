---

page_type: sample
languages:

* python
  products:
* azure-openai
* azure-container-apps
* azure
* langchain
* pgvector
  urlFragment: langchain-agent-python
  name: LangChain Sales Agent with MCP and Azure OpenAI (Python)
  description: A multi-step LangChain v1 sales-conversation agent that uses the Azure OpenAI Responses API, an MCP server with Postgres + pgvector for catalog and CRM tools, and ships with one command via azd up.

---

<div align="center">

# 🤖 LangChain Sales Agent

### Responses API + MCP + PostgreSQL + pgvector

<p>
  <img src="https://img.shields.io/badge/Python-3.11%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/LangChain-v1-1C3C3C?style=for-the-badge&logo=chainlink&logoColor=white" alt="LangChain"/>
  <img src="https://img.shields.io/badge/Azure%20OpenAI-Responses%20API-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white" alt="Azure OpenAI"/>
  <img src="https://img.shields.io/badge/MCP-FastMCP-6B4FBB?style=for-the-badge" alt="MCP"/>
  <img src="https://img.shields.io/badge/PostgreSQL-pgvector-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL"/>
  <img src="https://img.shields.io/badge/Azure%20Container%20Apps-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white" alt="Azure Container Apps"/>
</p>

<p>
  <a href="https://github.com/Azure-Samples/langchain-agent-python">
    <img src="https://img.shields.io/github/stars/Azure-Samples/langchain-agent-python?style=flat-square&logo=github" alt="GitHub Stars"/>
  </a>
  <a href="https://github.com/Azure-Samples/langchain-agent-python/network/members">
    <img src="https://img.shields.io/github/forks/Azure-Samples/langchain-agent-python?style=flat-square&logo=github" alt="GitHub Forks"/>
  </a>
  <img src="https://img.shields.io/github/license/Azure-Samples/langchain-agent-python?style=flat-square" alt="License"/>
  <img src="https://img.shields.io/github/last-commit/Azure-Samples/langchain-agent-python?style=flat-square" alt="Last Commit"/>
</p>

### A production-oriented reference architecture for a multi-step AI sales conversation.

<br/>

<a href="#quick-start">
  <img src="https://img.shields.io/badge/🚀%20Deploy%20to%20Azure-azd%20up-0078D4?style=for-the-badge" alt="Deploy to Azure"/>
</a>

<br/><br/>

**Built with Azure OpenAI Responses API • LangChain v1 • Model Context Protocol • PostgreSQL + pgvector • Managed Identity**

</div>

---

## 🧭 What This Sample Demonstrates

This repository shows how to build a **multi-step AI sales agent** using **LangChain v1** and the **Azure OpenAI Responses API**.

The agent guides a sales conversation through a six-step funnel using LangChain's **handoff pattern**, retrieves grounded business information through an **MCP server**, and uses **PostgreSQL + pgvector** for semantic search across product and sales content.

The architecture separates the public-facing agent from the MCP service and uses **Azure Container Apps** for deployment.

### Core capabilities

```text
┌──────────────────────────────────────────────────────────────┐
│                    LANGCHAIN SALES AGENT                     │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  🧠 Multi-step Sales Conversation                           │
│  🔄 Handoff-based Funnel State                               │
│  🔎 Semantic Retrieval with pgvector                         │
│  🔌 MCP Tool Integration                                     │
│  🛡️ Groundedness Validation                                  │
│  🧩 Middleware-based Query Refinement                         │
│  📚 Product / KB / Case Study Retrieval                      │
│  💰 Pricing & Plan Comparison                                 │
│  👤 Lead Qualification & AE Handoff                          │
│  🔐 Entra ID / Managed Identity                              │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

---

# 🖼️ Application Preview

The original project screenshots are retained below because they are important for understanding the user experience and debugging workflow.

### 💬 Sales Agent

![LangChain MCP Agent](images/app-image.png)

### 🐞 Agent Debug Panel

![Agent debug panel](images/debug-image.png)

### ☁️ GitHub Codespaces

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/Azure-Samples/langchain-agent-python)

---

# 📚 What You'll Learn

By working through this sample, you will learn how to:

* Build a **multi-step LangChain v1 agent** using the handoff pattern.
* Use **middleware** to refine user queries, control context, and validate grounded responses.
* Connect an agent to **Postgres + pgvector** for semantic retrieval.
* Use **HNSW indexes** with `text-embedding-3-small` embeddings.
* Expose business capabilities through **Model Context Protocol (MCP)** tools.
* Integrate **FastMCP** with a LangChain agent.
* Use the Azure OpenAI **Responses API** with hosted tools.
* Use **Entra ID / Managed Identity** instead of static API keys.
* Deploy independently scalable services with **Azure Container Apps**.
* Provision the environment with **Bicep + Azure Developer CLI (`azd`)**.
* Add observability through **Application Insights**.

---

# 🏗️ Architecture

The application is split into two independently deployed Container Apps:

```text
                         ┌─────────────────────────────┐
                         │        User / Browser       │
                         └──────────────┬──────────────┘
                                        │
                                        ▼
                     ┌────────────────────────────────────┐
                     │       Azure Container Apps         │
                     │                                    │
                     │        🤖 Sales Agent              │
                     │        LangChain v1                │
                     │        Starlette                   │
                     └───────────────┬────────────────────┘
                                     │
                            MCP over HTTP
                                     │
                                     ▼
                     ┌────────────────────────────────────┐
                     │       Azure Container Apps         │
                     │                                    │
                     │       🔌 MCP Server                │
                     │       FastMCP                      │
                     │       9 Read-only Tools            │
                     └───────────────┬────────────────────┘
                                     │
                    ┌────────────────┴────────────────┐
                    │                                 │
                    ▼                                 ▼
        ┌───────────────────────┐        ┌────────────────────────┐
        │ Azure PostgreSQL      │        │ Azure OpenAI           │
        │ Flexible Server       │        │                        │
        │ + pgvector            │        │ Chat + Embeddings      │
        └───────────────────────┘        └────────────────────────┘
```

![Zava Sales Agent architecture](images/architecture.png)

### 🔐 Security Boundary

The **agent is the only public-facing service**.

The MCP service is reachable only from within the Container Apps environment.

Azure access is secured through a **user-assigned managed identity** with RBAC access to Azure OpenAI and PostgreSQL.

---

# 🔄 The 6-Step Sales Funnel

The conversation follows a state-driven six-step funnel:

```text
                 ┌──────────┐
                 │  GREET   │
                 └────┬─────┘
                      │
                      ▼
                 ┌──────────┐
                 │ QUALIFY  │
                 └────┬─────┘
                      │
                      ▼
                 ┌──────────┐
                 │ EDUCATE  │
                 └────┬─────┘
                      │
                      ▼
                 ┌──────────┐
                 │ OBJECTION│
                 └────┬─────┘
                      │
                      ▼
                 ┌──────────┐
                 │   BOOK   │
                 └────┬─────┘
                      │
                      ▼
              ┌────────────────┐
              │ HANDOFF TO AE  │
              └────────────────┘
```

The original sales-funnel diagram is retained:

![Zava Sales Agent 6-step funnel](images/sales-funnel.svg)

The state machine is implemented in:

```text
agent/app/middleware/steps.py
```

while each step has a dedicated prompt under:

```text
agent/app/prompts/
```

Each state controls:

* The active system prompt
* The tools visible to the model
* The conversation stage
* Lead context
* Qualification information
* Objection history
* Grounding metadata

The state model is defined in `agent/app/state.py`.

---

# 🧠 Agent Architecture

The agent is constructed around a **two-tier model strategy**.

### Main model

Used for the user-facing sales conversation.

```python
main = ChatOpenAI(
    model="gpt-5-mini",
    use_responses_api=True,
    ...
)
```

### Utility model

Used for internal middleware tasks:

```python
nano = ChatOpenAI(
    model="gpt-5-nano",
    use_responses_api=True,
    tags=["nano-utility"],
)
```

The agent composes:

```text
                  User Message
                       │
                       ▼
              ┌──────────────────┐
              │ Query Refinement  │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │ Step Configuration│
              │ Prompt + Tools    │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │ Groundedness     │
              │ Validation       │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │ Conversation     │
              │ Summarization    │
              └────────┬─────────┘
                       │
                       ▼
                  Final Response
```

The implementation uses `create_agent`, `SalesState`, local tools, MCP tools, `SummarizationMiddleware`, and an `InMemorySaver` checkpointer.

---

# 🧩 Middleware

The middleware chain performs four major functions.

| Middleware         | Purpose                                               |
| ------------------ | ----------------------------------------------------- |
| Query refinement   | Resolves ambiguous references and improves the query  |
| Step configuration | Injects the step-specific prompt and filters tools    |
| Validation         | Checks whether knowledge-heavy responses are grounded |
| Summarization      | Compresses long conversation history                  |

### Tool filtering

A particularly important design choice is that the agent does **not** see every tool at every stage.

For example:

```text
EDUCATE
 ├── semantic_search_products
 ├── search_case_studies
 ├── search_kb_articles
 └── get_pricing

OBJECTION
 ├── search_case_studies
 ├── search_kb_articles
 ├── get_pricing
 └── compare_plans

BOOK
 └── propose_meeting_times
```

This is implemented through `STEP_CONFIG` in:

```text
agent/app/middleware/steps.py
```

The middleware injects the correct prompt and filters the available tools before every model invocation.

---

# 🔌 MCP Server

The MCP server is implemented with **FastMCP** and communicates with the agent over **streamable HTTP**.

It exposes nine read-only tools:

| Tool                       | Purpose                               |
| -------------------------- | ------------------------------------- |
| `get_current_utc_date`     | Resolve relative dates                |
| `get_table_schemas`        | Inspect available table structures    |
| `execute_sales_query`      | Read-only analytical SQL              |
| `semantic_search_products` | Semantic product retrieval            |
| `get_product_details`      | Retrieve detailed product information |
| `search_case_studies`      | Search customer case studies          |
| `search_kb_articles`       | Search the knowledge base             |
| `get_pricing`              | Retrieve pricing plans                |
| `compare_plans`            | Compare pricing/features              |

The MCP implementation connects to PostgreSQL using `asyncpg` and uses Azure OpenAI embeddings for semantic retrieval.

---

# 🔎 Retrieval with PostgreSQL + pgvector

The retrieval layer combines:

```text
User Query
    │
    ▼
Azure OpenAI Embedding
    │
    ▼
Vector Representation
    │
    ▼
pgvector Similarity Search
    │
    ▼
Relevant Product / KB / Case Study
    │
    ▼
Grounded Agent Response
```

The sample uses `text-embedding-3-small` vectors and **HNSW indexes** for semantic search.

### Indexed content includes

* Product catalogue
* Case studies
* Knowledge-base articles
* Pricing-related sales content

---

# ⚡ Embedding Cache

The MCP server contains an in-process bounded cache for repeated embedding requests.

The cache key includes:

```text
(deployment_name, query_text)
```

This means:

* Repeated searches can avoid another embedding request.
* Changing the embedding deployment naturally separates cache entries.
* The cache is bounded rather than growing indefinitely.

The implementation also protects concurrent identical embedding lookups with an async lock.

---

# 🛡️ SQL Guardrails

The analytics escape hatch is deliberately restricted.

Only:

```sql
SELECT
```

and:

```sql
WITH ...
```

queries are accepted.

The server blocks dangerous patterns such as:

```text
DROP
DELETE
INSERT
UPDATE
ALTER
TRUNCATE
GRANT
REVOKE
EXEC
CALL
COPY
```

Multiple SQL statements are also rejected.

This creates a **defense-in-depth** model:

```text
LLM-generated SQL
       │
       ▼
SQL Validation
       │
       ├── ❌ Forbidden
       │
       └── ✅ Read-only
               │
               ▼
        PostgreSQL Reader
```

The repository also describes the PostgreSQL role as read-only for this path.

---

# 🔐 Authentication

The sample is designed around **keyless Azure authentication**.

### Managed Identity

The container services use a user-assigned identity for access to:

* Azure OpenAI
* Azure Database for PostgreSQL

Instead of storing long-lived API keys, the application obtains Entra ID bearer tokens through Azure Identity.

```text
Container App
      │
      ▼
User-assigned Managed Identity
      │
      ├──────────────► Azure OpenAI
      │
      └──────────────► PostgreSQL
```

This removes the need for hard-coded credentials and aligns the sample with Azure RBAC-based access.

---

# ☁️ Infrastructure

Infrastructure is provisioned with:

```text
Azure Developer CLI (azd)
          +
       Bicep
```

The repository's `azure.yaml` defines two services:

```text
mcp-server
agent
```

Both are deployed as Azure Container Apps.

A `postprovision` hook is used to seed and initialize the database.

---

# 🚀 Quick Start

## Prerequisites

You need:

* An Azure subscription
* Azure Developer CLI (`azd`)
* Azure CLI
* Python 3.11+ for local development
* Docker for the full local stack

GitHub Codespaces provides the required development tools automatically.

---

## 1. Sign in

```bash
az login
azd auth login
```

---

## 2. Deploy Everything

```bash
azd up
```

This provisions the main Azure resources, including:

```text
Azure OpenAI
      +
PostgreSQL Flexible Server
      +
pgvector
      +
Container Apps Environment
      +
Agent Container
      +
MCP Container
```

The deployment also seeds the Zava product catalogue and sales knowledge base.

---

# ⏱️ Deployment Notes

The original sample estimates approximately **10–15 minutes** for a fresh deployment, with PostgreSQL provisioning being one of the slower steps.

### Default Azure region

```text
eastus2
```

Override it with:

```bash
azd env set AZURE_LOCATION <region>
```

The chat and middleware model deployments need a region where the selected models are available.

---

# ✅ After Deployment

You should see output similar to:

```text
🚀 Your LangChain Agent is Ready!

🌐 Web chat:
https://ca-agent-<id>.<region>.azurecontainerapps.io/

Health:
https://ca-agent-<id>.<region>.azurecontainerapps.io/api/health

MCP Server:
https://ca-mcp-<id>.<region>.azurecontainerapps.io/mcp
```

Open the **Web chat** URL to interact with the agent.

---

# 💬 Example Conversations

Try prompts such as:

```text
Hi, I run a 25-person property management company.
Do you work with teams like mine?
```

```text
We're already on Big-Box Pro.
Why should we switch?
```

```text
Can you show me your pricing tiers?
```

These exercise different stages of the sales funnel.

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
│   └── generate_sales_kb.py
│
├── infra/
│   └── Bicep templates
│
├── images/
│   ├── app-image.png
│   ├── debug-image.png
│   ├── architecture.png
│   └── sales-funnel.svg
│
└── azure.yaml
```

---

# 🧪 Local Development

There are two supported approaches.

## Option 1: Cloud PostgreSQL + Local Services

Recommended when you want to develop the Python services locally while using Azure infrastructure.

```bash
azd env get-values > .env.local

echo "MCP_SERVER_URL=http://localhost:8000" >> .env.local
```

### Terminal 1

```bash
cd mcp
source ../.env.local
python app.py
```

### Terminal 2

```bash
cd agent
source ../.env.local
PORT=8001 python app.py
```

Then open:

```text
http://localhost:8001
```

---

# 🐳 Option 2: Full Local Stack

Start PostgreSQL + pgvector:

```bash
docker compose up -d
```

Create local environment variables:

```bash
cp .env.example .env.local
```

Then initialize the database:

```bash
cd data

source ../.env.local

python generate_database.py
python generate_sales_kb.py
python regenerate_embeddings.py
```

After that, start the MCP and agent services.

---

# 🧰 VS Code Tasks

The repository includes development tasks for:

```text
▶ Start MCP Server
▶ Start Agent
▶ Start PostgreSQL (Docker)
▶ Initialize Database
```

Open:

```text
Command Palette
→ Tasks: Run Task
```

---

# 🛠️ Customization

## Add a New MCP Tool

Create a tool in:

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

Then whitelist it for the relevant funnel step:

```python
STEP_CONFIG["educate"]["tools"].add(
    "top_categories"
)
```

This is important because simply creating an MCP tool does **not** automatically expose it to every agent step.

---

# 🤖 Change the Model

Update:

```text
infra/main.parameters.json
```

For example:

```json
{
  "openAiModelName": {
    "value": "gpt-5-mini"
  }
}
```

The selected model must support the required Responses API capabilities.

---

# 📝 Customize Agent Behaviour

Each funnel stage has an independent prompt.

For example:

```text
agent/app/prompts/qualify.txt
```

controls qualification behaviour.

Tool permissions are defined in:

```text
agent/app/middleware/steps.py
```

After changing the agent:

```bash
azd deploy agent
```

---

# 🧠 Conversation State

The `SalesState` model maintains the state of the sales conversation.

Important fields include:

```text
current_step
intent
lead_id
lead_email
company_name
industry
team_size
budget
authority
need
timeline
current_tools
objection_history
last_retrieved_docs
awaiting_escalation_confirmation
```

This allows the conversation to maintain structured sales context instead of relying solely on chat history.

---

# 📅 Future Work: Work IQ MCP Integration

The current `book` stage uses:

```text
propose_meeting_times
```

and escalates actual calendar booking to a human AE.

A future extension described by the project is integration with Microsoft Work IQ MCP servers such as:

```text
mcp_CalendarServer
mcp_TeamsServer
mcp_MailTools
```

This could allow the agent to:

* Schedule meetings
* Read relevant email context
* Check Teams discussions
* Enrich lead conversations

The authentication and deployment model would require delegated Microsoft identity/OAuth handling.

---

# 📊 Monitoring & Observability

Application Insights is used for telemetry when deployed.

### Open monitoring

```bash
azd monitor
```

### Tail Container App logs

```bash
az containerapp logs show \
  -n <agent-name> \
  -g <rg-name> \
  --follow
```

The application captures information across:

```text
HTTP Request
     ↓
Agent Execution
     ↓
MCP Tool Calls
     ↓
Azure OpenAI Requests
     ↓
End-to-End Telemetry
```

---

# 🧹 Clean Up

To remove all Azure resources created by `azd up`:

```bash
azd down
```

This removes the resource group and associated provisioned resources.

---

# 🧱 Technology Stack

| Technology                 | Role                     |
| -------------------------- | ------------------------ |
| **Python 3.11+**           | Application development  |
| **LangChain v1**           | Agent orchestration      |
| **Azure OpenAI**           | LLM + embeddings         |
| **Responses API**          | Agent/tool interaction   |
| **Model Context Protocol** | Tool integration layer   |
| **FastMCP**                | MCP server               |
| **PostgreSQL**             | Operational data store   |
| **pgvector**               | Vector similarity search |
| **asyncpg**                | Async PostgreSQL access  |
| **Starlette**              | Agent web service        |
| **Azure Container Apps**   | Application hosting      |
| **Azure Developer CLI**    | Provisioning/deployment  |
| **Bicep**                  | Infrastructure as code   |
| **Entra ID**               | Authentication           |
| **Managed Identity**       | Keyless Azure access     |
| **Application Insights**   | Monitoring               |

---

# 📐 Design Principles

### 1. Separation of Concerns

```text
Agent
  │
  └── Conversation + orchestration

MCP
  │
  └── Data + business tools

PostgreSQL
  │
  └── Persistent data

Azure OpenAI
  │
  └── Generation + embeddings
```

### 2. Least-Privilege Tool Access

Each funnel stage only exposes the tools it needs.

### 3. Grounded Generation

Knowledge-heavy stages can validate responses against retrieved documents.

### 4. Keyless Authentication

Managed Identity avoids long-lived secrets.

### 5. Independent Deployment

The agent and MCP service are deployed as separate Container Apps.

### 6. Reproducible Infrastructure

`azd up` + Bicep provides a repeatable cloud deployment workflow.

---

# 🎯 Why This Architecture Matters

This sample demonstrates an architecture that goes beyond a simple chatbot.

Instead of:

```text
User → LLM → Answer
```

the system follows:

```text
User
  ↓
Conversation State
  ↓
Step-specific Prompt
  ↓
Step-specific Tool Permissions
  ↓
MCP
  ↓
PostgreSQL / pgvector
  ↓
Grounded Context
  ↓
Azure OpenAI Responses API
  ↓
Validation
  ↓
Sales Response
```

This makes the system easier to reason about, extend, secure, and operate.

---

# 🔗 Resources

* [Azure OpenAI Responses API](https://learn.microsoft.com/azure/ai-services/openai/how-to/responses)
* [LangChain](https://python.langchain.com/)
* [LangChain MCP Adapters](https://github.com/langchain-ai/langchain-mcp-adapters)
* [Model Context Protocol](https://modelcontextprotocol.io/)
* [FastMCP](https://github.com/jlowin/fastmcp)
* [PostgreSQL](https://www.postgresql.org/)
* [pgvector](https://github.com/pgvector/pgvector)
* [Azure Developer CLI](https://learn.microsoft.com/azure/developer/azure-developer-cli/)
* [Azure Container Apps](https://learn.microsoft.com/azure/container-apps/)
* [Azure OpenAI Models](https://learn.microsoft.com/azure/ai-services/openai/concepts/models)
* [Microsoft Work IQ Tooling Servers](https://learn.microsoft.com/en-us/microsoft-agent-365/tooling-servers-overview)

This sample is also inspired by the **Microsoft AI Tour WRK540 workshop** and reuses its product catalogue.

---

# 🤝 Contributing

Contributions are welcome.

Most contributions require agreement to a Contributor License Agreement.

See:

https://cla.opensource.microsoft.com

For questions or issues, open a GitHub issue in this repository.

---

# 📄 License

This project is licensed under the **MIT License**.

See [LICENSE](LICENSE) for details.

---

<div align="center">

## ⭐ Explore • Build • Extend

<p>
  <a href="https://github.com/Azure-Samples/langchain-agent-python">
    <img src="https://img.shields.io/badge/⭐%20Star%20Repository-181717?style=for-the-badge&logo=github&logoColor=white" alt="Star Repository"/>
  </a>
  <a href="https://codespaces.new/Azure-Samples/langchain-agent-python">
    <img src="https://img.shields.io/badge/⚡%20Open%20in%20Codespaces-0078D4?style=for-the-badge&logo=githubcodespaces&logoColor=white" alt="Open in Codespaces"/>
  </a>
</p>

<br/>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0078D4,50:5B5FC7,100:7F56D9&height=150&section=footer&text=LangChain%20%2B%20MCP%20%2B%20Azure%20OpenAI&fontSize=24&fontColor=ffffff&animation=fadeIn" width="100%" alt="Animated footer"/>

</div>
