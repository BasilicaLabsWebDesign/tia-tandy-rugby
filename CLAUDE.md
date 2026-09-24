# tia-tandy-rugby

Website for Tia Tandy, an 18-year-old dual-code rugby hooker from
Dartford (tiatandyrugby.com). No build step, no dependencies. Two
versions are maintained, with no links between them:

- **The public site** — multi-page, black-and-gold, served at the
  domain root: `public/index.html`, `bio.html`, `fixtures.html`,
  `match-reviews.html`, `achievements.html`, `pictures.html`,
  `sponsors.html`, `my-rugby-life.html`, `videos.html`, a page per
  club under `union/` and `league/`, plus the partnership pack PDF
  (`files/Tia_Tandy_Partnership_Pack.pdf`) and self-hosted match
  video in `video/`. `public/style.css` holds the look. The homepage
  Next Match band reads an inline fixture list in `public/index.html`
  and shows the first fixture from today onwards, falling back to
  "Fixture details coming soon"; the full list is written out on
  `fixtures.html`, so a fixture change means updating both.
- **The one-pager** — the original navy/chalk/red match-programme
  page, unlisted at `/v2/` (`public/v2/index.html`) by owner
  instruction. Keep its facts in step, condensed to suit the
  single-page format — never paste long-form copy into it, and never
  change its design language.

Shared photos and sponsor logos live in `public/img/`.

There is no template or page generator: every page is plain HTML,
edited in place. The nav and footer are repeated in all 18 public-site
pages — 9 at the top of `public/`, 6 in `public/union/` and 3 in
`public/league/` — so a site-wide change such as a nav or footer edit
means editing every one of them, and a new page also joins the nav,
the footer and `public/sitemap.xml`. The only script,
`tools/build_pack_partners_page.py`, rebuilds the Numbers and Current
Partners pages of the partnership-pack PDF and splices them back in.

## Deployment

Cloudflare Workers static assets: every push deploys via
`npx wrangler deploy`, which serves the `public/` directory as
configured in `wrangler.jsonc`. Anything that should ship must live
under `public/`.

## Release workflow

Every push to the default branch is a release. Work in small, complete
batches: implement, verify, then commit and push — never leave pushed
work unverified or half-finished.

### Versioning

A simple ascending vMAJOR.MINOR sequence (v1.0, v1.1, v1.2 …). Every
push increments the minor by one, regardless of size. Reserve a major
bump for a ground-up overhaul of the project.

### Release tags

With every push, provide release-tag text in the reply, in exactly this
shape — the repo owner creates the GitHub release manually from it, so
never push tags:

    Tag: v<next>  —  Title: <five to nine words, plain and evocative>
    Description: <one to three sentences of editorial prose describing
    what changed from the user's point of view — outcomes, not
    implementation. No bullet lists, no jargon, no file names.>

### Commits

A descriptive imperative first line (what the change does, not
"update X"), then a short prose body — dash bullets are fine there —
explaining what changed and why it matters. Never include model names
or tooling identifiers in commits, titles, or code.

One commit per coherent piece of work; multiple commits may share a
push, but each push gets exactly one version tag entry covering all of
them.
