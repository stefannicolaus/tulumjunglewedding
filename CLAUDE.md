# CLAUDE.md — Tulum Jungle Wedding

## Projekt

**Name:** Tulum Jungle Wedding  
**URL:** https://tulumjunglewedding.com  
**Stack:** Astro (static), nginx, Hetzner  
**Repo:** github.com/stefannicolaus/tulumjunglewedding (oder BU-Org)

---

## Server & Infrastruktur

- **Server:** `root@204.168.208.253`
- **Container:** `ca-website` (geteilter nginx-Container mit staging.casaarkaana.com)
- **nginx-Config:** `/etc/nginx/conf.d/tjw.conf` (bereits eingerichtet)
- **Web-Root:** `/usr/share/nginx/tjw-html/`
- **Domain:** `tulumjunglewedding.com` → Cloudflare → `204.168.208.253`
- **SSL:** Let's Encrypt, liegt im Container unter `/etc/letsencrypt/live/tulumjunglewedding.com/`

---

## Deploy

```bash
cd /Users/stefan/code/tulumjunglewedding  # oder dein lokaler Pfad
npm run build && \
rsync -az --delete dist/ root@204.168.208.253:/tmp/tjw-dist/ && \
ssh root@204.168.208.253 "docker cp /tmp/tjw-dist/. ca-website:/usr/share/nginx/tjw-html/ && \
  docker exec ca-website nginx -s reload"
```

**Voraussetzung:** SSH-Zugang zu `root@204.168.208.253` (SSH-Key muss auf dem Server hinterlegt sein — Stefan fragen falls nötig).

---

## Lokale Entwicklung

```bash
npm run dev
```

→ Öffne http://localhost:4321

---

## Dateien

```
src/
  layouts/BaseLayout.astro   — Shared Layout (Title, Meta, Canonical)
  pages/index.astro          — Startseite (Onepager)
  styles/                    — CSS
public/
  images/                    — Bilder
nginx.conf                   — Referenz-Config (nicht die aktive auf dem Server)
```

---

## Cloudflare

- **Account:** Asdrubal (casaarkaana@gmail.com)
- **Zone:** tulumjunglewedding.com
- **DNS:** A-Record zeigt auf 204.168.208.253, Cloudflare-proxied
- **www-Redirect:** in nginx (tjw.conf) geregelt — kein CF Page Rule nötig

---

## Wichtige Regeln

1. Nie direkt auf dem Server editieren — immer lokal bauen und deployen
2. Bilder in `public/images/` — nach Build werden sie zu `dist/images/`
3. Canonical URL ist hardcoded auf `https://tulumjunglewedding.com` im BaseLayout

---

## Für Asdrubal

Falls du keinen SSH-Zugang zum Server hast:
→ Stefan deployt für dich sobald du sagst "fertig, bitte deployen"  
→ Oder: Stefan richtet deinen SSH-Key auf dem Server ein (einmalig)
