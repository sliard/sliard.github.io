# Copilot instructions for `sliard.github.io`

## Build and local preview

This repository is a Ruby/Jekyll site managed with Bundler.

```bash
bundle install
bundle exec jekyll serve
bundle exec jekyll build
```

There is no repository-specific test suite or lint command checked into this repo.

## High-level architecture

The site has two distinct rendering stacks:

1. **Home page and blog** use the Hyde/Poole-style layout chain:
   - `_layouts/default.html`
   - `_includes/hyde_head.html`
   - `_includes/hyde_sidebar.html`
   - `public/css/*`
2. **`/cv`** uses a separate resume theme built from:
   - `_layouts/cv.html`
   - `_includes/head.html`
   - `_includes/sidebar.html`
   - `assets/css/main.scss`
   - Bootstrap / Font Awesome assets under `assets/plugins/`

Content is split by responsibility:

- `index.md` is the landing page content.
- `_posts/*.md` contains the archived and current blog posts.
- `blog/index.html` renders the paginated blog index from `paginator.posts`.
- `_data/data.yml` is the source of truth for CV content; the CV page is assembled from include partials such as `career-profile.html`, `experiences.html`, `projects.html`, `publications.html`, and `skills.html`.

Site-wide behavior lives in `_config.yml`, including pagination (`paginate`, `paginate_path`), plugins, metadata, and analytics.

## Key conventions

- Treat `_site/` as generated output only. It is gitignored and should not be edited by hand.
- For CV changes, prefer editing `_data/data.yml` instead of hardcoding content into templates. The include partials expect the existing nested structure such as `sidebar.languages`, `experiences`, `projects.assignments`, and `skills.toolset`.
- `experience.details`, `career-profile.summary`, and similar long-form fields are rendered with `markdownify`, so multiline YAML blocks are the intended format for rich CV content.
- The two site themes are intentionally separate. Blog styling changes usually belong under `public/` or the Hyde includes/layouts; CV styling changes belong under `assets/`, `_sass/`, and the CV-specific includes/layouts.
- Blog pagination depends on both `blog/index.html` and `_config.yml`. If you change one, keep the other in sync.
- Many archived posts keep explicit WordPress-era front matter such as `guid`, `id`, `permalink`, and `url`. Preserve those fields when editing historical posts unless the task is specifically to change routing or imported metadata.
- `_config.yml` is not hot-reloaded by `jekyll serve`; restart the server after changing configuration.
