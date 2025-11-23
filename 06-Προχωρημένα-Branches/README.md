# Επίπεδο 6: Προχωρημένα Branches

## Στόχοι Μάθησης
- Κατανόηση του rebase
- Merge strategies
- Cherry-picking commits
- Διαχείριση συγκρούσεων

## Θεωρία

### Merge vs Rebase

**Merge:**
- Δημιουργεί ένα νέο merge commit
- Διατηρεί το πλήρες ιστορικό
- Ασφαλέστερο για shared branches

**Rebase:**
- Ξαναγράφει το ιστορικό
- Δημιουργεί γραμμικό ιστορικό
- Κατάλληλο για feature branches

### Πότε να χρησιμοποιείτε κάθε μέθοδο
- **Merge**: Για integration από shared branches
- **Rebase**: Για cleanup του feature branch πριν το merge
- **Ποτέ rebase σε public branches!**

## Πρακτική Εφαρμογή

### Rebase

```bash
# Rebase του τρέχοντος branch στο main
git checkout feature-branch
git rebase main

# Interactive rebase για τα τελευταία 3 commits
git rebase -i HEAD~3

# Ακύρωση rebase
git rebase --abort

# Συνέχιση μετά από επίλυση conflicts
git rebase --continue
```

### Interactive Rebase

Με το interactive rebase μπορείτε να:
- Επεξεργαστείτε commit messages (reword)
- Συνδυάσετε commits (squash)
- Διαγράψετε commits (drop)
- Αλλάξετε τη σειρά των commits
- Επεξεργαστείτε τα περιεχόμενα των commits (edit)

```bash
git rebase -i HEAD~5

# Στον editor που ανοίγει:
# pick abc123 First commit
# squash def456 Second commit (θα συνδυαστεί με το πρώτο)
# reword ghi789 Third commit (θα αλλάξει μήνυμα)
# drop jkl012 Fourth commit (θα διαγραφεί)
```

### Cherry-Pick

Αντιγραφή συγκεκριμένων commits από ένα branch σε άλλο:

```bash
# Αντιγραφή ενός commit
git cherry-pick abc123

# Αντιγραφή πολλαπλών commits
git cherry-pick abc123 def456

# Αντιγραφή range commits
git cherry-pick abc123..def456

# Ακύρωση cherry-pick
git cherry-pick --abort
```

### Merge Strategies

```bash
# Fast-forward merge (default όταν είναι δυνατό)
git merge feature-branch

# Πάντα δημιουργία merge commit
git merge --no-ff feature-branch

# Squash όλα τα commits σε ένα
git merge --squash feature-branch
```

### Επίλυση Συγκρούσεων

```bash
# Όταν συμβεί σύγκρουση κατά το merge/rebase
git status  # Δείτε ποια αρχεία έχουν conflicts

# Τα αρχεία με conflicts θα έχουν markers:
# <<<<<<< HEAD
# Το δικό σας περιεχόμενο
# =======
# Το άλλο περιεχόμενο
# >>>>>>> branch-name

# Επεξεργαστείτε τα αρχεία για να λύσετε τα conflicts
# Διαγράψτε τα markers και κρατήστε το σωστό περιεχόμενο

# Προσθέστε τα λυμένα αρχεία
git add resolved-file.txt

# Ολοκληρώστε το merge
git commit

# Ή ολοκληρώστε το rebase
git rebase --continue
```

### Merge Tools

```bash
# Ρύθμιση merge tool
git config --global merge.tool vimdiff

# Χρήση merge tool για επίλυση conflicts
git mergetool

# Άλλα δημοφιλή merge tools:
# - meld
# - kdiff3
# - p4merge
# - Beyond Compare
```

## Ασκήσεις

### Άσκηση 1: Rebase Practice

```bash
# Δημιουργήστε test scenario
git checkout -b feature-a
echo "Feature A" > feature-a.txt
git add feature-a.txt
git commit -m "Add feature A"

git checkout main
echo "Main update" > main.txt
git add main.txt
git commit -m "Update main"

git checkout feature-a
git rebase main
```

### Άσκηση 2: Interactive Rebase

```bash
# Δημιουργήστε πολλαπλά commits
git checkout -b cleanup-branch
echo "Line 1" > file.txt
git add file.txt
git commit -m "Add line 1"

echo "Line 2" >> file.txt
git commit -am "Add line 2"

echo "Line 3" >> file.txt
git commit -am "Add line 3"

# Squash τα commits σε ένα
git rebase -i HEAD~3
```

### Άσκηση 3: Cherry-Pick

```bash
# Δημιουργήστε scenario
git checkout -b branch-a
echo "Feature" > feature.txt
git add feature.txt
git commit -m "Add feature"

git checkout main
git checkout -b branch-b

# Αντιγράψτε το commit από το branch-a
git log branch-a  # Βρείτε το commit hash
git cherry-pick <commit-hash>
```

## Προχωρημένα Workflows

### Git Flow

Δημοφιλές branching model:
- `main`: Production-ready code
- `develop`: Integration branch
- `feature/*`: Νέα features
- `release/*`: Release preparation
- `hotfix/*`: Production fixes

### GitHub Flow

Απλοποιημένο workflow:
- `main`: Always deployable
- Feature branches από το main
- Pull Requests για code review
- Merge στο main μετά το review
- Deploy αμέσως

### Trunk-Based Development

- Όλοι commit στο main (ή short-lived branches)
- Feature flags για WIP features
- Πολύ συχνή integration
- Continuous deployment

## Καλές Πρακτικές

### Για Rebase
- Χρησιμοποιήστε rebase για cleanup του δικού σας branch
- ΠΟΤΕ μην κάνετε rebase σε public/shared branches
- Χρησιμοποιήστε `git pull --rebase` για sync με remote

### Για Merge
- Χρησιμοποιήστε `--no-ff` για να διατηρήσετε το branch history
- Squash commits όταν merge feature branches στο main
- Γράψτε καλά merge commit messages

### Για Conflicts
- Επιλύστε conflicts όσο το δυνατόν νωρίτερα
- Κάντε sync τακτικά με το main branch
- Επικοινωνήστε με το team για μεγάλες αλλαγές

## Επόμενο Βήμα
Μετά την ολοκλήρωση αυτού του επιπέδου, προχωρήστε στο [Επίπεδο 7: Προχωρημένα Θέματα](../07-Προχωρημένα-Θέματα/)
