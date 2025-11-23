# Επίπεδο 7: Προχωρημένα Θέματα

## Στόχοι Μάθησης
- Χρήση του git stash
- Reset, revert και checkout
- Git tags και releases
- Git hooks και automation
- Submodules και subtrees

## 📓 Σύνοψη
Προχωρημένα εργαλεία διάσωσης και διαχείρισης: stash για προσωρινή αποθήκευση, reset/revert για αναίρεση, tags για releases, hooks για automation. Εδώ μαθαίνετε να διορθώνετε λάθη και να αυτοματοποιείτε.

## 🔑 Βασικές Έννοιες
- **Stash**: Προσωρινή αποθήκευση αλλαγών χωρίς commit.
- **Reset**: Μετακίνηση HEAD (--soft/--mixed/--hard).
- **Revert**: Δημιουργία νέου commit που αναιρεί παλιό.
- **Tag**: Ετικέτα σε commit (συνήθως για versions).
- **Reflog**: Ιστορικό όλων των HEAD κινήσεων (διάσωση!).
- **Bisect**: Binary search για bug-introducing commit.
- **Hooks**: Scripts που τρέχουν σε events (pre-commit, pre-push).

> Ιεραρχία καταστροφής: checkout < reset --soft < reset --mixed < reset --hard

## Θεωρία

### Git Stash
Το stash σας επιτρέπει να αποθηκεύσετε προσωρινά τις αλλαγές σας χωρίς να κάνετε commit.

### Reset vs Revert vs Checkout
- **Reset**: Μετακινεί το HEAD και (προαιρετικά) αλλάζει το staging/working directory
- **Revert**: Δημιουργεί νέο commit που αναιρεί προηγούμενο commit
- **Checkout**: Μετακινεί το HEAD ή επαναφέρει αρχεία

## Πρακτική Εφαρμογή

### Git Stash

```bash
# Αποθήκευση τρεχουσών αλλαγών
git stash

# Αποθήκευση με μήνυμα
git stash save "Work in progress on feature X"

# Προβολή stash list
git stash list

# Εφαρμογή του τελευταίου stash
git stash apply

# Εφαρμογή και διαγραφή του stash
git stash pop

# Εφαρμογή συγκεκριμένου stash
git stash apply stash@{2}

# Διαγραφή stash
git stash drop stash@{0}

# Διαγραφή όλων των stashes
git stash clear

# Stash συμπεριλαμβανομένων untracked files
git stash -u

# Δημιουργία branch από stash
git stash branch feature-from-stash
```

### Git Reset

```bash
# Soft reset: Κρατάει αλλαγές στο staging
git reset --soft HEAD~1

# Mixed reset (default): Κρατάει αλλαγές στο working directory
git reset HEAD~1
git reset --mixed HEAD~1

# Hard reset: Διαγράφει όλες τις αλλαγές (ΠΡΟΣΟΧΗ!)
git reset --hard HEAD~1

# Reset συγκεκριμένου αρχείου
git reset HEAD file.txt

# Reset σε συγκεκριμένο commit
git reset --hard abc123
```

### Git Revert

```bash
# Αναίρεση τελευταίου commit (δημιουργεί νέο commit)
git revert HEAD

# Αναίρεση συγκεκριμένου commit
git revert abc123

# Αναίρεση πολλαπλών commits
git revert abc123..def456

# Revert χωρίς αυτόματο commit
git revert -n HEAD
```

### Git Checkout (Επαναφορά αρχείων)

```bash
# Επαναφορά αρχείου από το τελευταίο commit
git checkout -- file.txt

# Επαναφορά από συγκεκριμένο commit
git checkout abc123 -- file.txt

# Επαναφορά όλων των αρχείων
git checkout -- .
```

### Git Tags

```bash
# Δημιουργία lightweight tag
git tag v1.0.0

# Δημιουργία annotated tag (προτιμάται)
git tag -a v1.0.0 -m "Release version 1.0.0"

# Προβολή όλων των tags
git tag
git tag -l "v1.*"

# Προβολή πληροφοριών tag
git show v1.0.0

# Tag συγκεκριμένου commit
git tag -a v1.0.1 abc123 -m "Bugfix release"

# Push tags στο remote
git push origin v1.0.0
git push origin --tags

# Διαγραφή tag
git tag -d v1.0.0
git push origin --delete v1.0.0

# Checkout tag
git checkout v1.0.0
```

### Git Reflog

```bash
# Προβολή όλων των αναφορών HEAD
git reflog

# Προβολή reflog για συγκεκριμένο branch
git reflog show main

# Επαναφορά σε προηγούμενη κατάσταση
git reset --hard HEAD@{5}
```

### Git Bisect (Εύρεση bug)

```bash
# Ξεκινήστε το bisect
git bisect start

# Σημειώστε το τρέχον commit ως bad
git bisect bad

# Σημειώστε ένα γνωστό good commit
git bisect good abc123

# Git θα κάνει checkout ένα commit στη μέση
# Δοκιμάστε το και σημειώστε:
git bisect good  # ή
git bisect bad

# Συνεχίστε μέχρι να βρεθεί το προβληματικό commit

# Τερματισμός bisect
git bisect reset
```

### Git Hooks

Git hooks είναι scripts που εκτελούνται αυτόματα σε συγκεκριμένα events.

