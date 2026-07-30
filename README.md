# Chasing the Sash — Website

Static one-page site, auto-deployed via GitHub Actions to GitHub Pages.

## One-time setup

1. Create a new **public** GitHub repo (e.g. `chasing-the-sash-site`).
2. Push these files to the `main` branch.
3. In the repo: **Settings → Pages → Build and deployment → Source: GitHub Actions**. (The workflow in `.github/workflows/deploy.yml` handles the rest.)
4. First push triggers the Action automatically — check the **Actions** tab for the green check.

## Point your GoDaddy domain at it

In GoDaddy → DNS management for `chasingthesash.com`, add:

| Type  | Name | Value                  |
|-------|------|------------------------|
| A     | @    | 185.199.108.153        |
| A     | @    | 185.199.109.153        |
| A     | @    | 185.199.110.153        |
| A     | @    | 185.199.111.153        |
| CNAME | www  | `<yourgithubusername>.github.io` |

Remove any existing GoDaddy "Website Builder"/forwarding A-records first so they don't conflict.

Back in GitHub: **Settings → Pages → Custom domain** → enter `chasingthesash.com` → Save (this also confirms the `CNAME` file in this repo). Tick **Enforce HTTPS** once it's available (can take a few hours for the cert to issue).

## Ongoing updates

Any push to `main` (including from Claude Code) redeploys automatically — no manual upload step.
