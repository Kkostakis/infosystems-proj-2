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

1o endpoint - create-user
Εδώ αρκεί στο Postman 

2o endpoint - login

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
