# infosystems-proj-2
<<2η υποχρεωτική εργασία στα πληροφοριακά συστήματα>>

Αρχικά, για την υλοποίηση της συγκεκριμένης εργασίας είναι απαραίτητη η διαγραφή όλων των container & images που σχετίζονται με mongodb με τις εντολές:
- docker images, docker ps
- docker images rm, docker rm
- 
και έπειτα δημιουργία image mongo με την εκτέλεση της εντολής:
- docker pull mongo
καθώς και η εγκατάσταση του docker-compose στο linux μέσω των οδηγιών στο παρακάτω link:
- https://computingforgeeks.com/how-to-install-latest-docker-compose-on-linux/
ο κώδικας όπως και την προηγούμενη φορά δέχεται τα δεδομένα από την εφαρμογή Postman.

Μέσα στο αρχείο .zip περιέχονται τα appinfo.py, docker-compose.yml, dockerfile, τα Users.json & Products.json.

1ο Βήμα - Eκκίνηση docker, postman, mongodb: sudo systemctl start docker sudo systemctl start mongod (*)και όσο αφορά το postman θα πρέπει αφού το έχετε εγκαταστήσει να πάτε στο directory που έχει εγκατασταθεί μέσω terminal και να το ξεκινήσετε ως εξής: ./'Postman Agent' !!!! Προσοχή επιπλέον είναι απαραίτητο να χρησιμοποιηθούν στην python οι βιβλιοθήκες pymongo, flask, os και bson.

2o Bήμα - Για την εκτέλεση του κώδικα και την ενοποίηση των λειτουργιών των δύο container θα πρέπει να εκτελεστούν οι εντολές:
- docker-compose build
- docker-compose up

3o Bήμα - Εκτέλση των endpoints(Eφόσον τρέχει το docker-compose up & το Postman Agent)

θα το ανοίξετε σε ένα tab, θα φτιάξετε ένα νέο workspace(+new workspace) το ονομάζετε όπως θέλετε και στην συνέχεια θα ανοίξετε μέσα στο workspace ένα νέο tab. Tώρα, στο νέο tab που έχετε ανοίξει θα παρατηρήσετε ότι υπάρχει μπροστά ένα label με GET εκεί μπορείτε να το αλλάξετε σε POST, PATCH, DELETE, PUT κλπ ανάλογα με το endpoint που έχετε. και ακριβώς στα δεξιά υπάρχει ένα κενό πλαίσιο στο οποίο πληκτρολογείτε το url ως εξής http://localhost:5000/name_of_endpoint ανάλογα με το endpoint που επιθυμείτε να εκτελέσετε και τέρμα δεξιά υπάρχει ένα κουμπί send το κάνετε κλικ και στέλνει οτιδήποτε έχετε βάλει στο body του request, header request κλπ.

1o endpoint - create-user
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά POST) μέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 1ο ερώτημα { "username": "a name", "password": "a password", "email" : "an email", "category" : "a category", "shopping_cart" : [], "orderHistory" : [] } και μετά απλά πατάτε send και θα δείτε πως το πρώτο ερώτημα ολοκληρώθηκε

2o endpoint - login
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά POST) μέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 2ο ερώτημα τα ίδια στοιχεία(εκτός από "shopping_cart" : [], "orderHistory" : []) που δώσατε για το 1ο γιατί εδώ θέλουμε να δούμε αν ο χρήστης που δημιουργήθηκε προηγουμένως έχει κάνει login και μετά απλά πατάτε send και θα δείτε πως το δεύτερο ερώτημα ολοκληρώθηκε. Προσοχή!!!! Αν η κατηγορία που έχει εισάγει ο χρήστης είναι user τότε θα μπορεί να υλοποιήσει μόνο τα endpoint(3o - 8o) καθώς η συνάρτηση admin_is_session_valid δεν θα του επιτρέψει να πάρει uuid από την συνάρτηση create_session αλλά μόνο από την συνάρτηση admin_create_session, το ίδιο θα ισχυεί για την περίπτωση που ο χρήστης εισάγει την κατηγορία administrator όπου θα μπορεί να υλοποιήσει μόνο τα endpoint(9ο - 11o) καθώς η συνάρτηση is_session_valid δεν θα του επιτρέψει να πάρει uuid από την συνάρτηση
admin_create_session αλλά μόνο από την συνάρτηση create_session.

