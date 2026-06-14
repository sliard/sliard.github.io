# liard.me — thème « Terminal »

Refonte complète du site personnel de Samuel Liard : un thème **Jekyll** sombre,
orienté systèmes / terminal, qui met en avant le **blog**, les **talks** et le **CV**.

- Accent menthe phosphore sur fond quasi-noir, grille de points discrète
- Typo : **Space Grotesk** (titres) · **JetBrains Mono** (interface) · **IBM Plex Sans** (corps)
- Blog avec **article vedette** + **filtres thème / année** (JavaScript, sans dépendance)
- Pages **Talks & écrits** (alimentées par `_data/`) et **CV**

---

## Démarrer en local

```bash
bundle install
bundle exec jekyll serve
# → http://127.0.0.1:4000
```

> Pré-requis : Ruby ≥ 3.0 et Bundler (`gem install bundler`).

Pour générer le site statique (dossier `_site/`) :

```bash
bundle exec jekyll build
```

---

## Structure

```
jekyll/
├── _config.yml            Réglages du site (titre, URL, permaliens, plugins)
├── Gemfile                Dépendances Ruby
├── index.html             Accueil (hero + 3 derniers articles)
├── blog.html              Liste du blog : vedette + filtres → /blog/
├── talks.html             Talks & écrits → /talks/
├── cv.md                  Page CV (à compléter) → /cv/
├── _layouts/
│   ├── default.html       Gabarit de base (head + nav + footer)
│   └── post.html          Gabarit d'article (vue lecture)
├── _includes/
│   ├── head.html  nav.html  footer.html
├── _sass/
│   ├── _variables.scss    Tous les tokens couleur / typo / espacement
│   ├── _base.scss  _layout.scss  _components.scss
├── assets/css/main.scss   Point d'entrée CSS (importe les partials)
├── _data/
│   ├── talks.yml          Conférences filmées
│   └── writings.yml       Articles longs (Medium…)
└── _posts/                Articles (exemples à remplacer)
```

---

## Ajouter un article

Créez un fichier `_posts/AAAA-MM-JJ-slug.md` :

```markdown
---
layout: post
title: "Titre de l'article"
date: 2026-05-01
theme: IA          # sert au filtre et au tag #IA
reading_time: 6    # minutes (optionnel)
featured: true     # met l'article « à la une » sur /blog/ (optionnel)
---

Votre contenu en Markdown…
```

- Les **permaliens** sont en `/:year/:month/:title/` (identiques à l'ancien site) — réglable dans `_config.yml`.
- Les **filtres** par thème et par année se construisent automatiquement à partir des `theme:` et des dates de vos posts.
- L'**article vedette** est le premier post `featured: true` (sinon le plus récent).

## Ajouter un talk / un écrit

Éditez `_data/talks.yml` ou `_data/writings.yml` — aucun template à toucher.

---

## Personnaliser le design

Tout est centralisé dans `_sass/_variables.scss` : couleurs, polices, rayons,
largeur max. Pour changer l'accent menthe, modifiez `$mint`. Pour repasser en
clair, ajustez `$bg`, `$text`, `$panel` et `$border` — le reste suit.
