
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>ZCMC Recrutement Vision - Portail candidat</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, system-ui, sans-serif;
        }
        body {
            background: linear-gradient(145deg, #e9f0fc 0%, #d9e3f0 100%);
            min-height: 100vh;
            padding: 2rem 1rem;
        }
        .container {
            max-width: 1300px;
            margin: 0 auto;
        }
        /* Cartes et UI */
        .card {
            background: rgba(255,255,255,0.95);
            backdrop-filter: blur(2px);
            border-radius: 2rem;
            box-shadow: 0 20px 35px -12px rgba(0,0,0,0.2);
            padding: 1.8rem;
            margin-bottom: 2rem;
            transition: 0.2s;
            border: 1px solid rgba(255,255,255,0.4);
        }
        .auth-card {
            max-width: 500px;
            margin: 4rem auto;
            text-align: center;
        }
        h1 {
            font-size: 1.8rem;
            font-weight: 700;
            background: linear-gradient(135deg, #00337C, #2A6F97);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 0.5rem;
        }
        .badge-zcmc {
            background: #0B2F5C;
            color: white;
            padding: 0.25rem 1rem;
            border-radius: 40px;
            font-size: 0.8rem;
            display: inline-block;
            margin-bottom: 1rem;
        }
        .timer {
            background: #11212E;
            color: #FFD966;
            font-size: 1.8rem;
            font-weight: bold;
            font-family: monospace;
            padding: 0.5rem 1.2rem;
            border-radius: 60px;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }
        .progress-ia {
            background: #e2e8f0;
            border-radius: 40px;
            height: 10px;
            width: 100%;
            overflow: hidden;
            margin: 0.5rem 0 1rem;
        }
        .progress-fill {
            background: linear-gradient(90deg, #2A6F97, #0F4C5F);
            width: 0%;
            height: 100%;
            border-radius: 40px;
            transition: width 0.3s ease;
        }
        .nav-tabs {
            display: flex;
            gap: 0.8rem;
            flex-wrap: wrap;
            margin-bottom: 2rem;
            border-bottom: 2px solid #cbd5e1;
            padding-bottom: 0.8rem;
        }
        .tab-btn {
            background: none;
            border: none;
            font-size: 1rem;
            font-weight: 600;
            padding: 0.6rem 1.4rem;
            border-radius: 40px;
            cursor: pointer;
            transition: 0.2s;
            color: #1e293b;
        }
        .tab-btn.active {
            background: #00337C;
            color: white;
            box-shadow: 0 6px 12px -8px #00337C;
        }
        .volet {
            display: none;
            animation: fade 0.2s ease;
        }
        .volet.active-volet {
            display: block;
        }
        @keyframes fade { from { opacity: 0; } to { opacity: 1; } }
        .question-block {
            background: #f8fafc;
            border-radius: 1.5rem;
            padding: 1.2rem;
            margin-bottom: 1.5rem;
            border-left: 6px solid #2A6F97;
        }
        .question-label {
            font-weight: 700;
            margin-bottom: 0.6rem;
            color: #0f172a;
        }
        input, select, textarea {
            width: 100%;
            padding: 0.7rem;
            border-radius: 1rem;
            border: 1px solid #cbd5e1;
            background: white;
        }
        .checkbox-group {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            margin-top: 0.5rem;
        }
        .checkbox-group label {
            display: flex;
            align-items: center;
            gap: 0.4rem;
            background: white;
            padding: 0.3rem 1rem;
            border-radius: 40px;
            border: 1px solid #cbd5e1;
        }
        .rh-section {
            background: #EFF6FF;
            border-radius: 1.5rem;
            padding: 1rem;
            margin-top: 2rem;
            border: 1px dashed #2c6e9e;
        }
        button {
            background: #00337C;
            color: white;
            border: none;
            padding: 0.7rem 1.5rem;
            border-radius: 2rem;
            font-weight: bold;
            cursor: pointer;
            transition: 0.2s;
        }
        button:hover {
            background: #001f4f;
            transform: scale(0.98);
        }
        .flex-end {
            display: flex;
            justify-content: flex-end;
            gap: 1rem;
            margin-top: 1rem;
        }
        .score-ai {
            background: #11212E;
            color: #BBE9FF;
            padding: 0.8rem;
            border-radius: 1.2rem;
            text-align: center;
            font-weight: bold;
            margin: 1rem 0;
        }
        footer {
            text-align: center;
            font-size: 0.7rem;
            color: #334155;
            margin-top: 2rem;
        }
        @media (max-width: 700px) {
            .card { padding: 1rem; }
            .tab-btn { padding: 0.4rem 1rem; font-size: 0.8rem; }
        }
    </style>
</head>
<body>
<div class="container" id="app">
    <!-- Écran d'authentification (privé par collaborateur) -->
    <div id="authScreen" class="auth-card card">
        <div class="badge-zcmc">ZCMC Recrutement Vision 🔒</div>
        <h1>🔐 Espace confidentiel</h1>
        <p style="margin-bottom: 1.5rem;">Chaque collaborateur possède un code unique.<br>Vos réponses restent privées et sauvegardées.</p>
        <input type="text" id="collabName" placeholder="Prénom et nom du collaborateur" style="margin-bottom: 1rem;">
        <input type="password" id="collabCode" placeholder="Code d'accès (fourni par RH)" style="margin-bottom: 1.5rem;">
        <button id="loginBtn">🔓 Accéder à mon espace</button>
        <p style="margin-top: 1rem; font-size: 0.8rem;">🔹 Le RH génère les codes (ex: ZCMC001).<br>Les données restent sur ce poste.</p>
    </div>

    <!-- Espace principal (masqué tant que non authentifié) -->
    <div id="mainSpace" style="display: none;">
        <div class="card" style="text-align: center;">
            <div class="badge-zcmc">ZCMC Recrutement Vision</div>
            <h1>📋 Évaluation intégrale 360°</h1>
            <div class="timer" id="timerDisplay">⏱️ 20:00</div>
            <div class="progress-ia"><div class="progress-fill" id="globalProgressFill"></div></div>
            <p id="aiAdvice" class="score-ai">🧠 IA Analyse : en attente de réponses...</p>
        </div>

        <!-- Navigation par volet = métiers -->
        <div class="card">
            <div class="nav-tabs" id="tabButtons">
                <button class="tab-btn active" data-volet="volet1">🎧 Conseiller Clientèle</button>
                <button class="tab-btn" data-volet="volet2">📱 Social Media Manager</button>
                <button class="tab-btn" data-volet="volet3">🎨 Graphiste / UI Motion</button>
            </div>

            <!-- VOLET 1 : Conseiller Clientèle (questionnaire détaillé) -->
            <div id="volet1" class="volet active-volet">
                <h3>🎯 Compétences & cas pratiques (Conseiller)</h3>
                <!-- Cases RH à cocher -->
                <div class="rh-section">
                    <strong>📌 Cases RH (à cocher selon validation)</strong><br>
                    <div class="checkbox-group" id="rhCases1">
                        <label><input type="checkbox" value="gestion_kpi"> Gestion des KPI (Taux satisfaction)</label>
                        <label><input type="checkbox" value="outils_crm"> Maîtrise CRM / Zendesk</label>
                        <label><input type="checkbox" value="empathie"> Empathie client avéré</label>
                        <label><input type="checkbox" value="vente_add"> Capacité upselling</label>
                        <label><input type="checkbox" value="gestion_stress"> Gestion du stress pic d'appels</label>
                        <label><input type="checkbox" value="ponctualite"> Ponctualité / Assiduité</label>
                    </div>
                </div>
                <!-- Questionnaire psychologique / clé -->
                <div class="question-block"><div class="question-label">🧠 Question 1 : Face à un client très en colère qui insulte, quelle est votre réaction ?</div><textarea rows="2" class="qtext" data-volet="1" data-qid="q1"></textarea></div>
                <div class="question-block"><div class="question-label">📊 Question 2 : Décrivez votre méthode pour prioriser plusieurs demandes urgentes.</div><textarea rows="2" class="qtext" data-volet="1" data-qid="q2"></textarea></div>
                <div class="question-block"><div class="question-label">🔍 Question 3 : Comment gérez-vous le feedback négatif d’un superviseur ?</div><textarea rows="2" class="qtext" data-volet="1" data-qid="q3"></textarea></div>
                <div class="question-block"><div class="question-label">🎯 Mise en situation : Vous avez un client qui menace de résilier. Que faites-vous en 3 étapes ?</div><textarea rows="3" class="qtext" data-volet="1" data-qid="q4"></textarea></div>
                <div class="question-block"><div class="question-label">📈 Évaluez votre aisance avec les outils digitaux (1 = faible, 5 = expert)</div><select class="qselect" data-volet="1" data-qid="q5"><option>1</option><option>2</option><option>3</option><option>4</option><option>5</option></select></div>
            </div>

            <!-- VOLET 2 : Social Media Manager -->
            <div id="volet2" class="volet">
                <h3>📱 Branding, engagement & crisis management</h3>
                <div class="rh-section">
                    <strong>📌 Cases RH (SMM)</strong><div class="checkbox-group" id="rhCases2">
                        <label><input type="checkbox" value="communaute"> Animation communauté</label>
                        <label><input type="checkbox" value="crisis"> Gestion de crise e-réputation</label>
                        <label><input type="checkbox" value="analytics"> Maîtrise Meta Business Suite</label>
                        <label><input type="checkbox" value="crea_tendance"> Création de tendances</label>
                        <label><input type="checkbox" value="reporting"> Reporting mensuel</label>
                    </div>
                </div>
                <div class="question-block"><div class="question-label">📢 Stratégie : Quel contenu viral proposeriez-vous pour ZCMC ?</div><textarea rows="2" class="qtext" data-volet="2" data-qid="q1"></textarea></div>
                <div class="question-block"><div class="question-label">⚠️ Gestion de crise : Un client insulte la marque sur X (Twitter). Réponse type ?</div><textarea rows="2" class="qtext" data-volet="2" data-qid="q2"></textarea></div>
                <div class="question-block"><div class="question-label">🧩 Outils : Citez 3 KPIs essentiels pour mesurer l'engagement.</div><textarea rows="2" class="qtext" data-volet="2" data-qid="q3"></textarea></div>
                <div class="question-block"><div class="question-label">💡 Question psychologique : Comment acceptez-vous les critiques sur une campagne que vous avez menée ?</div><textarea rows="2" class="qtext" data-volet="2" data-qid="q4"></textarea></div>
            </div>

            <!-- VOLET 3 : Graphiste / UI Motion -->
            <div id="volet3" class="volet">
                <h3>🎨 Suite Adobe, Design system & créativité</h3>
                <div class="rh-section">
                    <strong>📌 Cases RH (Design)</strong><div class="checkbox-group" id="rhCases3">
                        <label><input type="checkbox" value="photoshop"> Photoshop avancé</label>
                        <label><input type="checkbox" value="illustrator"> Illustrator / vectoriel</label>
                        <label><input type="checkbox" value="after_effects"> After Effects / motion</label>
                        <label><input type="checkbox" value="ui_ux"> Notions UI/UX</label>
                        <label><input type="checkbox" value="brief"> Respect des briefs</label>
                    </div>
                </div>
                <div class="question-block"><div class="question-label">🎬 Créativité : Décrivez votre processus de création d’une identité visuelle.</div><textarea rows="2" class="qtext" data-volet="3" data-qid="q1"></textarea></div>
                <div class="question-block"><div class="question-label">🖌️ Feedback : Comment réagissez-vous si un client rejette 3 versions successives ?</div><textarea rows="2" class="qtext" data-volet="3" data-qid="q2"></textarea></div>
                <div class="question-block"><div class="question-label">⚡ Outils : Maîtrisez-vous Figma ? Décrivez une collaboration avec un dev.</div><textarea rows="2" class="qtext" data-volet="3" data-qid="q3"></textarea></div>
                <div class="question-block"><div class="question-label">🧪 Test psychologique : Délais serrés + changement de brief 3h avant rendu. Gestion.</div><textarea rows="2" class="qtext" data-volet="3" data-qid="q4"></textarea></div>
            </div>

            <div class="flex-end">
                <button id="saveAllBtn">💾 Sauvegarder progression</button>
                <button id="exportRHBtn">📎 Exporter rapport RH (JSON)</button>
            </div>
        </div>
        <footer>🔒 Session privée – données enregistrées localement. ZCMC Recrutement Vision · IA d'aide à la décision</footer>
    </div>
</div>

<script>
    // ------------------ GESTION SESSION PRIVEE (code + stockage local dédié) ------------------
    let currentUserKey = null;      // clé unique "nom_code"
    let timerInterval = null;
    let timeSeconds = 20 * 60;      // 20 minutes
    let userData = {};              // stockage des réponses du collaborateur connecté

    // Initialisation : charger depuis localStorage pour l'utilisateur
    function loadUserData() {
        if (!currentUserKey) return;
        const raw = localStorage.getItem(`zcmc_${currentUserKey}`);
        if (raw) {
            userData = JSON.parse(raw);
        } else {
            userData = {
                rhCases: {1:[],2:[],3:[]},
                answers: {1:{},2:{},3:{}},
                lastUpdated: new Date().toISOString()
            };
        }
        // s'assurer des structures
        if (!userData.rhCases) userData.rhCases = {1:[],2:[],3:[]};
        if (!userData.answers) userData.answers = {1:{},2:{},3:{}};
        updateUIFromData();
        updateGlobalProgressAndAI();
    }

    function saveUserData() {
        if (!currentUserKey) return;
        userData.lastUpdated = new Date().toISOString();
        localStorage.setItem(`zcmc_${currentUserKey}`, JSON.stringify(userData));
    }

    // Synchroniser l'interface avec userData (cases RH, textareas, selects)
    function updateUIFromData() {
        // Restaurer cases RH volets 1,2,3
        for (let v=1; v<=3; v++) {
            const savedChecks = userData.rhCases[v] || [];
            const container = document.getElementById(`rhCases${v}`);
            if (container) {
                const checkboxes = container.querySelectorAll('input[type="checkbox"]');
                checkboxes.forEach(cb => {
                    cb.checked = savedChecks.includes(cb.value);
                });
            }
            // Restaurer les textareas et selects correspondants
            document.querySelectorAll(`.qtext[data-volet="${v}"]`).forEach(el => {
                const qid = el.getAttribute('data-qid');
                if (userData.answers[v] && userData.answers[v][qid] !== undefined) {
                    el.value = userData.answers[v][qid];
                } else { el.value = ''; }
            });
            document.querySelectorAll(`.qselect[data-volet="${v}"]`).forEach(el => {
                const qid = el.getAttribute('data-qid');
                if (userData.answers[v] && userData.answers[v][qid]) el.value = userData.answers[v][qid];
                else el.value = "3";
            });
        }
    }

    // Collecte des réponses depuis l'interface vers userData
    function collectUItoData() {
        for (let v=1; v<=3; v++) {
            // Cases RH
            const container = document.getElementById(`rhCases${v}`);
            if (container) {
                const checks = Array.from(container.querySelectorAll('input[type="checkbox"]:checked')).map(cb => cb.value);
                userData.rhCases[v] = checks;
            }
            // Questions texte
            if (!userData.answers[v]) userData.answers[v] = {};
            document.querySelectorAll(`.qtext[data-volet="${v}"]`).forEach(el => {
                const qid = el.getAttribute('data-qid');
                userData.answers[v][qid] = el.value;
            });
            document.querySelectorAll(`.qselect[data-volet="${v}"]`).forEach(el => {
                const qid = el.getAttribute('data-qid');
                userData.answers[v][qid] = el.value;
            });
        }
    }

    // IA de progression : calcule un score basé sur remplissage réponses + cases RH
    function computeAIScore() {
        let totalFill = 0;
        let maxFill = 0;
        for (let v=1; v<=3; v++) {
            const answers = userData.answers[v] || {};
            const textCount = Object.values(answers).filter(a => a && a.trim().length > 2).length;
            const totalTexts = document.querySelectorAll(`.qtext[data-volet="${v}"]`).length + document.querySelectorAll(`.qselect[data-volet="${v}"]`).length;
            totalFill += textCount;
            maxFill += totalTexts;
            // cases RH: bonus
            const nbRh = (userData.rhCases[v] || []).length;
            totalFill += nbRh * 0.8;
            maxFill += (document.querySelectorAll(`#rhCases${v} input`).length) * 0.8;
        }
        let pourcent = maxFill > 0 ? (totalFill / maxFill) * 100 : 0;
        pourcent = Math.min(100, pourcent);
        return { pourcent, advice: pourcent < 30 ? "⚠️ Questionnaire partiel – IA recommande plus de détails." : (pourcent > 75 ? "✅ Excellent niveau de détail. Profil solide recommandé." : "🟡 En bonne voie. Complétez certains volets pour expertise.") };
    }

    function updateGlobalProgressAndAI() {
        const { pourcent, advice } = computeAIScore();
        const progressFill = document.getElementById('globalProgressFill');
        if (progressFill) progressFill.style.width = pourcent + '%';
        const aiDiv = document.getElementById('aiAdvice');
        if (aiDiv) aiDiv.innerHTML = `🧠 IA Progression : ${Math.round(pourcent)}% complété<br>${advice}`;
    }

    function saveAndRefresh() {
        collectUItoData();
        saveUserData();
        updateGlobalProgressAndAI();
        alert("✅ Progression sauvegardée (privée pour ce collaborateur)");
    }

    // Timer 20 min
    function startTimer() {
        if (timerInterval) clearInterval(timerInterval);
        timerInterval = setInterval(() => {
            if (timeSeconds <= 0) {
                clearInterval(timerInterval);
                document.getElementById('timerDisplay').innerHTML = "⏱️ Temps écoulé !";
                alert("Les 20 minutes sont écoulées. Veuillez finaliser avec le RH.");
                return;
            }
            timeSeconds--;
            const mins = Math.floor(timeSeconds / 60);
            const secs = timeSeconds % 60;
            document.getElementById('timerDisplay').innerHTML = `⏱️ ${mins.toString().padStart(2,'0')}:${secs.toString().padStart(2,'0')}`;
        }, 1000);
    }

    // Export RH (rapport détaillé)
    function exportRHReport() {
        collectUItoData();
        const nomCollaborateur = currentUserKey.split('_')[0];
        const rapport = {
            collaborateur: nomCollaborateur,
            codeSession: currentUserKey,
            timestamp: new Date().toISOString(),
            scoresParVolet: {
                Conseiller: { casesRH: userData.rhCases[1], reponses_cle: userData.answers[1] },
                SocialMedia: { casesRH: userData.rhCases[2], reponses_cle: userData.answers[2] },
                Graphiste: { casesRH: userData.rhCases[3], reponses_cle: userData.answers[3] }
            },
            iaCompletion: computeAIScore().pourcent,
            recommandation_ia: computeAIScore().advice
        };
        const dataStr = JSON.stringify(rapport, null, 2);
        const blob = new Blob([dataStr], {type: "application/json"});
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = `rapport_ZCMC_${nomCollaborateur}.json`;
        a.click();
        URL.revokeObjectURL(url);
        alert("Rapport exporté pour le RH.");
    }

    // ----- Gestion authentification privée -----
    document.getElementById('loginBtn').addEventListener('click', () => {
        const name = document.getElementById('collabName').value.trim();
        const code = document.getElementById('collabCode').value.trim();
        if (!name || !code) { alert("Veuillez saisir votre nom et le code fourni par RH"); return; }
        // code simulé : n'importe quel code fonctionne pour la démo, mais peut être personnalisable : ici on exige "ZCMC"+chiffres
        if (!code.match(/^ZCMC\d{3}$/i) && code !== "RHMASTER") {
            alert("Code invalide. Format: ZCMC suivi de 3 chiffres (ex: ZCMC007). Contactez RH.");
            return;
        }
        currentUserKey = `${name}_${code}`;
        loadUserData();
        document.getElementById('authScreen').style.display = 'none';
        document.getElementById('mainSpace').style.display = 'block';
        startTimer();
        // Événements onchange pour sauvegarde auto optionnelle
        document.querySelectorAll('input, textarea, select').forEach(el => {
            el.addEventListener('change', () => { collectUItoData(); saveUserData(); updateGlobalProgressAndAI(); });
            el.addEventListener('input', () => { collectUItoData(); saveUserData(); updateGlobalProgressAndAI(); });
        });
        document.getElementById('saveAllBtn').addEventListener('click', saveAndRefresh);
        document.getElementById('exportRHBtn').addEventListener('click', exportRHReport);
        // navigation tabs
        document.querySelectorAll('.tab-btn').forEach(btn => {
            btn.addEventListener('click', (e) => {
                const voletId = btn.getAttribute('data-volet');
                document.querySelectorAll('.volet').forEach(v => v.classList.remove('active-volet'));
                document.getElementById(voletId).classList.add('active-volet');
                document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
            });
        });
    });
</script>
</body>
</html>
```
