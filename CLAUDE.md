# CLAUDE.md — 13x13

## Projekt

**13×13.ch** — unabhängige Medienplattform Wallis: 13 Autor:innen × 13 Texte/Jahr.
**Live:** https://13x13.ch (public Repo!) · **Repo:** github.com/bekuonen/13x13 · **Launch: 01.09.2026** — bis dahin Vorschau-Modus. Aktivstes Repo (286 Commits seit 2026-02).

## Stack

- **Hugo** (de-CH), eigene Layouts; Theme-Submodule `ananke` deklariert, aber faktisch ungenutzt (Site rendert über `layouts/`)
- **Sveltia CMS** — GitHub-Backend, Auth-Worker `cms-auth.bekuonen.workers.dev` (geteilt mit meerwert-ch)
- Taxonomien `tags` + `autoren` · Permalink-Schema für `empfehlungen`

## Projektstruktur

`content/` (ausgaben, autoren, empfehlungen, mitmachen, Standpunkte/Charta/Fragen) · `layouts/` · `static/admin/` (CMS) · `static/images/uploads/` (CMS-Medien) · `i18n/de.yaml` · `hugo.toml`. Details: `README.md` §Technik.

## Befehle

```bash
hugo server      # Dev http://localhost:1313
hugo --minify    # Produktions-Build → public/ (= Verifikation)
```

## Inhalte ändern

Ausgaben/Beiträge/Autoren → CMS `/admin/` oder `content/`. **Launch-Steuerung in `hugo.toml [params]`:** `vorschau` (Hinweis-Banner) + `launch` (Countdown-Datum) — **zum Launch am 01.09.2026 `vorschau = false`**. Begleitende Social-Kampagne: Skill `instapost-13x13` (archiviert in `04_Ressourcen/KI/Claude/Skills/_Veraltet_aus_Alt-Workspace/`).

## Deployment

**Cloudflare Pages**, Projekt `13x13` (Domains: 13x13.ch, 13x13.pages.dev) — belegt 2026-06-05. Weg: GitHub → Pages, Build bei jedem Push auf `main`. Build gemäss `cloudflare-build.toml` (hugo --minify → public/, **HUGO_VERSION 0.161.1** — Dashboard-Eintrag bestätigt 2026-06-05; bei Versionswechseln Datei UND Dashboard synchron halten).

## Secrets & ENV

Keine Secrets im Repo. CMS-Auth über Worker `cms-auth` (Secret in dessen Cloudflare-Umgebung).

## Stolperfallen

1. **CMS committet auf `main`** (Redaktionsbetrieb! Commits wie «Update Beitrag …») — vor jedem Push `git pull`
2. **Submodule `themes/ananke`:** deklariert, lokal nicht initialisiert — frischer Clone braucht ggf. kein `--recursive`, da Layouts eigenständig sind; nicht «reparieren» ohne Klärung
3. Test-Inhalte aus CMS-Erprobung möglich (Commits «Create/Update Beitrag “test”») — vor Launch Inhalts-Sweep
4. GitHub-**Beschreibung des Repos ist leer** (public!) — Audit-Befund 2026-06-05
6. **Versions-Pin = Datei + Dashboard:** `cloudflare-build.toml` wird von Pages nicht gelesen — bei Versionswechseln beide Stellen synchron ändern
5. Repo public: Alles hier (auch Entwürfe in `content/`) ist weltlesbar

## Arbeitsregeln

- **Governance-Regelwerk G1–G12** gilt (`iCloud 05_System/Grundsätze/Governance_Regelwerk.md`): Lesen direkt · Verändern nur nach Freigabe
- **Heimatort-Hinweis (G1):** Repo liegt derzeit in `~/Documents/GitHub/` — Handbuch-Heimat wäre `01_Projekte/13x13/Code/`; Umzug = freigabepflichtige Audit-Empfehlung
- Commits: Deutsch, beschreibend wie Historie
- Niemals: force-push auf `main` (public + Redaktion!) · `vorschau`-Toggle ohne ausdrücklichen Launch-Entscheid ändern

## Weiterführend

`README.md` (Konzept + Technik) · `static/admin/config.yml` (CMS-Collections) · Projektnotizen: Vault `03_Projekte/13x13/` · Referenzmodell: `lichtspur-natur/Code/CLAUDE.md`
