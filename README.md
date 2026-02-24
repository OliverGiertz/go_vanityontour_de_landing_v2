# go.vanityontour.de – Static Landing

Diese Seite ist **komplett statisch** (HTML/CSS). Kein Build-Step, kein Node, kein Stress.

## Lokal testen
Einfach den Ordner öffnen – oder z.B. mit Python:

```bash
python3 -m http.server 8080
```

Dann im Browser: http://localhost:8080

## Links anpassen
In `index.html` sind ein paar **Platzhalter-Links** (z.B. GitHub Repo / App-Store). Ersetze sie durch deine echten URLs.

---

# Deployment via GitHub Actions (SSH + rsync)

Die Workflow-Datei liegt hier:
`.github/workflows/deploy.yml`

## Voraussetzungen auf dem Server
- SSH-Zugriff
- Zielverzeichnis existiert (z.B. CloudPanel):
  - `/home/cloudpanel/htdocs/go.vanityontour.de/` (häufig)
  - oder dein eigener Pfad

- `rsync` installiert:
  - Debian/Ubuntu: `sudo apt-get update && sudo apt-get install -y rsync`

## GitHub Secrets anlegen (Repo → Settings → Secrets and variables → Actions)
- `SSH_HOST` (z.B. `your-server.example`)
- `SSH_USER` (z.B. `root` oder `cloudpanel`)
- `SSH_PORT` (z.B. `22`)
- `SSH_PRIVATE_KEY` (private key für den Deploy-User)
- `DEPLOY_PATH` (z.B. `/home/cloudpanel/htdocs/go.vanityontour.de/`)

## DNS (go.vanityontour.de)
Setze einen **A-Record** (oder AAAA) auf die Server-IP.
Alternativ ein CNAME auf eine passende Ziel-Subdomain, wenn du das so betreibst.

## Nginx (Beispiel)
Wenn du Nginx selbst konfigurierst:

```nginx
server {
  server_name go.vanityontour.de;
  root /home/cloudpanel/htdocs/go.vanityontour.de;
  index index.html;

  location / {
    try_files $uri $uri/ =404;
  }
}
```

Danach:
```bash
sudo nginx -t && sudo systemctl reload nginx
```
