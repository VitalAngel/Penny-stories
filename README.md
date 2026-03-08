Project: Penny Stories — youth storytelling & civic engagement
Description
Penny Stories invites kids (ages ~9–13) to finish Roald Dahl’s unfinished “Penny” story, publish their digital books, and contribute simple, consented opinions about the value of a penny. The site will host a community anthology, display submissions, and collect anonymized responses for basic civic-attitude exploration.

Goals

Build a kid-friendly front page with clear branding and a hero section.
Provide a simple submission workflow (form + file upload).
Publish selected stories as digital pages (Quarto/HTML).
Collect and visualize anonymized responses in a basic dashboard.
Grow iteratively: frontend → submission flow → backend → analytics.
Planned tech & tools

Frontend: HTML/CSS/JS (static → React/Vite if needed).
Content & docs: Quarto (.qmd) + Markdown for reproducible story pages.
Backend: Python (Flask or FastAPI) or AWS serverless (Lambda + API Gateway).
Data: start with SQLite, migrate to RDS if needed; enforce de-identification and consent.
Version control & hosting: Git + GitHub (Pages / Netlify); CI via GitHub Actions.
Development: PyCharm or VS Code; Quarto CLI for rendering.

Milestones (phase 1)

Complete Python basics (lessons 1–16).
Create GitHub repo and initial project structure.
Design branding and hero (mockup + CSS tokens).
Build and publish a static landing page via GitHub Pages.
Add a simple submission stub/form and Quarto story page example.

Notes

Store design assets in docs/ or static/; track tasks with Issues and Projects.
Prioritize privacy and age-appropriate consent for student submissions.

This README is a living document — update as you iterate.


index.qmd (paste into index.qmd at repo root)
title: "Penny Stories" format: html execute: echo: true
Penny Stories
Penny Stories
Finish the story. Share your voice. Celebrate young writers.

Submit a story
Penny Stories hero
About the project
Penny Stories invites children (ages ~9–13) to finish an unfinished story and share their digital books. This site will host the anthology, showcase selected works, and collect anonymized responses on the value of a penny for simple civic research.

Demo data table (example)

{python}


import pandas as pd
df = pd.DataFrame({"title":["Demo Story"], "author":["A Student"], "status":["published"]})
df

Submit (prototype)
This is a placeholder for the submission form. Later we will add a backend endpoint to accept files and metadata.

_quarto.yml (paste into _quarto.yml at repo root)
project:
  type: website
website:
  title: "Penny Stories"
  navbar:
 right:

text: "Home" href: index.html
text: "About" href: index.html#about
text: "Submit" href: index.html#submit
static/styles.css (create folder static/ and file static/styles.css)
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial;
  margin: 0;
  color: #222;
}
.hero {
  display: flex;
  gap: 2rem;
  align-items: center;
  padding: 3rem;
  background: linear-gradient(135deg,#fff8e6,#f7f0ff);
}
.hero-content { max-width: 600px; }
.hero h1 { margin: 0 0 0.5rem 0; font-size: 2.6rem; color:#2b2b7a; }
.hero p { margin: 0 0 1rem 0; font-size:1.1rem; }
.cta {
  display:inline-block;
  padding:0.6rem 1rem;
  background:#ff7a59;
  color:white;
  text-decoration:none;
  border-radius:6px;
}
.hero-image img { max-width:240px; height:auto; border-radius:8px; box-shadow:0 6px 18px rgba(0,0,0,0.08); }

.gitignore (paste into .gitignore at repo root)

Python
pycache/
.pyc
.venv/
venv/
.env
.env.
.ipynb_checkpoints

macOS
.DS_Store

Quarto output
_site/
.quarto/

IDEs
.idea/
.vscode/

.github/workflows/quarto-render.yml (create folders .github/workflows/ and paste file) name: Render and Publish Quarto Site on: push: branches:
main
jobs:
  build-and-deploy:
 runs-on: ubuntu-latest
 steps:

name: Checkout repo
uses: actions/checkout@v4

name: Setup Python
uses: actions/setup-python@v4
with:
  python-version: '3.10'

name: Install system deps
run: |
  sudo apt-get update
  sudo apt-get install -y pandoc

name: Install Quarto CLI
run: |
  wget https://github.com/quarto-dev/quarto-cli/releases/latest/download/quarto-linux-amd64.deb -O quarto.deb
  sudo dpkg -i quarto.deb || sudo apt-get -f install -y

name: Install Python deps
run: |
  python -m pip install --upgrade pip
  pip install pandas plotly

name: Render site
run: quarto render

name: Deploy to GitHub Pages
uses: peaceiris/actions-gh-pages@v3
with:
  github_token: ${{ secrets.GITHUB_TOKEN }}
  publish_dir: ./_site

Quick next steps (one-line reminders)

Save files above into your PyCharm project root (create folders static and .github/workflows).
Commit: git add . && git commit -m "Add starter site, Quarto config, styles, and workflow".
Push to GitHub (create repo on GitHub and add remote, or use PyCharm Git integration).
Install Quarto on mac: https://quarto.org/docs/get-started/ (so you can run quarto render locally).
When you push to main, the workflow will run and publish the site to gh-pages.
If you want, I can now:

Provide a brief paste-ready commit sequence for your terminal, or
Produce a tiny hero image SVG and a short consent-text stub for the submission form to include next. Which do you want next?
