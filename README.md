# Mommy Tree (Jekyll)

This repo contains the Jekyll version of the Mommy Tree site, ready for GitHub Pages.

## Quick setup
1. Create the GitHub repo `mommytreedoula.github.io` and push this directory.
2. In GitHub Pages settings, publish from the default branch root.
3. The `CNAME` file is already set to `mommytreedoula.com`.

## Local development
This repo uses Bundler to run the same GitHub Pages/Jekyll dependency family locally.

```bash
/opt/homebrew/opt/ruby@3.4/bin/bundle install
/opt/homebrew/opt/ruby@3.4/bin/bundle exec jekyll serve
```

For a one-time build check:

```bash
/opt/homebrew/opt/ruby@3.4/bin/bundle exec jekyll build
```

## Contact form
The contact form uses the Formspree endpoint configured in `index.html`:

```
https://formspree.io/f/mreojzev
```
