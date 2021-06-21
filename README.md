# infosystems-proj-2
<<2η υποχρεωτική εργασία στα πληροφοριακά συστήματα>>

Αρχικά, για την υλοποίηση της συγκεκριμένης εργασίας είναι απαραίτητη η δημιουργία image mongo με την εκτέλεση της εντολής:
- docker pull mongo
καθώς και η εγκατάσταση του docker-compose στο linux μέσω των οδηγιών στο παρακάτω link:
- https://computingforgeeks.com/how-to-install-latest-docker-compose-on-linux/
ο κώδικας όπως και την προηγούμενη φορά δέχεται τα δεδομένα από την εφαρμογή Postman.

Πρέπει αρχικά όπως στην προηγούμενη φορά να δημιουργηθεί ένα container έτσι ώστε να εκτελέσετε την παρακάτω εντολή στο directory όπου θα βρίσκονται τα json students.json και users.json docker cp Products.json mongodb:/Products.json docker exec -it mongodb mongoimport --db=InfoSys --collection=Products/ --file=Products.json docker cp Users.json mongodb:/users.json docker exec -it mongodb mongoimport --db=InfoSys --collection=Users --file=users.json

Mετά να σβηστεί το docker image με την εντολή docker image rm imagename και στην συνέχεια:

Μέσα στο αρχείο .zip περιέχονται τα appinfo.py, docker-compose.yml, dockerfile, τα Users.json & Products.json.

1ο Βήμα - Eκκίνηση docker, postman, mongodb: sudo systemctl start docker sudo systemctl start mongod (*)και όσο αφορά το postman θα πρέπει αφού το έχετε εγκαταστήσει να πάτε στο directory που έχει εγκατασταθεί μέσω terminal και να το ξεκινήσετε ως εξής: ./'Postman Agent' !!!! Προσοχή επιπλέον είναι απαραίτητο να χρησιμοποιηθούν στην python οι βιβλιοθήκες pymongo, flask, os και bson.

2o Bήμα - Για την εκτέλεση του κώδικα και την ενοποίηση των λειτουργιών των δύο container θα πρέπει να εκτελεστούν οι εντολές:
- docker-compose build
- docker-compose up

3o Bήμα - Εκτέλση των endpoints(Eφόσον τρέχει το docker-compose up & το Postman Agent)

θα το ανοίξετε σε ένα tab, θα φτιάξετε ένα νέο workspace(+new workspace) το ονομάζετε όπως θέλετε και στην συνέχεια θα ανοίξετε μέσα στο workspace ένα νέο tab. Tώρα, στο νέο tab που έχετε ανοίξει θα παρατηρήσετε ότι υπάρχει μπροστά ένα label με GET εκεί μπορείτε να το αλλάξετε σε POST, PATCH, DELETE, PUT κλπ ανάλογα με το endpoint που έχετε. και ακριβώς στα δεξιά υπάρχει ένα κενό πλαίσιο στο οποίο πληκτρολογείτε το url ως εξής http://localhost:5000/name_of_endpoint ανάλογα με το endpoint που επιθυμείτε να εκτελέσετε και τέρμα δεξιά υπάρχει ένα κουμπί send το κάνετε κλικ και στέλνει οτιδήποτε έχετε βάλει στο body του request, header request κλπ.

1ο endpoint -- create-user(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά POST) μέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 1ο ερώτημα { "username": "a name"(κατά προτίμηση να δώσετε ένα όνομα που υπάρχει στο students.json), "password": "a password" } και μετά απλά πατάτε send και θα δείτε πως το πρώτο ερώτημα ολοκληρώθηκε

2ο endpoint -- login(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά POST) μέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 2ο ερώτημα τα ίδια στοιχεία που δώσατε για το 1ο γιατί εδώ θέλουμε να δούμε αν ο χρήστης που δημιουργήθηκε προηγουμένως έχει κάνει login και μετά απλά πατάτε send και θα δείτε πως το δεύτερο ερώτημα ολοκληρώθηκε

1o endpoint - create-user
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά POST) μέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 1ο ερώτημα { "username": "a name", "password": "a password", "email" : "an email", "category" : "a category", "shopping_cart" : [], "orderHistory" : [] } και μετά απλά πατάτε send και θα δείτε πως το πρώτο ερώτημα ολοκληρώθηκε

2o endpoint - login
(εδώ θα πρέπει να έχετε επιλέξει στο postman πως το url αφορά POST) μέσα στο postman θα δείτε ένα πλαίσιο απο κάτω στο ίδιο tab όπου έχει διάφορες επιλογές εμείς θα επιλέξουμε raw -> text -> JSON και στο πλαίσιο(body request) αυτό θα γράψετε για το 2ο ερώτημα τα ίδια στοιχεία(εκτός από "shopping_cart" : [], "orderHistory" : []) που δώσατε για το 1ο γιατί εδώ θέλουμε να δούμε αν ο χρήστης που δημιουργήθηκε προηγουμένως έχει κάνει login και μετά απλά πατάτε send και θα δείτε πως το δεύτερο ερώτημα ολοκληρώθηκε

- Για τον απλό χρήστη

3o endpoint(3 endpoints) 
- getProductCategory


- getProductName

- getProductID


4o endpoint - insertProduct
5o endpoint - showProduct
6o endpoint - deleteProduct
7o endpoint - purchaseProduct
8o endpoint - remove-user

- Για τον διαχειρηστή

9o endpoint - adminInsertProduct
10o endpoint - adminRemoveProduct
11o endpoint - adminUpdateProduct