- Για τον απλό χρήστη(Προσοχή, πρέπει πρώτα να κάνει log in ως administrator για να προστεθούν δεδομένα στο DSMarkets)

3o endpoint(3 endpoints) 
- getProductCategory
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά GET) Aρχικά, μέσα στον κώδικα της python θα δείτε την εντολή uuid = request.headers.get('authorization'), στην συνέχεια θα πάτε στο postman και θα ψάξετε για την επιλογή headers κάνετε κλικ και τώρα απλά θα πρέπει να πάτε στο πινακάκι με τα keys and values στο πλαίσιο του key θα χρησιμοποιήσετε ως όνομα το authorization και σαν value το uuid που επιστρέφει το 2o endpoint και θα κάνετε tick αυτήν την σειρά του πίνακα(στα αριστερά υπάρχει το tick button). Mέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 3ο ερώτημα {"category": "a category that exists in Products.json(Products collection in DSMarkets)"} μετά απλά πατάτε send και θα δείτε πως το τρίτο ερώτημα ολοκληρώθηκε.

- getProductName
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά GET) Aρχικά, μέσα στον κώδικα της python θα δείτε την εντολή uuid = request.headers.get('authorization'), στην συνέχεια θα πάτε στο postman και θα ψάξετε για την επιλογή headers κάνετε κλικ και τώρα απλά θα πρέπει να πάτε στο πινακάκι με τα keys and values στο πλαίσιο του key θα χρησιμοποιήσετε ως όνομα το authorization και σαν value το uuid που επιστρέφει το 2o endpoint και θα κάνετε tick αυτήν την σειρά του πίνακα(στα αριστερά υπάρχει το tick button). Mέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 3ο ερώτημα {"category": "a category that exists in Products.json(Products collection in DSMarkets)"} μετά απλά πατάτε send και θα δείτε πως το τρίτο ερώτημα ολοκληρώθηκε.

- getProductID
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά GET) Aρχικά, μέσα στον κώδικα της python θα δείτε την εντολή uuid = request.headers.get('authorization'), στην συνέχεια θα πάτε στο postman και θα ψάξετε για την επιλογή headers κάνετε κλικ και τώρα απλά θα πρέπει να πάτε στο πινακάκι με τα keys and values στο πλαίσιο του key θα χρησιμοποιήσετε ως όνομα το authorization και σαν value το uuid που επιστρέφει το 2o endpoint και θα κάνετε tick αυτήν την σειρά του πίνακα(στα αριστερά υπάρχει το tick button). Mέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 3ο ερώτημα {"unique_id": "a unique_id that exists in Products.json(Products collection in DSMarkets)"} μετά απλά πατάτε send και θα δείτε πως το τρίτο ερώτημα ολοκληρώθηκε.

4o endpoint - insertProduct
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά PATCH) Aρχικά, μέσα στον κώδικα της python θα δείτε την εντολή uuid = request.headers.get('authorization'), στην συνέχεια θα πάτε στο postman και θα ψάξετε για την επιλογή headers κάνετε κλικ και τώρα απλά θα πρέπει να πάτε στο πινακάκι με τα keys and values στο πλαίσιο του key θα χρησιμοποιήσετε ως όνομα το authorization και σαν value το uuid που επιστρέφει το 2o endpoint και θα κάνετε tick αυτήν την σειρά του πίνακα(στα αριστερά υπάρχει το tick button). Mέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 4ο ερώτημα {"unique_id": "a unique_id that exists in Products.json(Products collection in DSMarkets)", "stock":a stock number, "email": "an email that exists in Users.json(Users collection in DSMarkets)"} μετά απλά πατάτε send και θα δείτε πως το τέταρτο ερώτημα ολοκληρώθηκε.

