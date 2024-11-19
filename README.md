<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Messagerie Anonyme</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 20px;
            background-color: #f4f4f4;
        }
        h1 {
            text-align: center;
            width: 100%;
        }
        #formContainer {
            width: 60%; /* Élargir la largeur du conteneur du formulaire */
            padding: 30px; /* Augmenter le padding */
            background: white;
            border: 1px solid #ddd;
            border-radius: 10px; /* Arrondir les coins */
            margin-bottom: 20px;
        }
        #messagesContainer {
            display: none; /* Masquer par défaut */
            width: 60%; /* Élargir la largeur du conteneur des messages */
            padding: 30px; /* Augmenter le padding */
            background: white;
            border: 1px solid #ddd;
            border-radius: 10px; /* Arrondir les coins */
            max-height: 500px;
            overflow-y: auto;
        }
        .message {
            padding: 15px; /* Augmenter le padding des bulles */
            margin: 10px 0; /* Espacement entre les messages */
            border-radius: 20px; /* Arrondir les coins des bulles */
            position: relative;
            max-width: 90%; /* Élargir la largeur des bulles */
            word-wrap: break-word; /* Permettre le retour à la ligne */
        }
        .message-time {
            font-size: 0.9em; /* Taille de la police */
            color: #555; /* Couleur du texte */
            margin-bottom: 5px;
        }
        .message.sent {
            background-color: #d3d3d3; /* Couleur grise pour les messages envoyés */
            align-self: flex-end; /* Aligner à droite */
        }
        .message.received {
            background-color: #b0b0b0; /* Couleur grise plus foncée pour les messages reçus */
            align-self: flex-start; /* Aligner à gauche */
        }
        form {
            display: flex;
            flex-direction: column;
            align-items: flex-start;
        }
        textarea {
            width: 100%;
            height: 120px; /* Hauteur du textarea */
            margin-bottom: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
            padding: 10px;
            font-size: 1em; /* Taille de la police */
        }
        button {
            align-self: center;
            margin-top: 10px; /* Espacement au-dessus du bouton */
            padding: 10px 20px; /* Augmenter le padding des boutons */
            font-size: 1em; /* Taille de la police des boutons */
        }
        #returnButton {
            display: none; /* Masquer le bouton de retour par défaut */
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h1>Messagerie Anonyme</h1>
    
    <div id="formContainer">
        <form id="messageForm">
            <textarea id="messageInput" placeholder="Écrivez votre message ici..."></textarea>
            <button type="submit">Envoyer</button>
        </form>
        <button id="scrollToMessages">Voir les messages</button> <!-- Bouton pour voir les messages -->
        <button id="returnButton">Retour au formulaire</button> <!-- Bouton de retour -->
    </div>
    
    <div id="messagesContainer">
        <h2>Messages Anonymes</h2>
        <div id="messages"></div>
    </div>

    <script>
        const form = document.getElementById('messageForm');
        const messageInput = document.getElementById('messageInput');
        const messagesDiv = document.getElementById('messages');
        const scrollToMessagesBtn = document.getElementById('scrollToMessages');
        const messagesContainer = document.getElementById('messagesContainer');
        const returnButton = document.getElementById('returnButton');

        form.addEventListener('submit', function(event) {
            event.preventDefault();
            const messageText = messageInput.value.trim();
            if (messageText) {
                const messageDiv = document.createElement('div');
                messageDiv.className = 'message sent'; // Classe pour message envoyé

                // Obtenir la date et l'heure actuelles
                const now = new Date();
                const dateTime = now.toLocaleString(); // Format de date et heure

                // Créer les éléments pour le message et la date
                const timeDiv = document.createElement('div');
                timeDiv.className = 'message-time';
                timeDiv.textContent = dateTime; // Affiche la date et l'heure

                const textDiv = document.createElement('div');
                textDiv.textContent = messageText;

                // Ajouter la date et le texte au message
                messageDiv.appendChild(timeDiv);
                messageDiv.appendChild(textDiv);
                messagesDiv.prepend(messageDiv); // Ajoute le message en haut de la liste
                messageInput.value = ''; // Réinitialise le champ de saisie
            }
        });

        // Fonction pour afficher la section des messages
        scrollToMessagesBtn.addEventListener('click', function() {
            messagesContainer.style.display = 'block'; // Affiche la section des messages
            messagesContainer.scrollIntoView({ behavior: 'smooth' }); // Fait défiler vers la section
            form.style.display = 'none'; // Masque le formulaire
            returnButton.style.display = 'block'; // Affiche le bouton de retour
        });

        // Fonction pour revenir au formulaire
        returnButton.addEventListener('click', function() {
            messagesContainer.style.display = 'none'; // Masque la section des messages
            form.style.display = 'flex'; // Affiche le formulaire
            returnButton.style.display = 'none'; // Masque le bouton de retour
        });
    </script>
</body>
</html>
