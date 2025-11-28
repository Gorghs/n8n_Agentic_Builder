# n8n Agentic Builder

A high-precision framework designed by **karthick v** to automate the creation of production-ready n8n workflows using AI agents. This tool converts plain language requirements into valid, security-hardened n8n JSON files.

## What it does
- **Automated Workflow Engineering**: Uses specialized AI prompts to generate complete n8n JSON files.
- **QA & Compliance**: Automatically validates workflows for best practices and importability.
- **Security Hardening**: Reviews designs for risks like SSRF, auth leaks, and data exposure.
- **Template Management**: Organizes reusable patterns for rapid automation deployment.

## How to run
1. **Prepare Prompts**: Copy the system prompts from the `./prompts/` directory.
2. **Engage Agent**: Use these prompts in your preferred AI terminal agent (like Claude Code or similar).
3. **Generate**: Provide your automation requirements to the **Build Captain**.
4. **Export**: The agent will output a `.json` file to the `./workflows/` directory.
5. **Import**: Open your n8n instance and go to **Import from File** to upload the generated JSON.

---
*Made with love by karthick v*
