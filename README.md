# 🤖 Customer Support Triage Agent

A multi-agent customer support system built with **LangChain** and **DeepSeek** that automatically classifies customer support tickets, retrieves company policies, generates customer responses, and reviews those responses before they are sent.

This project demonstrates an **Orchestrator–Subagent architecture**, where multiple AI agents collaborate to solve a real-world customer support problem.

---

# 📌 Business Problem

Customer support teams often spend significant time manually classifying tickets, looking up company policies, drafting responses, and reviewing replies before sending them to customers.

This project automates that workflow by using AI agents while still protecting high-risk decisions through a human approval checkpoint.

---

# 🚀 Features

* Multi-Agent Architecture
* Triage Agent
* Policy Agent
* Reviewer/Critic Agent
* Shared State Management
* Tool Calling with LangChain
* CSV Data Source
* Tool Logging
* Human Approval Gate
* Automatic Retry when review fails

---

# 🏗️ System Architecture

```
Customer Ticket
       │
       ▼
  Orchestrator
       │
       ▼
  get_ticket Tool
       │
       ▼
  Triage Agent
       │
       ├── Flagged?
       │      │
       │      ├── YES → Human Approval Required
       │      │
       │      └── NO
       ▼
  Policy Agent
       │
       ▼
 search_policy Tool
       │
       ▼
 Reviewer Agent
       │
       ├── Approved?
       │      │
       │      ├── YES → Send Response
       │      │
       │      └── NO
       ▼
 Policy Agent Retry
       │
       ▼
 Reviewer Retry
       │
       ├── Approved → Final Response
       └── Rejected → Human Approval
```

---

# 📂 Project Structure

```
customer_support_triage_agent/

│── config.py
│── tools.py
│── subagents.py
│── agent.py
│── orchestrator.py
│── main.py
│── tickets.csv
│── policies.csv
│── tool_log.txt
│── README.md
```

---

# 🛠️ Technologies Used

* Python
* LangChain
* DeepSeek API
* Pandas
* CSV
* Regular Expressions (Regex)

---

# 📋 Project Requirements

This project satisfies all assignment requirements.

### ✅ At Least Two Tools

* **get_ticket()**

  * Retrieves a customer ticket from `tickets.csv`.

* **search_policy()**

  * Searches `policies.csv` for the matching support policy.

* **get_all_policies()**

  * Returns all available policies when needed.

---

### ✅ Working Agent Loop

The application uses LangChain's `create_agent()` to create three AI agents:

* Triage Agent
* Policy Agent
* Reviewer Agent

The Orchestrator coordinates these agents, allowing them to call tools, observe results, and determine the next step in the workflow.

---

### ✅ Real Data Source

The project reads data from:

* `tickets.csv`
* `policies.csv`

using the Pandas library.

No responses are hardcoded.

---

### ✅ Tool Logging

Every tool call is recorded in:

```
tool_log.txt
```

The log includes:

* Tool name
* Arguments
* Returned result

---

### ✅ Human Approval Checkpoint

High-risk actions are protected with an approval gate.

If:

* the Triage Agent flags a ticket, or
* the Reviewer Agent rejects the generated response twice,

the ticket is routed to a human supervisor instead of sending an automatic response.

---

# ⚙️ Installation

Clone the repository

```bash
git clone https://github.com/yourusername/customer-support-triage-agent.git
```

Move into the project folder

```bash
cd customer-support-triage-agent
```

Create a virtual environment

```bash
python -m venv .venv
```

Activate the virtual environment

Windows

```bash
.venv\Scripts\activate
```

macOS/Linux

```bash
source .venv/bin/activate
```

Install dependencies

```bash
pip install -r requirements.txt
```

---

# 🔑 Environment Variables

Create a `.env` file in the project directory.

```text
DEEPSEEK_API_KEY=your_api_key_here
```

---

# ▶️ Running the Project

Run the application

```bash
python main.py
```

The program will:

1. Display all available tickets.
2. Ask for a ticket ID (or `ALL`).
3. Process the ticket through the multi-agent workflow.
4. Display the final result.
5. Save all tool calls to `tool_log.txt`.

---

# 🔄 Workflow

1. Load ticket from `tickets.csv`.
2. Create the shared state.
3. Send the ticket to the Triage Agent.
4. Determine the ticket category.
5. If flagged, route to human review.
6. Otherwise, send to the Policy Agent.
7. Retrieve the correct policy.
8. Generate a customer response.
9. Send the response to the Reviewer Agent.
10. If approved, return the response.
11. If rejected, retry once.
12. If still rejected, require human approval.

---

# 📚 What I Learned

Through this project I gained experience with:

* Multi-Agent AI Systems
* LangChain Agents
* Tool Calling
* Orchestrator–Subagent Architecture
* Shared State Management
* Human Approval Gates
* Tool Logging
* CSV Data Integration
* Prompt Engineering
* LLM Workflows

---

# 🚀 Future Improvements

* Store tickets in a SQL database
* Add conversation memory
* Connect to a live customer support API
* Deploy using Streamlit
* Add email integration after approval
* Support multiple reviewers

---

# 👩‍💻 Author

**Shweta Patil**

Data & AI Engineer

Passionate about Generative AI, AI Agents, Machine Learning, and building intelligent software solutions.

---

# 📄 License

This project was developed for educational purposes as part of the Innovation Fellowship (IF) program.
