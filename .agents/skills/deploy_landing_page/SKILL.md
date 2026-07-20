---
name: deploy-landing-page
description: Guide and automate the deployment of the landing page project to GitHub and Vercel. Triggered when the user asks to deploy, publish, ship, or release the landing page.
---

# Deploy Landing Page Skill

This skill guides the agent in deploying the landing page project to both GitHub and Vercel.

## Pre-requisites
- Git must be configured with the remote `origin` pointing to the GitHub repo: `https://github.com/mikeboysen/pjtbd-landing.git`
- Vercel CLI must be installed and authenticated.
- The project must be linked to Vercel (contains `.vercel/project.json`).

## Deployment Procedure

Follow these steps exactly when triggered to deploy:

1. **Check Git Status**
   - Run `git status` to see if there are any uncommitted changes.
   - If there are uncommitted changes, ask the user if they want to commit them or discard them before proceeding.
   - Stage and commit the changes if requested:
     ```bash
     git add .
     git commit -m "<descriptive message>"
     ```

2. **Push to GitHub**
   - Push the current branch to GitHub:
     ```bash
     git push origin main
     ```

3. **Deploy to Vercel**
   - Run the production build and deployment via Vercel CLI (always use `cmd /c` on Windows to prevent UI locks):
     ```bash
     cmd /c vercel --prod
     ```

4. **Verify Deployment**
   - Once the Vercel deploy completes, copy the production URL (e.g. `https://pjtbd-landing.vercel.app`).
   - Run a quick sanity check to confirm the page is up.
   - Report the deployed URL and GitHub commit SHA back to the user.
