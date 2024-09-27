# checkponit-mongodb

Étape 1 : Créer une base de données appelée "contact" et une collection appelée "contactlist"
const mongoose = require('mongoose');  

// Connexion à MongoDB  
mongoose.connect('mongodb://localhost:27017/contact', {  
    useNewUrlParser: true,  
    useUnifiedTopology: true  
});  

// Définir le schéma pour la collection  
const contactSchema = new mongoose.Schema({  
    nom: String,  
    prenom: String,  
    email: String,  
    age: Number  
});  

// Créer le modèle pour la collection  
const Contact = mongoose.model('contactlist', contactSchema);  
Étape 2 : Insérer les documents dans "contactlist"
const contacts = [  
    { nom: 'Ben', prenom: 'Moris', email: 'ben@gmail.com', age: 26 },  
    { nom: 'Kefi', prenom: 'Seif', email: 'kefi@gmail.com', age: 15 },  
    { nom: 'Emilie', prenom: 'Brouge', email: 'emilie.b@gmail.com', age: 40 },  
    { nom: 'Alex', prenom: 'Brown', age: 4 },  
    { nom: 'Denzel', prenom: 'Washington', age: 3 }  
];  

// Insérer les contacts dans la base de données  
Contact.insertMany(contacts)  
    .then(() => console.log('Contacts insérés avec succès'))  
    .catch(err => console.error(err));  
Étape 3 : Afficher toute la liste des contacts
Contact.find()  
    .then(contacts => {  
        console.log('Liste des contacts:', contacts);  
    })  
    .catch(err => console.error(err));  
Étape 4 : Afficher toutes les informations sur une seule personne en utilisant son ID
Pour afficher un contact par ID, vous pouvez utiliser le code suivant :

const contactId = 'ID_DU_CONTACT'; // Remplacez par un ID valide  

Contact.findById(contactId)  
    .then(contact => {  
        console.log('Informations sur le contact:', contact);  
    })  
    .catch(err => console.error(err));  
Étape 5 : Afficher tous les contacts ayant un âge > 18
Contact.find({ age: { $gt: 18 } })  
    .then(contacts => {  
        console.log('Contacts ayant plus de 18 ans:', contacts);  
    })  
    .catch(err => console.error(err));  
Étape 6 : Afficher tous les contacts ayant un âge > 18 et dont le nom contient "ah"
Contact.find({ age: { $gt: 18 }, nom: { $regex: /ah/i } })  
    .then(contacts => {  
        console.log('Contacts ayant plus de 18 ans et dont le nom contient "ah":', contacts);  
    })  
    .catch(err => console.error(err));  
Étape 7 : Changer le prénom du contact de "Kefi Seif" en "Kefi Anis"
Contact.findOneAndUpdate(  
    { prenom: 'Seif', nom: 'Kefi' },  
    { prenom: 'Kefi Anis' },  
    { new: true }  
)  
.then(contact => {  
    console.log('Contact mis à jour:', contact);  
})  
.catch(err => console.error(err));  
Étape 8 : Supprimer les contacts qui ont moins de 5 ans
Contact.deleteMany({ age: { $lt: 5 } })  
    .then(result => {  
        console.log(`Contacts supprimés: ${result.deletedCount}`);  
    })  
    .catch(err => console.error(err));  
Étape 9 : Afficher toute la liste des contacts
Réutilisez le code d'affichage de la liste des contacts :

Contact.find()  
    .then(contacts => {  
        console.log('Liste des contacts:', contacts);  
    })  
    .catch(err => console.error(err)); 
