# Glance — Homelab Dashboard

A self-hosted, single-page dashboard built with [Glance](https://github.com/glanceapp/glance). This repo holds the configuration (`glance.yml`) that drives my personal homelab dashboard — a central hub for monitoring services, launching apps, and staying up to date on what's happening across my home network and beyond.

---

## Pages

### Home
The landing page. Keeps it minimal and always useful at a glance (no pun intended).

- **Clock** — 12-hour time display
- **All Services** — unified health monitor covering every infra and media service on the network
- **Bookmarks** — quick links organized into three groups:
  - *My Site* — lavaugh.com
  - *Daily Drivers* — Gmail, YouTube, GitHub, Reddit
  - *AI Agents* — Claude, Gemini, ChatGPT

### Infrastructure
Dedicated view for managing the homelab stack.

- **Core Services monitor** — live status for Proxmox, Home Assistant, Nginx Proxy Manager, Pi-hole, and TwinGate
- **Manage bookmarks** — direct links into each infra admin UI with descriptions
- **Software Updates** — GitHub release tracker for all self-hosted projects (Home Assistant, NPM, Pi-hole, Radarr, Sonarr, Prowlarr, Overseerr, qBittorrent, Glance itself)
- **Homelab Community** — RSS feed wall pulling from r/homelab, r/selfhosted, r/Proxmox, and r/Plex

### Media
Everything related to the Plex media server ecosystem.

- **Media Services monitor** — live status for Overseerr, Plex, qBittorrent, Radarr, Sonarr, and Prowlarr
- **Launch bookmarks** — one-click access into each media service with descriptions
- **Latest Trailers** — YouTube grid pulling new trailers from Warner Bros., Universal Pictures, and Rotten Tomatoes
- **Movie & TV News** — RSS feed wall from Variety Film, Collider, r/movies, and r/television

---

## Auto-Deploy via GitHub Actions

Pushing to `main` triggers a GitHub Actions workflow (`.github/workflows/deploy.yml`) that runs on a **self-hosted runner** living on my home server.

```
push to main
    └── GitHub Actions (self-hosted runner)
            ├── git pull origin main  →  /opt/glance
            └── systemctl restart glance
```

The workflow pulls the latest config directly onto the server and restarts the Glance service — no manual SSH required. Any change to `glance.yml` committed and pushed to `main` is live within seconds.
