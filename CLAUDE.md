# Academic CV Website

Personal academic website built with Hugo and the HugoBlox Academic CV template.

## Tech Stack
- Hugo (static site generator, Go-based modules)
- HugoBlox Kit (Academic CV template)
- Tailwind CSS v4
- Pagefind (search indexing)
- pnpm (package manager)

## Project Structure
```
config/_default/   -- Hugo and HugoBlox configuration (hugo.yaml, params.yaml, menus.yaml)
content/           -- Site content (authors, blog, courses, events, projects, publications, slides)
data/authors/      -- Author profile data
layouts/_partials/ -- Template overrides
assets/media/      -- Images and media files
static/uploads/    -- Static file uploads
hugoblox.yaml      -- Template metadata and deploy target
netlify.toml       -- Netlify build configuration
```

## Common Commands
```bash
# Development server (with drafts)
hugo server -D

# Production build
hugo --gc --minify && pnpm run pagefind

# Install dependencies (required before first build)
pnpm install
```

## Key Conventions
- Content pages use Hugo front matter in YAML format
- Author profiles live in content/authors/ with _index.md files
- Site identity and theme are configured in config/_default/params.yaml under the `hugoblox:` key
- Navigation menus are defined in config/_default/menus.yaml
- Template overrides go in layouts/_partials/ (overrides HugoBlox defaults)
- Hugo modules are managed via go.mod, not npm

## Slides / Presentations
Two options for adding slide decks to the site:

### Option A: Hugo built-in Reveal.js (recommended)
- Already supported via the `slides` module in go.mod
- Create slides in `content/slides/<talk-name>/index.md` using Markdown with `---` separators
- No extra build step — Hugo handles everything

### Option B: Slidev (external build, same repo)
- Keep Slidev source files in a separate folder (e.g. `slidev-decks/<talk-name>/slides.md`)
- Build with `slidev build` and output to `static/slides/<talk-name>/`
- Hugo serves `static/` as-is, so slides are available at `/slides/<talk-name>/`
- Embed in talk pages via iframe: `<iframe src="/slides/<talk-name>/" width="100%" height="500px"></iframe>`
- If using Netlify, add Slidev build step to `netlify.toml` build command, or build locally and commit output to `static/`
