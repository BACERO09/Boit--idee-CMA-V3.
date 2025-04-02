# Boite-id-e-V2

<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Boîte à Idées - CMA Industry</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        #ideas { margin-top: 20px; display: none; }
        .idea { border-bottom: 1px solid #ccc; padding: 10px; }
        .stats { margin-top: 20px; }
        #loginPage { display: block; }
        #adminPage { display: none; }
    </style>
</head>
<body>
    <div id="loginPage">
        <h1>Connexion Administrateur</h1>
        <input type="password" id="password" placeholder="Mot de passe" />
        <button onclick="login()">Se connecter</button>
    </div>

    <div id="adminPage">
        <h1>Boîte à Idées - CMA Industry</h1>
        <textarea id="ideaInput" placeholder="Déposez votre idée ici..." rows="4" cols="50"></textarea>
        <br>
        <button onclick="submitIdea()">Soumettre</button>

        <h2>Historique des Idées</h2>
        <div id="ideas"></div>

        <h2>Indicateurs d'Efficacité</h2>
        <div class="stats">Total d'idées soumises : <span id="totalIdeas">0</span></div>
    </div>

    <script>
        const correctPassword = "tonMotDePasse";  // Remplace par ton mot de passe
        let ideas = JSON.parse(localStorage.getItem('ideas')) || [];

        function login() {
            const enteredPassword = document.getElementById('password').value;
            if (enteredPassword === correctPassword) {
                document.getElementById('loginPage').style.display = 'none';
                document.getElementById('adminPage').style.display = 'block';
                displayIdeas();
            } else {
                alert("Mot de passe incorrect");
            }
        }

        function submitIdea() {
            let ideaText = document.getElementById('ideaInput').value.trim();
            if (ideaText) {
                let idea = { text: ideaText, date: new Date().toLocaleString() };
                ideas.push(idea);
                localStorage.setItem('ideas', JSON.stringify(ideas));
                document.getElementById('ideaInput').value = '';
                displayIdeas();
            }
        }

        function displayIdeas() {
            let ideasDiv = document.getElementById('ideas');
            ideasDiv.innerHTML = '';
            ideas.forEach(idea => {
                let div = document.createElement('div');
                div.classList.add('idea');
                div.innerHTML = `<strong>Soumis le :</strong> ${idea.date}<br>${idea.text}`;
                ideasDiv.appendChild(div);
            });
            document.getElementById('totalIdeas').innerText = ideas.length;
        }
    </script>
</body>
</html>
