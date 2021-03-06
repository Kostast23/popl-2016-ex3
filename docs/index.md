---
layout: default
---

<h1 style="color:red">Παράδοση εργασίας: Κυριακή 26/2/2017, 23.59μμ.</h1>

# [](#header-1)Συχνές Ερωτήσεις


> Γιατί δεν έλαβα απάντηση στην ερώτηση μου;

* Δεν έστειλες την ερώτηση σε ένα από τα δύο emails που αναφέρονται στην
εκφώνηση της εργασίας.
* Η ερώτηση σου έχει ήδη απαντηθεί και αναρτηθεί εδώ.

> Πού μπορώ να μάθω περισσότερα για τη Haskell;

* Ένα καλό ξεκίνημα (πέρα από τις σημειώσεις του μαθήματος) θα ήταν το
[learnyouahaskell.com](http://learnyouahaskell.com)

> Προσπαθώντας να τρέξουμε το βοηθητικό αρχείο σε Windows WinGHCi 8.0.1 παίρνουμε
το error **Failed to load interface for ‘System.Random’**.

Μπορείτε να [κατεβάσετε το cabal](https://www.haskell.org/cabal/release/cabal-install-1.24.0.2/cabal-install-1.24.0.2-x86_64-unknown-mingw32.zip)
(package manager της Ηaskell) και να βάλετε το cabal.exe στον ίδιο φάκελο με το
ghci (συνήθως C:\Program Files\Haskell Platform\YOUR_VERSION\bin). Εν συνεχεία
ανοίγετε μία κονσόλα σε αυτόν τον φάκελο και τρέχετε:

* cabal update
* cabal install random

> Χρειάζεται να γίνεται έλεγχος για την ορθότητα των ορισμάτων των συναρτήσεων;

Όχι, δεν χρειάζεται. Αν δωθεί οτιδήποτε δεν προβλέπεται από την εκφώνηση, π.χ.
λάθος width/height ή συντεταγμένες εκτός των ορίων ή maze χωρίς λύση, θεωρείται
undefined behaviour.

> Η showMaze επιστρέφει ένα string που περιέχει χαρακτήρες *'\n'*. Είναι σωστό να
καλούμε την putStrLn μέσα στην showMaze ώστε να εκτυπώνεται σωστά ο λαβύρινθος;

Δεν χρειάζεται να καλείτε την putStrLn. Γυρνάτε το String με τα *'\n'*, ώστε αν
καλέσουμε **putStrLn (showMaze m)** να γίνεται κανονικά η εκτύπωση.

> Στον ορισμό του Maze προσθέσαμε το derinving (Show). Να το αφήσουμε και για
δική σας διευκόλυνση;

Δεν υπάρχει πρόβλημα, αφού δεν αλλάζει κάτι στην ουσία του data type.

> Στο Bonus ερώτημα ισχύει ο περιορισμός της υλοποίησης του DFS (μη αποθήκευση
των κελιών που έχουν επισκεφθεί);

Όχι, δεν ισχύει (θα το αναφέραμε αν ίσχυε).

> Ο αλγόριθμος DFS που πρέπει να υλοποιήσουμε, θα πρέπει οπωσδήποτε να έχει ως
αρχικό κόμβο το κελί αρχής που δίνεται ή μπορεί να ξεκινά την αναζήτηση π.χ. από
το κελί (0,0) (για να έχει και νόημα η αναπαράσταση του maze ως δέντρου);

Πρώτον, η αναπαράσταση δεν θα πρέπει να είναι δέντρο. Το data type Maze (το
οποίο πρέπει να το χρησιμοποιήσετε όπως το δίνουμε) αναπαριστά τον λαβύρινθο σαν
μια λίστα από tuples από bools, τα οποία λένε αν υπάρχει ο δεξιός και ο κάτω
τοίχος για κάθε κελί. Απλώς για την δημιουργία του λαβυρίνθου χρησιμοποιούμε
αλγόριθμο που δημιουργεί δέντρα. Όμως, η αναπαράσταση του λαβυρίνθου μοιάζει πιο
πολύ με γράφο ο οποίος τυχαίνει να μην έχει κύκλους οπότε να είναι και δέντρο
(εκτός απ το bonus, όπου δεν είναι πια δέντρο).

Δεύτερον, ακόμα και αν προσεγγίσετε το γράφο του Maze σαν δέντρο (που είναι οκ,
αν κρατήσετε το data type ίδιο άρα το αναπαριστάτε σαν γράφο), ένα δέντρο
εξακολουθεί να είναι δέντρο όποιον κόμβο και αν θεωρήσετε σαν ρίζα. Οπότε
μπορείτε να θεωρήσετε σαν ρίζα το κελί αρχής για την εφαρμογή του DFS. Φαίνεται 
πιο λογικό, αφού ξεκινάς από έναν κόμβο και ψάχνεις έναν άλλο, αντί να ξεκινήσεις
από έναν αυθαίρετο κόμβο όπως τον (0,0) και να ψάχνεις δύο κόμβους. Επίσης, είναι
και πιο εύκολο, αφού ξεκινώντας πάντα από το (0,0) πρέπει να θεωρήσεις διάφορες
περιπτώσεις (π.χ. να είναι οι δύο κόμβοι σε διαφορετικά υποδέντρα του (0,0) ή στο
ίδιο, άρα το μονοπάτι είτε περνάει από το (0,0) είτε όχι).

> Γιατί η συνάρτηση `myRand = rand 3000`, η οποίο έφτιαξα, επιστρέφει πάντα τον
ίδιο αριθμό;

Αυτό είναι λογικό αν σκεφτείς πως ουσιαστικά όρισες μια μεταβλητή `myRand` και
της έδωσες την τιμή που γυρνάει το `rand 3000`, οπότε η `rand` καλέστηκε μόνο
μία φορά, όταν όρισες την `myRand`.

Αυτή είναι η κανονική συμπεριφορά της Haskell, η οποία λέει πως κάθε συνάρτηση
είναι pure, δηλαδή δεν έχει side effects και θα γυρνάει πάντα την ίδια τιμή αν
πάρει τα ίδια ορίσματα. Αυτό προφανώς δεν ισχύει για την `rand` που δώσαμε,
επειδή χρησιμοποιήσαμε μια χακιά (βάλαμε το unsafePerformIO), ώστε να μην
χρειαστεί να χρησιμοποιήσετε monads. Επομένως, αυτό που κάνει η haskell σε αυτήν
την περίπτωση είναι το σωστό, αλλά όχι αυτό που θέλεις.

Για να κάνεις αυτό που θες, μπορείς να ορίσεις την `myRand` με ένα όρισμα το
οποίο δεν θα χρησιμοποιήσεις μετά, ώστε να αναγκάσεις τη Haskell να κάνει
evaluate πάλι την `rand`, π.χ. `myRand _ = rand 3000`.

