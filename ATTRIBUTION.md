# Attribution und Drittanbieter-Lizenzen

Diese Vorlage für das AI Automation Bootcamp nutzt und bündelt Arbeit von Romuald Członkowski (n8n-mcp / n8n-skills). Vielen Dank!

## Grundlage / Inspiration
- Die Idee und Grundlage dieser Starter-Vorlage stammt von **snipKI**: https://snipki.de

## n8n-mcp (MCP-Server)
- Quelle: https://github.com/czlonkowski/n8n-mcp
- Wird zur Laufzeit via `npx -y n8n-mcp` geladen (nicht in diesem Repository enthalten).

## Gebündelte n8n-Skills (vendored)
Die folgenden Skills unter `.claude/skills/` stammen **unverändert** aus dem Projekt
[`czlonkowski/n8n-skills`](https://github.com/czlonkowski/n8n-skills) und stehen unter MIT-Lizenz:

`n8n-code-javascript`, `n8n-code-python`, `n8n-expression-syntax`,
`n8n-mcp-tools-expert`, `n8n-node-configuration`, `n8n-validation-expert`,
`n8n-workflow-patterns`

**Update:** Diese Skills sind ein Snapshot. Aktuelle Version bei Bedarf aus
`czlonkowski/n8n-skills` (`skills/*`) nachziehen.

```
MIT License

Copyright (c) 2025 Romuald Członkowski

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## grill-me (Skill)
Der Skill `.claude/skills/grill-me/` ist **adaptiert** von
[mattpocock/skills](https://github.com/mattpocock/skills) (`grilling` + `grill-me`)
und steht unter MIT-Lizenz:

```
MIT License

Copyright (c) 2026 Matt Pocock

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## Eigene Skills und Code
Alle übrigen Skills (`idee-klaeren`, `m365-google-freigaben`, `meetingnotizen`,
`mail-triage-entwuerfe`, `bericht-zeitgesteuert`, `terminkoordination`,
`daten-visualisieren`, `praesentation`, `n8n-dokumentation`, `n8n-testdaten`,
`n8n-pruefbericht`, `n8n-security-audit`, `frontend-build`, `frontend-scaffold`,
`backend-fastapi`) sowie `frontend-starter/` und `backend-example/` stehen unter der
MIT-Lizenz dieses Repositorys (siehe `LICENSE`).

## Bewusst nicht enthalten
Die Dokument-Skills von Anthropic für PowerPoint, Word und Excel (`pptx`, `docx`, `xlsx`
aus [anthropics/skills](https://github.com/anthropics/skills)) stehen unter einer
proprietären Lizenz. Sie sind nicht Teil dieses Repositorys, und nichts hier ist daraus
abgeleitet.
