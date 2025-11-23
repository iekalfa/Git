# Git - Εκπαιδευτικό Αποθετήριο

Καλώς ήρθατε στο εκπαιδευτικό αποθετήριο για την εκμάθηση του Git και GitHub!

## Μέθοδος Διδασκαλίας: Spiral Curriculum

Αυτό το curriculum ακολουθεί τη μέθοδο **Spiral Curriculum**, όπου οι έννοιες εισάγονται σταδιακά και επανεπισκέπτονται σε μεγαλύτερο βάθος σε κάθε επίπεδο. Ξεκινάτε με τα βασικά και προχωράτε σταδιακά σε πιο προχωρημένα θέματα.

## Δομή Curriculum

Το curriculum είναι οργανωμένο σε 8 επίπεδα, από αρχάριο έως προχωρημένο:

### [📚 Επίπεδο 1: Βασικά του Git](./01-Βασικά-Git/)
Εισαγωγή στο version control, εγκατάσταση και αρχική ρύθμιση του Git.

**Θέματα:**
- Τι είναι το Git και γιατί το χρειαζόμαστε
- Εγκατάσταση σε διάφορα λειτουργικά συστήματα
- Βασική ρύθμιση (user.name, user.email)
- Δημιουργία πρώτου repository

### [⚙️ Επίπεδο 2: Βασικές Λειτουργίες](./02-Βασικές-Λειτουργίες/)
Οι καθημερινές εντολές που χρησιμοποιείτε συνέχεια.

**Θέματα:**
- `git add`, `git commit`, `git status`
- Ο κύκλος ζωής των αρχείων
- Staging area και commits
- `git log` και `git diff`

### [🌿 Επίπεδο 3: Εισαγωγή στα Branches](./03-Εισαγωγή-στα-Branches/)
Κατανόηση και χρήση των branches για παράλληλη ανάπτυξη.

**Θέματα:**
- Τι είναι τα branches και γιατί είναι χρήσιμα
- Δημιουργία και εναλλαγή branches
- Συγχώνευση (merge) branches
- Διαγραφή branches

### [☁️ Επίπεδο 4: Απομακρυσμένα Repositories](./04-Απομακρυσμένα-Repositories/)
Σύνδεση με το GitHub και συνεργασία με άλλους.

**Θέματα:**
- Remote repositories και GitHub
- `git clone`, `git push`, `git pull`
- Σύνδεση τοπικού repository με GitHub
- `git fetch` vs `git pull`

### [🤝 Επίπεδο 5: Συνεργασία στο GitHub](./05-Συνεργασία-GitHub/)
Επαγγελματική συνεργασία μέσω του GitHub.

**Θέματα:**
- GitHub workflow
- Pull Requests και Code Review
- Forks και contribution σε open source
- Issues και project management

### [🔀 Επίπεδο 6: Προχωρημένα Branches](./06-Προχωρημένα-Branches/)
Προχωρημένες τεχνικές διαχείρισης branches.

**Θέματα:**
- `git rebase` και πότε να το χρησιμοποιείτε
- Interactive rebase
- Cherry-picking commits
- Merge strategies
- Επίλυση συγκρούσεων

### [🔧 Επίπεδο 7: Προχωρημένα Θέματα](./07-Προχωρημένα-Θέματα/)
Προχωρημένα εργαλεία και τεχνικές.

**Θέματα:**
- `git stash` για προσωρινή αποθήκευση
- `git reset`, `git revert`, `git checkout`
- Git tags και releases
- Git hooks και automation
- Git reflog και bisect
- Submodules

### [🚀 Επίπεδο 8: Χαρακτηριστικά GitHub](./08-Χαρακτηριστικά-GitHub/)
Εκμετάλλευση όλων των δυνατοτήτων του GitHub.

**Θέματα:**
- GitHub Actions για CI/CD
- GitHub Projects για project management
- GitHub Pages για documentation
- Security features (Dependabot, Code Scanning)
- GitHub CLI
- GitHub API

## Πώς να Χρησιμοποιήσετε αυτό το Αποθετήριο

1. **Ξεκινήστε από το Επίπεδο 1** και προχωρήστε σειριακά
2. **Διαβάστε τη θεωρία** σε κάθε επίπεδο
3. **Εξασκηθείτε με τα παραδείγματα** που παρέχονται
4. **Κάντε τις ασκήσεις** για να εμπεδώσετε τις γνώσεις
5. **Προχωρήστε στο επόμενο επίπεδο** όταν νιώσετε άνετα

## Προτεινόμενη Διάρκεια ανά Επίπεδο

- **Επίπεδα 1-2**: 1-2 ώρες το καθένα
- **Επίπεδα 3-5**: 2-3 ώρες το καθένα
- **Επίπεδα 6-8**: 3-4 ώρες το καθένα

## Προαπαιτούμενα

- Βασική γνώση υπολογιστών
- Εξοικείωση με command line (προαιρετικό αλλά συνιστάται)
- Λογαριασμός GitHub (από το Επίπεδο 4 και μετά)

## Πρόσθετοι Πόροι

- [Git Official Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com)
- [Pro Git Book (δωρεάν)](https://git-scm.com/book/el/v2)
- [GitHub Learning Lab](https://lab.github.com)
- [Git Cheat Sheet](https://training.github.com/downloads/github-git-cheat-sheet.pdf)

## Συνεισφορά

Βρήκατε κάποιο λάθος ή θέλετε να προσθέσετε κάτι; Οι συνεισφορές είναι ευπρόσδεκτες!

1. Fork το repository
2. Δημιουργήστε feature branch (`git checkout -b feature/improvement`)
3. Commit τις αλλαγές σας (`git commit -am 'Προσθήκη νέας ενότητας'`)
4. Push το branch (`git push origin feature/improvement`)
5. Δημιουργήστε Pull Request

## Άδεια Χρήσης

Αυτό το εκπαιδευτικό υλικό είναι διαθέσιμο για ελεύθερη χρήση στο πλαίσιο της εκπαίδευσης.

---

**Καλή Μάθηση!** 🎓

Ξεκινήστε το ταξίδι σας από το [Επίπεδο 1: Βασικά του Git](./01-Βασικά-Git/)!
