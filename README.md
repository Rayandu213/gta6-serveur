# gta6-serveur
découvrir un nouvelle aspect du jeux
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grand Theft Auto VI - Serveur Rchehidi</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background: radial-gradient(circle, #1a0826 0%, #05020a 100%);
            color: #ffffff;
            font-family: 'Impact', 'Arial Black', sans-serif;
            text-align: center;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
        }

        /* Effet rétro scanlines */
        body::before {
            content: " ";
            display: block;
            position: absolute;
            top: 0; left: 0; bottom: 0; right: 0;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.06), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.06));
            z-index: 2;
            background-size: 100% 4px, 6px 100%;
            pointer-events: none;
        }

        .bg-animation {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(180deg, rgba(255,0,127,0.05) 0%, rgba(127,0,255,0) 100%);
            animation: pulseBg 8s infinite alternate ease-in-out;
            z-index: 1;
            pointer-events: none;
        }

        @keyframes pulseBg {
            0% { opacity: 0.3; transform: scale(1); }
            100% { opacity: 0.8; transform: scale(1.05); }
        }

        #siteContainer {
            position: relative;
            z-index: 5;
            transition: opacity 0.8s ease;
        }

        .logo-container {
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        h1 {
            font-size: 4rem;
            margin: 0;
            background: linear-gradient(45deg, #ff007f, #7f00ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 20px rgba(255, 0, 127, 0.5);
        }

        h2 {
            font-size: 8rem;
            margin: -20px 0 20px 0;
            color: #ffffff;
            font-style: italic;
            text-shadow: 4px 4px 0px #ff007f, -4px -4px 0px #7f00ff;
        }

        p {
            font-family: 'Arial', sans-serif;
            font-size: 1.5rem;
            color: #b3a1c9;
            margin-bottom: 40px;
            font-weight: bold;
        }

        .btn-play {
            background: linear-gradient(90deg, #ff007f 0%, #7f00ff 100%);
            color: white;
            font-family: 'Arial', sans-serif;
            font-size: 1.3rem;
            font-weight: bold;
            text-transform: uppercase;
            padding: 15px 40px;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 0 25px #ff007f;
            transition: all 0.3s ease;
            text-decoration: none;
            display: inline-block;
        }

        .btn-play:hover {
            transform: scale(1.1);
            box-shadow: 0 0 35px #7f00ff;
            background: linear-gradient(90deg, #7f00ff 0%, #ff007f 100%);
        }

        /* Modale Connexion */
        .modal {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(5, 2, 10, 0.9);
            backdrop-filter: blur(8px);
            justify-content: center;
            align-items: center;
            z-index: 100;
        }

        .modal-content {
            background: #13061c;
            padding: 40px;
            border-radius: 20px;
            border: 2px solid #ff007f;
            box-shadow: 0 0 40px rgba(255, 0, 127, 0.3);
            max-width: 450px;
            width: 90%;
            font-family: 'Arial', sans-serif;
        }

        .modal-title {
            font-family: 'Impact', sans-serif;
            font-size: 2rem;
            letter-spacing: 1px;
            color: #fff;
            margin-bottom: 20px;
        }

        .progress-bar-container {
            background: #251236;
            border-radius: 10px;
            height: 15px;
            width: 100%;
            overflow: hidden;
            margin: 25px 0;
        }

        .progress-bar {
            background: linear-gradient(90deg, #ff007f, #7f00ff);
            height: 100%;
            width: 0%;
            box-shadow: 0 0 10px #ff007f;
            transition: width 0.1s linear;
        }

        .server-info {
            font-size: 1.1rem;
            color: #b3a1c9;
            line-height: 1.6;
        }

        .ip-highlight {
            color: #ff007f;
            font-weight: bold;
        }

        .btn-close {
            margin-top: 20px;
            background: transparent;
            color: #554366;
            border: 1px solid #554366;
            padding: 8px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.2s;
        }

        .btn-close:hover { color: #fff; border-color: #fff; }

        /* Écran d'intégration du Trailer Plein Écran */
        .trailer-screen {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: #000;
            z-index: 200;
            justify-content: center;
            align-items: center;
        }

        .trailer-screen iframe {
            width: 100vw;
            height: 100vh;
            border: none;
        }

        .footer-text {
            position: absolute;
            bottom: 20px;
            font-family: 'Arial', sans-serif;
            font-size: 0.9rem;
            color: #554366;
            z-index: 5;
        }
    </style>
</head>
<body>

    <div class="bg-animation"></div>

    <div id="siteContainer">
        <div class="logo-container">
            <h1>Grand Theft Auto</h1>
            <h2>VI</h2>
        </div>
        <p>Le serveur de Rchehidi est prêt. Vice City vous attend...</p>
        <a href="#" class="btn-play" onclick="openModal(event)">Lancer la partie</a>
    </div>

    <!-- Fenêtre contextuelle -->
    <div id="connectionModal" class="modal">
        <div class="modal-content">
            <div class="modal-title">CONNEXION EN COURS</div>
            <div class="server-info" id="statusText">Initialisation du protocole...</div>
            <div class="progress-bar-container">
                <div id="loadingBar" class="progress-bar"></div>
            </div>
            <div class="server-info">
                Hôte : <span class="ip-highlight">Raspberry Pi OS</span><br>
                IP locale : <span class="ip-highlight">192.168.1.50</span> (Port: 7777)
            </div>
            <button class="btn-close" onclick="closeModal()">Annuler</button>
        </div>
    </div>

    <!-- Conteneur pour le Trailer d'introduction -->
    <div id="trailerScreen" class="trailer-screen">
        <!-- Utilisation d'un lecteur YouTube masqué pour les contrôles et automatisé (autoplay) -->
        <iframe id="trailerVideo" src="" allow="autoplay; encrypted-media" allowfullscreen></iframe>
    </div>

    <div class="footer-text">
        © 2026 Rockstar Games, Inc. Hébergé fièrement sur Raspberry Pi OS.
    </div>

    <script>
        function openModal(event) {
            event.preventDefault();
            const modal = document.getElementById('connectionModal');
            const bar = document.getElementById('loadingBar');
            const status = document.getElementById('statusText');
            
            modal.style.display = 'flex';
            bar.style.width = '0%';
            status.innerText = "Recherche du serveur local...";

            let progress = 0;
            const interval = setInterval(() => {
                progress += Math.floor(Math.random() * 8) + 2;
                if (progress >= 100) {
                    progress = 100;
                    clearInterval(interval);
                    status.innerHTML = "✅ <span style='color:#00ffcc;'>Chargement de l'environnement...</span>";
                    
                    // Lancer la transition vers le trailer après une courte pause
                    setTimeout(launchGameTrailer, 1000);
                } else if (progress > 30 && progress < 65) {
                    status.innerText = "Liaison avec l'adresse 192.168.1.50...";
                } else if (progress >= 65) {
                    status.innerText = "Génération de la carte de Vice City...";
                }
                bar.style.width = progress + '%';
            }, 100);

            window.currentLoading = interval;
        }

        function closeModal() {
            document.getElementById('connectionModal').style.display = 'none';
            clearInterval(window.currentLoading);
        }

        function launchGameTrailer() {
            // Fermer la modale et cacher l'accueil du site
            document.getElementById('connectionModal').style.display = 'none';
            document.getElementById('siteContainer').style.opacity = '0';
            
            // Configurer l'URL de la vidéo avec Autoplay et Loop activés
            const videoFrame = document.getElementById('trailerVideo');
            // Utilise l'ID du trailer officiel de GTA 6
            videoFrame.src = "https://youtube.com";
            
            // Afficher l'écran vidéo plein écran
            document.getElementById('trailerScreen').style.display = 'flex';
        }
    </script>
</body>
</html>
