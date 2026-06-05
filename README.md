# 13×13.ch

Regionale Medienplattform für den Kanton Wallis.

## Was ist 13×13.ch?

[13×13.ch](https://13x13.ch) ist eine unabhängige Medienplattform aus dem Wallis. Das Konzept: Dreizehn Walliser Autor:innen schreiben dreizehn Texte im Jahr — exklusiv für die Plattform. Keine Agenturmeldungen, keine Aggregation, keine Beliebigkeit.

Die Texte haben Haltung, Tiefe und regionalen Bezug. Sie richten sich an Leserinnen und Leser, die mehr wollen als schnelle Schlagzeilen.

## Wer steckt dahinter?

Gegründet und betrieben von Bernhard Kuonen, Wallis/Schweiz.

**Kontakt:** 📧 13@13x13.ch · **Launch:** 01.09.2026 (Vorschau-Modus aktiv, s. unten)

---

## Technik

### Stack

- **Hugo** (de-CH), eigene Layouts in `layouts/` (Theme-Submodule `ananke` ist deklariert, die Site nutzt aber eigene Templates)
- **Sveltia CMS** (`static/admin/`) — GitHub-Backend auf dieses Repo (`main`), Auth über den Worker `cms-auth.bekuonen.workers.dev`
- Taxonomien: `tags`, `autoren` · i18n: `i18n/de.yaml`

### Schnellstart

```bash
hugo server          # Dev-Server http://localhost:1313
hugo --minify        # Produktions-Build → public/
```

### Projektstruktur

```
content/             _index, ausgaben/, autoren/, empfehlungen/, mitmachen/,
                     standpunkte, charta, fragen, kontakt, danke
layouts/             eigene Templates (ausgaben, autoren, empfehlungen, mitmachen …)
assets/css/ + static/css/   Stylesheets
static/admin/        Sveltia CMS (Collections: Ausgaben, Beiträge, Autoren …)
static/images/uploads/      CMS-Medienablage
i18n/de.yaml         Übersetzungs-Strings
hugo.toml            Site-Config inkl. Vorschau-/Launch-Steuerung
```

### Vorschau-Modus & Launch

`hugo.toml [params]`: `vorschau = true` blendet den Hinweis ein («Beiträge dienen der Illustration …»), `launch = '2026-09-01T00:00:00'` steuert den Countdown. **Zum Launch:** `vorschau = false` setzen.

### Inhalte pflegen

1. **CMS:** `/admin/` (Sveltia, committet direkt auf `main`) — Ausgaben, Beiträge, Autoren
2. **Direkt:** Markdown in `content/`

### Deployment

**Cloudflare Pages**, Projekt `13x13`, Domains `13x13.ch` + `13x13.pages.dev` *(belegt 2026-06-05: Wrangler-Projektliste, DNS, Live-Header)*.
Weg: **GitHub → Cloudflare Pages → Build bei Push auf `main`** (auch CMS-Commits triggern). Build: `hugo --minify` → `public/`, **HUGO_VERSION 0.161.1** — versioniert in [`cloudflare-build.toml`](./cloudflare-build.toml), Dashboard entsprechend gesetzt (bestätigt 2026-06-05). `.nojekyll` ist ein Relikt ohne Funktion auf Pages.
