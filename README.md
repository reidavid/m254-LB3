# Camunda Prozess: GitHub Issue-Erstellung mit E-Mail-Benachrichtigung

## 📌 Ziel

Dieses Projekt zeigt einen automatisierten Workflow mit Camunda 8, bei dem:

1. Ein Nutzer ein Online-Formular ausfüllt.
2. Nach Absenden wird automatisch eine E-Mail an vordefinierte Empfänger gesendet.
3. Zusätzlich wird über die GitHub API ein Issue im entsprechenden Repository erstellt.

☁️ Architektur

## Gehostet in einer AWS EC2 Instanz

- Bereitgestellt mit Docker
- Camunda läuft als Container mit:
  - Web Modeler
  - Tasklist
  - Connectors (REST & Mail)

## 📦 Komponenten

- Camunda 8 (Docker-basiert) – BPMN Engine

- REST Connector – zum Erstellen von GitHub-Issues

- Mail Connector – für E-Mail-Versand via Gmail SMTP

- Gmail App-Passwort – für Authentifizierung beim Mailversand

- GitHub Personal Access Token – zum Erstellen von Issues

## 📂 Struktur
```
.
├── docker-compose.yml            # Startet Camunda & benötigte Services
├── process/
│   └── issue_creation.bpmn       # BPMN-Prozess mit Formular, Mail- & REST-Aufruf
├── forms/
│   └── bug_report.form           # Camunda Form für Nutzereingabe
└── README.md                     # Diese Datei
```
## ⚙️ Konfiguration

### GitHub

- Token erstellen unter: https://github.com/settings/tokens

- Scopes: mindestens repo

- REST Connector-Einstellungen:

    - URL: https://api.github.com/repos/<owner>/<repo>/issues

    - Auth: Bearer

    - Token: <DEIN_PERSONAL_ACCESS_TOKEN>

Header:
```
{
  "Accept": "application/vnd.github+json",
  "Authorization": "Bearer <DEIN_PERSONAL_ACCESS_TOKEN>",
  "Content-Type": "application/json"
}
```
Gmail SMTP (Mail Connector)

Gmail-Konto benötigt ein App-Passwort


### ▶️ Ablauf

Nutzer ruft den Prozess über die Camunda Tasklist oder ein Frontend auf.

Formular wird angezeigt und ausgefüllt.

Nach Absenden:

wird eine E-Mail mit den Formulardaten an vordefinierte Empfänger geschickt.

wird ein GitHub-Issue mit denselben Daten im angegebenen Repository erstellt.

🛠️ Anpassen

Empfängeradresse: Im Mail Connector konfigurieren.

GitHub-Repo/Labels: Im REST Connector anpassen.

Formularfelder: In der .form Datei erweitern.

Mail-Text & Betreff: Direkt im Connector definieren.