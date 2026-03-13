# Rufplan Development Roadmap

Interactive development roadmap for Rufplan — the AEC marketplace platform. Track progress across all features from March through September 2026 launch.

## Live Site

Deployed via **AWS Amplify** from this repo. Every push to `main` triggers a new deploy.

## How Progress Tracking Works

Progress is stored in `progress.json` at the root of this repo. This is the **source of truth** for task completion.

### For the Developer — Checking Off Tasks

1. Open `progress.json`
2. Find the task key (keys follow the pattern below)
3. Change `false` to `true`
4. Commit and push

```bash
# Example: mark "Cognito User Pool setup" as complete
# That's March (mar), section 0, task 3, sub-item 0 → key: "mar-0-3-sub-0"

git add progress.json
git commit -m "✅ Cognito User Pool setup complete"
git push
```

The site will auto-redeploy with the updated checkmarks.

### Key Format

- **Main tasks:** `{monthId}-{sectionIndex}-{taskIndex}`
- **Sub-tasks:** `{monthId}-{sectionIndex}-{taskIndex}-sub-{subIndex}`

Month IDs: `mar`, `apr`, `may`, `jun`, `jul`, `aug`, `sep`

### Quick Reference — Finding the Right Key

Open the site, expand the dropdown for the task you completed, and count the position:
- Section index starts at 0 (first section header in a card)
- Task index starts at 0 (first task in that section)
- Sub-item index starts at 0

Or just search `progress.json` — the `_instructions` field at the top explains the pattern.

## Local Development

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/rufplan-roadmap.git
cd rufplan-roadmap

# Serve locally (any static server works)
npx serve .
# or
python3 -m http.server 8000
```

Open `http://localhost:8000` (or whatever port your server uses).

## Deploying to AWS Amplify

1. Push this repo to GitHub
2. Go to [AWS Amplify Console](https://console.aws.amazon.com/amplify)
3. Click **"Host web app"** → connect your GitHub repo
4. Amplify auto-detects this as a static site — no build settings needed
5. Deploy

Every push to `main` will auto-deploy the updated roadmap + progress.

## Project Structure

```
rufplan-roadmap/
├── index.html          # The full roadmap (single-file app)
├── progress.json       # ← Developer edits this to check off tasks
├── README.md           # This file
└── .gitignore
```

## Stack

The roadmap tracks development of Rufplan across:
- **AWS** — Cognito, RDS/Aurora, Lambda, API Gateway, S3, CloudFront, AppSync, SES, Amplify
- **Stripe** — Subscription billing
- **React** — Frontend framework
