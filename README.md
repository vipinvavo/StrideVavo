# StrideVavo

AI-powered **STRIDE** threat modeling for Bitvavo Product Security. Describe your application or point to a GitHub repo (or upload an architecture diagram), pick an LLM, and get structured threats, attack trees, mitigations, DREAD assessments, and test cases.

**Product Security @ Bitvavo**

---

## Features

- **STRIDE threat model** — Generate Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege threats from a text description, GitHub repo URL, or uploaded architecture image (multimodal models).
- **Attack tree** — Visualize attack paths and preconditions from the same context.
- **Deep analysis** — From an existing threat model:
  - **Mitigations** — Suggested controls and remediations.
  - **DREAD** — Risk scoring (Damage, Reproducibility, Exploitability, Affected users, Discoverability).
  - **Test cases** — Security test ideas, including GenAI/Agentic-specific cases.

Multiple **LLM backends**: OpenAI, Anthropic, Google AI, Mistral, Groq, Ollama, LM Studio. No data is stored; everything is session-only.

---

## Requirements

- Python 3.12+
- Dependencies in `requirements.txt` (e.g. `streamlit`, `openai`, `anthropic`, `tiktoken`, `python-dotenv`, `PyGithub`, `requests`)

---

## Quick start

1. **Clone and enter the project**
   ```bash
   cd stride-gpt-master
   ```

2. **Create a virtual environment and install dependencies**
   ```bash
   python -m venv .venv
   source .venv/bin/activate   # Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. **Configure API keys (optional; only for providers you use)**  
   Create a `.env` in the project root, for example:
   ```env
   OPENAI_API_KEY=sk-...
   ANTHROPIC_API_KEY=sk-ant-...
   GOOGLE_API_KEY=...
   MISTRAL_API_KEY=...
   GROQ_API_KEY=...
   ```
   For **Ollama** / **LM Studio**, no keys are required; set endpoints if different from defaults:
   ```env
   OLLAMA_ENDPOINT=http://localhost:11434
   LM_STUDIO_ENDPOINT=http://localhost:1234
   ```
   For **GitHub repo analysis**, add:
   ```env
   GITHUB_API_KEY=...
   ```

4. **Run the app**
   ```bash
   streamlit run main.py
   ```
   Open the URL shown (default: http://localhost:8501).

---

## Docker

```bash
docker build -t stridevavo .
docker run -p 8501:8501 --env-file .env stridevavo
```

The app listens on port 8501 with XSRF protection enabled.

---

## UI overview

- **Sidebar** — Model provider and model selection, API keys (or endpoints for Ollama/LM Studio), optional GitHub token and token limit for repo analysis.
- **Main area** — Three tabs:
  1. **Threats** — Input (text / GitHub URL / image), app type, sensitivity, internet-facing, auth; generate and view STRIDE threat model.
  2. **Attack Tree** — Generate and view attack tree from the same context.
  3. **Deep Analysis** — Buttons for Mitigations, DREAD, and Test Cases (require an existing threat model). Results can be downloaded as Markdown.

Theme: terminal/hacker style (dark background, neon green accents, JetBrains Mono).

---

## Environment variables

| Variable | Purpose |
|----------|--------|
| `OPENAI_API_KEY` | OpenAI API |
| `ANTHROPIC_API_KEY` | Anthropic (Claude) |
| `GOOGLE_API_KEY` | Google AI (Gemini) |
| `MISTRAL_API_KEY` | Mistral |
| `GROQ_API_KEY` | Groq |
| `GITHUB_API_KEY` | GitHub repo analysis (optional) |
| `OLLAMA_ENDPOINT` | Ollama server (default: `http://localhost:11434`) |
| `LM_STUDIO_ENDPOINT` | LM Studio server (default: `http://localhost:1234`) |

---

## License

See repository license file. For internal Bitvavo Product Security use; adapt as needed for your organization.
