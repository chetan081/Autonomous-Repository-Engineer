# Autonomous-Repository-Engineer
An autonomous multi-agent software engineering pipeline built in n8n. Utilizes a hybrid LLM architecture (Gemini &amp; Groq) to read GitHub issues, performs self-correcting planning/coding loops, and autonomously deliver production-ready Python solutions.

# Autonomous AI Software Engineer (n8n Pipeline)

An autonomous, multi-agent software engineering pipeline built inside n8n. This project demonstrates an event-driven DevOps pipeline that listens for incoming GitHub issues, orchestrates a closed-loop collaboration between specialized AI personas to write and QA code, and automatically handles the self-correction loop until the solution is production-ready.

## 📐 Workflow Architecture

Below is the complete blueprint of the autonomous orchestration layer designed in n8n:

![n8n Workflow Architecture](workflow.png)

### 🧠 How the Agentic Loop Works

1. **GitHub Trigger Event:** The pipeline acts as a webhook listener on the target repository, activating instantly when a new issue is opened with the specific label `agent-task`.
2. **The Planner Agent (Groq/Gemini):** Takes the raw issue title and description. Acting as a Solutions Architect, it maps out a language-agnostic technical implementation plan, variable paths, and edge cases *without* writing any code.
3. **The Coder Agent (Cloud Inference):** Ingests the architectural plan. Acting as a Python Developer, it generates the robust code block requested, isolated cleanly inside Markdown syntax.
4. **The Reviewer Agent (Lead QA Persona):** Evaluates the code against the original plan for syntax errors, logical holes, or execution optimization. 
5. **The Conditional Loop (IF Node):** 
   * If the Reviewer appends `STATUS: FAIL` along with code feedback, the pipeline dynamically routes execution **back to the Coder Agent**, passing the exact failure logs to trigger self-healing.
   * If the Reviewer evaluates the code as production-ready, it responds with `STATUS: PASS`, breaking the loop and pushing execution to the deployment node.
6. **Automated Delivery:** The final verified code is pushed back directly into the repository as an issue comment or pull request artifact.

---

## 🛠️ Tech Stack & Advanced Paradigms

* **Orchestration:** n8n (Advanced AI / Basic LLM Chains)
* **AI Architecture:** Multi-Agent Collaboration & Closed-Loop Self-Correction
* **Inference Layer:** Hybrid Cloud Deployment leveraging high-throughput API endpoints (Groq / Google Gemini) for rapid evaluation and execution.
* **Integrations:** Event-driven GitHub REST API / Webhooks

---

## 🚀 Key Engineering Takeaways

* **Determinism in Non-Deterministic Systems:** Enforcing strict string validation bounds (`STATUS: PASS / FAIL`) over LLM outputs to predictably control workflow routing graph branches.
* **Context Preservation Across Loops:** Designing expression fields (`{{ $node["Planner Agent"].json.text }}`) capable of maintaining core project requirements stable while downstream nodes dynamically update code feedback states.
* **Resource Optimization:** Designing a modular persona chain that isolates responsibilities, preventing context window bloating and maximizing code quality.

---

## 📄 License
This architecture is open-source and available under the [MIT License](LICENSE).