```bash
# Hooks βρίσκονται στο .git/hooks/

# Κοινά hooks:
# - pre-commit: Πριν το commit
# - prepare-commit-msg: Προετοιμασία commit message
# - commit-msg: Έλεγχος commit message
# - post-commit: Μετά το commit
# - pre-push: Πριν το push
# - post-merge: Μετά το merge
```

Παράδειγμα pre-commit hook:
```bash
#!/bin/sh
# .git/hooks/pre-commit

# Έλεγχος για trailing whitespace
git diff-index --check --cached HEAD --
```

### Git Aliases

```bash
# Δημιουργία alias
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit

# Πιο σύνθετα aliases
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual 'log --graph --oneline --all'

# Χρήση alias
git st
git co main
git visual
```

### Git Submodules

```bash
# Προσθήκη submodule
git submodule add https://github.com/user/repo.git path/to/submodule

# Clone repository με submodules
git clone --recursive https://github.com/user/repo.git

# Ενημέρωση submodules
git submodule update --init --recursive

# Pull αλλαγών στα submodules
git submodule update --remote

# Προβολή status submodules
git submodule status
```

## Ασκήσεις

### Άσκηση 1: Stash Workflow
```bash
# Εργασία σε feature
echo "Feature work" >> feature.txt
git add feature.txt

# Αλλαγή προτεραιότητας - stash την εργασία
git stash save "WIP: feature development"

# Κάντε bugfix
git checkout -b hotfix
# ... κάντε fix ...
git commit -am "Fix critical bug"
git checkout main

# Επιστροφή στο feature
git stash pop
```

### Άσκηση 2: Reset Scenarios
```bash
# Ακύρωση τελευταίου commit αλλά κρατήστε αλλαγές
git reset --soft HEAD~1

# Επαναφορά αρχείου
git checkout -- wrongfile.txt

# Επαναφορά σε παλιό commit (ΠΡΟΣΟΧΗ!)
git reset --hard abc123
```

### Άσκηση 3: Tagging Release
```bash
# Δημιουργήστε release tag
git tag -a v1.0.0 -m "First stable release"

# Προβολή tag
git show v1.0.0

# Push tag
git push origin v1.0.0
```

## Καλές Πρακτικές

### Για Stash
- Χρησιμοποιήστε περιγραφικά μηνύματα
- Μην κρατάτε stashes για μεγάλο χρονικό διάστημα
- Εφαρμόστε stashes σύντομα

### Για Reset
- Χρησιμοποιήστε `--soft` για ακύρωση commits
- Αποφύγετε `--hard` σε shared branches
- Χρησιμοποιήστε revert αντί για reset σε public commits

### Για Tags
- Χρησιμοποιήστε semantic versioning (v1.2.3)
- Annotated tags είναι καλύτερα από lightweight
- Tag σημαντικά milestones και releases

## ✅ Checklist Εμπέδωσης
- [ ] Χρησιμοποίησα `git stash` για προσωρινή αποθήκευση.
- [ ] Έκανα `git reset` για ακύρωση commit (με --soft).
- [ ] Έκανα `git revert` για αναίρεση public commit.
- [ ] Δημιούργησα annotated tag για release.
- [ ] Κατανοώ τη διαφορά reset vs revert vs checkout.

## 🧪 Mini Quiz
1. Τι κρατά το stash; (α) Uncommitted changes ✓ (β) Commits
2. `git reset --hard`; (α) Διαγράφει όλα ✓ (β) Κρατά στο staging
3. Για public commit χρησιμοποιούμε; (α) revert ✓ (β) reset

## ⚠️ Συνηθισμένα Λάθη
- `git reset --hard` χωρίς backup → χάνετε δουλειά.
- Reset σε public commit → ξαναγράφετε ιστορία.
- Stash πολλές αλλαγές και ξεχνάτε τι έχετε.
- Lightweight tags αντί annotated → λείπουν metadata.

## 💡 Συμβουλή Διάσωσης
Αν κάνατε λάθος: `git reflog` → βρείτε το παλιό commit → `git reset --hard HEAD@{N}`

## 🔁 Recovery Strategies

| Σενάριο | Λύση |
|---------|------|
| Θέλω να ακυρώσω τελευταίο commit | `git reset --soft HEAD~1` |
| Έκανα λάθος merge | `git reset --hard ORIG_HEAD` |
| Διέγραψα κατά λάθος branch | `git reflog` → `git checkout -b branch SHA` |
| Θέλω να αναιρέσω public commit | `git revert SHA` |
| Έχασα αλλαγές | `git reflog` + `git reset` |

## 🎯 Quick Command Reference
```bash
# Stash
git stash save "message"
git stash list
git stash pop

# Reset levels
git reset --soft HEAD~1   # Ακύρωση commit, κρατά staging
git reset --mixed HEAD~1  # Ακύρωση commit, αφαιρεί από staging
git reset --hard HEAD~1   # Ακύρωση commit, διαγραφή αλλαγών

# Tags
git tag -a v1.0.0 -m "Release 1.0"
git push origin v1.0.0

# Reflog
git reflog
git reset --hard HEAD@{2}
```

## 📝 Προσωπικές Σημειώσεις
```
(π.χ. "Έσωσα το project με reflog!")
```

## Επόμενο Βήμα
Μετά την ολοκλήρωση αυτού του επιπέδου, προχωρήστε στο [Επίπεδο 8: Χαρακτηριστικά GitHub](../08-Χαρακτηριστικά-GitHub/)
