# Επίπεδο 4: Απομακρυσμένα Repositories

## Στόχοι Μάθησης
- Σύνδεση με απομακρυσμένα repositories
- Αποστολή αλλαγών (push)
- Λήψη αλλαγών (pull, fetch)
- Κλωνοποίηση repositories

## 📓 Σύνοψη
Μέχρι τώρα όλα ήταν τοπικά. Τώρα μαθαίνουμε να συνδεόμαστε με το GitHub (ή GitLab/Bitbucket), να ανεβάζουμε (push) και να κατεβάζουμε (pull/fetch) αλλαγές. Αυτό ανοίγει τον δρόμο για συνεργασία.

## 🔑 Βασικές Έννοιες
- **Remote**: Απομακρυσμένος server που φιλοξενεί το repository.
- **origin**: Το προεπιλεγμένο όνομα του κύριου remote.
- **clone**: Αντιγραφή ολόκληρου repository από remote.
- **push**: Αποστολή τοπικών commits στο remote.
- **pull**: Fetch + Merge (λήψη και ενσωμάτωση).
- **fetch**: Λήψη αλλαγών χωρίς merge.
- **Tracking branch**: Τοπικό branch συνδεδεμένο με remote branch.

> Ροή: Τοπικό commit → `git push` → Remote repository → Άλλοι κάνουν `git pull`

## Θεωρία

### Τι είναι τα Remote Repositories;
Τα remote repositories είναι εκδόσεις του project σας που φιλοξενούνται σε διαδικτυακούς servers όπως το GitHub, GitLab, ή Bitbucket.

### Git vs GitHub
- **Git**: Το σύστημα ελέγχου εκδόσεων (τοπικό εργαλείο)
- **GitHub**: Μια πλατφόρμα φιλοξενίας για Git repositories (διαδικτυακή υπηρεσία)

### Αυθεντικοποίηση (Authentication)
Για να στείλετε κώδικα (push) στο GitHub, πρέπει να αποδείξετε την ταυτότητά σας. Το GitHub απαιτεί **Personal Access Tokens (PAT)** ή **SSH Keys** αντί για τον κωδικό πρόσβασης του λογαριασμού σας.

#### Πώς να δημιουργήσετε ένα Personal Access Token (PAT)
1. Στο GitHub, πηγαίνετε: **Settings** (πάνω δεξιά στο προφίλ) -> **Developer settings** (τέρμα κάτω αριστερά) -> **Personal access tokens** -> **Tokens (classic)**.
2. Πατήστε **Generate new token (classic)**.
3. Δώστε ένα όνομα (π.χ. "My Laptop") και επιλέξτε διάρκεια (Expiration).
4. Στα **Select scopes**, τσεκάρετε το κουτάκι **repo** (για πλήρη έλεγχο των repositories).
5. Πατήστε **Generate token**.
6. **Αντιγράψτε το token!** Δεν θα μπορέσετε να το δείτε ξανά.
7. Όταν το Git στο τερματικό σας ζητήσει **Password**, κάντε επικόλληση αυτό το token.

> **Tip:** Σε πολλά τερματικά, η επικόλληση κωδικού δεν φαίνεται στην οθόνη για λόγους ασφαλείας. Απλά πατήστε Enter μετά την επικόλληση.

#### Εναλλακτικά: Χρήση SSH Keys (Πιο ασφαλές & βολικό)
Τα SSH keys σας επιτρέπουν να συνδέεστε χωρίς να πληκτρολογείτε κωδικούς κάθε φορά.

1. **Δημιουργία κλειδιού:**
   Ανοίξτε το τερματικό (**Git Bash** για Windows ή Terminal για macOS/Linux) και τρέξτε:
   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
   > **Σημείωση:** Στα Windows 10/11, η εντολή λειτουργεί συνήθως και στο PowerShell.
   
   Πατήστε Enter σε όλα (για default ρυθμίσεις).

2. **Αντιγραφή του δημόσιου κλειδιού:**
   ```bash
   # Εμφάνιση του κλειδιού για αντιγραφή
   cat ~/.ssh/id_ed25519.pub
   ```
   Αντιγράψτε το κείμενο που ξεκινάει με `ssh-ed25519...`.

3. **Προσθήκη στο GitHub:**
   - Πηγαίνετε **Settings** -> **SSH and GPG keys**.
   - Πατήστε **New SSH key**.
   - Δώστε ένα τίτλο και κάντε επικόλληση το κλειδί στο πεδίο "Key".
   - Πατήστε **Add SSH key**.

4. **Χρήση SSH URL:**
   Για να το χρησιμοποιήσετε, πρέπει να αλλάξετε το remote URL ή να κάνετε clone με SSH:
   ```bash
   # Αλλαγή υπάρχοντος remote σε SSH
   git remote set-url origin git@github.com:username/repository.git
   ```

## Πρακτική Εφαρμογή

### Προβολή Remote Repositories
Για να δείτε με ποιους απομακρυσμένους servers είναι συνδεδεμένο το τοπικό σας repository, χρησιμοποιούμε την εντολή `git remote`. Το όνομα `origin` είναι το προεπιλεγμένο όνομα που δίνει το Git στον server από τον οποίο κάνατε clone.

```bash
# Προβολή remotes
git remote

# Προβολή με λεπτομέρειες (URLs)
git remote -v

# Προβολή πληροφοριών για συγκεκριμένο remote
git remote show origin
```

### Προσθήκη Remote Repository
Αν δημιουργήσατε ένα repository τοπικά και θέλετε να το ανεβάσετε στο GitHub, πρέπει πρώτα να προσθέσετε τη διεύθυνση του remote server.

