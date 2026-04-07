# OpenClaw Publisher — Legal Site

Static site that hosts the Terms of Service, Privacy Policy, and homepage
URLs required by the TikTok Developer Portal (and any other API portal that
asks for them).

## Files
- `index.html`   — homepage / Web URL
- `terms.html`   — Terms of Service URL
- `privacy.html` — Privacy Policy URL

Replace every `REPLACE_WITH_YOUR_EMAIL@example.com` placeholder with your
real contact email before publishing.

## How to host on GitHub Pages

1. Create a new **public** repository on GitHub named `openclaw-publisher`
   (https://github.com/new). Do NOT initialize with a README.

2. From this folder, run:
   ```bash
   cd /home/iryna/openclaw-publisher-site
   # First, replace the placeholder email everywhere
   sed -i 's/REPLACE_WITH_YOUR_EMAIL@example.com/your.real@email.com/g' *.html

   git init -b main
   git add index.html terms.html privacy.html README.md
   git commit -m "Initial legal site"
   git remote add origin https://github.com/<YOUR_GH_USERNAME>/openclaw-publisher.git
   git push -u origin main
   ```
   (Use `gh auth login` first if your machine isn't already authenticated to
   GitHub, or push over SSH with `git@github.com:...` instead of HTTPS.)

3. Enable Pages:
   - GitHub web → your repo → **Settings** → **Pages**
   - **Source**: `Deploy from a branch`
   - **Branch**: `main`, folder: `/ (root)`
   - **Save**
   - Wait ~30 seconds. Pages will publish at:
     ```
     https://<YOUR_GH_USERNAME>.github.io/openclaw-publisher/
     ```

4. Confirm the three URLs return HTTP 200:
   ```bash
   curl -sI https://<YOUR_GH_USERNAME>.github.io/openclaw-publisher/index.html   | head -1
   curl -sI https://<YOUR_GH_USERNAME>.github.io/openclaw-publisher/terms.html   | head -1
   curl -sI https://<YOUR_GH_USERNAME>.github.io/openclaw-publisher/privacy.html | head -1
   ```

5. Paste these into the TikTok Developer Portal app form:

   | Field                  | Value                                                                                  |
   |------------------------|----------------------------------------------------------------------------------------|
   | Web/Desktop URL        | `https://<YOUR_GH_USERNAME>.github.io/openclaw-publisher/`                             |
   | Terms of Service URL   | `https://<YOUR_GH_USERNAME>.github.io/openclaw-publisher/terms.html`                   |
   | Privacy Policy URL     | `https://<YOUR_GH_USERNAME>.github.io/openclaw-publisher/privacy.html`                 |
   | Redirect URI (Login Kit) | `http://localhost:8766/callback`                                                    |

6. Use the same URLs for the second TikTok app (satisfying-stories account).
   One repo, one Pages site, two TikTok apps point at it.

## Updating
After the first push, edits go through normal git:
```bash
cd /home/iryna/openclaw-publisher-site
# edit files
git add -A && git commit -m "..." && git push
```
GitHub Pages re-deploys automatically.
