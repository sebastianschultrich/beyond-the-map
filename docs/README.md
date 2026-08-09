# Beyond the Map – Technical Documentation

**Project:** Beyond the Map / Latitude Nine North  
**Status:** Foundation Phase  
**Documentation date:** 09 August 2026

---

## Purpose

This document describes the technical foundation of the Beyond the Map digital platform.

Its purpose is to keep the infrastructure understandable, maintainable and recoverable over the long term.

The guiding principle is:

**Keep the infrastructure simple, documented and reproducible.**

---

# 1. Development Environment

The current development environment consists of:

- Visual Studio Code
- Git
- GitHub Desktop
- GitHub
- Cloudflare Workers
- Live Server for local website testing

Primary GitHub repository:

`sebastianschultrich/beyond-the-map`

Production branch:

`main`

The website is developed locally and deployed automatically through GitHub and Cloudflare.

---

# 2. Repository Structure

The project repository is organized as follows:

```text
beyond-the-map/
│
├── archive/
├── articles/
│
├── assets/
│   ├── icons/
│   ├── images/
│   └── logos/
│
├── brandbook/
├── docs/
├── newsletter/
├── roadmap/
│
├── website/
│   ├── assets/
│   │   ├── icons/
│   │   ├── images/
│   │   └── logos/
│   └── index.html
│
├── whitepaper/
│
├── .gitattributes
└── README.md
```

## Asset separation

There is an intentional separation between:

`assets/`

and:

`website/assets/`

### Project assets

The root-level directory:

`assets/`

contains project-wide source material and master assets.

Examples:

- original logos
- brand graphics
- source images
- design elements
- master icons
- reusable visual material

These files are not necessarily published directly on the website.

### Website assets

The directory:

`website/assets/`

contains files that are actually used by the public website.

Examples:

```text
website/assets/icons/favicon.svg
website/assets/logos/beyond-the-map.svg
website/assets/images/hero.webp
```

This separation prevents working files and master assets from becoming mixed with production website files.

---

# 3. Local Website Development

The current website entry point is:

`website/index.html`

Website changes should first be tested locally before being published.

## Local testing procedure

1. Open `website/index.html` in Visual Studio Code.
2. Make the required change.
3. Save with `Ctrl + S`.
4. Right-click `index.html`.
5. Select `Open with Live Server`.
6. Verify the result in the browser.

The local address will normally resemble:

`http://127.0.0.1:5500/website/index.html`

The exact port may vary.

## Browser cache

If a saved change does not appear:

`Ctrl + F5`

performs a hard browser refresh.

---

# 4. Publishing Workflow

The normal production workflow is:

```text
Visual Studio Code
        │
        ▼
Edit files
        │
        ▼
Ctrl + S
        │
        ▼
Local test with Live Server
        │
        ▼
GitHub Desktop
        │
        ▼
Review Changes
        │
        ▼
Commit to main
        │
        ▼
Push origin
        │
        ▼
GitHub
        │
        ▼
Cloudflare automatic build
        │
        ▼
Cloudflare deployment
        │
        ▼
Production website
```

The workflow was successfully tested end-to-end during the foundation phase.

---

# 5. GitHub Workflow

After a local change has been tested:

1. Open GitHub Desktop.
2. Verify that the correct repository is selected.
3. Open `Changes`.
4. Review every changed file.
5. Enter a concise commit summary.
6. Add an optional description when useful.
7. Select `Commit to main`.
8. Select `Push origin`.

## Commit messages

Commit summaries should describe the purpose of the change.

Good examples:

```text
Add project README
Create project directory structure
Add technical documentation
Update landing page
Add Beyond the Map favicon
```

Avoid unclear messages such as:

```text
Changes
Update
Test
Stuff
```

---

# 6. Fetch vs Push

These commands perform different tasks.

## Fetch origin

`Fetch origin`

checks whether GitHub contains remote changes that are not yet available locally.

Direction:

```text
GitHub
   ↓
Local repository
```

## Push origin

`Push origin`

publishes local commits to GitHub.

Direction:

```text
Local repository
   ↓
GitHub
```

For normal website publishing after a local edit, the important command is:

`Push origin`

---

# 7. Cloudflare Deployment

Cloudflare is connected directly to the GitHub repository.

Current configuration:

```text
Repository:        sebastianschultrich/beyond-the-map
Production branch: main
Build command:     None
Deploy command:    npx wrangler deploy
Root directory:    /
```

Automatic Git builds are enabled.

A new push to:

`main`

automatically triggers a Cloudflare build and deployment.

The successful production chain is therefore:

```text
VS Code
→ Git
→ GitHub
→ Cloudflare
→ Production
```

No manual upload to Cloudflare is required for normal website updates.

---

# 8. Production Domains

The current digital architecture uses:

## Primary platform

`schultrich.com`

This is the primary public website.

## Expedition project

`latitude9north.com`

Latitude Nine North represents the long-term expedition project within the Beyond the Map ecosystem.

