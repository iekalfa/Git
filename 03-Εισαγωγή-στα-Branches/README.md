# Επίπεδο 3: Εισαγωγή στα Branches

## Στόχοι Μάθησης
- Κατανόηση της έννοιας των branches
- Δημιουργία και εναλλαγή branches
- Συγχώνευση (merge) branches

## 📓 Σύνοψη
Τα branches σας επιτρέπουν να εργάζεστε σε πολλές «παράλληλες πραγματικότητες» ταυτόχρονα. Ένα branch για νέο feature, ένα για bugfix, ένα για πείραμα – όλα χωρίς να επηρεάζουν το κύριο `main`. Μετά συγχωνεύετε (merge) πίσω.

## 🔑 Βασικές Έννοιες
- **Branch**: Ανεξάρτητη γραμμή ανάπτυξης (δείκτης σε commit).
- **HEAD**: Δείκτης στο τρέχον branch και commit.
- **main/master**: Το προεπιλεγμένο κύριο branch.
- **Merge**: Συγχώνευση αλλαγών από ένα branch σε άλλο.
- **Fast-forward**: Merge χωρίς νέο commit (όταν δεν υπάρχει divergence).

> Αναλογία: Branches = παράλληλες γραμμές του χρόνου, merge = επανένωση.

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
Για να δείτε ποια branches υπάρχουν στο repository σας και σε ποιο βρίσκεστε αυτή τη στιγμή (σημειώνεται με αστερίσκο `*`), χρησιμοποιήστε την εντολή `git branch`.

```bash
# Προβολή τοπικών branches
git branch

# Προβολή όλων των branches (τοπικών και remote)
git branch -a

# Προβολή του τρέχοντος branch
git branch --show-current
```

### Δημιουργία Νέου Branch
Όταν θέλετε να ξεκινήσετε δουλειά σε ένα νέο feature, δημιουργείτε ένα νέο branch. Αυτό δημιουργεί έναν νέο δείκτη στο τρέχον commit, επιτρέποντάς σας να προχωρήσετε ανεξάρτητα.

```bash
# Δημιουργία νέου branch
git branch feature-login

# Δημιουργία και μετάβαση σε νέο branch
git checkout -b feature-signup

# Νέος τρόπος (Git 2.23+)
git switch -c feature-dashboard
```

### Εναλλαγή μεταξύ Branches
Για να αλλάξετε το περιβάλλον εργασίας σας και να μεταβείτε σε άλλο branch, χρησιμοποιείτε το `checkout` (ή `switch`). Το Git θα αλλάξει αυτόματα τα αρχεία στον φάκελό σας για να ταιριάζουν με την έκδοση του branch που επιλέξατε.

```bash
# Εναλλαγή σε υπάρχον branch
git checkout main

# Νέος τρόπος (Git 2.23+)
git switch main
```

### Συγχώνευση Branches (Merge)
Όταν ολοκληρώσετε τη δουλειά σε ένα branch, πρέπει να ενσωματώσετε τις αλλαγές πίσω στον κύριο κορμό (συνήθως στο `main`). Αυτή η διαδικασία ονομάζεται συγχώνευση (merge).

```bash
# Μεταβείτε στο branch προορισμού (π.χ. main)
git checkout main

# Συγχωνεύστε το άλλο branch
git merge feature-login
```

### Διαγραφή Branch
Αφού ένα branch έχει συγχωνευθεί επιτυχώς και δεν το χρειάζεστε πια, καλό είναι να το διαγράφετε για να διατηρείτε το repository καθαρό.

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

## ✅ Checklist Εμπέδωσης
- [ ] Δημιούργησα branch με `git branch` ή `git checkout -b`.
- [ ] Έκανα commits σε branch χωρίς να επηρεάσω το `main`.
- [ ] Συγχώνευσα branch στο `main` με `git merge`.
- [ ] Διέγραψα branch μετά το merge με `git branch -d`.
- [ ] Κατανοώ ότι το `git log --graph` δείχνει την ιστορία branches.

## 🧪 Mini Quiz
1. Τι δείχνει το `*` στο `git branch`; (α) Το τρέχον branch ✓ (β) Το πιο πρόσφατο
2. Το `git checkout -b X` κάνει; (α) Δημιουργεί και αλλάζει σε X ✓ (β) Μόνο δημιουργεί
3. Μετά το merge, πρέπει; (α) Να διαγράψετε το branch χειροκίνητα ✓ (β) Διαγράφεται αυτόματα

## ⚠️ Συνηθισμένα Λάθη
- Ξεχνάτε να επιστρέψετε στο `main` πριν το merge.
- Διαγράφετε branch πριν το merge (χάνετε δουλειά).
- Δημιουργείτε branches με ασαφή ονόματα (π.χ. `test1`, `branch2`).

## 💡 Συμβουλή
Χρησιμοποιήστε περιγραφικά ονόματα: `feature-login`, `bugfix-header`, `experiment-animations`.

## 🔁 Ανακεφαλαίωση
Δημιουργία branch → Εργασία → Commits → Επιστροφή στο main → Merge → Διαγραφή branch.

## 📝 Στρατηγική Branches
- **Feature branches**: Για νέα χαρακτηριστικά.
- **Bugfix branches**: Για διορθώσεις.
- **Experiment branches**: Για δοκιμές (μπορεί να μην γίνει ποτέ merge).

## Επόμενο Βήμα
Μετά την ολοκλήρωση αυτού του επιπέδου, προχωρήστε στο [Επίπεδο 4: Απομακρυσμένα Repositories](../04-Απομακρυσμένα-Repositories/)