```bash
# Προσθήκη νέου remote
git remote add origin https://github.com/username/repository.git

# Αλλαγή URL του remote
git remote set-url origin https://github.com/username/new-repo.git

# Μετονομασία remote
git remote rename origin upstream
```

### Κλωνοποίηση Repository (Clone)
Η εντολή `git clone` χρησιμοποιείται για να κατεβάσετε ένα αντίγραφο ενός υπάρχοντος repository από το διαδίκτυο στον υπολογιστή σας. Αυτή η εντολή δημιουργεί αυτόματα το φάκελο, αρχικοποιεί το git και κατεβάζει όλο το ιστορικό.

```bash
# Κλωνοποίηση repository
git clone https://github.com/username/repository.git

# Κλωνοποίηση σε συγκεκριμένο φάκελο
git clone https://github.com/username/repository.git my-folder

# Κλωνοποίηση συγκεκριμένου branch
git clone -b develop https://github.com/username/repository.git
```

### Αποστολή Αλλαγών (Push)
Η εντολή `git push` χρησιμοποιείται για να ανεβάσετε τα τοπικά σας commits στο απομακρυσμένο repository. Είναι το βήμα που δημοσιεύει τη δουλειά σας στους συνεργάτες σας.

```bash
# Push στο remote branch
git push origin main

# Push όλων των branches
git push --all origin

# Push με force (προσοχή!)
git push --force origin main

# Ορισμός upstream branch (Tracking)
# Το -u (ή --set-upstream) συνδέει το τοπικό branch με το remote
# ώστε μελλοντικά να αρκεί σκέτο 'git push' ή 'git pull'
git push -u origin main
```

### Διαχείριση Remote Branches
Μερικές φορές χρειάζεται να διαγράψετε ένα branch όχι μόνο τοπικά, αλλά και από τον server (π.χ. όταν ένα feature έχει ολοκληρωθεί και συγχωνευθεί).

```bash
# Διαγραφή remote branch
git push origin --delete feature-branch

# Καθαρισμός τοπικών αναφορών σε διεγραμμένα remote branches
git fetch --prune
```

### Λήψη Αλλαγών (Pull)
Η εντολή `git pull` χρησιμοποιείται για να κατεβάσετε τις αλλαγές από το απομακρυσμένο repository και να τις ενσωματώσετε (merge) απευθείας στο τρέχον branch σας. Είναι ο πιο συνηθισμένος τρόπος να συγχρονίσετε τη δουλειά σας.

```bash
# Pull αλλαγών από το remote
git pull origin main

# Pull = Fetch + Merge
# Είναι ισοδύναμο με:
git fetch origin
git merge origin/main
```

### Λήψη χωρίς Merge (Fetch)
Η εντολή `git fetch` κατεβάζει τα δεδομένα από το remote repository αλλά **δεν** αλλάζει τα αρχεία σας. Σας επιτρέπει να δείτε τι έχουν κάνει οι άλλοι πριν αποφασίσετε να κάνετε merge.

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

### Authentication Error (Password removed)
Αν δείτε το μήνυμα:
`remote: Support for password authentication was removed... Please use a personal access token instead.`

**Λύση:** Σημαίνει ότι βάλατε τον κωδικό του GitHub σας. Πρέπει να βάλετε το **Personal Access Token (PAT)** όταν σας ζητηθεί το `Password`.

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

## ✅ Checklist Εμπέδωσης
- [ ] Δημιούργησα Personal Access Token ή SSH key.
- [ ] Κατανοώ τη διαφορά `fetch` vs `pull`.
- [ ] Έκανα `clone` repository και δουλεύω σε τοπικό αντίγραφο.
- [ ] Έκανα `push` αλλαγές και τις είδα στο GitHub.
- [ ] Έκανα `pull` αλλαγές από άλλους και συγχρονίστηκα.

## 🧪 Mini Quiz
1. Τι κάνει το `git clone`; (α) Αντιγράφει όλο το history ✓ (β) Μόνο τα αρχεία
2. Η διαφορά fetch/pull; (α) Fetch δεν κάνει merge ✓ (β) Είναι το ίδιο
3. Το `-u` στο `git push -u`; (α) Ορίζει tracking ✓ (β) Force push

## ⚠️ Συνηθισμένα Λάθη
- Push χωρίς πρώτα pull → conflicts και rejected push.
- Χρήση password αντί για PAT → authentication error.
- Force push σε shared branch → χάνετε δουλειά άλλων.
- Ξεχνάτε το `-u` → κάθε φορά πρέπει να γράφετε `origin main`.

## 💡 Συμβουλή
Πάντα `git pull` πριν ξεκινήσετε δουλειά – αποφεύγει conflicts.

## 🔁 Ανακεφαλαίωση Ροής
1. `git clone` (μία φορά) ή `git pull` (κάθε μέρα)
2. Κάνετε αλλαγές και commits
3. `git push` για να μοιραστείτε

## 🔐 Authentication Quick Reference
- **HTTPS + PAT**: Εύκολο, token ως password.
- **SSH**: Πιο ασφαλές, χωρίς κωδικούς κάθε φορά.

## 📝 Προσωπικές Σημειώσεις
```
(π.χ. "Δημιούργησα SSH key για πρώτη φορά")
```

## Επόμενο Βήμα
Μετά την ολοκλήρωση αυτού του επιπέδου, προχωρήστε στο [Επίπεδο 5: Συνεργασία στο GitHub](../05-Συνεργασία-GitHub/)
