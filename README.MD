# n8n Agentic Builder: Terminal agent + prompts = n8n Automation Workflows


This repo contains **high-precision AI agent prompts** to generate **ready-to-import n8n workflow JSON files**.

The goal is to make it easy to:
1. Use a terminal AI agent as a **workflow engineer** to build production-ready n8n automations in JSON format.
2. Validate and harden those workflows with dedicated **QA** and **Security** agents.
3. Store and version-control both the **prompts** (brains) and the **workflows** (artifacts).
4. Side note: This is a small personal project maintained by **karthick v** aimed to automate automations ( yes you read that right ). Improvements will be actively made to the prompts.

---

## Repository Structure
```
n8n/
├── prompts/
│   ├── n8n_Build_Captain.md
│   ├── n8n_QA_Compliance.md
│   └── n8n_Security_Architect.md
│
├── workflows/
│   ├── workflow-1.json
│   ├── workflow-2.json
│
├── samples/
│   ├── n8n_sample.json
│   └── (future ones samples here)
│
└── README.md
```


---

### `prompts/`
Contains **three specialized Claude Code system prompts**:

1. **n8n_Build_Captain.md**  
   - The *orchestrator* agent.  
   - Builds full n8n workflows from a plain-language spec.  
   - Outputs valid, import-ready JSON + README + sample payloads.

2. **n8n_QA_Compliance.md**  
   - The *quality assurance* agent.  
   - Validates JSON importability, node conventions, error handling, and adherence to n8n best practices.  
   - Returns targeted JSON patches and test plans.

3. **n8n_Security_Architect.md**  
   - The *security review* agent.  
   - Identifies risks in workflow design (auth, PII, DoS, SSRF, etc.).  
   - Suggests and provides JSON fragments for hardening.

---

### `workflows/`
- This is where **all importable `.json` n8n workflows** live for you.
- Each JSON file should be valid for **direct import** into n8n via UI or CLI.
- These files are to remain private for your own use. If you wish to organize templates, you can place `.json` files into the templates directory for reuse across projects. Please remember to not share any of your secrets or private keys within your workflows.

---

### `templates/`

- The `Templates` directory contains curated workflow JSON files for reuse.
If you’ve created a reusable workflow, you can place your JSON file in the `Templates` directory for better organization.

- All templates are maintained to ensure quality and functionality.
Once saved, your workflow will be available for adaptation in future tasks.

---

### `samples/`
- Stores **canonical "reference" exports** for n8n workflows — known-good examples that follow best practices and pass QA/Security reviews.
- These samples are not production workflows (skeleton); they exist to **prime AI agents** and serve as schema/style references.
- Example: `n8n_sample.json` contains a minimal but complete pattern (Trigger → HTTP → Transform → Respond + Error handling).
- If you expand to other platforms (Make.com, Zapier, etc.), their samples can also live here, using their respective formats.

---

## How to Use the Agents

1. **Open three Claude Code chats(optional, can be done with just one chat)**:
   - **Chat A** → Paste `n8n_Build_Captain.md` (Build Captain)
   - **Chat B** → Paste `n8n_QA_Compliance.md` (QA & Compliance)
   - **Chat C** → Paste `n8n_Security_Architect.md` (Security Architect)

2. **Feed your automation spec** (trigger, data flow, APIs, credentials) into Chat A.  
   The Build Captain will produce:
   - `WORKFLOW.json`
   - `README.md` (workflow-specific)
   - Sample payloads

3. **Send the output** from Chat A to:
   - **Chat B** → for QA & Compliance review
   - **Chat C** → for Security review

4. **Apply patches** from QA & Security, then have Build Captain produce a **final JSON**.

5. **Save final workflow JSON** into `/workflows/` and commit to repo.

----

## Terminal Prompt Sample:

```
You are the Terminal Agent responsible for coordinating three specialized roles.
Each role has its own detailed system prompt defined in the following files:

- Build Captain → ./prompts/n8n_Build_Captain.md
- QA Agent → ./prompts/n8n_QA_Compliance.md
- Security Agent → ./prompts/n8n_Security_Architect.md

Follow the instructions in those markdown files to ensure each role behaves as designed.

---

**Task:**
Create a production-ready n8n workflow JSON with the following requirements:

- What you want goes here

---

**Final Output:**

- Specify what you want to be outputted here.

```



---

## Importing into n8n

**UI Method:**
- Go to the n8n Editor UI → **Import from File** → Select the `.json` file.

**CLI Method (self-hosted):**
```bash
n8n import:workflow --input=./workflows/your-workflow.json
