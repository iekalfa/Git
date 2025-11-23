# Επίπεδο 5: Συνεργασία στο GitHub

## Στόχοι Μάθησης
- Κατανόηση του GitHub workflow
- Δημιουργία και διαχείριση Pull Requests
- Code review και συνεργασία
- Forks και contribution σε open source

## 📓 Σύνοψη
Εδώ μαθαίνουμε τον επαγγελματικό τρόπο συνεργασίας: Forks, Pull Requests, Code Review, Issues. Αυτό είναι το workflow που χρησιμοποιούν όλες οι ομάδες και τα open source projects.

**Προαπαιτούμενα:** Συνδυάζουμε γνώσεις από Επίπεδο 3 (branches) και Επίπεδο 4 (remotes) για επαγγελματική συνεργασία.

## 🔑 Βασικές Έννοιες
- **Fork**: Προσωπικό αντίγραφο repository άλλου.
- **Pull Request (PR)**: Αίτημα συγχώνευσης αλλαγών σας.
- **upstream**: Το αρχικό repository (όταν έχετε fork).
- **origin**: Το δικό σας fork.
- **Code Review**: Έλεγχος κώδικα πριν το merge.
- **Issue**: Αναφορά bug, feature request ή συζήτηση.

> Ροή: Fork → Clone → Branch → Commits → Push → Pull Request → Review → Merge

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
Αφού κάνετε fork, το repository ανήκει σε εσάς. Τώρα πρέπει να το κατεβάσετε στον υπολογιστή σας για να εργαστείτε. Επίσης, είναι καλή πρακτική να συνδέσετε και το αρχικό repository (ως `upstream`) για να παίρνετε ενημερώσεις.

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
Για να προτείνετε αλλαγές, δεν πειράζετε ποτέ το `main` branch. Δημιουργείτε πάντα ένα ξεχωριστό branch, κάνετε εκεί τη δουλειά σας και το στέλνετε στο GitHub.

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
Όσο εσείς εργάζεστε, το αρχικό project μπορεί να έχει προχωρήσει. Πρέπει να συγχρονίζετε το fork σας τακτικά για να αποφύγετε συγκρούσεις.

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
Μπορείτε να κλείσετε αυτόματα ένα issue όταν γίνει merge το PR σας, χρησιμοποιώντας ειδικές λέξεις-κλειδιά στο μήνυμα του commit ή στην περιγραφή του PR.

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

## ✅ Checklist Εμπέδωσης
- [ ] Έκανα fork repository και το clone τοπικά.
- [ ] Δημιούργησα Pull Request και περίμενα review.
- [ ] Έκανα code review σε PR άλλου.
- [ ] Σύνδεσα PR με issue χρησιμοποιώντας `fixes #N`.
- [ ] Ενημέρωσα το fork μου από το upstream.

## 🧪 Mini Quiz
1. Τι είναι το fork; (α) Αντίγραφο στο δικό σας account ✓ (β) Clone τοπικά
2. Το PR; (α) Αίτημα merge ✓ (β) Issue
3. Πώς κλείνω issue αυτόματα; (α) `fixes #123` στο commit ✓ (β) Χειροκίνητα

## ⚠️ Συνηθισμένα Λάθη
- Push στο upstream αντί για το origin (δεν έχετε δικαιώματα).
- Μεγάλα PRs (>500 γραμμές) → δύσκολο review.
- Κακογραμμένες περιγραφές PR → δεν καταλαβαίνει κανείς τι κάνετε.
- Ξεχνάτε να ενημερώσετε το fork από upstream → conflicts.

## 💡 Συμβουλή για Reviewers
- Κάντε constructive comments: "Θα ήταν καλύτερο αν..." αντί "Λάθος!".

## 💡 Συμβουλή για Authors
- Μικρά, focused PRs → γρηγορότερο review και merge.

## 🔁 Ανακεφαλαίωση Workflow
1. Fork repository
2. Clone το fork σας
3. Προσθέστε upstream remote
4. Δημιουργήστε feature branch
5. Κάντε commits
6. Push στο origin (fork)
7. Δημιουργήστε PR από fork → upstream
8. Αντιμετωπίστε review comments
9. Μετά το merge, ενημερώστε fork από upstream

## 📋 PR Description Template
```markdown
## Τι αλλάζει
[Σύντομη περιγραφή]

## Γιατί
[Αιτιολόγηση]

## Πώς δοκιμάστηκε
- [ ] Τοπικά tests
- [ ] Manual testing

## Screenshots (αν UI)
[Εικόνες]

## Fixes
Fixes #123
```

## 📝 Προσωπικές Σημειώσεις
```
(π.χ. "Πρώτο μου PR σε open source project!")
```

## Επόμενο Βήμα
Μετά την ολοκλήρωση αυτού του επιπέδου, προχωρήστε στο [Επίπεδο 6: Προχωρημένα Branches](../06-Προχωρημένα-Branches/)
