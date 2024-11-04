<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Invito 18° Compleanno di Samuel</title>
    <style>
        /* Reset del browser */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #0a0f36, #1d3a6f);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            overflow: hidden;
        }

        /* Struttura della lettera */
        .envelope {
            position: relative;
            width: 480px;
            height: 320px;
            background: #002244;
            border: 6px solid #FFD700;
            border-radius: 10px;
            cursor: pointer;
            overflow: hidden;
            box-shadow: 0 15px 25px rgba(0, 0, 0, 0.6);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .envelope:hover {
            transform: scale(1.05);
            box-shadow: 0 20px 30px rgba(0, 0, 0, 0.7);
        }

        /* Lembo superiore */
        .flap {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 60%;
            background: linear-gradient(to bottom, #013a72, #002244);
            border-bottom: 6px solid #FFD700;
            border-top-left-radius: 8px;
            border-top-right-radius: 8px;
            transform-origin: top;
            transition: transform 0.8s ease-in-out;
            z-index: 2;
        }

        .envelope.open .flap {
            transform: rotateX(-180deg);
        }

        /* Sigillo della lettera */
        .seal {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            width: 50px;
            height: 50px;
            background-color: #FFD700;
            border-radius: 50%;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.3);
            z-index: 3;
            transition: transform 0.4s ease;
        }

        .envelope.open .seal {
            transform: scale(0);
        }

        .seal:before {
            content: "18";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 18px;
            font-weight: bold;
            color: #002244;
        }

        /* Contenuto della lettera */
        .content {
            display: none;
            opacity: 0;
            background-color: #002244;
            color: #FFD700;
            border-radius: 8px;
            padding: 40px;
            text-align: center;
            font-size: 1.2em;
            transition: opacity 0.6s ease;
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
        }

        .envelope.open .content {
            display: block;
            opacity: 1;
            animation: fadeInContent 1.2s ease-in-out;
        }

        .content h1 {
            font-size: 26px;
            margin-bottom: 20px;
            animation: textPopUp 0.8s ease forwards;
        }

        .content p {
            margin: 10px 0;
            animation: textSlideIn 0.8s ease forwards;
        }

        /* Animazioni */
        @keyframes fadeInContent {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes textPopUp {
            0% { transform: scale(0); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        @keyframes textSlideIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Bottone RSVP */
        .rsvp-button {
            background: #FFD700;
            color: #002244;
            border: none;
            padding: 12px 24px;
            font-size: 18px;
            border-radius: 8px;
            cursor: pointer;
            margin-top: 20px;
            transition: transform 0.3s, background-color 0.3s;
            animation: buttonPopIn 1s ease forwards 0.6s;
        }

        .rsvp-button:hover {
            background: #ffcc00;
            transform: scale(1.1);
        }

        .rsvp-button:active {
            animation: confirmAnimation 0.5s ease;
        }

        @keyframes confirmAnimation {
            0% { transform: scale(1); box-shadow: 0 0 10px 5px #FFD700; }
            50% { transform: scale(1.2); box-shadow: 0 0 15px 10px #ffcc00; }
            100% { transform: scale(1); box-shadow: 0 0 0px 0px #FFD700; }
        }

        /* Effetti Particelle */
        .particle {
            position: absolute;
            width: 8px;
            height: 8px;
            background: #FFD700;
            border-radius: 50%;
            pointer-events: none;
            animation: floatUp 1.5s ease forwards;
        }

        @keyframes floatUp {
            0% { opacity: 1; transform: translateY(0); }
            100% { opacity: 0; transform: translateY(-80px); }
        }
    </style>
</head>
<body>
    <div class="envelope" onclick="openEnvelope()">
        <div class="flap"></div>
        <div class="seal"></div>
        <div class="content">
            <h1>🎉 Festa per i 18 anni di Samuel 🎉</h1>
            <p>Unisciti a me per celebrare i miei 18 anni!</p>
            <p><strong>📅 Quando:</strong> 5 gennaio 2025</p>
            <p><strong>📍 Dove:</strong> La Trattoria, Sava(TA)</p>
            <button class="rsvp-button" onclick="showAlert(event)">Conferma la tua presenza</button>
        </div>
    </div>

    <script>
        function openEnvelope() {
            const envelope = document.querySelector(".envelope");
            envelope.classList.toggle("open");

            // Creazione particelle dorate alla prima apertura
            if (envelope.classList.contains("open")) {
                for (let i = 0; i < 40; i++) {
                    createParticle();
                }
            }
        }

        function createParticle() {
            const particle = document.createElement("div");
            particle.classList.add("particle");

            particle.style.left = `${Math.random() * 100 + 50}%`;
            particle.style.top = `${Math.random() * 100 + 50}%`;

            document.body.appendChild(particle);

            particle.addEventListener("animationend", () => {
                particle.remove();
            });
        }

        function showAlert(event) {
            event.stopPropagation(); // Evita di chiudere la lettera
            alert("Rispondi al sondaggio sul gruppo!");
        }
    </script>
</body>
</html>
