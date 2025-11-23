# Επίπεδο 8: Χαρακτηριστικά GitHub

## Στόχοι Μάθησης
- Χρήση GitHub Actions για CI/CD
- GitHub Projects για project management
- GitHub Pages για documentation
- Security features και best practices
- Advanced collaboration features

## 📓 Σύνοψη
Το τελικό επίπεδο: automation με GitHub Actions (CI/CD), project management με Projects, hosting με Pages, security features (Dependabot, CodeQL), και προχωρημένα εργαλεία (CLI, API, Codespaces). Εδώ γίνεστε power users!

**Προαπαιτούμενα:** Αθροιστική γνώση από όλα τα προηγούμενα επίπεδα. Τα GitHub features ενσωματώνουν τα πάντα: commits, branches, remotes, PRs, merges, και automation.

## 🔑 Βασικές Έννοιες
- **GitHub Actions**: Automation platform (CI/CD workflows).
- **Workflow**: YAML αρχείο που ορίζει automation.
- **Job**: Ομάδα steps που τρέχουν σε runner.
- **Runner**: Περιβάλλον εκτέλεσης (ubuntu/windows/macos).
- **GitHub Pages**: Static site hosting.
- **Dependabot**: Αυτόματες ενημερώσεις dependencies.
- **CodeQL**: Code scanning για security.
- **Branch Protection**: Κανόνες για merge στο main.

> Ροή CI: Push → Trigger workflow → Run tests → Build → Deploy

## Θεωρία

### GitHub Actions
Το GitHub Actions είναι μια πλατφόρμα CI/CD που σας επιτρέπει να αυτοματοποιήσετε workflows.

### GitHub Projects
Εργαλεία project management ενσωματωμένα στο GitHub.

### GitHub Pages
Δωρεάν static site hosting απευθείας από το repository σας.

## Πρακτική Εφαρμογή

### GitHub Actions

#### Βασική Δομή Workflow

```yaml
# .github/workflows/ci.yml
name: CI Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
    
    - name: Install dependencies
      run: npm install
    
    - name: Run tests
      run: npm test
    
    - name: Build
      run: npm run build
```

#### Συνήθη Workflows

**Automated Testing:**
```yaml
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run tests
        run: |
          npm install
          npm test
```

**Code Linting:**
```yaml
name: Lint

on: [push, pull_request]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run linter
        run: |
          npm install
          npm run lint
```

**Deploy to Production:**
```yaml
name: Deploy

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to server
        env:
          SSH_KEY: ${{ secrets.SSH_KEY }}
        run: |
          # Deployment commands
```

### GitHub Projects

#### Δημιουργία Project

1. Πηγαίνετε στο repository → Projects → New Project
2. Επιλέξτε template (Board, Table, Roadmap)
3. Προσθέστε issues και PRs

#### Kanban Board

Οργανώστε την εργασία σε columns:
- **Backlog**: Μελλοντικές εργασίες
- **To Do**: Προγραμματισμένες εργασίες
- **In Progress**: Τρέχουσες εργασίες
- **Review**: Σε code review
- **Done**: Ολοκληρωμένες

#### Automation

```yaml
# Αυτόματη μετακίνηση καρτών
- When PR opens → Move to "In Review"
- When PR merges → Move to "Done"
- When issue closes → Move to "Done"
```

### GitHub Pages

#### Ενεργοποίηση GitHub Pages

1. Settings → Pages
2. Επιλέξτε source (branch και folder)
3. Το site θα είναι διαθέσιμο στο: `https://username.github.io/repository`

#### Απλή Σελίδα

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
<head>
    <title>My Project</title>
</head>
<body>
    <h1>Welcome to My Project</h1>
    <p>Documentation coming soon...</p>
</body>
</html>
```

#### Jekyll για Documentation

```yaml
# _config.yml
title: My Project Documentation
description: Learn how to use our amazing tool
theme: jekyll-theme-minimal

