<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Boîte à Idées - CMA Industry</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        #ideas { margin-top: 20px; }
        .idea { border-bottom: 1px solid #ccc; padding: 10px; }
        .stats { margin-top: 20px; }
        #loginPage { display: block; }
        #adminPage { display: none; }
    </style>
</head>
<body>
    <!-- Page utilisateur (tous les utilisateurs peuvent soumettre des idées) -->
    <h1>Boîte à Idées - CMA Industry</h1>
    <h2>Soumettre une idée</h2>
    <textarea id="ideaInput" placeholder="Déposez votre idée ici..." rows="4" cols="50"></textarea>
    <br>
    <button onclick="submitIdea()">Soumettre</button>

    <h2>Indicateurs d'Efficacité</h2>
    <div class="stats">Total d'idées soumises : <span id="totalIdeas">0</span></div>

    <br><br>

    <!-- Page de connexion pour l'historique (accessible uniquement par l'administrateur) -->
    <div id="loginPage">
        <h1>Connexion Administrateur</h1>
        <input type="password" id="password" placeholder="Mot de passe" />
        <button onclick="login()">Se connecter</button>
    </div>

    <div id="adminPage">
        <h2>Historique des Idées</h2>
        <div id="ideas"></div>
    </div>

    <!-- Ajouter Firebase -->
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-firestore.js"></script>
    
    <script>
        // Configuration Firebase pour ton projet
        const firebaseConfig = {
            apiKey: "AIzaSyDXXXXXXXXXXXXXXXXXXXXXXX",  // Remplace par ta clé API Firebase
            authDomain: "boite-a-idee-cma.firebaseapp.com",
            projectId: "boite-a-idee-cma",
            storageBucket: "boite-a-idee-cma.appspot.com",
            messagingSenderId: "123456789012",
            appId: "1:123456789012:web:abc123def456ghi789",
            measurementId: "G-XYZ1234ABC"
        };

        // Initialiser Firebase
        const app = firebase.initializeApp(firebaseConfig);
        const db = firebase.firestore();

        const correctPassword = "tonMotDePasse";  // Remplace par ton mot de passe

        // Fonction de soumission d'idée par les utilisateurs
        function submitIdea() {
            let ideaText = document.getElementById('ideaInput').value.trim();
            if (ideaText) {
                const idea = { text: ideaText, date: new Date().toLocaleString() };
                db.collection("ideas").add(idea)  // Ajouter l'idée dans Firestore
                    .then(() => {
                        document.getElementById('ideaInput').value = ''; // Clear the input
                        alert("Idée soumise !");
                        displayIdeas();  // Actualiser les idées
                    })
                    .catch((error) => {
                        console.error("Erreur lors de la soumission de l'idée: ", error);
                        alert("Une erreur est survenue. Réessayez plus tard.");
                    });
            } else {
                alert("Veuillez entrer une idée avant de soumettre.");
            }
        }

        // Fonction pour afficher le nombre d'idées soumises
        function displayIdeaCount() {
            db.collection("ideas").get()
                .then(querySnapshot => {
                    document.getElementById('totalIdeas').innerText = querySnapshot.size;
                })
                .catch((error) => {
                    console.error("Erreur lors du chargement du nombre d'idées : ", error);
                });
        }

        // Fonction de connexion pour l'administrateur
        function login() {
            const enteredPassword = document.getElementById('password').value;
            if (enteredPassword === correctPassword) {
                // Connexion réussie, cacher la page de connexion et afficher l'administration
                document.getElementById('loginPage').style.display = 'none';
                document.getElementById('adminPage').style.display = 'block';
                displayIdeas();
            } else {
                alert("Mot de passe incorrect");
            }
        }

        // Fonction pour afficher l'historique des idées
        function displayIdeas() {
            const ideasDiv = document.getElementById('ideas');
            ideasDiv.innerHTML = '';
            db.collection("ideas").get()
                .then(querySnapshot => {
                    querySnapshot.forEach(doc => {
                        const idea = doc.data();
                        const div = document.createElement('div');
                        div.classList.add('idea');
                        div.innerHTML = `<strong>Soumis le :</strong> ${idea.date}<br>${idea.text}`;
                        ideasDiv.appendChild(div);
                    });
                })
                .catch((error) => {
                    console.error("Erreur lors du chargement des idées : ", error);
                });
        }

        // Affichage initial des idées soumises
        displayIdeaCount();
    </script>
</body>
</html>
