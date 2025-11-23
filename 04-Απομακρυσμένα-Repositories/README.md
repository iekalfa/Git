# Επίπεδο 4: Απομακρυσμένα Repositories

## Στόχοι Μάθησης
- Σύνδεση με απομακρυσμένα repositories
- Αποστολή αλλαγών (push)
- Λήψη αλλαγών (pull, fetch)
- Κλωνοποίηση repositories

## Θεωρία

### Τι είναι τα Remote Repositories;
Τα remote repositories είναι εκδόσεις του project σας που φιλοξενούνται σε διαδικτυακούς servers όπως το GitHub, GitLab, ή Bitbucket.

### Git vs GitHub
- **Git**: Το σύστημα ελέγχου εκδόσεων (τοπικό εργαλείο)
- **GitHub**: Μια πλατφόρμα φιλοξενίας για Git repositories (διαδικτυακή υπηρεσία)

## Πρακτική Εφαρμογή

### Προβολή Remote Repositories

```bash
# Προβολή remotes
git remote

# Προβολή με λεπτομέρειες (URLs)
git remote -v

# Προβολή πληροφοριών για συγκεκριμένο remote
git remote show origin
```

### Προσθήκη Remote Repository

```bash
# Προσθήκη νέου remote
git remote add origin https://github.com/username/repository.git

# Αλλαγή URL του remote
git remote set-url origin https://github.com/username/new-repo.git

# Μετονομασία remote
git remote rename origin upstream
```

### Κλωνοποίηση Repository (Clone)

```bash
# Κλωνοποίηση repository
git clone https://github.com/username/repository.git

# Κλωνοποίηση σε συγκεκριμένο φάκελο
git clone https://github.com/username/repository.git my-folder

# Κλωνοποίηση συγκεκριμένου branch
git clone -b develop https://github.com/username/repository.git
```

### Αποστολή Αλλαγών (Push)

```bash
# Push στο remote branch
git push origin main

# Push όλων των branches
git push --all origin

# Push με force (προσοχή!)
git push --force origin main

# Ορισμός upstream branch
git push -u origin main
```

### Λήψη Αλλαγών (Pull)

```bash
# Pull αλλαγών από το remote
git pull origin main

# Pull = Fetch + Merge
# Είναι ισοδύναμο με:
git fetch origin
git merge origin/main
```

### Λήψη χωρίς Merge (Fetch)

```bash
# Fetch όλων των branches από το remote
git fetch origin

# Fetch συγκεκριμένου branch
git fetch origin main

# Fetch όλων των remotes
git fetch --all
```

## Ασκήσεις

### Άσκηση 1: Δημιουργία Repository στο GitHub
1. Συνδεθείτε στο GitHub
2. Δημιουργήστε ένα νέο repository
3. Συνδέστε το τοπικό σας repository με το GitHub
4. Κάντε push το κώδικά σας

```bash
git remote add origin https://github.com/yourusername/your-repo.git
git branch -M main
git push -u origin main
```

### Άσκηση 2: Clone και Contribution
1. Κάντε clone ένα υπάρχον repository
2. Δημιουργήστε ένα νέο branch
3. Κάντε μερικές αλλαγές και commit
4. Κάντε push το νέο branch

```bash
git clone https://github.com/username/repository.git
cd repository
git checkout -b my-feature
# Κάντε αλλαγές
git add .
git commit -m "Προσθήκη νέου χαρακτηριστικού"
git push -u origin my-feature
```

### Άσκηση 3: Συγχρονισμός με Remote
1. Κάντε αλλαγές στο GitHub (μέσω web interface)
2. Κάντε fetch τις αλλαγές
3. Κάντε merge τις αλλαγές
4. Εναλλακτικά, χρησιμοποιήστε pull

```bash
git fetch origin
git merge origin/main
# Ή απλά
git pull origin main
```

## Συνηθισμένα Προβλήματα

### Σύγκρουση κατά το Push
Αν το remote έχει αλλαγές που δεν έχετε τοπικά:
```bash
# Πρώτα κάντε pull
git pull origin main
# Λύστε τυχόν conflicts
# Μετά κάντε push
git push origin main
```

### Rejected Push
```bash
# Αν το push απορριφθεί, πρώτα κάντε pull
git pull --rebase origin main
git push origin main
```

## Καλές Πρακτικές

- Κάντε pull πριν ξεκινήσετε να εργάζεστε
- Κάντε push συχνά για να μοιράζεστε την πρόοδό σας
- Χρησιμοποιήστε περιγραφικά ονόματα για τα branches
- Μην κάνετε force push σε shared branches

## Επόμενο Βήμα
Μετά την ολοκλήρωση αυτού του επιπέδου, προχωρήστε στο [Επίπεδο 5: Συνεργασία στο GitHub](../05-Συνεργασία-GitHub/)
