# Επίπεδο 5: Συνεργασία στο GitHub

## Στόχοι Μάθησης
- Κατανόηση του GitHub workflow
- Δημιουργία και διαχείριση Pull Requests
- Code review και συνεργασία
- Forks και contribution σε open source

## Θεωρία

### GitHub Workflow
Ο τυπικός workflow συνεργασίας στο GitHub περιλαμβάνει:
1. Fork του repository (για εξωτερικά projects)
2. Clone του repository
3. Δημιουργία feature branch
4. Υλοποίηση αλλαγών και commits
5. Push του branch
6. Δημιουργία Pull Request
7. Code review
8. Merge στο κύριο branch

### Τι είναι το Pull Request;
Ένα Pull Request (PR) είναι ένα αίτημα για να συγχωνεύσετε τις αλλαγές σας σε ένα άλλο branch. Επιτρέπει code review και συζήτηση πριν το merge.

## Πρακτική Εφαρμογή

### Forking Repository

1. Πηγαίνετε στο repository που θέλετε να συνεισφέρετε
2. Κάντε κλικ στο κουμπί "Fork" στο GitHub
3. Τώρα έχετε ένα αντίγραφο στο δικό σας account

### Cloning Forked Repository

```bash
# Clone το forked repository
git clone https://github.com/yourusername/repository.git
cd repository

# Προσθέστε το original repository ως upstream
git remote add upstream https://github.com/originalowner/repository.git

# Ελέγξτε τα remotes
git remote -v
```

### Δημιουργία Pull Request

```bash
# Δημιουργήστε νέο branch για το feature σας
git checkout -b feature-new-functionality

# Κάντε τις αλλαγές σας
# ...

# Commit τις αλλαγές
git add .
git commit -m "Προσθήκη νέας λειτουργικότητας"

# Push στο GitHub
git push origin feature-new-functionality
```

Στη συνέχεια:
1. Πηγαίνετε στο GitHub repository
2. Κάντε κλικ "Compare & pull request"
3. Γράψτε περιγραφή του PR
4. Κάντε κλικ "Create pull request"

### Ενημέρωση Fork από Upstream

```bash
# Fetch αλλαγές από το upstream
git fetch upstream

# Μεταβείτε στο main branch
git checkout main

# Merge τις αλλαγές από το upstream
git merge upstream/main

# Push στο δικό σας fork
git push origin main
```

### Code Review

Ως Reviewer:
- Ελέγξτε τις αλλαγές προσεκτικά
- Κάντε constructive comments
- Ζητήστε αλλαγές αν χρειάζεται
- Εγκρίνετε (approve) το PR αν είναι καλό

Ως Author:
- Απαντήστε σε comments
- Κάντε τις ζητούμενες αλλαγές
- Push νέα commits στο ίδιο branch
- Ζητήστε re-review

## Issues

### Δημιουργία Issue

Τα Issues χρησιμοποιούνται για:
- Bug reports
- Feature requests
- Ερωτήσεις και συζητήσεις
- Παρακολούθηση εργασιών

### Σύνδεση PR με Issues

```bash
# Στο μήνυμα commit ή στην περιγραφή του PR
git commit -m "Διόρθωση bug στο login (fixes #42)"
```

Λέξεις-κλειδιά που κλείνουν issues:
- `fixes #123`
- `closes #123`
- `resolves #123`

## Ασκήσεις

### Άσκηση 1: Contribution σε Δημόσιο Repository
1. Βρείτε ένα repository με "good first issue" label
2. Κάντε fork το repository
3. Clone το forked repository
4. Δημιουργήστε feature branch
5. Κάντε την αλλαγή
6. Push και δημιουργήστε Pull Request

### Άσκηση 2: Code Review
1. Βρείτε ένα ανοιχτό Pull Request
2. Διαβάστε τις αλλαγές
3. Κάντε comments σε γραμμές κώδικα
4. Κάντε γενικό review comment

### Άσκηση 3: Διαχείριση Conflicts
1. Δημιουργήστε PR που έχει conflicts
2. Ενημερώστε το branch σας από το main
3. Λύστε τα conflicts τοπικά
4. Push την επίλυση

```bash
# Ενημέρωση με το main branch
git checkout main
git pull origin main
git checkout feature-branch
git merge main

# Λύστε τα conflicts
# Επεξεργαστείτε τα αρχεία με conflicts
git add .
git commit -m "Επίλυση conflicts"
git push origin feature-branch
```

## Καλές Πρακτικές για Pull Requests

### Μηνύματα Commit
- Χρησιμοποιήστε περιγραφικά μηνύματα
- Πρώτη γραμμή: σύντομη περίληψη (<50 χαρακτήρες)
- Κενή γραμμή
- Λεπτομερής περιγραφή (αν χρειάζεται)

### PR Description
- Εξηγήστε τι αλλάζει το PR
- Γιατί χρειάζεται αυτή η αλλαγή
- Πώς έχει δοκιμαστεί
- Screenshots για UI changes
- Αναφέρετε σχετικά issues

### Μέγεθος PR
- Κρατήστε τα PRs μικρά και focused
- Ένα PR = Ένα feature/bugfix
- Μεγάλα PRs είναι δύσκολα στο review

## GitHub Projects και Automation

### Projects
Χρησιμοποιήστε GitHub Projects για:
- Οργάνωση issues και PRs
- Kanban boards
- Milestone tracking

### GitHub Actions (Preview)
- Automated testing
- CI/CD pipelines
- Automated workflows

## Επόμενο Βήμα
Μετά την ολοκλήρωση αυτού του επιπέδου, προχωρήστε στο [Επίπεδο 6: Προχωρημένα Branches](../06-Προχωρημένα-Branches/)
