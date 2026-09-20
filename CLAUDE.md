# AI Automation Bootcamp: Desktop-Vorlage (Claude Code + n8n)

Diese Datei lädt Claude Code beim Öffnen des Projekts automatisch. Sie enthält die Arbeitsweise, die Bootcamp-Regeln und die wichtigsten n8n-Konventionen. **Einrichtung noch nicht erledigt?** Dann zuerst das Runbook in [README.md](README.md) abarbeiten.

## Worum geht es?
Das **AI Automation Bootcamp** ist ein Bootcamp der **Österreich Werbung (ÖW)** in Kooperation mit **buildbar**: 21. bis 24.09.2026 bei der ÖW in Wien, Trainer Friedemann Schütz. Die Teilnehmenden kommen aus Tourismusorganisationen (LTOs, DMOs, TVBs, Kulturbetriebe). **Jede:r arbeitet am eigenen Vorhaben** aus dem eigenen Berufsalltag.

Am Ende hat jede Person:
1. eine **erste funktionierende Workflow-Lösung** in n8n,
2. ein **eigenes Code-Repository** (privat, auf dem eigenen GitHub-Konto),
3. einen **klaren nächsten Schritt** für die eigene Organisation.

Ablauf: **Tag 1** Planung im Sparring mit der KI (Skills `idee-klaeren` und `grill-me`). **Ab Tag 2** Umsetzung. **Tag 4** Feinschliff, Tests, Dokumentation, Repository aufräumen und Ergebnisse vorstellen.

**Desktop-Variante:** Claude Code läuft lokal auf dem Rechner der Person. n8n ist über den MCP-Server `n8n-mcp` angebunden, der per `npx` lokal startet (stdio). n8n-URL und API-Key stehen in der eigenen `.mcp.json`. Diese Datei ist gitignored und gelangt nie ins Repository.

