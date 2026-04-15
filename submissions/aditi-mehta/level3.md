# Level 3 Submission - Aditi Mehta

### Agent Repository Linked
**URL:** https://github.com/Dynamic-ctrl/lpi-smile-agent

### Agent Description
I built a Python agent that takes a user's project idea and runs it against the LPI methodology. Instead of using a heavy framework, I wrote a script that securely interfaces with the Node MCP server via standard input/output. It queries two tools, grabs the data, and passes it to a local Ollama model to generate a plan.

### LPI Tools Referenced
1. `smile_overview`
2. `get_insights`

### Setup Instructions
1. Clone the agent repo linked above.
2. Run `pip install -r requirements.txt`.
3. Make sure the LPI sandbox is built and Ollama is running.
4. Run: `python agent.py "Create a smart hospital"`

### Explainability Evidence
I hardcoded a rule into the LLM system prompt requiring it to cite its sources. By telling it to explicitly print `[Tool: smile_overview]` or `[Tool: get_insights]`, the user can track exactly which piece of advice came from which MCP tool.

### Security Awareness
I added basic input validation and sanitization. The script uses a regex function to strip out weird characters from the terminal arguments to prevent prompt injection, and it limits the string length before passing anything to the LLM or the subprocess.