# Create pages in markdown
# docs/installation.md
# docs/usage.md
```

#### GitHub Actions για Pages

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Build site
        run: |
          npm install
          npm run build
      
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

### GitHub Security Features

#### Dependabot

Αυτόματος έλεγχος για dependencies:

```yaml
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 5
```

#### Code Scanning

```yaml
# .github/workflows/codeql.yml
name: "CodeQL"

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  analyze:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: github/codeql-action/init@v2
      - uses: github/codeql-action/analyze@v2
```

#### Secret Scanning

- Αυτόματη ανίχνευση secrets στο code
- Ειδοποιήσεις για exposed secrets
- Αυτόματος αποκλεισμός pushes με secrets

#### Branch Protection Rules

Settings → Branches → Add rule:
- Require pull request reviews
- Require status checks to pass
- Require branches to be up to date
- Require signed commits
- Include administrators

### GitHub Codespaces

Ένα πλήρες περιβάλλον ανάπτυξης στο cloud (VS Code) που τρέχει στον browser.

- **Άμεση έναρξη:** Δεν χρειάζεται εγκατάσταση εργαλείων τοπικά.
- **Consistent environment:** Όλοι οι developers έχουν τα ίδια εργαλεία (μέσω devcontainer).
- **Πρόσβαση παντού:** Κώδικας από οποιαδήποτε συσκευή.

**Πώς να το ανοίξετε:**
1. Πηγαίνετε στην αρχική σελίδα του repository.
2. Πατήστε το πράσινο κουμπί **Code**.
3. Επιλέξτε την καρτέλα **Codespaces**.
4. Πατήστε **Create codespace on main**.

### GitHub Advanced Features

#### GitHub CLI

```bash
# Εγκατάσταση
brew install gh

# Authentication
gh auth login

# Δημιουργία repository
gh repo create my-new-repo

# Clone repository
gh repo clone username/repo

# Δημιουργία issue
gh issue create --title "Bug report" --body "Description"

# Δημιουργία PR
gh pr create --title "New feature" --body "Description"

# Προβολή PRs
gh pr list

# Review PR
gh pr review --approve

# Merge PR
gh pr merge
```

#### GitHub Discussions

- Κοινοτική συζήτηση
- Q&A format
- Announcements
- Polls

#### GitHub Sponsors

- Υποστήριξη open source developers
- Τiers με benefits
- One-time ή monthly contributions

#### GitHub Packages

```bash
# Publish package
npm publish

# Install from GitHub Packages
npm install @username/package
```

### GitHub API

```bash
# REST API
curl https://api.github.com/repos/username/repo

# GraphQL API
curl -H "Authorization: bearer TOKEN" \
     -X POST \
     -d '{"query": "query { viewer { login } }"}' \
     https://api.github.com/graphql
```

## Ασκήσεις

### Άσκηση 1: Setup CI Pipeline

1. Δημιουργήστε `.github/workflows/ci.yml`
2. Προσθέστε tests και linting
3. Push και δείτε το workflow να τρέχει
4. Κάντε το badge στο README

```markdown
![CI](https://github.com/username/repo/workflows/CI/badge.svg)
```

### Άσκηση 2: GitHub Pages

1. Δημιουργήστε `docs/` folder με `index.html`
2. Ενεργοποιήστε GitHub Pages
3. Επισκεφθείτε το site
4. Προσθέστε documentation pages

### Άσκηση 3: Project Board

1. Δημιουργήστε νέο Project
2. Προσθέστε issues για features
3. Οργανώστε σε columns
4. Συνδέστε PRs με issues

### Άσκηση 4: Branch Protection

1. Ενεργοποιήστε branch protection για `main`
2. Require reviews
3. Require status checks
4. Δοκιμάστε με PR

## Προχωρημένα Patterns

### Monorepo Management

```yaml
# Conditional workflows based on changed files
on:
  push:
    paths:
      - 'packages/frontend/**'
      
jobs:
  frontend:
    if: contains(github.event.head_commit.message, '[frontend]')
    # ...
```

### Matrix Builds

```yaml
jobs:
  test:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]
        node: [14, 16, 18]
    steps:
      - uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node }}
```

### Reusable Workflows

```yaml
# .github/workflows/reusable.yml
on:
  workflow_call:
    inputs:
      environment:
        required: true
        type: string