## Arbeitsweise (so verhältst du dich)
- **Zielgruppe:** Touristiker:innen mit wenig oder keiner Code-Erfahrung. Erkläre in **einfacher Sprache**, ohne unerklärten Fachjargon, in der du-Form.
- **Ein Vorhaben pro Person, passend für vier Tage.** Lieber ein Ablauf, der wirklich läuft, als drei halbfertige.
- **Erst die Idee klären:** Ist die Person unsicher, beschreibt sie ihr Vorhaben vage oder geht es direkt nach der Einrichtung los, nutze **zuerst** den Skill `idee-klaeren` (freundliches Interview, Ergebnis: Prozess-Steckbrief). Biete das aktiv an. Hat jemand einen **fertigen Plan** und will ihn prüfen lassen („grill mich“), nimm den Skill `grill-me`, aber **nur auf ausdrücklichen Wunsch**.
- **Themen-Skills nutzen:** Passt das Vorhaben zu einem Bootcamp-Thema, lies vor dem Planen den passenden Skill (siehe [Themen-Skills](#themen-skills)).
- **Freigaben früh prüfen:** Braucht das Vorhaben Postfach, Kalender, Teams oder ein Google-Konto, kläre das am Tag 1 **vor dem Bauen** (siehe [Freigaben früh prüfen](#freigaben-früh-prüfen-microsoft-365-und-google)).
- **Sei proaktiv:** Führe den Standard-Prozess **selbstständig** durch. Frag nicht für jeden Schritt um Erlaubnis.
- **Nach jedem Workflow automatisch (ohne Nachfrage):** validieren, mit **Testdaten testen** (Skill `n8n-testdaten`), mit **Sticky Notes dokumentieren** (Skill `n8n-dokumentation`), **Security-Check** (Skill `n8n-security-audit`). Ist der Workflow fertig, zusätzlich einen kurzen **Prüfbericht** (Skill `n8n-pruefbericht`).
- **Silent Execution:** Werkzeuge ohne Zwischenkommentar ausführen, danach **kurz und verständlich** berichten, was gebaut, getestet und dokumentiert wurde.
- **Frontend zeigen = DU startest es:** Will die Person ihre App ansehen, übernimm das selbst: falls nötig `npm install`, dann `npm run dev` **im Hintergrund** starten und die URL **`http://localhost:3000`** nennen bzw. die Vorschau öffnen. Die Person tippt keine Befehle. Läuft der Server schon, nenn einfach die URL.
- **Event-Infos (Agenda, Zeiten, Ort, Ansprechpersonen, Themen):** Lies **https://buildbar.at/oew/claude.md** per WebFetch (reines Markdown, aktuell, ohne Zugangsdaten) und antworte daraus. Weitere Seiten: Event-Seite https://buildbar.at/oew, Themen https://buildbar.at/oew/themen, Grundlagen https://buildbar.at/oew/grundlagen, Anleitung Desktop https://buildbar.at/oew/starten/desktop.
- **Zugangsdaten** (zentrale n8n, KI-Zugang, Supabase, Bootcamp-Passwort) stehen nur im Zugangsbereich **https://buildbar.at/oew#zugang**. Den öffnet die Person selbst im Browser.
- **Vorrang:** Beschreibt ein Skill einen anderen Hosting-Weg oder einen fremden Account, gelten im Bootcamp die Abläufe in dieser Datei.

## n8n-Zugang
- **Zentrale Bootcamp-n8n:** `https://n8n-oew.buildbar.at`. URL, Login und API-Key stehen im Zugangsbereich. Alle Teilnehmenden teilen sich **einen Login** und sehen **alle Workflows, Credentials und Data Tables**. Daher gilt:
  - Alles, was du anlegst, bekommt den **Vornamen der Person als Präfix**: Workflows (`Anna: Anfragen sortieren`), Credentials (`Anna Gmail`), Data Tables (`anna_anfragen`), Webhook- und Formularpfade (`anna-anfragen`). Ausnahme: das gemeinsame Credential „Anthropic“. Es gibt genau eines, nicht neu anlegen, wenn es schon existiert. In Skills und Beispiel-Workflows heißt dieses Präfix „Kürzel“ (Platzhalter wie `kuerzel`, `<kürzel>`, `DEIN-KUERZEL`, Beispiel `mk`): Dort überall den Vornamen der Person einsetzen.
  - **Importe und Vorlagen** bekommen dasselbe Präfix: Beispiele aus `examples/workflows/` und Vorlagen aus `n8n_deploy_template` (Parameter `name`) sofort umbenennen (z. B. `Anna: hello-webhook`) und Webhook- und Formularpfade ändern (z. B. `anna-hello`), bevor du aktivierst. Sonst kollidieren die Pfade mit den Workflows anderer, und Testaufrufe landen bei fremden Workflows.
  - **Nie** Workflows, Credentials oder Data Tables anderer Personen ändern, aktivieren, deaktivieren oder löschen. Listen immer auf das eigene Präfix filtern.
  - **Vor jedem Ändern oder Löschen** (Workflow-Update, Autofix, Data Table, Zeilen, Spalten, Ausführungen) den Namen des Ziels holen und prüfen, dass er mit dem Vornamen der Person beginnt. Stimmt das Präfix nicht, nichts tun und nachfragen. Data-Table-Aktionen, Ausführungen und das Löschen von Workflows bestätigt die Person per Klick.
  - Keine echten personenbezogenen Daten und keine privaten Passwörter in die zentrale n8n. Jede:r mit dem gemeinsamen Login kann dort hinterlegte Credentials verwenden. Für Konten deshalb Testkonten oder Beispieldaten nehmen.
  - Zeitgesteuerte Workflows nicht im Minutentakt laufen lassen und nach dem Testen wieder deaktivieren, wenn sie nicht dauerhaft laufen sollen.
- **Eigene n8n:** erlaubt, wenn sie einen **API-Zugang** hat (Key in n8n unter Settings, n8n API, Create API Key).
- **Nicht geeignet:** die kostenlose **n8n-Cloud-Testversion**. Sie hat keinen API-Zugang, damit kann `n8n-mcp` nicht arbeiten.
- **Verbindung ändern:** URL und Key stehen in `.mcp.json` (`N8N_API_URL`, `N8N_API_KEY`). Nach einer Änderung muss die Person die App neu starten. Den Key nie ausgeben, nie in andere Dateien schreiben, nie committen.

## KI-Zugang (Anthropic)
- Für KI-Bausteine in n8n (z. B. Anthropic Chat Model am AI Agent) gibt es im Zugangsbereich einen **Anthropic-API-Key mit Ausgabelimit**. In n8n gehört er in ein Credential mit dem Namen **„Anthropic“**.
- Prüfe zuerst, ob das Credential „Anthropic“ in der n8n schon existiert, und verwende es. Fehlt es, trägt die Person den Key im n8n-Editor selbst als Credential ein (Typ Anthropic, Name „Anthropic“).

## OpenAI (Embeddings, Sprache zu Text, Text zu Sprache)

- Auf der zentralen Bootcamp-n8n liegt ein Credential **„OpenAI“**. Es deckt drei Dinge ab, die Anthropic nicht kann:
  - **Embeddings** für die Vektorsuche (`text-embedding-3-small`, 1536 Zahlen — passt genau zur Tabelle `documents` in der ÖW-Supabase). Rezept in `docs/datenbank.md`, fertiges Beispiel in `examples/workflows/wissensbasis-supabase.json`.
  - **Sprache zu Text** (`whisper-1`, `gpt-4o-transcribe`): aus einer Audiodatei ein Transkript machen, etwa für Meeting-Notizen.
  - **Text zu Sprache** (`tts-1`): aus Text eine Audiodatei.
- **Für das Schreiben von Texten bleibt Anthropic der Normalfall.** OpenAI ist für die drei Sachen oben da, nicht als zweites Chat-Modell.
- ⚠️ **Audiodateien sind personenbezogen.** Wer eine Besprechung aufnimmt, braucht die Zustimmung aller Beteiligten, und das Transkript gehört danach an einen Ort mit Loeschfrist. Die Aufnahme selbst sollte den Ablauf nicht überleben: transkribieren, Datei löschen, nur den Text behalten.

## Google-Daten (DataForSEO)

- Auf der zentralen Bootcamp-n8n liegt ein Credential **„DataForSEO“** (Typ *Basic Auth*). Damit lassen sich **Google-Einträge** abfragen: Öffnungszeiten, Adresse, Telefon, Bewertungen, Kategorien.
- Verwendung: **HTTP Request**-Node auf `https://api.dataforseo.com/v3/business_data/google/my_business_info/live`, Methode POST, Authentifizierung *Predefined Credential Type* → *Basic Auth* → „DataForSEO“.
- ⚠⚠ **Jede Abfrage kostet echtes Geld**, rund **0,005 USD je Betrieb**. Das ist der einzige Baustein im Bootcamp, bei dem das so ist. Deshalb:
  - **Zuerst mit genau einem Betrieb testen**, nicht mit einer Liste.
  - Vor einem Lauf über viele Betriebe kurz überschlagen: 100 Betriebe täglich sind rund 19 USD im Monat, stündlich sind es rund 400.
  - Keine Schleife über eine ganze Tabelle bauen, ohne die Zeilenzahl vorher zu begrenzen.
- **Land setzen.** Ohne `location_name` sucht der Dienst in Deutschland. Für Österreich `"location_name": "Austria"` mitgeben, besser zusätzlich `latitude`/`longitude`. Sonst trifft er bei gleichnamigen Hütten den falschen Betrieb — und meldet keinen Fehler.
- Der Dienst **liest nur**. Ein Google-Eintrag lässt sich darüber nicht ändern; dafür bräuchte es die Google-Business-Profile-API und eine Rolle im jeweiligen Eintrag.

- Der Key gehört **nie** in Workflow-Parameter, Code-Nodes, Frontend (auch nicht lokal in `.env.local`), Deploy-`env` oder das Repository.
- Das Budget des Schlüssels ist begrenzt: mit wenigen, kleinen Beispielen testen statt mit großen Datenmengen.

## Freigaben früh prüfen (Microsoft 365 und Google)
Viele Vorhaben scheitern nicht an n8n, sondern an fehlenden Freigaben. Kläre das deshalb **am Tag 1 im Steckbrief, bevor gebaut wird**, mit dem Skill `m365-google-freigaben`. Fehlt der Skill, nutze die Fakten in diesem Abschnitt.
- **Outlook-Postfach und Kalender (Microsoft 365):** In Standard-Tenants (von Microsoft empfohlene Consent-Policy) braucht der Zugriff eine **Admin-Freigabe** der IT.
- **Teams (Teams-Node, Teams-Transkripte):** braucht **immer** eine Admin-Freigabe (Admin-Consent).
- **IMAP mit Passwort** ist bei Exchange Online abgeschaltet und daher kein Ausweg.
- **Google (Gmail, Kalender, Drive, Sheets, Slides):** Auf einer selbst gehosteten n8n (wie der Bootcamp-n8n) braucht es eine **eigene OAuth-App**. Steht sie im Status „Testing“, laufen die Refresh-Tokens **nach 7 Tagen** ab.
- **Bis die Freigabe da ist:** mit Beispieldaten, Datei-Upload oder n8n-Formular bauen, sodass später nur die Anbindung getauscht wird. Offene Freigaben kommen als nächster Schritt in die README.

## Themen-Skills
Für die sechs Bootcamp-Themen gibt es eigene Skills. Lies den passenden Skill, sobald ein Vorhaben in die Richtung geht:

| Thema | Skill |
|-------|-------|
| Meetingnotizen strukturieren | `meetingnotizen` |
| E-Mail-Anfragen sortieren und Antwortentwürfe vorbereiten | `mail-triage-entwuerfe` |
| Wiederkehrende Berichte erstellen | `bericht-zeitgesteuert` |
| Terminfindung und Koordination erleichtern | `terminkoordination` |
| Daten analysieren und visualisieren | `daten-visualisieren` |
| Präsentationen effizienter erstellen | `praesentation` |
| Freigaben für Microsoft 365 und Google klären | `m365-google-freigaben` |

Zu jedem Thema gibt es einen importierbaren Beispiel-Workflow unter `examples/workflows/` (der Skill nennt die Datei). Auf der zentralen Bootcamp-n8n beim Import Namen und Pfade mit dem Vornamen versehen (siehe [n8n-Zugang](#n8n-zugang)).

Fehlt ein Skill unter `.claude/skills/`, nimm die Themenbeschreibung aus https://buildbar.at/oew/claude.md bzw. https://buildbar.at/oew/themen als Grundlage.

Gut zu wissen: n8n hat **keinen PowerPoint-Node**. Für Folien gibt es den **Google Slides Node** (u. a. Replace Text in einer Vorlage).

## Workflow-Erstellung: Standard-Prozess
Diesen Ablauf führst du **automatisch** durch (Schritte 6 bis 9 und 11 ohne Extra-Aufforderung):

1. `tools_documentation()`: Best Practices laden
2. `search_templates({query: "..."})`: passende Vorlage prüfen
3. Passt eine Vorlage: `n8n_deploy_template({templateId, name: "<Vorname>: <Titel>"})`, **Autor nennen**. Auf der zentralen Bootcamp-n8n danach Webhook- und Formularpfade mit dem Vornamen versehen.
4. Sonst: `search_nodes()` → `get_node({detail: "standard"})` → `n8n_create_workflow()`
5. Iterativ erweitern: `n8n_update_partial_workflow({id, intent, operations})`
6. Validieren: `n8n_validate_workflow({id})` → `n8n_autofix_workflow({id})`
7. Testdaten generieren und **in der Instanz testen**. Das fängt Laufzeitfehler, die der statische Validator nicht sieht (Skill `n8n-testdaten`)
8. **Workflow dokumentieren** mit Sticky Notes (Skill `n8n-dokumentation`)
9. Security-Checkliste (Skill `n8n-security-audit`)
10. Aktivieren: `n8n_update_partial_workflow({operations: [{type: "activateWorkflow"}]})`
11. **Prüfbericht** erstellen, sobald der Workflow fertig ist (Skill `n8n-pruefbericht`)

## Kritische Konventionen

### nodeType-Formate (je nach Tool unterschiedlich!)
| Tool-Kategorie | Format | Beispiel |
|---------------|--------|----------|
| Search/Validate | `nodes-base.*` | `nodes-base.slack` |
| Workflow-Tools | `n8n-nodes-base.*` | `n8n-nodes-base.slack` |
| AI/LangChain | `@n8n/n8n-nodes-langchain.*` | `@n8n/n8n-nodes-langchain.agent` |

### Webhook-Datenstruktur
Webhook-Daten liegen unter `.body`:
```
FALSCH:  {{$json.email}}
RICHTIG: {{$json.body.email}}
```

### Expression-Syntax
- Expressions immer mit `{{}}`: `{{$json.field}}`
- In **Code Nodes KEIN** `{{}}`: `$json.field`
- Node-Namen mit Leerzeichen in Quotes: `{{$node["HTTP Request"].json.data}}`
- Node-Namen sind case-sensitive

### IF-Node Multi-Output Routing (KRITISCH!)
IF-Nodes haben zwei Outputs. `branch` setzen, sonst landen beide Connections am selben Output:
```json
{type: "addConnection", source: "If", target: "True Handler", sourcePort: "main", targetPort: "main", branch: "true"}
{type: "addConnection", source: "If", target: "False Handler", sourcePort: "main", targetPort: "main", branch: "false"}
```
Switch-Node: `case: 0`, `case: 1`, …

### addConnection-Syntax (vier separate String-Parameter!)
```json
{ "type": "addConnection", "source": "Webhook", "target": "Slack", "sourcePort": "main", "targetPort": "main" }
```
`removeConnection` hat dasselbe Format.

### AI-Workflow-Connections
Für LangChain/AI-Nodes `sourceOutput` nutzen: `ai_languageModel`, `ai_tool`, `ai_memory`, `ai_embedding`, `ai_vectorStore`, `ai_outputParser`, `ai_document`, `ai_textSplitter`.

⚠️ **AI-Tool-Node-Namen:** Der Name eines als Tool verbundenen Nodes (`ai_tool`) wird zum **Funktionsnamen fürs LLM**. Daher **nur Buchstaben, Ziffern und Unterstriche** (kein Leerzeichen, Bindestrich, keine Klammer, kein Umlaut, nicht mit Ziffer beginnen). Beispiel: `hello_webhook_aufrufen`, nicht „hello-webhook aufrufen“.

⚠️ **AI-Sub-Nodes haben kein „Execute“:** Tool-, Modell- und Memory-Nodes laufen **nur, wenn der Agent sie aufruft**. Den Workflow über den **Chat** starten, **nicht** einen Sub-Node einzeln per „Test step“ ausführen (sonst Fehler „has a supplyData method but no execute method“).

⚠️ **HTTP-Tool für Agents:** den **regulären HTTP Request als Tool** verwenden (`n8n-nodes-base.httpRequestTool`, v4.x) mit `$fromAI('feld','Beschreibung','string')` für Werte, die das LLM füllt. **Nicht** den Legacy-Node `@n8n/n8n-nodes-langchain.toolHttpRequest` (v1.1, deprecated). Fast jeder Standard-Node kann als Tool an den Agent gehängt werden.

### Ein grüner Lauf ist kein Beweis

Die teuersten Fehler in n8n melden **keinen Fehler**. Der Ablauf läuft durch, ist
grün, und das Ergebnis ist trotzdem falsch. Beim Vorabbau der Bootcamp-Use-Cases
waren das **neun von dreizehn** gefundenen Stolperstellen.

**Deshalb nach jedem Abruf prüfen, ob das ERWARTETE Ergebnis da ist**, nicht ob der
Aufruf funktioniert hat:

```javascript
const zeilen = $input.all();
if (zeilen.length < ERWARTET) {
  throw new Error('Nur ' + zeilen.length + ' statt ' + ERWARTET + '. Nicht weiterarbeiten.');
}
```

Diese fünf kosten sonst je eine halbe Stunde Suche (alle am 19.09.2026 gemessen):

| Wo | Was still passiert |
|---|---|
| **HTTP-Node, Query-Parameter** | Ein Parameter lässt sich **nicht mehrfach** senden. Wer `parameters=a`, `parameters=b` einzeln anlegt, sendet nur den letzten. Als Komma-Liste schreiben: `parameters=a,b` |
| **Datei-Upload** | n8n hängt einen **Index** an den Feldnamen: hochgeladen als `datei`, angekommen als `datei0`. Und die Endung wird aus dem **MIME-Typ** geraten, nicht aus dem Namen — `report.xlsx` kann als `bin` ankommen |
| **PDF einlesen** | Ein **eingescanntes** PDF hat keine Textebene. `extractFromFile` liefert einen leeren String, ohne zu scheitern. Auf Mindestlänge prüfen |
| **Leeres Ergebnis** | **0 Items stoppen die ganze Kette.** Ein korrekt leeres Ergebnis (etwa: kein Feiertag in dieser Woche) sieht dann aus wie ein Absturz. `alwaysOutputData` setzen |
| **Zählfelder von APIs** | Felder wie `total_rows` meinen oft den **Gesamtbestand**, nicht die Treffer der Abfrage. Nie als Trefferzahl lesen, immer die Liste selbst zählen |

**Und für Logik, die man prüfen kann:** erst ausserhalb von n8n testen, dann
einbauen. n8n speichert kaputten Code stillschweigend, der Fehler kommt zur
Laufzeit — und vor Publikum ist das der schlechteste Zeitpunkt.

### Mailversand: Brevo, nicht SMTP

**Mailversand funktioniert.** Das Credential **„Brevo"** liegt auf der zentralen Bootcamp-n8n
und ist einsatzbereit. Nimm den Node **`n8n-nodes-base.sendInBlue`** (heisst im Editor „Brevo"),
`resource: "email"`, `operation: "send"`:

```
sender        <Absender aus dem Zugangsbereich>  (muss in Brevo verifiziert sein)
receipients   empfaenger@example.com           (Achtung: n8n schreibt das Feld falsch,
                                                mit "ei" statt "i" — receipients)
subject       {{ $json.betreff }}
textContent   {{ $json.bericht }}
sendHTML      false, oder true für HTML
```

Kontingent: **300 Mails pro Tag**, für das Bootcamp reichlich.

⚠️ **Nimm nicht den Node „Send Email".** Der spricht SMTP, und die Ports 25, 465 und 587 sind
auf dem Server gesperrt (wie bei fast allen Hostern, gegen Spam-Versand). Der Node wartet
**240 Sekunden** und meldet dann nur `Connection timeout` — er sieht also nicht nach einem
Konfigurationsfehler aus, sondern nach einem hängenden Workflow. Brevo läuft über HTTPS und
hat das Problem nicht.

**Eigener Absender?** In Brevo muss jede Absenderadresse verifiziert sein. Wer eine eigene
verwenden will, trägt sie unter Senders ein und bestätigt die Mail. Für alles andere den
Absender aus dem Zugangsbereich nehmen.

**Ohne Versand geht es auch:** Ergebnis in eine Data Table schreiben oder den Webhook die
fertige Liste zurückgeben lassen und im Frontend anzeigen. Für Berichte, die jemand prüfen
soll, bevor sie rausgehen, eignet sich zusätzlich ein Outlook- oder Gmail-**Entwurf**
(`resource: "draft"`).

## Best Practices

### Do
- **Template-First:** immer Templates prüfen, bevor von Scratch gebaut wird
- **Explicit Parameters:** ALLE Parameter explizit setzen (Default-Werte sind die häufigste Fehlerquelle)
- Workflows **iterativ** bauen, `intent` bei Updates angeben
- Nach signifikanten Änderungen validieren, Validation-Profil `runtime`
- Batch-Operationen in **einem** `n8n_update_partial_workflow`-Call
- `includeExamples: true` für echte Konfigurationsbeispiele
- **Zahlen aus der Quelle:** Kennzahlen, Summen und Diagrammwerte rechnet n8n aus den echten Daten, nicht die KI

### Don't
- nodeType-Prefix vergessen
- Validation vor Aktivierung überspringen
- Expression-Syntax in Code Nodes verwenden
- **Code Nodes nutzen, wenn Standard-Nodes verfügbar sind** (Code ist der letzte Ausweg)
- Fremde Workflows auf der zentralen Bootcamp-n8n anfassen

## Datenbank und EU-Bausteine
Meistens braucht es keine externe Datenbank. Die Bausteine laufen auf EU-Infrastruktur, Zugangsdaten stehen im Zugangsbereich https://buildbar.at/oew#zugang:
- **n8n Data Tables** (Standard, in jeder n8n eingebaut, per MCP `n8n_manage_datatable`): für Daten, die zu einem Workflow gehören. Auf der zentralen n8n mit Namenspräfix.
- **NocoDB** (`https://nocodb.buildbar.at`): Tabellen im Browser, ähnlich wie Excel. Self-Service: Die Person legt dort einen eigenen Account und einen API-Token an, du bindest den Token als NocoDB-Credential in n8n ein.
- **ÖW-Supabase:** Postgres mit Login, Datei-Uploads und Vektorsuche. Project-URL, `anon`-Key und `service_role`-Key stehen im Zugangsbereich. Der **`service_role`-Key nur serverseitig** als Credential in n8n, **nie** im Frontend, in `env` für den Deploy oder im Repository. Das Frontend nutzt höchstens den `anon`-Key, und nur mit Row Level Security auf den Tabellen.

Details: `docs/datenbank.md`.

## App öffentlich veröffentlichen (EU-Adresse, ohne Hosting-Account)
Lokal zeigst du die App auf `http://localhost:3000`. Will die Person eine **öffentliche Adresse** („stell mein Frontend online“, „veröffentliche meine App“), gehst **du** so vor. Die Person tippt keine Befehle.

**Voraussetzungen:** GitHub-CLI angemeldet (`gh auth status`, sonst `gh auth login` mit Browser-Login durch die Person). Das Projekt liegt im **eigenen privaten Repository** (siehe [Dein Repository zum Mitnehmen](#dein-repository-zum-mitnehmen-ergebnis-regel)). `npm run build` im Frontend-Ordner ist grün. Das **Bootcamp-Passwort** steht im Zugangsbereich https://buildbar.at/oew#zugang, die Person schreibt es dir in den Chat. Schreib es nie in eine Datei.

1. Aktuellen Stand committen und pushen: `git push`. Vorher mit `git remote get-url origin` prüfen, dass `origin` auf das eigene private Repository zeigt und nicht auf die Vorlage `freddy-schuetz/oew-ai-automation-bootcamp`. Zeigt es noch auf die Vorlage, zuerst das eigene Repository anlegen (siehe [Dein Repository zum Mitnehmen](#dein-repository-zum-mitnehmen-ergebnis-regel), Schritt 6).
2. Deploy vorbereiten:
   ```bash
   curl -s -X POST https://deploy-oew.buildbar.at/prepare -d repo=<owner>/<name> --data-urlencode password=<BOOTCAMP-PASSWORT>
   ```
   Antwort: `deployId` und `public_key`.
3. Den Public Key als **read-only Deploy-Key** ans private Repository hängen (die Person bestätigt den Aufruf per Klick):
   ```bash
   gh api repos/<owner>/<name>/keys -f title=buildbar-deploy -f key='<public_key>' -F read_only=true
   ```
4. Veröffentlichen:
   ```bash
   curl -s -X POST https://deploy-oew.buildbar.at/publish -d deployId=<deployId> -d base_dir=/frontend-starter --data-urlencode password=<BOOTCAMP-PASSWORT> --data-urlencode env=$'NEXT_PUBLIC_N8N_BASE=https://n8n-oew.buildbar.at\nNEXT_PUBLIC_SUPABASE_URL=...'
   ```
   Antwort: die URL, z. B. `https://app-xxxx.buildbar.at`. **Der erste Build dauert einige Minuten.**

- `base_dir` ist der Frontend-Ordner im Repository (Standard `/frontend-starter`). `env` enthält eine Zeile `KEY=VALUE` je Variable.
- ⚠️ **`NEXT_PUBLIC_*`-Werte landen im Browser-Code** und sind damit öffentlich: nur n8n-URL, Supabase-URL und Supabase-`anon`-Key. **Nie** in `env` oder ins Repository: `service_role`-Key, KI-Schlüssel, n8n-API-Key, Bootcamp-Passwort.
- ⚠️ **Offener KI-Proxy im Frontend-Starter:** `frontend-starter/app/api/chat/route.ts` leitet Chat-Nachrichten **ohne Login** an Anthropic weiter. Er ist deshalb standardmäßig **aus** und läuft nur mit `CHAT_ENABLED=true`; eingebaute Grenzen dämpfen Missbrauch nur. Lokal ist das in Ordnung. Wird die App mit `ANTHROPIC_API_KEY` und `CHAT_ENABLED=true` veröffentlicht, kann **jede Person, die die Adresse kennt**, den Schlüssel über die App nutzen und das Ausgabelimit aufbrauchen. Deshalb beim Veröffentlichen ohne Schutz (Login, Zugangscode) **weder `ANTHROPIC_API_KEY` noch `CHAT_ENABLED=true`** in `env` (erst recht nicht den Bootcamp-KI-Schlüssel), und die KI-Funktion lieber über einen n8n-Workflow laufen lassen. Weise die Person darauf hin, bevor du veröffentlichst.

## Dein Repository zum Mitnehmen (Ergebnis-Regel)
Am Ende des Bootcamps liegt **alles** im **eigenen privaten GitHub-Repository** der Person. Das ist Teil des Ergebnisses, nicht optional. Lege das Repository **früh** an (spätestens, sobald der erste Workflow läuft), pushe nach jedem Meilenstein und räume es am Tag 4 gemeinsam mit der Person auf. Die Person tippt keine Befehle.

1. **GitHub-Login:** `gh auth status`. Nicht angemeldet: `gh auth login` starten, die Person bestätigt im Browser. Fehlt `gh`: Windows `winget install --id GitHub.cli`, macOS `brew install gh`, danach App neu starten.
2. **Workflows exportieren:** Jeden Workflow der Person mit `n8n_get_workflow({id, mode: "full"})` holen und als JSON unter `workflows/<kurzer-name>.json` speichern. Vor dem Speichern nur `name`, `nodes`, `connections` und `settings` behalten. `pinData`, `id`, `versionId`, `activeVersionId`, `shared`, `meta` und `tags` entfernen, bei `credentials` in den Nodes nur den Namen lassen und die `id` löschen. Keys oder Passwörter in Parametern ebenfalls entfernen. Beim Import in eine andere n8n werden Credentials ohnehin neu zugeordnet.
3. **README schreiben:** Ersetze den Vorlagen-Text in `README.md` durch eine README zum eigenen Vorhaben: welches Problem es löst, welche Workflows es gibt (Dateien unter `workflows/`), welche Credentials und Freigaben nötig sind, wie man die Workflows in eine andere n8n importiert, aktueller Stand und Grenzen und zum Schluss **„Nächster Schritt“**: ein konkreter Schritt für die Organisation (z. B. „IT um Admin-Freigabe für das Postfach bitten“ oder „Workflow in die n8n der Organisation übernehmen“). Der Prüfbericht darf als `docs/pruefbericht.md` dazu.
4. **Vor dem Commit prüfen:** `git status`. `.mcp.json`, `.env.local` und `backup/` dürfen nicht auftauchen (sind gitignored). Keine Keys, keine Passwörter, keine echten personenbezogenen Daten im Repository.
5. **Commit:** `git add -A` und `git commit -m "<kurze Beschreibung>"`. Fragt git nach Name und E-Mail, frag die Person und setze beides mit `git config user.name` und `git config user.email` nur für dieses Repository.
6. **Privates Repository anlegen und pushen:** Der Klon zeigt noch auf die öffentliche Vorlage. Deshalb zuerst `git remote rename origin vorlage`, dann:
   ```bash
   gh repo create ai-automation-bootcamp --private --source=. --remote=origin --push
   ```
   Ist der Name schon vergeben (z. B. weil die Person auch den Browser-Weg genutzt hat), frag nach einem anderen Namen. Danach reicht `git push`.
7. **Link nennen** und kurz zeigen, wo Workflows und README liegen.

## Sicherheit
1. **API-Keys niemals** in Workflow-Parametern: n8n **Credentials** nutzen!
2. Security-Checkliste vor Aktivierung (Skill `n8n-security-audit`)
3. Keine personenbezogenen Daten in Node-Namen, Sticky Notes, Testdaten oder im Repository
4. `.mcp.json`, `.env*`, `.codex/config.toml` und `opencode.json` bleiben lokal (gitignored). Nie committen, nie ausgeben.
5. Offener KI-Proxy in `frontend-starter/app/api/chat/route.ts`: siehe Warnung im Abschnitt zum Veröffentlichen
6. **Lizenz:** Die Dokument-Skills von Anthropic (pptx, docx, xlsx aus `anthropics/skills`) sind proprietär lizenziert. **Nicht** kopieren, nicht nachbauen, nichts daraus ableiten.
7. Workflow-Änderungen werden automatisch nach `backup/` gesichert (Hook, lokal, gitignored)

## Geladene Skills
**Am Anfang (Tag 1):** `idee-klaeren` klärt Idee und Prozess und macht daraus einen Bau-Auftrag (Steckbrief), Ideen-Menü in `docs/tourismus-ideen.md` · `grill-me` ist der Härtetest für einen **fertigen** Plan, **nur auf ausdrücklichen Wunsch** („grill mich“) · `m365-google-freigaben` prüft früh, welche Freigaben das Vorhaben braucht.
**Themen:** `meetingnotizen`, `mail-triage-entwuerfe`, `bericht-zeitgesteuert`, `terminkoordination`, `daten-visualisieren`, `praesentation`
**n8n:** `n8n-mcp-tools-expert`, `n8n-workflow-patterns`, `n8n-node-configuration`, `n8n-expression-syntax`, `n8n-validation-expert`, `n8n-code-javascript`, `n8n-code-python` (von czlonkowski/n8n-skills) · `n8n-testdaten`, `n8n-dokumentation`, `n8n-security-audit`, `n8n-pruefbericht`
**Frontend/Backend (optional):** `frontend-build`, `frontend-scaffold`, `backend-fastapi`, lauffähige Beispiele in `frontend-starter/` und `backend-example/`.
