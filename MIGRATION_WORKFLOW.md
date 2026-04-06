# Migration Workflow (Wix -> GitHub Pages)

This workflow incorporates the migration checklist and the solutions log practices. It is designed to be reusable for any future site moves.

## 1) Intake And Inventory
1. Record the source domain and target domain.
2. Decide canonical host before any build or DNS changes (`www` vs apex).
3. Export or list all current public routes from the old host.
4. Export or list all important media/assets currently hotlinked from the old host.
5. Identify forms, email capture, and any dynamic features that need static-host alternatives.

## 2) Build In Repo First
1. Create a repo and build locally before touching DNS.
2. Recreate all important routes as static files or directories.
3. Keep old URL paths whenever possible to avoid broken links and SEO loss.
4. Localize assets into the repo (`images/`, `assets/`) instead of hotlinking old-host media.
5. Replace dynamic forms with static-compatible handlers (Formspree, FormSubmit).

## 3) Replace Placeholder Templates With Real Content
1. Remove stock template/demo content immediately.
2. Build a custom homepage and section structure that reflects the real site content.
3. Create a design token system for colors, typography, spacing, and radii.
4. Add accessibility improvements as standard (skip link, readable contrast, reduced-motion support).
5. Add light motion only if it improves scanning and hierarchy.

## 4) Route Migration Pass
1. Migrate all sitemap routes into the static repo.
2. Keep internal links pointing to local routes, not the old domain.
3. Add consistent subpage layout classes for visual cohesion across routes.

## 5) Assets And Links Policy
1. Store images locally in the repo where possible.
2. For external links, verify URL and authorship before linking.
3. If a link or authorship is uncertain, list the title as plain text until verified.
4. Remove or replace defunct links.

## 6) Configure GitHub Pages
1. Add a deploy workflow for Pages on push to `main`.
2. Add a deploy trigger for merged PRs to avoid missed publishes.
3. Add `CNAME` with the target custom domain.
4. Add `.nojekyll` only when serving a pure static site without Jekyll processing.
5. Add or update `robots.txt` and `sitemap.xml` for the production domain.

## 7) Pre-Cutover Verification
1. Check every primary route on the GitHub Pages URL.
2. Verify forms submit and email delivery works.
3. Verify canonical URLs and sitemap routes are consistent with live route style.
4. Verify all major media assets load locally from the repo.

## 8) DNS Cutover Sequence
1. Lower DNS TTL (for example 300-3600 seconds) before changing records.
2. Point `www` to GitHub Pages via CNAME (`<user>.github.io`).
3. Keep mail records (MX, SPF, DKIM, mail CNAMEs) unchanged.
4. Wait for propagation and certificate issuance.

## 9) SSL And HSTS Validation
1. Confirm the custom domain serves a valid certificate.
2. If HSTS or cert warnings appear during propagation, wait and recheck after DNS/cert settle.
3. Confirm expected hostnames redirect correctly or intentionally do not.

## 10) Post-Cutover Cleanup
1. Re-test key routes and form submissions on the final domain.
2. Confirm GitHub Actions deployment succeeds on the latest commit.
3. Keep old hosting active until custom-domain HTTPS is fully stable.
4. Cancel old hosting only after successful live verification.

## 11) Governance And Tracking
1. Track migration decisions and fixes in `SOLUTIONS.md`.
2. Use PR-based deploys for auditability and rollback safety.
3. Keep a migration checklist in the repo and update when new lessons are learned.

## 12) Required Artifacts Checklist
1. `CNAME` with the custom domain.
2. `.nojekyll` when appropriate.
3. `robots.txt` with the production domain.
4. `sitemap.xml` with the production domain.
5. Deploy workflow for GitHub Pages.
6. `SOLUTIONS.md` log with dated fixes and outcomes.

## 13) Solutions Log Pattern
1. Date and title per fix.
2. Problem description.
3. Solution summary with exact file paths.
4. Outcome statement.

