# Guide: Create a Pull Request on GitHub (New Repo Workflow)

This is is here to help you will create your **own repository**, add your some content on a feature branch, and open a **Pull Request (PR)** to request feedback from classmates.

---

## What is a Pull Request?

A **Pull Request (PR)** proposes changes from one branch (yours) into another branch (usually `main`).  
It enables **discussion, review, and approval** before merging.

---

## Prerequisites

- A GitHub account
- Git installed on your computer
- A terminal (or Git Bash) and a code editor

---

## Step-by-Step

### 1) Create a New Repository on GitHub
1. Go to GitHub and click the **+** (top-right) → **New repository**.  
2. Name it (e.g., `semantic-html-exercise`).  
3. Set **Visibility** to **Public** so classmates can see it.  
4. **Do not** add a README, .gitignore, or license (we want your first PR to add the initial content).  
5. Click **Create repository**.

> If you accidentally added a README, that’s OK—your first PR will just add your HTML files alongside it.

---

### 2) Clone Your Repository Locally
```bash
git clone https://github.com/YOUR-USERNAME/semantic-html-exercise.git
cd semantic-html-exercise
```

**Attention**: Replace `YOUR-USERNAME` with your github username.

---

### 3) Create a Feature Branch
(Always avoid committing directly to `main`.)
```bash
git checkout -b add-my-semantic-refactor
```

After `-b` is the name of your branch, this can by anything you want, for example, I like
making my branches follow a URL path pattern, like so: `feature/refactring-page`.

---

### 4) Add Your Files
Create your initial content (for this exercise, an `index.html` with your semantic refactor).
```bash
# Example on macOS/Linux:
touch index.html

# Example on Windows PowerShell:
ni index.html
```
Open `index.html` in your editor and add your code.

---

### 5) Stage and Commit Your Changes
```bash
git add index.html
git commit -m "Add first version of semantic HTML refactor"
```

---

### 6) Push Your Branch to GitHub
```bash
git push origin add-my-semantic-refactor
```

---

### 7) Open the Pull Request
1. Go to your repository on GitHub.  
2. You should see a banner: **Compare & pull request** → click it.  
   - If not, go to **Pull requests** → **New pull request**, then select:
     - **Base**: `main`
     - **Compare**: `add-my-semantic-refactor`
3. Fill in the PR form:
   - **Title**: `Add first version of semantic HTML refactor`
   - **Description**: Briefly explain what you did and what feedback you want (e.g., *heading structure*, *use of `<section>` & `<article>`*, *form accessibility*).
4. Click **Create pull request**.

---

## Requesting Feedback

- Mention classmates with `@username`.  
- Ask **specific** questions, for example:
  - “Is my heading hierarchy (`h1` → `h2` → `h3`) correct?”
  - “Did I use `<section>`, `<article>`, `<aside>`, and `<nav>` appropriately?”
  - “Any improvements for accessibility (labels, alt text, landmarks)?”

---

## Good Code Review Practices

- **Be constructive**: propose solutions, not just problems.  
- **Be specific**: explain *why* a change helps.  
- **Be respectful**: critique the code, not the author.  
- **Keep PRs focused**: smaller, clear changes are easier to review.

**Recommended reading:**
- GitHub Docs — *About Pull Requests*: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests  
- Atlassian — *Code Review Best Practices*: https://www.atlassian.com/agile/software-development/code-reviews  
- Google — *How to Do a Code Review*: https://google.github.io/eng-practices/review/

---

## Troubleshooting

- **No “Compare & pull request” banner?**  
  Go to **Pull requests** → **New pull request**, choose **base: `main`** and **compare: your branch**.

- **“Nothing to compare” message?**  
  Make sure you committed changes on your feature branch and pushed it to GitHub.

- **Wrong repo URL on clone?**  
  Check the URL on your repo’s **Code** (green) button and copy the HTTPS link again.

---

## Submission Checklist

- [ ] Branch created from `main` (e.g., `add-my-semantic-refactor`)  
- [ ] `index.html` added with your semantic refactor  
- [ ] Commit message is clear  
- [ ] PR opened to `main` with a short, helpful description  
- [ ] Specific feedback requested from classmates

Good luck, and happy reviewing!
