🛡️ Jhonson-Tool : Simulation d'Abus de Confiance et d'Exfiltration de Données

Introduction

Ce projet, nommé "Jhonson-Tool", est une simulation pédagogique conçue pour illustrer le comportement des attaquants dans le cadre de cyberattaques et, plus spécifiquement, pour démontrer comment des outils d'apparence légitime peuvent abuser de la confiance de l'utilisateur.

L'objectif principal est de sensibiliser à la menace des charges utiles (payloads) dynamiques et des vecteurs d'exfiltration de données discrets, souvent activés par des actions utilisateur apparemment inoffensives.

🔑 Fonctionnalités Légitimes (Façade)

L'outil se présente comme une boîte à outils de développeur inoffensive, offrant les services suivants :

Encodeur/Décodeur de Caractères : Permet d'encoder ou de décoder des chaînes de caractères dans divers formats (Base64, URL Encoding, etc.).

Analyseur/Générateur JWT : Outil utilitaire pour l'inspection et la manipulation de JSON Web Tokens.

Bloc-notes Sécurisé : Un simple éditeur de texte permettant à l'utilisateur de prendre des notes, avec une fonction de "Sauvegarde".

🚩 Le Vecteur d'Attaque : L'Abus de Confiance

L'attaque est déclenchée lors d'une interaction utilisateur standard qui implique la confiance : le clic sur le bouton "Sauvegarder" du bloc-notes.

Mécanisme de l'Attaque

Déclenchement : L'utilisateur clique sur le bouton "Sauvegarder" dans le bloc-notes.

Téléchargement Discret : Au lieu d'effectuer une sauvegarde locale ou sécurisée, l'outil exécute une fonction asynchrone qui télécharge un script malveillant (Payload Python) à partir du serveur de l'attaquant.

Exécution Automatique : Le script téléchargé est immédiatement exécuté en arrière-plan, souvent en exploitant des vulnérabilités ou des autorisations implicites.

💣 La Charge Utile Dynamique (Le Script Python)

La force et la complexité de cette simulation résident dans la nature dynamique du script d'attaque. Le script Python téléchargé n'est pas statique ; l'attaquant peut le personnaliser en temps réel pour adapter ses intentions, rendant la détection par des méthodes de signature traditionnelles beaucoup plus difficile.

Le script d'attaque réalise les actions suivantes :

Vol de Données Ciblées : Récupération de fichiers spécifiques, de l'historique de navigation ou de configurations sensibles.

Espionnage (Reconnaissance) : Prise de captures d'écran et activation discrète de la webcam pour prendre une photo de l'utilisateur à son insu.

Exfiltration des Données : Compression des données volées (y compris la photo) et téléversement chiffré vers un point de terminaison contrôlé par l'attaquant (serveur C2).

💻 Simulation de l'Interface (HTML & CSS)

Voici une représentation simplifiée du composant "Bloc-notes" de l'outil, illustrant le point de confiance ciblé par l'attaque.

<div class="notepad-container">
    <h2>Bloc-notes Sécurisé</h2>
    <p class="warning-text">Utilisez cet espace pour vos notes temporaires.</p>
    <textarea placeholder="Commencez à rédiger vos notes ici..." 
              style="width: 100%; height: 250px; padding: 10px; border: 1px solid #ddd; resize: none;"></textarea>
    
    <!-- C'est ce bouton qui déclenche le script d'attaque en arrière-plan. -->
    <button onclick="simulateAttackDownload()" 
            style="background-color: #3b82f6; color: white; padding: 10px 20px; border: none; border-radius: 8px; cursor: pointer; margin-top: 15px; font-weight: bold; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);">
        💾 Sauvegarder
    </button>
    
    <div id="status-message" style="margin-top: 10px; font-style: italic; color: #10b981;">
        <!-- Message de façade affiché à l'utilisateur -->
        Sauvegarde locale effectuée avec succès.
    </div>
</div>

<style>
  .notepad-container {
    max-width: 600px;
    margin: 20px auto;
    padding: 20px;
    border: 2px solid #3b82f6;
    border-radius: 12px;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
    font-family: Arial, sans-serif;
  }
  .warning-text {
    color: #ef4444;
    font-size: 0.9rem;
  }
  /* Le code JavaScript simulé ici représenterait la logique d'arrière-plan */
  /* Dans la vraie application, cette fonction contacterait le serveur de l'attaquant. */
  function simulateAttackDownload() {
    console.log("LOG: L'utilisateur a cliqué sur Sauvegarder.");
    console.log("ACTION: Connexion au serveur C2 (Attaquant) en cours...");
    // Simuler le téléchargement et l'exécution de l'exécutable Python
    setTimeout(() => {
      console.log("SUCCESS: Script Python personnalisé téléchargé et exécuté en tâche de fond (PID: 1452).");
      console.log("PAYLOAD: Vol des données sensibles, capture webcam et exfiltration des fichiers vers l'attaquant...");
      document.getElementById('status-message').innerText = "Sauvegarde locale effectuée avec succès. (Fichiers exfiltrés en arrière-plan)";
      document.getElementById('status-message').style.color = '#ef4444'; 
    }, 1500);
  }
</style>


🎯 Objectif Pédagogique

Ce projet démontre l'importance cruciale de :

L'inspection du code source : Ne jamais faire confiance à une application sans vérifier son fonctionnement interne, surtout si elle gère des données sensibles.

Le principe du moindre privilège : Restreindre les autorisations pour limiter les dégâts potentiels d'un script d'exfiltration.

La détection comportementale : Les systèmes de sécurité devraient surveiller l'activité anormale des processus (comme un utilitaire de bloc-notes initiant une connexion sortante pour télécharger un exécutable).
