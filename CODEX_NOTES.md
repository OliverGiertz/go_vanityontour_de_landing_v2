# CODEX_NOTES.md – Deploy & Betrieb (Copy/Paste für Codex)

## Ziel
Statische Landingpage soll automatisch bei jedem Push auf `main` nach `go.vanityontour.de` deployed werden.

## Repo-Struktur
- `index.html`
- `assets/css/style.css`
- `assets/img/*`
- `.github/workflows/deploy.yml`

## Deployment-Mechanik
- GitHub Actions Workflow:
  - Checkout Repo
  - SSH-Key in Runner schreiben
  - `rsync` der Dateien auf Server
  - Optional: Berechtigungen setzen

## GitHub Secrets (Actions)
- `SSH_HOST`: Hostname oder IP
- `SSH_USER`: SSH-User
- `SSH_PORT`: SSH-Port (default 22)
- `SSH_PRIVATE_KEY`: Private Key (PEM/OPENSSH)
- `DEPLOY_PATH`: Zielpfad auf dem Server (CloudPanel: `/home/cloudpanel/htdocs/go.vanityontour.de/`)

## Server Anforderungen
- SSH aktiv
- `rsync` installiert
- Zielordner existiert und ist beschreibbar
- Webserver (Nginx/Apache) zeigt auf `DEPLOY_PATH`

## DNS
- `go.vanityontour.de` → A/AAAA auf Server-IP
- SSL via Let's Encrypt (CloudPanel kann das)

## Hinweise
- OpenGraph Bild: ersetze `assets/img/og.jpg` (1200x630)
- Links in `index.html` aktualisieren (App Store, GitHub Repo URLs, Social URLs)
