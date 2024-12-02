
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestión de la Ansiedad</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f0f0f0;
            margin: 0;
            padding: 20px;
        }
        .section {
            display: none;
            margin-top: 20px;
        }
        #low, #medium, #high, #crisis {
            display: none;
        }
        video {
            width: 300px;
            height: auto;
        }
        button {
            padding: 10px 20px;
            margin-top: 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        #five-senses, #pop-up {
            display: none;
        }
        #pop-up {
            background-color: white;
            border: 2px solid black;
            padding: 20px;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 10;
        }
        #mask {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            z-index: 9;
        }
    </style>
</head>
<body>
    <h1>Gestión de la Ansiedad</h1>
    <p>Identifica tu nivel de estrés</p>

    <button onclick="showSection('low')">Bajo</button>
    <button onclick="showSection('medium')">Medio</button>
    <button onclick="showSection('high')">Alto</button>
    <button onclick="showSection('crisis')">Al borde de una crisis</button>

    <!-- Bajo -->
    <div id="low" class="section">
        <h2>Nivel Bajo</h2>
        <audio controls>
            <source src="https://www.soundjay.com/nature/cascade-1.mp3" type="audio/mp3">
            Tu navegador no soporta este audio.
        </audio>
        <p>Ejercicio de respiración: Inhala por 4 segundos, retén 4 segundos, exhala por 4 segundos.</p>
        <button onclick="location.reload()">Volver a inicio</button>
    </div>

    <!-- Medio -->
    <div id="medium" class="section">
        <h2>Nivel Medio</h2>
        <p>Haz estiramientos monitorizados por el siguiente video. Mantén cada postura durante el tiempo indicado y respira cuando se te diga.</p>
        <video controls>
            <source src="https://www.w3schools.com/html/mov_bbb.mp4" type="video/mp4">
            Tu navegador no soporta este video.
        </video>
        <button onclick="location.reload()">Volver a inicio</button>
    </div>

    <!-- Alto -->
    <div id="high" class="section">
        <h2>Nivel Alto</h2>
        <div id="five-senses">
            <p>Ejercicio de externalización: Usa tus cinco sentidos para relajarte.</p>
            <div id="sense-1">
                <h3>1. ¿Qué ves?</h3>
                <p>Describe 5 cosas que puedas ver.</p>
            </div>
            <div id="sense-2" style="display:none;">
                <h3>2. ¿Qué escuchas?</h3>
                <p>Describe 4 cosas que puedas oír.</p>
            </div>
            <div id="sense-3" style="display:none;">
                <h3>3. ¿Qué tocas?</h3>
                <p>Describe 3 cosas que puedas tocar.</p>
            </div>
            <div id="sense-4" style="display:none;">
                <h3>4. ¿Qué hueles?</h3>
                <p>Describe 2 cosas que puedas oler.</p>
            </div>
            <div id="sense-5" style="display:none;">
                <h3>5. ¿Qué saboreas?</h3>
                <p>Describe 1 cosa que puedas saborear.</p>
            </div>
            <button onclick="nextSense()">Siguiente</button>
            <button onclick="prevSense()">Anterior</button>
        </div>
        <button onclick="showPopUp()">Finalizar</button>
    </div>

    <!-- Crisis -->
    <div id="crisis" class="section">
        <h2>Al borde de una crisis</h2>
        <p>Aquí tienes pasos detallados para calmarte en situaciones extremas:</p>
        <ul>
            <li>Respira profundamente.</li>
            <li>Cuenta hacia atrás de 10 a 1.</li>
            <li>Visualiza un lugar seguro.</li>
            <li>Repite frases de afirmación como "Estoy a salvo".</li>
        </ul>
        <button onclick="location.reload()">Volver a inicio</button>
    </div>

    <!-- Pop-up -->
    <div id="pop-up">
        <p>¿Te sientes más relajado?</p>
        <button onclick="resetPage()">Sí</button>
        <button onclick="askQuestion()">No</button>
    </div>

    <!-- Máscara oscura -->
    <div id="mask"></div>

    <script>
        let currentSense = 1;
        
        function showSection(sectionId) {
            document.querySelectorAll('.section').forEach(section => section.style.display = 'none');
            document.getElementById(sectionId).style.display = 'block';
            if (sectionId === 'high') {
                currentSense = 1;
                document.getElementById('five-senses').style.display = 'block';
                showSense(currentSense);
            }
        }

        function nextSense() {
            if (currentSense < 5) {
                currentSense++;
                showSense(currentSense);
            }
        }

        function prevSense() {
            if (currentSense > 1) {
                currentSense--;
                showSense(currentSense);
            }
        }

        function showSense(senseNumber) {
            document.querySelectorAll('#five-senses > div').forEach(sense => sense.style.display = 'none');
            document.getElementById(`sense-${senseNumber}`).style.display = 'block';
        }

        function showPopUp() {
            document.getElementById('pop-up').style.display = 'block';
            document.getElementById('mask').style.display = 'block';
        }

        function resetPage() {
            location.reload();
        }

        let questionIndex = 0;
        const questions = [
            "¿El fuego se puede tocar?",
            "¿El agua tiene color?",
            "¿Puedes ver el viento?",
            "¿Las estrellas están cerca?",
            "¿Es posible oír el silencio?"
        ];

        function askQuestion() {
            if (questionIndex < questions.length) {
                document.getElementById('pop-up').innerHTML = `<p>${questions[questionIndex]}</p><button onclick='resetPage()'>Sí</button><button onclick='nextQuestion()'>No</button>`;
                questionIndex++;
            } else {
                document.getElementById('pop-up').innerHTML = "<p>Parece que ya has reflexionado suficiente. ¡Vuelve a intentarlo más tarde!</p><button onclick='resetPage()'>Volver a inicio</button>";
            }
        }

        function nextQuestion() {
            askQuestion();
        }
    </script>
</body>
</html>
