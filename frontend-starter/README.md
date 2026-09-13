# Frontend-Starter (Next.js 16 + React 19 + Tailwind 4)

Minimaler, lauffähiger Starter für Oberflächen im AI Automation Bootcamp.

## Start
**Am einfachsten:** Sag Claude *„Starte mein Frontend.“* Claude übernimmt `npm install`, startet den Dev-Server im Hintergrund und gibt dir die URL **`http://localhost:3000`**. Du musst nichts tippen.

Manuell geht es natürlich auch:
```bash
npm install
cp .env.local.example .env.local   # NEXT_PUBLIC_N8N_BASE eintragen
npm run dev                        # http://localhost:3000
```

## Was ist drin?
- **`/` (Muster A, n8n-Webhook):** Formular → POST an `${NEXT_PUBLIC_N8N_BASE}/webhook/${NEXT_PUBLIC_HELLO_PATH}` (ohne Angabe: `hello`).
  Baue dazu in n8n den Workflow aus `../examples/workflows/hello-webhook.json`. Auf der zentralen Bootcamp-n8n gilt ein Webhook-Pfad für alle, deshalb den Pfad mit eigenem Kürzel wählen (z. B. `anna-hello`) und in `.env.local` bzw. beim Veröffentlichen `NEXT_PUBLIC_HELLO_PATH=anna-hello` setzen.
- **`/chat` (Muster C, KI-Chat, optional):** Token-Streaming von Claude über das AI SDK (Paket `ai`).
  Braucht `ANTHROPIC_API_KEY` **und** `CHAT_ENABLED=true` in `.env.local`. Siehe Warnung unten.

## ⚠️ Warnung: `/api/chat` ist ein offener KI-Proxy
`app/api/chat/route.ts` leitet Chat-Nachrichten **ohne Login** an Claude weiter.

- Der Chat ist deshalb **standardmäßig aus** und läuft nur mit `CHAT_ENABLED=true`.
- **Lokal** (`localhost`) ist das in Ordnung.
- **Öffentlich veröffentlicht** mit `ANTHROPIC_API_KEY` und `CHAT_ENABLED=true` kann **jede Person, die die Adresse kennt**, auf Kosten des Keys chatten und das Ausgabelimit aufbrauchen. Die eingebauten Grenzen (Anfragegröße, Anzahl Nachrichten, Antwortlänge) dämpfen Missbrauch nur.
- Deshalb beim Veröffentlichen **keinen `ANTHROPIC_API_KEY`** und kein `CHAT_ENABLED=true` mitgeben, solange die App keinen Schutz (Login, Zugangscode) hat. Für KI im Bootcamp ist **n8n** der Normalfall (KI-Nodes mit der Credential „Anthropic“), das Frontend ruft dann nur den n8n-Webhook auf.

## Struktur
```
app/page.tsx          Webhook-Formular (Muster A)
app/chat/page.tsx     KI-Chat (Muster C)
app/api/chat/route.ts Streaming-Endpoint (Muster C, ohne Login, standardmäßig aus)
lib/n8n.ts            Webhook-Helper
lib/ai/model.ts       LLM-Provider und Modell (Anthropic)
.env.local.example    Liste der Env-Variablen (Platzhalter)
```

## Veröffentlichen
Lokal reicht `npm run dev`. Für eine öffentliche EU-Adresse (`https://app-xxxx.buildbar.at`) sag Claude *„Stell mein Frontend online.“* Claude veröffentlicht die App über `deploy-oew.buildbar.at` aus deinem privaten GitHub-Repository (Ablauf in `../CLAUDE.md`). Vorher muss `npm run build` grün sein.

- `env` beim Veröffentlichen: nur öffentliche Werte wie `NEXT_PUBLIC_N8N_BASE`, `NEXT_PUBLIC_HELLO_PATH`, `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`. Alles mit `NEXT_PUBLIC_` landet im Browser-Code.
- Nie ins Repository oder in `env`: Supabase-`service_role`-Key, n8n-API-Key, Bootcamp-Passwort und ohne Schutz auch kein KI-Schlüssel.

Backend-Logik gehört nach n8n (Muster A). Für eigene Rechen- oder Datenbanklogik siehe `../backend-example/`.
