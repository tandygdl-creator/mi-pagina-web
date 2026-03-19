[temp.html](https://github.com/user-attachments/files/26121434/temp.html)
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sorteo Oficial · Mundialito Command Center</title>
    <!-- Google Fonts: estilo moderno y deportivo -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,400;14..32,600;14..32,700;14..32,800&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        body {
            background: linear-gradient(145deg, #2c0a0a 0%, #4d1212 100%); /* vino profundo */
            color: #fff4e6;
            min-height: 100vh;
            padding: 2rem 1.5rem;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .container {
            max-width: 1300px;
            width: 100%;
        }

        /* Header con brillo dorado */
        .title-section {
            text-align: center;
            margin-bottom: 1.5rem;
        }

        .title-section h1 {
            font-size: 2.8rem;
            font-weight: 800;
            letter-spacing: 2px;
            text-transform: uppercase;
            background: linear-gradient(135deg, #f9e2a1 0%, #dbb45c 50%, #f9e2a1 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 4px 15px rgba(212, 175, 55, 0.4);
            margin-bottom: 0.5rem;
        }

        .title-section p {
            color: #e6c27a;
            font-size: 1.2rem;
            font-weight: 600;
            border-bottom: 2px solid #b88b3b;
            display: inline-block;
            padding-bottom: 6px;
            margin-bottom: 1rem;
        }

        /* Barra informativa de fechas y sede */
        .info-bar {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 2rem;
            background: rgba(45, 15, 15, 0.85);
            border: 2px solid #d4af37;
            border-radius: 60px;
            padding: 1rem 2rem;
            margin: 1.5rem 0 2rem 0;
            backdrop-filter: blur(4px);
            box-shadow: 0 8px 20px rgba(0,0,0,0.6);
        }

        .info-bar span {
            font-size: 1.2rem;
            font-weight: 600;
            color: #fadf8a;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
        }

        .info-bar span strong {
            color: #ffffff;
            font-weight: 800;
            background: #a0522d;
            padding: 0.2rem 1rem;
            border-radius: 40px;
            letter-spacing: 0.5px;
            border: 1px solid #e4b84a;
        }

        /* tarjetas y elementos con temática copa */
        .card {
            background: rgba(45, 15, 15, 0.75);
            backdrop-filter: blur(4px);
            border: 1px solid #c9a24d;
            border-radius: 2rem;
            box-shadow: 0 20px 30px -10px rgba(0, 0, 0, 0.7), 0 0 0 2px rgba(212, 175, 55, 0.2) inset;
            padding: 1.8rem 1.5rem;
        }

        .gold-text {
            color: #f5d371;
            font-weight: 600;
            letter-spacing: 0.5px;
        }

        /* Ruleta principal */
        .roulette-panel {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-bottom: 3rem;
        }

        .wheel-display {
            background: #1f0a0a;
            border: 4px solid #d4af37;
            border-radius: 80px;
            padding: 1.2rem 3rem;
            margin-bottom: 1.8rem;
            box-shadow: 0 0 30px #e4b441;
            width: fit-content;
        }

        #spinning-name {
            font-size: 3.2rem;
            font-weight: 800;
            color: #fadf8a;
            text-shadow: 0 0 8px #ffd966;
            min-width: 360px;
            text-align: center;
            letter-spacing: 2px;
            transition: transform 0.08s ease;
        }

        .spinning-active {
            animation: pulse-gold 0.15s infinite alternate;
        }

        @keyframes pulse-gold {
            0% { text-shadow: 0 0 5px #f1c40f; transform: scale(1); }
            100% { text-shadow: 0 0 25px #f7dc6f; transform: scale(1.02); }
        }

        .button-group {
            display: flex;
            gap: 1.2rem;
            flex-wrap: wrap;
            justify-content: center;
        }

        .btn {
            background: linear-gradient(145deg, #a67c2f, #7f621d);
            border: none;
            border-radius: 60px;
            padding: 1rem 2.2rem;
            font-size: 1.3rem;
            font-weight: 700;
            color: #231f1a;
            text-transform: uppercase;
            letter-spacing: 1.5px;
            cursor: pointer;
            box-shadow: 0 8px 0 #4a3a15, 0 10px 20px rgba(0,0,0,0.3);
            transition: all 0.08s linear;
            border: 1px solid #f5d371;
        }

        .btn:hover {
            background: linear-gradient(145deg, #c79c3e, #9e7a2c);
            transform: translateY(-2px);
            box-shadow: 0 10px 0 #4a3a15, 0 15px 25px black;
        }

        .btn:active {
            transform: translateY(5px);
            box-shadow: 0 3px 0 #4a3a15, 0 8px 15px black;
        }

        .btn:disabled {
            opacity: 0.4;
            transform: translateY(5px);
            box-shadow: 0 3px 0 #4a3a15;
            pointer-events: none;
        }

        .btn-gold {
            background: linear-gradient(145deg, #e4b135, #b88927);
            box-shadow: 0 8px 0 #7a5c1e, 0 10px 20px black;
        }

        /* Grupos */
        .groups-section {
            margin: 3rem 0;
        }

        .groups-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 1.8rem;
            margin-top: 1.5rem;
        }

        .group-card {
            background: rgba(35, 12, 12, 0.9);
            border-radius: 1.8rem;
            border: 2px solid #d4af37;
            padding: 1.5rem 1rem;
            text-align: center;
            box-shadow: 0 15px 20px -8px black;
        }

        .group-title {
            font-size: 2rem;
            font-weight: 800;
            color: #f5d371;
            border-bottom: 3px solid #a98135;
            padding-bottom: 0.6rem;
            margin-bottom: 1.2rem;
        }

        .team-list {
            list-style: none;
            font-size: 1.2rem;
            font-weight: 500;
        }

        .team-list li {
            padding: 0.5rem 0;
            border-bottom: 1px dashed #b68b40;
            color: #fff0d2;
        }

        .team-list li:last-child {
            border-bottom: none;
        }

        /* partidos */
        .matches-section {
            margin: 3rem 0;
        }

        .matches-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 1.5rem;
            margin-top: 1.5rem;
        }

        .group-matches {
            background: #2d1313;
            border-radius: 1.5rem;
            padding: 1.5rem;
            border-left: 8px solid #e0b354;
        }

        .group-matches h3 {
            color: #fad571;
            font-size: 1.6rem;
            margin-bottom: 1rem;
            border-bottom: 2px solid #b49450;
            padding-bottom: 6px;
        }

        .match-item {
            background: #411d1d;
            margin: 0.7rem 0;
            padding: 0.7rem;
            border-radius: 2rem;
            font-weight: 600;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border: 1px solid #bd9b4b;
            color: #ffeec2;
        }

        .vs-badge {
            background: #d4af37;
            color: #2c0a0a;
            font-weight: 800;
            padding: 0.2rem 1rem;
            border-radius: 40px;
            font-size: 0.9rem;
        }

        /* fase final explicativa */
        .knockout-section {
            display: flex;
            flex-wrap: wrap;
            gap: 1.5rem;
            justify-content: center;
            margin-top: 3rem;
        }

        .knockout-card {
            background: #321b1b;
            border: 2px solid #e4b84a;
            border-radius: 2rem;
            padding: 1.8rem 2rem;
            flex: 1 1 200px;
            min-width: 220px;
            text-align: center;
            box-shadow: 0 15px 25px -10px #0a0000;
        }

        .knockout-card .emblem {
            font-size: 2.5rem;
            margin-bottom: 0.5rem;
        }

        .knockout-card h4 {
            color: #ecc96a;
            font-size: 1.7rem;
            margin-bottom: 0.8rem;
        }

        .knockout-card p {
            font-size: 1.2rem;
            font-weight: 600;
            line-height: 1.5;
        }

        .gold-rule {
            color: #fad248;
            font-weight: 800;
        }

        .footer-share {
            margin-top: 3rem;
            display: flex;
            justify-content: center;
        }

        #copyResultsBtn {
            background: #b68d3c;
            font-size: 1.2rem;
            padding: 0.8rem 2rem;
        }

        .counter {
            font-size: 1.2rem;
            color: #ffdb9d;
            margin-top: 0.8rem;
        }

        @media (max-width: 900px) {
            .groups-grid, .matches-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            .info-bar {
                flex-direction: column;
                align-items: center;
                gap: 1rem;
                border-radius: 40px;
            }
        }
        @media (max-width: 600px) {
            .groups-grid, .matches-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
<div class="container">
    <!-- Encabezado copa -->
    <div class="title-section">
        <h1>⚽ Sorteo Oficial ⚽</h1>
        <p>MUNDIALITO COMMAND CENTER</p>
    </div>

    <!-- 📅 NUEVA BARRA INFORMATIVA: FECHAS Y SEDE (sin afectar funcionalidad) -->
    <div class="info-bar">
        <span>📅 <strong>Fase de grupos:</strong> martes 24 al jueves 26</span>
        <span>🗓️ <strong>Semifinales y final:</strong> viernes 27</span>
        <span>📍 <strong>La nave de coches</strong></span>
    </div>

    <!-- Ruleta / tragamonedas -->
    <div class="roulette-panel card">
        <div class="wheel-display">
            <div id="spinning-name">⚡ GIRAR ⚡</div>
        </div>
        <div class="button-group">
            <button class="btn" id="spinBtn" autofocus>🎲 Girar / Sortear equipo</button>
            <button class="btn btn-gold" id="generateMatchesBtn">📅 Generar partidos</button>
            <button class="btn" id="resetBtn">⟲ Reiniciar sorteo</button>
        </div>
        <div class="counter" id="teamsLeftCounter">Equipos disponibles: 12</div>
    </div>

    <!-- Visualización de grupos -->
    <div class="groups-section">
        <h2 class="gold-text" style="font-size: 2rem; margin-bottom: 0.5rem;">🌟 GRUPOS DEL MUNDIALITO</h2>
        <div class="groups-grid" id="groupsContainer">
            <!-- se llena con JS -->
        </div>
    </div>

    <!-- Calendario de partidos (fase de grupos) -->
    <div class="matches-section">
        <h2 class="gold-text" style="font-size: 2rem; margin-bottom: 0.5rem;">⏳ CALENDARIO - FASE DE GRUPOS</h2>
        <div class="matches-grid" id="matchesContainer"></div>
    </div>

    <!-- Explicación fase final (estática con diseño de tarjetas) -->
    <div class="knockout-section">
        <div class="knockout-card">
            <div class="emblem">🏆</div>
            <h4>CLASIFICAN</h4>
            <p><span class="gold-rule">1er lugar</span> de cada grupo</p>
        </div>
        <div class="knockout-card">
            <div class="emblem">⚔️</div>
            <h4>SEMIFINAL 1</h4>
            <p>Ganador A vs <br> Ganador C</p>
        </div>
        <div class="knockout-card">
            <div class="emblem">⚔️</div>
            <h4>SEMIFINAL 2</h4>
            <p>Ganador B vs <br> Ganador D</p>
        </div>
        <div class="knockout-card">
            <div class="emblem">🏅</div>
            <h4>GRAN FINAL</h4>
            <p>Ganador S1 vs <br> Ganador S2</p>
        </div>
        <div class="knockout-card">
            <div class="emblem">🥇</div>
            <h4>¡EL CAMPEÓN</h4>
            <p>se lo lleva todo!</p>
        </div>
    </div>

    <!-- botón extra para compartir (copia resultados) -->
    <div class="footer-share">
        <button class="btn" id="copyResultsBtn">📋 Copiar resultados</button>
    </div>
</div>

<script>
    (function() {
        // ------------- LISTA ORIGINAL DE EQUIPOS -------------
        const TEAMS = [
            "JassBrina", "Maquinas de fuego", "Los Crepusculones", "Los Pumas de Pabe",
            "Los Tempos", "Los Monkiki’s", "Ultimo", "NightRaid", "Las Chivas de Jalpa",
            "Pilar Blanco FC", "Los viajeros FC", "Los pitufos de Lagos"
        ];

        // ------------- ESTADO GLOBAL -------------
        let remainingTeams = [...TEAMS];
        const groups = {
            A: [],
            B: [],
            C: [],
            D: []
        };
        let matches = [];          // array de objetos { group, team1, team2 }
        let picksCount = 0;        // 0 a 11, controla asignación secuencial a grupos
        let spinning = false;
        let spinInterval = null;
        let spinTimeout = null;

        // ------------- REFERENCIAS DOM -------------
        const spinningNameDiv = document.getElementById('spinning-name');
        const spinBtn = document.getElementById('spinBtn');
        const generateBtn = document.getElementById('generateMatchesBtn');
        const resetBtn = document.getElementById('resetBtn');
        const copyBtn = document.getElementById('copyResultsBtn');
        const teamsLeftSpan = document.getElementById('teamsLeftCounter');
        const groupsContainer = document.getElementById('groupsContainer');
        const matchesContainer = document.getElementById('matchesContainer');

        // ------------- FUNCIONES DE RENDERIZADO -------------
        function renderGroups() {
            let html = '';
            const groupOrder = ['A', 'B', 'C', 'D'];
            groupOrder.forEach(letter => {
                const teamList = groups[letter].map(t => `<li>${t}</li>`).join('');
                html += `
                    <div class="group-card">
                        <div class="group-title">GRUPO ${letter}</div>
                        <ul class="team-list">
                            ${teamList || '<li style="opacity:0.5;">— esperando —</li>'}
                        </ul>
                    </div>
                `;
            });
            groupsContainer.innerHTML = html;
        }

        function renderMatches() {
            if (!matches || matches.length === 0) {
                matchesContainer.innerHTML = '<div style="grid-column:1/-1; text-align:center; padding:2rem; background:#2f1515; border-radius:3rem;">⚡ Genera los partidos para ver el calendario ⚡</div>';
                return;
            }

            // agrupar por grupo
            const matchesByGroup = { A: [], B: [], C: [] , D: [] };
            matches.forEach(m => {
                if (matchesByGroup[m.group]) matchesByGroup[m.group].push(m);
            });

            let html = '';
            for (let letter of ['A','B','C','D']) {
                const groupMatches = matchesByGroup[letter] || [];
                let matchesList = '';
                if (groupMatches.length > 0) {
                    groupMatches.forEach(m => {
                        matchesList += `
                            <div class="match-item">
                                <span>${m.team1}</span>
                                <span class="vs-badge">VS</span>
                                <span>${m.team2}</span>
                            </div>
                        `;
                    });
                } else {
                    matchesList = '<p style="opacity:0.6; text-align:center;">⏳ partidos por definir</p>';
                }

                html += `
                    <div class="group-matches">
                        <h3>GRUPO ${letter}</h3>
                        ${matchesList}
                    </div>
                `;
            }
            matchesContainer.innerHTML = html;
        }

        function updateTeamsCounter() {
            teamsLeftSpan.innerText = `Equipos disponibles: ${remainingTeams.length}`;
        }

        // ------------- LÓGICA DE ASIGNACIÓN POR GRUPO -------------
        function assignTeamToGroup(team) {
            // determinar grupo según picksCount (0-2 => A, 3-5 => B, 6-8 => C, 9-11 => D)
            if (picksCount < 3) groups.A.push(team);
            else if (picksCount < 6) groups.B.push(team);
            else if (picksCount < 9) groups.C.push(team);
            else groups.D.push(team);
            picksCount++;
        }

        // ------------- GENERAR PARTIDOS (round robin grupo de 3) -------------
        function generateMatchesFromGroups() {
            // sólo generar si los 4 grupos tienen 3 equipos
            if (groups.A.length !== 3 || groups.B.length !== 3 || groups.C.length !== 3 || groups.D.length !== 3) {
                alert("Aún no están todos los grupos completos (faltan " + (12 - picksCount) + " equipos).");
                return false;
            }

            matches = [];
            const groupLetters = ['A','B','C','D'];
            groupLetters.forEach(letter => {
                const groupTeams = groups[letter];
                // round robin: 3 equipos -> 3 partidos (1v2, 1v3, 2v3)
                matches.push({ group: letter, team1: groupTeams[0], team2: groupTeams[1] });
                matches.push({ group: letter, team1: groupTeams[0], team2: groupTeams[2] });
                matches.push({ group: letter, team1: groupTeams[1], team2: groupTeams[2] });
            });
            renderMatches();
            return true;
        }

        // ------------- RESET COMPLETO -------------
        function fullReset() {
            // cancelar cualquier spin en curso
            if (spinInterval) clearInterval(spinInterval);
            if (spinTimeout) clearTimeout(spinTimeout);
            spinning = false;
            spinBtn.disabled = false;
            spinningNameDiv.classList.remove('spinning-active');

            remainingTeams = [...TEAMS];
            groups.A = [];
            groups.B = [];
            groups.C = [];
            groups.D = [];
            matches = [];
            picksCount = 0;

            spinningNameDiv.innerText = '⚡ GIRAR ⚡';
            renderGroups();
            renderMatches();
            updateTeamsCounter();
        }

        // ------------- SELECCIONAR EQUIPO ALEATORIO (sin eliminación) -------------
        function getRandomRemainingTeam() {
            if (remainingTeams.length === 0) return null;
            const randomIndex = Math.floor(Math.random() * remainingTeams.length);
            return remainingTeams[randomIndex];
        }

        // ------------- ACCIÓN DE GIRAR (SORTEO CON ANIMACIÓN) -------------
        function startSpin() {
            if (spinning) return;
            if (remainingTeams.length === 0) {
                alert("¡Ya se sortearon todos los equipos!");
                return;
            }

            spinning = true;
            spinBtn.disabled = true;
            spinningNameDiv.classList.add('spinning-active');

            // cambio rápido de nombres
            spinInterval = setInterval(() => {
                const randomTeam = getRandomRemainingTeam();
                if (randomTeam) spinningNameDiv.innerText = randomTeam;
            }, 80);

            // duración aleatoria entre 800ms y 2000ms
            const spinDuration = 800 + Math.floor(Math.random() * 1300);
            spinTimeout = setTimeout(() => {
                // detener intervalo
                if (spinInterval) clearInterval(spinInterval);
                spinInterval = null;
                spinningNameDiv.classList.remove('spinning-active');

                // elegir equipo final (aleatorio de los que quedan)
                if (remainingTeams.length > 0) {
                    const randomIndex = Math.floor(Math.random() * remainingTeams.length);
                    const selectedTeam = remainingTeams[randomIndex];

                    // eliminar de remainingTeams
                    remainingTeams.splice(randomIndex, 1);
                    // asignar a grupo
                    assignTeamToGroup(selectedTeam);
                    // mostrar el seleccionado
                    spinningNameDiv.innerText = selectedTeam;

                    // refrescar grupos y contador
                    renderGroups();
                    updateTeamsCounter();

                    // si ya no quedan equipos, deshabilitar botón
                    if (remainingTeams.length === 0) {
                        spinBtn.disabled = true;
                    } else {
                        spinBtn.disabled = false;
                    }
                } else {
                    spinningNameDiv.innerText = '¡COMPLETO!';
                    spinBtn.disabled = true;
                }

                spinning = false;
                // reactivar botón (si quedan equipos)
                if (remainingTeams.length > 0) {
                    spinBtn.disabled = false;
                }

                // limpiar timeout
                if (spinTimeout) clearTimeout(spinTimeout);
                spinTimeout = null;
            }, spinDuration);
        }

        // ------------- COPIAR RESULTADOS AL PORTAPAPELES -------------
        function copyResultsToClipboard() {
            let text = '🌟 MUNDIALITO COMMAND CENTER - RESULTADOS DEL SORTEO 🌟\n\n';
            text += '📅 Fase de grupos: martes 24 al jueves 26\n';
            text += '🗓️ Semifinales y final: viernes 27\n';
            text += '📍 Sede: La nave de coches\n\n';

            // grupos
            for (let letter of ['A','B','C','D']) {
                text += `GRUPO ${letter}: ${groups[letter].join(' · ') || 'vacío'}\n`;
            }
            text += '\n📅 PARTIDOS DE GRUPO:\n';
            if (matches.length === 0) {
                text += 'Todavía no se generaron los partidos.\n';
            } else {
                matches.forEach(m => {
                    text += `Grupo ${m.group}: ${m.team1} VS ${m.team2}\n`;
                });
            }

            text += '\n⚔️ FASE FINAL:\n';
            text += 'Clasifica 1er lugar de cada grupo.\n';
            text += 'Semifinal 1: Ganador A vs Ganador C\n';
            text += 'Semifinal 2: Ganador B vs Ganador D\n';
            text += 'Gran Final: Ganador S1 vs Ganador S2\n';
            text += '¡EL CAMPEÓN SE LO LLEVA TODO!';

            navigator.clipboard.writeText(text).then(() => {
                alert('✅ Resultados copiados al portapapeles');
            }).catch(() => {
                alert('❌ No se pudo copiar, hazlo manualmente');
            });
        }

        // ------------- EVENT LISTENERS -------------
        spinBtn.addEventListener('click', startSpin);

        generateBtn.addEventListener('click', () => {
            generateMatchesFromGroups();
        });

        resetBtn.addEventListener('click', fullReset);

        copyBtn.addEventListener('click', copyResultsToClipboard);

        // ------------- INICIALIZAR VISTA -------------
        fullReset(); // de paso renderiza todo limpio

        // adicional: si se intenta generar partidos sin grupos llenos, el propio generateMatchesFromGroups alerta
        // también bloqueamos botón girar al final
    })();
</script>
</body>
</html>
