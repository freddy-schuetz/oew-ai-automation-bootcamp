# AGENTS.md: AI Automation Bootcamp, Desktop-Vorlage (für Codex, OpenCode und andere Agents)

Diese Datei richtet sich an Coding-Agents, die **AGENTS.md** lesen (OpenAI **Codex**, **OpenCode**, Cursor, Gemini CLI, …). Die Vorlage gehört zum **AI Automation Bootcamp** der Österreich Werbung in Kooperation mit buildbar (https://buildbar.at/oew).

> **Du nutzt Claude Code?** Dann brauchst du diese Datei nicht. Nimm **[README.md](README.md)** und **CLAUDE.md** (mit Skills und dem Einrichtungssatz „Richte mir https://github.com/freddy-schuetz/oew-ai-automation-bootcamp ein.“).

## Setup (einmalig)

1. **n8n-Zugang mit API-Key:**
   - **Zentrale Bootcamp-n8n:** `https://n8n-oew.buildbar.at`. URL, Login und API-Key stehen im Zugangsbereich https://buildbar.at/oew#zugang.
   - **Eigene n8n** mit API-Zugang: API-Key in n8n unter Settings, n8n API, Create API Key.
   - Die kostenlose **n8n-Cloud-Testversion reicht nicht**, sie hat keinen API-Zugang.
2. **n8n-mcp anbinden** (läuft per `npx`, keine Installation nötig; Node.js muss installiert sein):

   **Codex**: `~/.codex/config.toml` (global) oder `.codex/config.toml` (im Projekt, nur bei „trusted projects“). Vorlage: [`.codex/config.toml.example`](.codex/config.toml.example)
   ```toml
   [mcp_servers.n8n-mcp]
   command = "npx"
   args = ["-y", "n8n-mcp"]
   [mcp_servers.n8n-mcp.env]
   N8N_API_URL = "https://n8n-oew.buildbar.at"
   N8N_API_KEY = "DEIN_KEY"
   MCP_MODE = "stdio"
   ```

   **OpenCode**: `opencode.json`. Vorlage: [`opencode.json.example`](opencode.json.example)
   ```json
   { "mcp": { "n8n-mcp": { "type": "local",
     "command": ["npx", "-y", "n8n-mcp"],
     "environment": { "N8N_API_URL": "https://n8n-oew.buildbar.at", "N8N_API_KEY": "DEIN_KEY", "MCP_MODE": "stdio" } } } }
   ```

3. **Verbindung testen:** Agent bitten, `n8n_health_check` aufzurufen. Das muss OK liefern.
4. ⚠️ **Keys niemals committen.** Die echten Konfigurationen (`.codex/config.toml`, `opencode.json`, `.mcp.json`) stehen in `.gitignore`.

## Arbeitsregeln: CLAUDE.md ist die einzige Quelle

**Lies [CLAUDE.md](CLAUDE.md) und befolge sie 1:1.** Dort stehen die Arbeitsweise (Idee klären, Freigaben früh prüfen), die Regeln für die gemeinsame Bootcamp-n8n, der Standard-Prozess, alle kritischen n8n-Konventionen, das Veröffentlichen über `deploy-oew.buildbar.at`, die Ergebnis-Regel (alles im eigenen privaten GitHub-Repository) und die Sicherheitsregeln. Diese Datei ergänzt nur das agent-spezifische Setup und wiederholt die Regeln bewusst **nicht**, damit die Versionen nicht auseinanderlaufen.

**Skills:** Wo CLAUDE.md von „Skills“ spricht, sind Markdown-Ordner unter `.claude/skills/<name>/SKILL.md` gemeint. **OpenCode lädt Claude-Code-Skills nativ.** Lädt dein Agent sie nicht automatisch (z. B. Codex), lies die passende `SKILL.md` als Anleitung, sobald die Situation passt: `idee-klaeren` bei vager Idee, `m365-google-freigaben` bei Postfach, Kalender, Teams oder Google, die Themen-Skills (`meetingnotizen`, `mail-triage-entwuerfe`, `bericht-zeitgesteuert`, `terminkoordination`, `daten-visualisieren`, `praesentation`), `n8n-testdaten` nach dem Bauen, `n8n-dokumentation` für Sticky Notes, `n8n-security-audit` vor der Aktivierung, `n8n-pruefbericht` am Ende.

## Wissen und Beispiele

- Tiefes n8n-Wissen liefert der **n8n-mcp-Server** selbst: starte mit `tools_documentation()`.
- Event-Infos (Agenda, Ort, Themen): https://buildbar.at/oew/claude.md
- Importierbare **Lern-Workflows** mit Sticky-Notes-Erklärungen: `examples/workflows/` · **Ideen-Menü**: `docs/tourismus-ideen.md` · Datenbank-Wahl: `docs/datenbank.md`.
- **Frontend/Backend** (optional): lauffähige Beispiele in `frontend-starter/` (Next.js 16) und `backend-example/` (FastAPI), Details in deren README.