5o endpoint - showProduct
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά GET) Aρχικά, μέσα στον κώδικα της python θα δείτε την εντολή uuid = request.headers.get('authorization'), στην συνέχεια θα πάτε στο postman και θα ψάξετε για την επιλογή headers κάνετε κλικ και τώρα απλά θα πρέπει να πάτε στο πινακάκι με τα keys and values στο πλαίσιο του key θα χρησιμοποιήσετε ως όνομα το authorization και σαν value το uuid που επιστρέφει το 2o endpoint και θα κάνετε tick αυτήν την σειρά του πίνακα(στα αριστερά υπάρχει το tick button). Mέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 5ο ερώτημα {"email": "an email that exists in Users.json(Users collection in DSMarkets)"} μετά απλά πατάτε send και θα δείτε πως το πέμπτο ερώτημα ολοκληρώθηκε.

6o endpoint - deleteProduct
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά DELETE) Aρχικά, μέσα στον κώδικα της python θα δείτε την εντολή uuid = request.headers.get('authorization'), στην συνέχεια θα πάτε στο postman και θα ψάξετε για την επιλογή headers κάνετε κλικ και τώρα απλά θα πρέπει να πάτε στο πινακάκι με τα keys and values στο πλαίσιο του key θα χρησιμοποιήσετε ως όνομα το authorization και σαν value το uuid που επιστρέφει το 2o endpoint και θα κάνετε tick αυτήν την σειρά του πίνακα(στα αριστερά υπάρχει το tick button). Mέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 6ο ερώτημα {"unique_id": "a unique_id that exists in Products.json(Products collection in DSMarkets)", "stock":a stock number that exists in Products.json(Products collection in DSMarkets), "email": "an email that exists in Users.json(Users collection in DSMarkets)"} μετά απλά πατάτε send και θα δείτε πως το έκτο ερώτημα ολοκληρώθηκε.

7o endpoint - purchaseProduct
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά POST) Aρχικά, μέσα στον κώδικα της python θα δείτε την εντολή uuid = request.headers.get('authorization'), στην συνέχεια θα πάτε στο postman και θα ψάξετε για την επιλογή headers κάνετε κλικ και τώρα απλά θα πρέπει να πάτε στο πινακάκι με τα keys and values στο πλαίσιο του key θα χρησιμοποιήσετε ως όνομα το authorization και σαν value το uuid που επιστρέφει το 2o endpoint και θα κάνετε tick αυτήν την σειρά του πίνακα(στα αριστερά υπάρχει το tick button). Mέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 7ο ερώτημα {"email": "an email that exists in Users.json(Users collection in DSMarkets)", "card_code": "a number with length 16(otherwise it won't work)"} μετά απλά πατάτε send και θα δείτε πως το έβδομο ερώτημα ολοκληρώθηκε.

8o endpoint - remove-user
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά DELETE) Aρχικά, μέσα στον κώδικα της python θα δείτε την εντολή uuid = request.headers.get('authorization'), στην συνέχεια θα πάτε στο postman και θα ψάξετε για την επιλογή headers κάνετε κλικ και τώρα απλά θα πρέπει να πάτε στο πινακάκι με τα keys and values στο πλαίσιο του key θα χρησιμοποιήσετε ως όνομα το authorization και σαν value το uuid που επιστρέφει το 2o endpoint και θα κάνετε tick αυτήν την σειρά του πίνακα(στα αριστερά υπάρχει το tick button). Mέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 8ο ερώτημα {"username": "a username that exists in Users.json(Users collection in DSMarkets)", "password": "a password that exists in Users.json(Users collection in DSMarkets)", "email" : "an email that exists in Users.json(Users collection in DSMarkets)"} μετά απλά πατάτε send και θα δείτε πως το όγδοο ερώτημα ολοκληρώθηκε.

- Για τον διαχειρηστή

