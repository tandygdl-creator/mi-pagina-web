[temp.html](https://github.com/user-attachments/files/26519510/temp.html)
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Mario Quest: Mitos del Engagement</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none;
        }

        body {
            min-height: 100vh;
            background: linear-gradient(145deg, #0b2b2f 0%, #1a4a5f 100%);
            font-family: 'Courier New', 'Press Start 2P', 'Segoe UI', monospace;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }

        /* contenedor estilo consola */
        .game-container {
            max-width: 1000px;
            width: 100%;
            background: #2c1a0e;
            border-radius: 2rem;
            border: 6px solid #f7b32b;
            box-shadow: 0 20px 30px rgba(0,0,0,0.5), inset 0 1px 4px rgba(255,215,0,0.3);
            overflow: hidden;
        }

        /* escenario Mario */
        .mario-stage {
            background: #7ec8e0;
            background-image: linear-gradient(to bottom, #87CEEB 0%, #87CEEB 55%, #6b8c42 55%, #5a7a32 100%);
            padding: 1rem;
            min-height: 380px;
            position: relative;
            display: flex;
            flex-direction: column;
            align-items: center;
            border-bottom: 4px solid #e2b13b;
        }

        .top-bar {
            display: flex;
            justify-content: space-between;
            width: 100%;
            padding: 0.5rem;
            background: #000000aa;
            border-radius: 2rem;
            margin-bottom: 1rem;
            color: #ffef8f;
            font-weight: bold;
            font-size: 0.9rem;
        }

        .mario-character {
            background: #e52525;
            width: 70px;
            height: 70px;
            border-radius: 20px 20px 10px 10px;
            position: relative;
            box-shadow: 0 6px 0 #8b0000;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.5rem;
            transition: transform 0.2s;
        }

        .path {
            background: #c9a87b;
            height: 50px;
            width: 95%;
            border-radius: 30px;
            margin: 0.5rem 0;
            display: flex;
            align-items: center;
            justify-content: space-around;
            padding: 0 10px;
            box-shadow: inset 0 2px 5px rgba(0,0,0,0.2);
        }

        .step-block {
            width: 50px;
            height: 50px;
            background: #e3bc7c;
            border-radius: 12px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            transition: 0.2s;
            box-shadow: 0 4px 0 #8b6946;
        }
        .step-block.active {
            background: #f5da6e;
            box-shadow: 0 0 0 2px gold;
            transform: scale(1.05);
        }
        .step-block.completed {
            background: #f5da6e;
            opacity: 0.7;
        }

        .question-modal {
            background: #fff3e0;
            border-radius: 2rem;
            margin: 1rem;
            padding: 1rem;
            border: 4px solid #e6a017;
            box-shadow: 0 10px 20px black;
            width: 90%;
        }

        .question-text {
            font-size: 1.2rem;
            font-weight: bold;
            margin-bottom: 1rem;
            color: #2d3e2b;
            text-align: center;
        }

        .options {
            display: flex;
            gap: 1rem;
            justify-content: center;
            margin: 1rem 0;
        }

        .opt-btn {
            background: #fedc83;
            border: none;
            padding: 0.6rem 1.2rem;
            border-radius: 2rem;
            font-weight: bold;
            cursor: pointer;
            font-family: monospace;
            font-size: 1rem;
            transition: 0.1s;
        }
        .opt-btn:hover {
            background: #f3b33d;
            transform: scale(0.98);
        }

        .feedback {
            background: #efe2ce;
            padding: 0.6rem;
            border-radius: 1rem;
            margin: 0.5rem 0;
            font-size: 0.8rem;
        }

        .next-btn {
            background: #4c8b3c;
            color: white;
            border: none;
            padding: 0.6rem;
            border-radius: 3rem;
            font-weight: bold;
            width: 100%;
            cursor: pointer;
            font-size: 1rem;
        }
        .next-btn:disabled {
            opacity: 0.5;
        }

        .advance-btn {
            background: #d48b2c;
            padding: 0.6rem 1.5rem;
            border: none;
            border-radius: 2rem;
            font-weight: bold;
            color: white;
            font-size: 1rem;
            cursor: pointer;
            margin-top: 0.5rem;
            font-family: monospace;
        }

        @keyframes bounce {
            0% { transform: translateY(0); }
            50% { transform: translateY(-12px); }
            100% { transform: translateY(0); }
        }
        .jump {
            animation: bounce 0.3s ease;
        }

        button:disabled {
            opacity: 0.6;
            cursor: not-allowed;
        }
    </style>
</head>
<body>
<div class="game-container">
    <div class="mario-stage">
        <div class="top-bar">
            <span>⭐ MONEDAS: <span id="coinCount">0</span></span>
            <span>🔥 RACHA: <span id="streakCount">0</span></span>
            <span>📦 PASO: <span id="stepCount">0</span>/<span id="totalSteps">0</span></span>
        </div>
        <div class="mario-character" id="mario">
            <span>🍄</span>
        </div>
        <div id="pathContainer" class="path"></div>
        <button id="advanceBtn" class="advance-btn">➡️ AVANZAR ➡️</button>
        <div id="questionModal" class="question-modal" style="display: none;"></div>
    </div>
</div>

<script>
    // ------------------- PREGUNTAS VERDADERO O FALSO (10) -------------------
    const questions = [
        {
            text: "Si respondo que no entiendo mi compensación, me van a bajar el sueldo.",
            correct: false,
            explanation: "❌ FALSO. La pregunta busca saber si la empresa comunica con claridad tus beneficios (vales, bonos, sueldo). No tiene impacto en el monto de tu nómina."
        },
        {
            text: "El anonimato está garantizado al 100% en esta plataforma.",
            correct: true,
            explanation: "✅ VERDADERO. Las encuestas de Perceptyx están diseñadas para que los líderes solo vean tendencias grupales, no respuestas individuales."
        },
        {
            text: "Debo calificar alto a mi líder para que el equipo se vea bien.",
            correct: false,
            explanation: "❌ FALSO. El objetivo es la retroalimentación real. Si hay algo que mejorar en el liderazgo, la encuesta es la herramienta para detectarlo objetivamente."
        },
        {
            text: "La 'Burocracia' se refiere a los protocolos de seguridad que debo seguir.",
            correct: false,
            explanation: "❌ FALSO. Se refiere a procesos lentos o innecesarios que no agregan valor y dificultan tu trabajo diario. La seguridad nunca se considera burocracia negativa."
        },
        {
            text: "Si pongo un comentario escrito, nadie lo va a leer.",
            correct: false,
            explanation: "❌ FALSO. Los comentarios son analizados por temas (como Cultura o Mejora Continua) y son la base principal para crear planes de acción."
        },
        {
            text: "La encuesta mide si puedo ser yo mismo/a en el trabajo (Autenticidad).",
            correct: true,
            explanation: "✅ VERDADERO. Se evalúa si sientes la libertad de expresar tu personalidad y opiniones sin miedo a ser juzgado."
        },
        {
            text: "El 'Engagement' solo significa que estoy feliz en mi puesto.",
            correct: false,
            explanation: "❌ FALSO. Significa qué tan conectado te sientes con los objetivos de la empresa y qué tan motivado estás para contribuir a ellos."
        },
        {
            text: "Si hay una baja calificación en 'Trato Justo', el sistema nos castiga.",
            correct: false,
            explanation: "❌ FALSO. Una baja calificación (como el actual -19 en trato justo) indica que la empresa debe revisar sus procesos de equidad, no que el equipo será sancionado."
        },
        {
            text: "Responder la encuesta toma más de 30 minutos.",
            correct: false,
            explanation: "❌ FALSO. El tiempo promedio registrado es de 11 minutos y 33 segundos. Es un proceso ágil."
        },
        {
            text: "Mi participación no cambia nada en la empresa.",
            correct: false,
            explanation: "❌ FALSO. La participación histórica ha sido del 100%, lo que da mucha fuerza a la voz del equipo para exigir mejoras en procesos y comunicación."
        }
    ];

    // Estados del juego
    let currentStep = 0;           // 0 = antes de empezar, luego 1..10
    let coins = 0;
    let streak = 0;
    let answered = false;          // si ya respondió la pregunta actual
    let waitingForNext = false;    // esperando a que pulse "Siguiente" después de responder
    let userResults = [];           // guarda si acertó (true/false) en cada pregunta
    let gameFinished = false;

    // Elementos DOM
    const pathContainer = document.getElementById('pathContainer');
    const advanceBtn = document.getElementById('advanceBtn');
    const questionModal = document.getElementById('questionModal');
    const coinSpan = document.getElementById('coinCount');
    const streakSpan = document.getElementById('streakCount');
    const stepCountSpan = document.getElementById('stepCount');
    const totalStepsSpan = document.getElementById('totalSteps');
    const mario = document.getElementById('mario');

    totalStepsSpan.innerText = questions.length;

    // Construir el camino con bloques estilo Mario
    function buildPath() {
        pathContainer.innerHTML = '';
        for (let i = 0; i < questions.length; i++) {
            const block = document.createElement('div');
            block.classList.add('step-block');
            if (i < currentStep) {
                block.classList.add('completed');
                block.innerHTML = '⭐';
            } else if (i === currentStep) {
                block.classList.add('active');
                block.innerHTML = '❓';
            } else {
                block.innerHTML = '?';
            }
            pathContainer.appendChild(block);
        }
    }

    function updateStatsUI() {
        coinSpan.innerText = coins;
        streakSpan.innerText = streak;
        stepCountSpan.innerText = currentStep;
        buildPath();
    }

    // Mostrar pregunta actual
    function showQuestion() {
        if (gameFinished) return;
        if (currentStep >= questions.length) {
            endGame();
            return;
        }

        const q = questions[currentStep];
        const alreadyAnswered = (userResults[currentStep] !== undefined);

        let optionsHtml = `
            <div class="options">
                <button class="opt-btn" data-value="true">✅ Verdadero</button>
                <button class="opt-btn" data-value="false">❌ Falso</button>
            </div>
        `;

        let feedbackHtml = `<div id="feedbackArea" class="feedback">⭐ Elige una respuesta para ganar monedas y seguir avanzando.</div>`;

        questionModal.innerHTML = `
            <div class="question-text">🔍 ${q.text}</div>
            ${optionsHtml}
            ${feedbackHtml}
            <button id="nextQuestionBtn" class="next-btn" disabled>➡️ SIGUIENTE AVANCE</button>
        `;
        questionModal.style.display = 'block';

        // Si ya había respondido (por reinicio no debería, pero por si acaso)
        if (alreadyAnswered) {
            const isCorrect = userResults[currentStep];
            const correctText = q.correct ? "Verdadero" : "Falso";
            const userChoice = isCorrect ? (q.correct ? "Verdadero" : "Falso") : (q.correct ? "Falso" : "Verdadero");
            const emoji = isCorrect ? "✅" : "❌";
            document.getElementById('feedbackArea').innerHTML = `
                <strong>${emoji} ${isCorrect ? "¡Correcto!" : "Incorrecto"}</strong><br>
                Tu respuesta: ${userChoice}<br>
                Respuesta correcta: ${correctText}<br>
                ${q.explanation}
            `;
            // deshabilitar opciones
            document.querySelectorAll('.opt-btn').forEach(btn => btn.disabled = true);
            document.getElementById('nextQuestionBtn').disabled = false;
            answered = true;
        }

        // Eventos de respuesta
        const optBtns = document.querySelectorAll('.opt-btn');
        optBtns.forEach(btn => {
            btn.addEventListener('click', (e) => {
                if (answered || gameFinished) return;
                const selected = btn.getAttribute('data-value') === 'true';
                const isCorrect = (selected === q.correct);
                // actualizar monedas y racha
                if (isCorrect) {
                    coins++;
                    streak++;
                    mario.classList.add('jump');
                    setTimeout(() => mario.classList.remove('jump'), 300);
                } else {
                    streak = 0;
                }
                userResults[currentStep] = isCorrect;
                updateStatsUI();

                const correctText = q.correct ? "Verdadero" : "Falso";
                const userChoice = selected ? "Verdadero" : "Falso";
                const emoji = isCorrect ? "✅" : "❌";
                const feedbackDiv = document.getElementById('feedbackArea');
                feedbackDiv.innerHTML = `
                    <strong>${emoji} ${isCorrect ? "¡Correcto!" : "Incorrecto"}</strong><br>
                    Tu respuesta: <strong>${userChoice}</strong><br>
                    Respuesta correcta: <strong>${correctText}</strong><br>
                    ${q.explanation}
                `;

                answered = true;
                // deshabilitar opciones
                optBtns.forEach(b => b.disabled = true);
                // habilitar botón siguiente
                document.getElementById('nextQuestionBtn').disabled = false;
            });
        });

        const nextModalBtn = document.getElementById('nextQuestionBtn');
        nextModalBtn.addEventListener('click', () => {
            if (!answered) return;
            questionModal.style.display = 'none';
            currentStep++;
            answered = false;
            waitingForNext = false;
            updateStatsUI();
            if (currentStep < questions.length) {
                advanceBtn.disabled = false;
                advanceBtn.innerText = '➡️ AVANZAR ➡️';
            } else {
                endGame();
            }
        });
    }

    function endGame() {
        gameFinished = true;
        const totalCorrect = userResults.filter(r => r === true).length;
        const percentage = Math.round((totalCorrect / questions.length) * 100);
        let message = "";
        if (percentage >= 90) message = "🏆 ¡SUPER MARIO SABIO! Conoces todos los mitos. ¡El faro brilla con fuerza!";
        else if (percentage >= 70) message = "⭐ ¡BUEN TRABAJO! Casi un experto. Repasa los detalles para dominarlos.";
        else message = "🍄 ¡Ánimo! Cada pregunta te enseña algo nuevo. ¡Juega de nuevo para mejorar!";

        let resumen = `<div style="background:#fff0cf; border-radius:2rem; padding:1.5rem; text-align:center;">`;
        resumen += `<div style="font-size:3rem;">🏁</div>`;
        resumen += `<h2>¡Aventura completada!</h2>`;
        resumen += `<div style="font-size:2rem;">⭐ ${totalCorrect} / ${questions.length}</div>`;
        resumen += `<div>🎯 Precisión: ${percentage}%</div>`;
        resumen += `<p>${message}</p>`;
        resumen += `<button id="restartGameBtn" style="background:#c96f1e; border:none; padding:0.7rem; border-radius:2rem; font-weight:bold; cursor:pointer;">🔄 JUGAR DE NUEVO</button>`;
        resumen += `<div style="margin-top:1rem; font-size:0.7rem;">📊 Datos reales de la encuesta: Participación 100% · Engagement 91% · ¡Tu voz importa!</div>`;
        resumen += `</div>`;

        questionModal.innerHTML = resumen;
        questionModal.style.display = 'block';
        advanceBtn.disabled = true;

        const restartBtn = document.getElementById('restartGameBtn');
        if (restartBtn) {
            restartBtn.addEventListener('click', () => location.reload());
        }
    }

    // Evento del botón avanzar (inicia pregunta)
    advanceBtn.addEventListener('click', () => {
        if (waitingForNext) return;
        if (gameFinished) return;
        if (currentStep >= questions.length) {
            endGame();
            return;
        }
        if (!answered && questionModal.style.display !== 'block') {
            // mostrar pregunta
            waitingForNext = true;
            advanceBtn.disabled = true;
            showQuestion();
        }
    });

    // Inicializar
    function init() {
        currentStep = 0;
        coins = 0;
        streak = 0;
        answered = false;
        waitingForNext = false;
        userResults = [];
        gameFinished = false;
        updateStatsUI();
        advanceBtn.disabled = false;
        questionModal.style.display = 'none';
    }
    init();
</script>
</body>
</html>