## Brand architecture

The intended relationship is:

```text
Beyond the Map
│
├── Expedition Risk Management
├── Overland
├── Consulting / Auditing
├── Publishing
│
└── Latitude Nine North
    └── Long-term expedition project
```

The domain architecture may evolve when Ghost is introduced.

Any future DNS or hosting changes should be documented here.

---

# 9. Website Assets

Production website assets belong under:

`website/assets/`

Current structure:

```text
website/assets/
│
├── icons/
├── images/
└── logos/
```

## Icons

Location:

`website/assets/icons/`

Examples:

- favicon
- browser icons
- application icons

## Images

Location:

`website/assets/images/`

Examples:

- hero images
- article graphics
- background images

## Logos

Location:

`website/assets/logos/`

Examples:

- Beyond the Map wordmark
- Beyond the Map symbol
- Latitude Nine North marks

Master/source versions should normally remain in the root-level `assets/` directory.

---

# 10. Empty Directories and .gitkeep

Git does not track empty directories.

To preserve the intended project structure, otherwise empty directories contain:

`.gitkeep`

Example:

```text
articles/
└── .gitkeep
```

`.gitkeep` is a convention rather than a special Git command.

Once a directory contains a real tracked file, its `.gitkeep` file can normally be removed.

Example:

Before:

```text
docs/
└── .gitkeep
```

After documentation has been added:

```text
docs/
└── README.md
```

The `.gitkeep` file is no longer required.

---

# 11. Troubleshooting

## Website change does not appear locally

Check:

1. Was the correct file edited?
2. Was the file saved with `Ctrl + S`?
3. Is Live Server displaying `website/index.html`?
4. Perform `Ctrl + F5`.

---

## GitHub Desktop shows no changes

Check:

1. Was the file saved?
2. Is the correct repository open?
3. Is the file located inside the repository?
4. Is the file ignored by `.gitignore`?
5. Is the item actually a file rather than an empty directory?

Remember:

Git does not track empty directories.

---

## GitHub does not show the latest change

Check:

1. Was the change committed?
2. Was `Push origin` selected?
3. Does the commit appear in GitHub Desktop History?
4. Does the commit appear on GitHub?

---

## Cloudflare does not start a build

Check:

1. Was the commit pushed to GitHub?
2. Was it pushed to `main`?
3. Is Cloudflare still connected to the correct repository?
4. Is the production branch still `main`?
5. Open Cloudflare Build History.

---

## Cloudflare build succeeds but website looks unchanged

Check:

1. Was the correct production file changed?
2. Perform `Ctrl + F5`.
3. Verify the active Cloudflare deployment.
4. Verify that the production domain points to the correct Worker.
5. Compare the GitHub version of the file with the local version.

---

# 12. Recovery on a New Computer

If the original development computer is replaced or lost, the project should be recoverable from GitHub.

## Required software

Install:

1. Git
2. GitHub Desktop
3. Visual Studio Code
4. Live Server extension for Visual Studio Code

## Restore repository

Clone:

`sebastianschultrich/beyond-the-map`

using GitHub Desktop.

Open the cloned repository in Visual Studio Code.

The repository should restore:

- website source
- documentation
- project structure
- tracked assets
- Git history

Cloudflare remains connected to GitHub independently of the local computer.

Therefore a replacement computer does not require rebuilding the production website infrastructure from scratch.

## Important

Files that exist only locally and have never been committed and pushed cannot be recovered from GitHub.

For important project files:

**Commit and push regularly.**

---

# 13. Backup Principle

GitHub is the primary version-controlled source repository.

However, important master material may eventually warrant an additional independent backup.

Candidates include:

- Brand Book source files
- original photography
- logo masters
- expedition documentation
- whitepapers
- important research material

Git should not automatically be treated as a replacement for a comprehensive long-term backup strategy.

---

# 14. Future Infrastructure

The current architecture is intentionally simple.

Potential future additions include:

- Ghost publishing
- newsletter infrastructure
- custom email
- analytics
- structured article publishing
- downloadable whitepapers
- additional Beyond the Map pages
- Latitude Nine North integration

These components should only be introduced when they provide a clear operational benefit.

New infrastructure must be documented in this file.

---

# 15. Technical Guiding Principles

The Beyond the Map platform should remain:

- simple
- maintainable
- documented
- portable
- recoverable
- secure
- independent of unnecessary services

The standard rule for website changes is:

**Edit → Save → Test → Review → Commit → Push → Verify**

When infrastructure changes:

**Change it once. Document it immediately.**

---

## Current Foundation Status

As of 09 August 2026:

- Git installed and configured
- Visual Studio Code configured
- GitHub Desktop configured
- GitHub repository operational
- `main` production branch operational
- Cloudflare connected to GitHub
- Automatic Cloudflare builds operational
- Automatic deployments tested successfully
- Production website operational
- Repository documentation established

---

**Beyond the Map**  
*Preparing for the road long before the first mile.*