9o endpoint - adminInsertProduct
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά POST) Aρχικά, μέσα στον κώδικα της python θα δείτε την εντολή uuid = request.headers.get('authorization'), στην συνέχεια θα πάτε στο postman και θα ψάξετε για την επιλογή headers κάνετε κλικ και τώρα απλά θα πρέπει να πάτε στο πινακάκι με τα keys and values στο πλαίσιο του key θα χρησιμοποιήσετε ως όνομα το authorization και σαν value το uuid που επιστρέφει το 2o endpoint και θα κάνετε tick αυτήν την σειρά του πίνακα(στα αριστερά υπάρχει το tick button). Mέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 9ο ερώτημα {"email" : "an email that exists in Users.json(Users collection in DSMarkets), "name" : "a name ", "price" : a price , "description" : "a description", "category" : "a category",  "stock" : a stock number} μετά απλά πατάτε send και θα δείτε πως το ένατο ερώτημα ολοκληρώθηκε.

Extra endpoint getObjectId
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά GET) Aρχικά, μέσα στον κώδικα της python θα δείτε την εντολή uuid = request.headers.get('authorization'), στην συνέχεια θα πάτε στο postman και θα ψάξετε για την επιλογή headers κάνετε κλικ και τώρα απλά θα πρέπει να πάτε στο πινακάκι με τα keys and values στο πλαίσιο του key θα χρησιμοποιήσετε ως όνομα το authorization και σαν value το uuid που επιστρέφει το 2o endpoint και θα κάνετε tick αυτήν την σειρά του πίνακα(στα αριστερά υπάρχει το tick button). Mέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 9ο ερώτημα {"email" : "an email that exists in Users.json(Users collection in DSMarkets), "name" : "the name of the product you inserted in the previous endpoint"} για να μπορέσει ο χρήστης να πάρει το objectid του προιόντος που εισήγαγε στo προηγούμενο endpoint στο αποτέλεσμα που θα εμφανιστεί απλά πάρτε copy paste το _id: $oid : ...... που θα προκύψει στο postman.

10o endpoint - adminRemoveProduct
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά DELETE) Aρχικά, μέσα στον κώδικα της python θα δείτε την εντολή uuid = request.headers.get('authorization'), στην συνέχεια θα πάτε στο postman και θα ψάξετε για την επιλογή headers κάνετε κλικ και τώρα απλά θα πρέπει να πάτε στο πινακάκι με τα keys and values στο πλαίσιο του key θα χρησιμοποιήσετε ως όνομα το authorization και σαν value το uuid που επιστρέφει το 2o endpoint και θα κάνετε tick αυτήν την σειρά του πίνακα(στα αριστερά υπάρχει το tick button). Mέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 10ο ερώτημα {"_id":"ObjectId that exists in mongodb in Products Collection"(εδώ χρησιμοποιείται η συνάρτηση ObjectID από την βιβλιοθήκη bson)} μετά απλά πατάτε send και θα δείτε πως το δέκατο ερώτημα ολοκληρώθηκε.

11o endpoint - adminUpdateProduct
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά PATCH) Aρχικά, μέσα στον κώδικα της python θα δείτε την εντολή uuid = request.headers.get('authorization'), στην συνέχεια θα πάτε στο postman και θα ψάξετε για την επιλογή headers κάνετε κλικ και τώρα απλά θα πρέπει να πάτε στο πινακάκι με τα keys and values στο πλαίσιο του key θα χρησιμοποιήσετε ως όνομα το authorization και σαν value το uuid που επιστρέφει το 2o endpoint και θα κάνετε tick αυτήν την σειρά του πίνακα(στα αριστερά υπάρχει το tick button). Mέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 11ο ερώτημα {"_id":"ObjectId that exists in mongodb in Products Collection"(εδώ χρησιμοποιείται η συνάρτηση ObjectID από την βιβλιοθήκη bson), "name" : "a name", "price" : a price, "description" : "a description", "category" : "a category",  "stock" : a stock number (*)} μετά απλά πατάτε send και θα δείτε πως το τελευταίο ερώτημα ολοκληρώθηκε. Προσοχή!!!! Εδώ στο Postman ο χρήστης δεν είναι υποχρεωμένος να καταγράψει όλα τα παραπάνω στοιχεία(*) καθώς μπορεί να  μην επιθυμεί να τροποιήσει όλα τα στοιχεία για ένα συγκεκριμένο προιόν.  