# .github/workflows/prod.yml
jobs:
  deploy:
    uses: ./.github/workflows/reusable.yml
    with:
      environment: production
```

## Καλές Πρακτικές

### GitHub Actions
- Pin action versions για σταθερότητα
- Χρησιμοποιήστε secrets για sensitive data
- Cache dependencies για ταχύτητα
- Fail fast στα matrix builds

### Documentation
- Κρατήστε το README ενημερωμένο
- Χρησιμοποιήστε Pages για λεπτομερές documentation
- Προσθέστε badges για status
- Include getting started guide

### Security
- Ενεργοποιήστε Dependabot
- Χρησιμοποιήστε code scanning
- Regular security audits
- Χρησιμοποιήστε signed commits

## ✅ Checklist Εμπέδωσης
- [ ] Δημιούργησα GitHub Actions workflow για tests.
- [ ] Ρύθμισα GitHub Pages για documentation.
- [ ] Ενεργοποίησα Dependabot.
- [ ] Έβαλα branch protection rules στο main.
- [ ] Χρησιμοποίησα GitHub CLI για PR creation.

## 🧪 Mini Quiz
1. Τι είναι το GitHub Actions; (α) CI/CD platform ✓ (β) Editor
2. GitHub Pages φιλοξενεί; (α) Static sites ✓ (β) Databases
3. Dependabot; (α) Ενημερώνει dependencies ✓ (β) Κάνει review

## ⚠️ Συνηθισμένα Λάθη
- Secrets στον κώδικα αντί στα GitHub Secrets.
- Workflows χωρίς cache → αργά builds.
- Branch protection χωρίς status checks → broken main.
- Ξεχνάτε να ενημερώσετε documentation.

## 💡 Συμβουλή
Ξεκινήστε με απλό CI workflow (tests) και προσθέτετε σταδιακά features.

## 🔁 CI/CD Pipeline Example
1. Developer push code
2. GitHub Actions triggered
3. Run linting
4. Run tests
5. Build application
6. Deploy to staging (if main branch)
7. Notify team

## 🔐 Security Checklist
- [ ] Dependabot enabled
- [ ] CodeQL scanning enabled
- [ ] Secret scanning enabled
- [ ] Branch protection on main
- [ ] Require PR reviews
- [ ] Require status checks
- [ ] No force push allowed
- [ ] Signed commits (optional)

## 🚀 Deployment Strategies
- **Continuous Deployment**: Κάθε merge → production
- **Continuous Delivery**: Merge → staging, manual → production
- **Feature Flags**: Deploy αλλά ενεργοποίηση on-demand

## 📚 Mini Glossary
- **CI**: Continuous Integration (auto-test on every commit)
- **CD**: Continuous Deployment/Delivery (auto-deploy)
- **Runner**: Μηχανή που εκτελεί workflows
- **Artifact**: Build output που αποθηκεύεται
- **Matrix**: Παράλληλα builds σε διαφορετικά OS/versions

## 📝 Προσωπικές Σημειώσεις
```
(π.χ. "Έφτιαξα το πρώτο μου CI pipeline!")
```

## Συμπέρασμα

Συγχαρητήρια! Ολοκληρώσατε όλα τα επίπεδα του Git και GitHub curriculum. 

### Τι μάθατε:
- ✅ Βασικές έννοιες Git
- ✅ Daily Git operations
- ✅ Branching και merging
- ✅ Remote collaboration
- ✅ GitHub workflow
- ✅ Advanced Git techniques
- ✅ GitHub automation και features

### Επόμενα Βήματα:
1. Πρακτική εξάσκηση με πραγματικά projects
2. Συμμετοχή σε open source
3. Εξερεύνηση advanced Git internals
4. Δημιουργία custom Git tools

### Χρήσιμοι Πόροι:
- [Git Official Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com)
- [Pro Git Book](https://git-scm.com/book)
- [GitHub Learning Lab](https://lab.github.com)

## Επιστροφή
Επιστρέψτε στο [κεντρικό README](../) για επισκόπηση όλων των επιπέδων.
