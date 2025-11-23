# Επίπεδο 3: Εισαγωγή στα Branches

## Στόχοι Μάθησης
- Κατανόηση της έννοιας των branches
- Δημιουργία και εναλλαγή branches
- Συγχώνευση (merge) branches

## Θεωρία

### Τι είναι τα Branches;
Τα branches (κλαδιά) σας επιτρέπουν να αποκλίνετε από την κύρια γραμμή ανάπτυξης και να εργάζεστε ανεξάρτητα χωρίς να επηρεάζετε το κύριο κώδικα.

### Γιατί χρησιμοποιούμε Branches;
- Ανάπτυξη νέων χαρακτηριστικών (features)
- Διόρθωση σφαλμάτων (bug fixes)
- Πειραματισμός με νέες ιδέες
- Παράλληλη εργασία σε διαφορετικές εργασίες

### Το Default Branch: main/master
Το `main` (ή `master` σε παλαιότερα repositories) είναι το προεπιλεγμένο branch που δημιουργείται όταν αρχικοποιείτε ένα repository.

## Πρακτική Εφαρμογή

### Προβολή Branches

```bash
# Προβολή τοπικών branches
git branch

# Προβολή όλων των branches (τοπικών και remote)
git branch -a

# Προβολή του τρέχοντος branch
git branch --show-current
```

### Δημιουργία Νέου Branch

```bash
# Δημιουργία νέου branch
git branch feature-login

# Δημιουργία και μετάβαση σε νέο branch
git checkout -b feature-signup

# Νέος τρόπος (Git 2.23+)
git switch -c feature-dashboard
```

### Εναλλαγή μεταξύ Branches

```bash
# Εναλλαγή σε υπάρχον branch
git checkout main

# Νέος τρόπος (Git 2.23+)
git switch main
```

### Συγχώνευση Branches (Merge)

```bash
# Μεταβείτε στο branch προορισμού (π.χ. main)
git checkout main

# Συγχωνεύστε το άλλο branch
git merge feature-login
```

### Διαγραφή Branch

```bash
# Διαγραφή branch που έχει συγχωνευθεί
git branch -d feature-login

# Αναγκαστική διαγραφή branch
git branch -D feature-old
```

## Ασκήσεις

1. Δημιουργήστε ένα νέο branch με όνομα `feature-greeting`
2. Μεταβείτε στο νέο branch
3. Δημιουργήστε ένα αρχείο `greeting.txt` με το περιεχόμενο "Hello from feature branch"
4. Κάντε commit το αρχείο
5. Επιστρέψτε στο `main` branch
6. Συγχωνεύστε το `feature-greeting` branch
7. Διαγράψτε το `feature-greeting` branch
8. Ελέγξτε το ιστορικό με `git log --graph --oneline`

## Απλό Παράδειγμα

```bash
# Βρίσκεστε στο main branch
git checkout -b add-footer

# Κάντε τις αλλαγές σας
echo "Footer content" > footer.html
git add footer.html
git commit -m "Προσθήκη footer"

# Επιστροφή στο main
git checkout main

# Συγχώνευση
git merge add-footer

# Καθαρισμός
git branch -d add-footer
```

## Επόμενο Βήμα
Μετά την ολοκλήρωση αυτού του επιπέδου, προχωρήστε στο [Επίπεδο 4: Απομακρυσμένα Repositories](../04-Απομακρυσμένα-Repositories/)
