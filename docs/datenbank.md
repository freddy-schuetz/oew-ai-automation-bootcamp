# 🗄️ Brauche ich eine Datenbank? Niederschwellig zuerst

Kurz: **Meistens brauchst du keine externe Datenbank.** Wähle danach, *wo die Daten leben*:

| Fall | Lösung | Aufwand |
|------|--------|---------|
| Daten gehören zu einem **n8n-Workflow** | **n8n Data Tables** | ⭐ keiner (eingebaut) |
| **Tabellen im Browser**, ähnlich wie Excel | **NocoDB** (`nocodb.buildbar.at`, EU) | niedrig (eigener Account und Token) |
| **Login, Datei-Uploads, Suche in Dokumenten, veröffentlichte App** | **ÖW-Supabase** (EU) | niedrig (Zugangsdaten aus dem Zugangsbereich) |
| **Lokaler Prototyp** oder ein einzelner Backend-Prozess mit Volume | **SQLite** | keiner (eine Datei) |

> Zugangsdaten für die Bootcamp-Bausteine (zentrale n8n, KI-Zugang, Supabase) stehen im **Zugangsbereich https://buildbar.at/oew#zugang**. Das Passwort gibt es im Online-Kick-off.

---

## 1. n8n Data Tables: Standard für Workflows

In **jeder n8n eingebaut**. Keine Anmeldung, kein Connection-String, kein eigener Server.

- Tabellen mit Spalten anlegen und aus Workflows **lesen, schreiben, aktualisieren, löschen** (Node **„Data Table“**), oder Claude macht es per MCP (`n8n_manage_datatable`).
- Der Speicherplatz ist begrenzt: gut für Listen, Status und Zwischenergebnisse, nicht für große Dateien oder Massendaten.
- Ideal für: Lookups, Status merken, kleine Listen, Duplikate erkennen, Zwischenspeicher.
- Sag zu Claude: *„Leg eine Data Table für Anfragen mit den Spalten name, email und status an und schreib im Workflow neue Einträge hinein.“*
- ⚠️ **Zentrale Bootcamp-n8n:** Alle Teilnehmenden sehen alle Data Tables. Tabellen mit deinem Vornamen benennen (z. B. `anna_anfragen`), nur eigene Tabellen ändern und keine echten personenbezogenen Daten speichern.
- Winziger Zustand ohne Tabelle: n8n **Workflow Static Data** (Schlüssel und Werte).

→ **Für die allermeisten n8n-Vorhaben ist das der richtige und einfachste Weg.**

## 2. NocoDB: Tabellen im Browser

Für „Claude, speicher das in einer Tabelle, die ich im Browser sehe und bearbeite“. EU-Instanz unter **https://nocodb.buildbar.at**.

- **Self-Service:** Dort legst du dir einen **eigenen Account und einen API-Token** an. Claude bindet den Token als **NocoDB-Credential** in n8n ein (Node „NocoDB“).
- Ideal für: Anfragen oder Anmeldungen sammeln, Listen, die Kolleg:innen im Browser pflegen sollen.
- Gemeinsam genutzte Instanz: **eigene Tabellen**, keine echten personenbezogenen Daten.

## 3. ÖW-Supabase: Login, Uploads, Suche in Dokumenten

Wenn eine **veröffentlichte App** und/oder **mehrere Dienste** eine gemeinsame Postgres-Datenbank brauchen, oder du **Login**, **Datei-Uploads** oder **Vektorsuche (pgvector, Suche nach Sinn statt Stichwort)** willst.

- **Zugangsdaten** (Project-URL, `anon`-Key, `service_role`-Key) stehen im **Zugangsbereich https://buildbar.at/oew#zugang**. Keine eigene Anmeldung nötig.
- **n8n:** Node **„Supabase“** mit Project-URL und `service_role`-Key als Credential.
- **Next.js:** `@supabase/supabase-js` mit Project-URL und **nur dem `anon`-Key** (als `env` beim Veröffentlichen, nie im Repository).
- **FastAPI (optional):** Zugriff serverseitig mit Project-URL und Key, nie aus dem Browser.
- ⚠️ **`service_role`-Key nur serverseitig** in n8n: **nie** im Frontend, nie in `env` beim Veröffentlichen, nie im Repository. Er umgeht alle Zugriffsregeln.
- ⚠️ Tabellen, die ein Frontend mit dem `anon`-Key liest oder schreibt, brauchen **Row Level Security** mit passenden Regeln. Sonst kann jede Person mit dem Key alles lesen und ändern.
- Gemeinsam genutzte Instanz: **eigene Tabellen mit Präfix**, keine echten personenbezogenen Daten.
- Soll deine Lösung dauerhaft in deiner Organisation laufen, gehört sie auf eine eigene Datenbank. Das ist ein typischer nächster Schritt für die README.

## 4. SQLite: nur lokal oder ein einzelner Prozess

Kein Setup, eine Datei. Gut für **lokale Prototypen** oder ein **Backend, das als ein dauerhafter Prozess mit Volume** läuft (z. B. `backend-example` als Docker-Container mit gemountetem Volume).

- ⚠️ **Nicht für veröffentlichte Apps:** Verlass dich dort nicht auf eine lokale Datei. Nach einem neuen Build kann die `.sqlite`-Datei weg sein. Für eine veröffentlichte App ist Supabase die richtige Wahl.

---

### Faustregel
**n8n-Workflow → Data Tables. Tabellen im Browser → NocoDB. Login, Uploads, Vektoren oder veröffentlichte App → ÖW-Supabase. Nur lokal → SQLite.**
