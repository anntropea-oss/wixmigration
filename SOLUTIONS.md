## [2026-05-05 12:49] Outdated Events Content Published
- Problem: The public events page shows outdated schedule entries ("TBD | January 2022", "February 2022", "March 2022"), which can mislead visitors and make the site appear unmaintained. Found in `mommytreedoula.github.io/upcoming-classes-events.md`.
- Root Cause: Migration content appears to have been carried over without a freshness pass.
- Solution: No code fix applied in this review; issue logged for content update/removal.
- Files Changed: `SOLUTIONS.md`
- Status: Open
- Verification: Reviewed `upcoming-classes-events.md` and confirmed 2022 date strings are currently rendered in page content.

## [2026-05-05 12:51] Removed Upcoming Events Page
- Problem: The public events page showed outdated schedule entries from 2022 and was still linked from navigation and listed in the sitemap.
- Root Cause: Migration content appears to have been carried over without a freshness pass.
- Solution: Removed the upcoming events page, removed the primary navigation link, and removed the URL from the sitemap.
- Files Changed: `mommytreedoula.github.io/upcoming-classes-events.md`, `mommytreedoula.github.io/_includes/nav.html`, `mommytreedoula.github.io/sitemap.xml`, `SOLUTIONS.md`
- Status: Resolved
- Verification: Ran `rg -n "upcoming-classes-events|Upcoming Classes|Upcoming"` in `mommytreedoula.github.io` and confirmed no matches remain.

## [2026-05-05 12:51] Local Jekyll Command Missing
- Problem: A local verification build could not be run because the `jekyll` command is not installed in the shell environment.
- Root Cause: Local Ruby/Jekyll tooling is not available on this machine or not on `PATH`.
- Solution: No code fix applied; static reference verification was used instead.
- Files Changed: `SOLUTIONS.md`
- Status: Open
- Verification: Ran `jekyll build` in `mommytreedoula.github.io` and received `zsh:1: command not found: jekyll`.

## [2026-05-05 12:49] Non-Canonical Service URL Slug In Navigation And SEO
- Problem: The abortion doula page is exposed at `/copy-of-birth-doula/` and referenced in navigation, footer, 404 recommendations, sitemap, and schema data. This slug is a migration artifact and weak for UX/SEO.
- Root Cause: Original Wix-like placeholder filename/permalink was retained during migration.
- Solution: No code fix applied in this review; issue logged to rename route to a canonical slug and implement redirect mapping.
- Files Changed: `SOLUTIONS.md`
- Status: Open
- Verification: Confirmed references in `_includes/nav.html`, `_includes/footer.html`, `index.html`, `404.html`, `_includes/schema.html`, and `sitemap.xml`.

## [2026-05-05 12:49] Stale Copyright Year In Footer
- Problem: Footer displays `© 2023 by Ann Tropea`, which is stale as of 2026 and can reduce trust.
- Root Cause: Hard-coded year in footer template.
- Solution: No code fix applied in this review; issue logged to make year dynamic or update annually.
- Files Changed: `SOLUTIONS.md`
- Status: Open
- Verification: Confirmed hard-coded value in `mommytreedoula.github.io/_includes/footer.html`.

## [2026-05-05 12:57] Added Local Jekyll Bundler Setup
- Problem: The repo did not have a local dependency manifest for reproducing the GitHub Pages/Jekyll build, and the system `jekyll` command was unavailable.
- Root Cause: Local Ruby/Jekyll dependencies had not been committed to the project.
- Solution: Added a `Gemfile` pinned to the current `github-pages` gem family, generated `Gemfile.lock`, installed Homebrew Ruby 3.4 for compatibility, and documented local build/serve commands in the README.
- Files Changed: `mommytreedoula.github.io/Gemfile`, `mommytreedoula.github.io/Gemfile.lock`, `mommytreedoula.github.io/README.md`, `SOLUTIONS.md`
- Status: Resolved
- Verification: Ran `/opt/homebrew/opt/ruby@3.4/bin/bundle install` successfully, then ran `/opt/homebrew/opt/ruby@3.4/bin/bundle exec jekyll build` successfully.

## [2026-05-05 12:57] Ignored Local Jekyll Build Artifacts
- Problem: Running a local Jekyll build generated `_site/`, which appeared as an untracked build artifact.
- Root Cause: The repo did not have a `.gitignore` for standard Jekyll and Bundler generated paths.
- Solution: Added `.gitignore` entries for `_site/`, `.jekyll-cache/`, `.sass-cache/`, `.bundle/`, and `vendor/bundle/`.
- Files Changed: `mommytreedoula.github.io/.gitignore`, `SOLUTIONS.md`
- Status: Resolved
- Verification: Ran `git status --short` after adding `.gitignore` and confirmed `_site/` no longer appears as an untracked path.

## [2026-05-05 13:03] Excluded Solutions Log From Published Site
- Problem: Adding `SOLUTIONS.md` to the repository caused Jekyll to generate `_site/SOLUTIONS.html` and `_site/SOLUTIONS.md`, which would publish the internal troubleshooting log.
- Root Cause: Root-level Markdown files are processed/copied by Jekyll unless excluded or otherwise configured.
- Solution: Added `SOLUTIONS.md` to the Jekyll `exclude` list in `_config.yml`.
- Files Changed: `mommytreedoula.github.io/_config.yml`, `mommytreedoula.github.io/SOLUTIONS.md`
- Status: Resolved
- Verification: Ran `/opt/homebrew/opt/ruby@3.4/bin/bundle exec jekyll build`, then checked `_site` and confirmed no `SOLUTIONS` files are generated.
