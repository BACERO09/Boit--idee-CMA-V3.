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
    <!-- Page de connexion -->
    <div id="loginPage">
        <h1>Connexion Administrateur</h1>
        <input type="password" id="password" placeholder="Mot de passe" />
        <button onclick="login()">Se connecter</button>
    </div>

    <!-- Page principale avec boîte à idées -->
    <div id="adminPage">
        <h1>Boîte à Idées
