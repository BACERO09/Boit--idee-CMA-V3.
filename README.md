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
    </style>
</head>
<body>
    <h1>Boîte à Idées - CMA Industry</h1>
    <textarea id="ideaInput" placeholder="Déposez votre idée ici..." rows="4" cols="50"></textarea>
    <br>
    <button onclick="submitIdea()">Soumettre</button>
    
    <h2>Historique des Idées</h2>
    <div id="ideas"></div>
    
    <h2>Indicateurs d'Efficacité</h2>
    <div class="stats">Total d'idées soumises : <span id="totalIdeas">0</span></div>
    
    <script>
        let ideas = JSON.parse(localStorage.getItem('ideas')) || [];
        
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
        
        displayIdeas();
    </script>
</body>
</html>
