<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AcolheEscola — Portal de Apoio ao Estudante</title>
    <style>
        /* ===================================================
           VARIÁVEIS DE CORES E ESTILOS (MODERNO / VIBRANTE)
           =================================================== */
        :root {
            --bg-body: #f8fafc;
            --bg-card: #ffffff;
            --bg-header: rgba(255, 255, 255, 0.85);
            --text-main: #0f172a;
            --text-muted: #64748b;
            --border-color: #e2e8f0;
            
            /* Gradiente Principal */
            --primary-grad: linear-gradient(135deg, #6366f1 0%, #a855f7 100%);
            --primary-color: #6366f1;
            --primary-hover: #4f46e5;
            
            --shadow-sm: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
            --shadow-lg: 0 10px 25px -5px rgba(99, 102, 241, 0.15);
        }

        body.dark-mode {
            --bg-body: #0f172a;
            --bg-card: #1e293b;
            --bg-header: rgba(30, 41, 59, 0.85);
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border-color: #334155;
            --shadow-lg: 0 10px 25px -5px rgba(0, 0, 0, 0.5);
        }

        /* Estilos Globais */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            transition: background-color 0.3s, color 0.3s, border-color 0.3s;
        }

        body {
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            background-color: var(--bg-body);
            color: var(--text-main);
            line-height: 1.6;
            padding-bottom: 60px;
        }

        /* ===================================================
           CABEÇALHO E NAVEGAÇÃO
           =================================================== */
        .header {
            position: sticky;
            top: 0;
            backdrop-filter: blur(12px);
            background-color: var(--bg-header);
            border-bottom: 1px solid var(--border-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 5%;
            z-index: 1000;
        }

        .logo {
            font-size: 1.4rem;
            font-weight: 800;
            background: var(--primary-grad);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .navbar ul {
            display: flex;
            list-style: none;
            gap: 1.5rem;
        }

        .navbar a {
            text-decoration: none;
            color: var(--text-muted);
            font-weight: 600;
            padding: 0.5rem 0.8rem;
            border-radius: 8px;
            transition: all 0.2s;
        }

        .navbar a:hover, .navbar a.active {
            color: var(--primary-color);
            background-color: rgba(99, 102, 241, 0.1);
        }

        .tools {
            display: flex;
            gap: 0.5rem;
        }

        .tools button {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            color: var(--text-main);
            padding: 0.4rem 0.7rem;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            box-shadow: var(--shadow-sm);
        }

        .tools button:hover {
            border-color: var(--primary-color);
        }

        /* ===================================================
           ESTRUTURA DE SEÇÕES E CARDS
           =================================================== */
        .container {
            max-width: 950px;
            margin: 2rem auto;
            padding: 0 1.5rem;
        }

        .tab-content {
            display: none;
            animation: fadeIn 0.4s ease-in-out;
        }

        .tab-content.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(8px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .hero {
            text-align: center;
            padding: 3rem 1.5rem;
            background: var(--primary-grad);
            color: white;
            border-radius: 20px;
            box-shadow: var(--shadow-lg);
            margin-bottom: 2.5rem;
        }

        .hero h2 { font-size: 2.2rem; margin-bottom: 0.8rem; }
        .hero p { font-size: 1.1rem; opacity: 0.95; max-width: 600px; margin: 0 auto 1.5rem auto; }

        .btn-action {
            background-color: #ffffff;
            color: var(--primary-color);
            border: none;
            padding: 0.8rem 1.6rem;
            font-size: 1rem;
            font-weight: 700;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            transition: transform 0.2s;
        }

        .btn-action:hover {
            transform: scale(1.03);
        }

        .grid-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 1.5rem;
            margin-top: 1.5rem;
        }

        .card {
            background-color: var(--bg-card);
            border: 1px solid var(--border-color);
            padding: 1.5rem;
            border-radius: 16px;
            box-shadow: var(--shadow-sm);
        }

        .card h3 { color: var(--primary-color); margin-bottom: 0.5rem; }

        /* ===================================================
           FORMULÁRIOS, QUIZ E COMPONENTES
           =================================================== */
        textarea {
            width: 100%;
            padding: 1rem;
            background: var(--bg-card);
            color: var(--text-main);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            resize: vertical;
            margin: 1rem 0;
            font-family: inherit;
        }

        .quiz-box {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 16px;
            padding: 1.5rem;
            margin-bottom: 1.2rem;
        }

        .quiz-box label {
            display: block;
            margin: 0.5rem 0;
            padding: 0.5rem;
            border-radius: 8px;
            cursor: pointer;
        }

        .quiz-box label:hover {
            background-color: rgba(99, 102, 241, 0.05);
        }

        .alert-box {
            background: rgba(99, 102, 241, 0.1);
            border-left: 4px solid var(--primary-color);
            padding: 1.2rem;
            border-radius: 8px;
            margin-top: 1.5rem;
        }

        .hidden { display: none; }

        /* Rodapé e Botão Topo */
        footer {
            text-align: center;
            padding: 2rem;
            border-top: 1px solid var(--border-color);
            color: var(--text-muted);
            margin-top: 4rem;
        }

        #btn-top {
            position: fixed;
            bottom: 25px;
            right: 25px;
            background: var(--primary-grad);
            color: white;
            border: none;
            width: 45px;
            height: 45px;
            border-radius: 50%;
            cursor: pointer;
            box-shadow: var(--shadow-lg);
            display: none;
            font-weight: bold;
        }

        /* Responsividade */
        @media (max-width: 768px) {
            .header { flex-direction: column; gap: 1rem; }
            .navbar ul { gap: 0.5rem; }
        }
    </style>
</head>
<body>

    <header class="header">
        <div class="logo">🛡️ AcolheEscola</div>
        <nav class="navbar">
            <ul>
                <li><a href="#" class="nav-link active" onclick="switchTab('inicio')">Início</a></li>
                <li><a href="#" class="nav-link" onclick="switchTab('escuta')">Portal de Escuta</a></li>
                <li><a href="#" class="nav-link" onclick="switchTab('quiz')">Quiz Interativo</a></li>
                <li><a href="#" class="nav-link" onclick="switchTab('referencias')">Referências</a></li>
            </ul>
        </nav>
        <div class="tools">
            <button id="btn-theme" title="Modo Escuro/Claro">🌙</button>
            <button id="btn-font-inc" title="Aumentar Fonte">A+</button>
            <button id="btn-font-dec" title="Diminuir Fonte">A-</button>
        </div>
    </header>

    <main class="container">

        <section id="inicio" class="tab-content active">
            <div class="hero">
                <h2>Bem-vindo ao Portal de Apoio ao Estudante</h2>
                <p>Aqui você encontrará informações, orientações e apoio sobre situações vivenciadas no ambiente escolar. Você não está sozinho!</p>
                <button class="btn-action" onclick="switchTab('escuta')">Precisa conversar? Acesse a Escuta</button>
            </div>

            <h2>Entendendo o Bullying</h2>
            <p style="color: var(--text-muted);">O bullying envolve comportamentos agressivos, intencionais e repetitivos sem motivação evidente, provocando dor e sofrimento físico ou emocional.</p>
            
            <div class="grid-cards">
                <div class="card">
                    <h3>💬 Verbal</h3>
                    <p>Apelidos pejorativos, xingamentos, ofensas e piadas de mau gosto recorrentes.</p>
                </div>
                <div class="card">
                    <h3>🤝 Relacional</h3>
                    <p>Isolamento forçado, espalhar boatos, ignorar ou excluir o colega socialmente.</p>
                </div>
                <div class="card">
                    <h3>🛑 Físico</h3>
                    <p>Empurrões, agressões físicas, intimidação corporal ou danos a pertences pessoais.</p>
                </div>
            </div>
        </section>

        <section id="escuta" class="tab-content">
            <h2>Espaço de Escuta Simulada</h2>
            <p style="color: var(--text-muted);">Escreva o que está sentindo. Este é um ambiente seguro de simulação e nenhum dado será salvo.</p>

            <form id="form-escuta">
                <textarea id="desabafo" rows="5" placeholder="Sinta-se à vontade para desabafar aqui..." required></textarea>
                <button type="submit" class="btn-action" style="background: var(--primary-grad); color: white;">Enviar Desabafo</button>
            </form>

            <div id="mensagem-acolhimento" class="alert-box hidden"></div>

            <div style="margin-top: 3rem;">
                <h3>Onde buscar ajuda real?</h3>
                <div class="grid-cards">
                    <div class="card">
                        <h3>🏫 Na Escola</h3>
                        <p>Procure orientação com um professor, pedagogo ou com a direção.</p>
                    </div>
                    <div class="card">
                        <h3>📞 Canais Oficiais</h3>
                        <p><strong>Disque 100</strong> (Direitos Humanos)<br><strong>Disque 188</strong> (CVV - Apoio Emocional)</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="quiz" class="tab-content">
            <h2>Quiz: Teste seus Conhecimentos</h2>
            <p style="color: var(--text-muted); margin-bottom: 1.5rem;">Responda às perguntas abaixo sobre atitudes de respeito e prevenção ao bullying.</p>

            <form id="quiz-form">
                <div class="quiz-box">
                    <p><strong>1. Dar apelidos ofensivos repetidamente a um colega é:</strong></p>
                    <label><input type="radio" name="q1" value="a"> Apenas uma brincadeira comum</label>
                    <label><input type="radio" name="q1" value="b"> Bullying verbal</label>
                    <label><input type="radio" name="q1" value="c"> Uma demonstração de carinho</label>
                </div>

                <div class="quiz-box">
                    <p><strong>2. O que fazer ao presenciar um colega sendo intimidado?</strong></p>
                    <label><input type="radio" name="q2" value="a"> Filmar com o celular e postar</label>
                    <label><input type="radio" name="q2" value="b"> Ignorar para não virar o próximo alvo</label>
                    <label><input type="radio" name="q2" value="c"> Buscar ajuda de um professor ou adulto de confiança</label>
                </div>

                <div class="quiz-box">
                    <p><strong>3. Excluir propositalmente um estudante dos grupos é considerado:</strong></p>
                    <label><input type="radio" name="q3" value="a"> Bullying relacional/social</label>
                    <label><input type="radio" name="q3" value="b"> Algo normal que todo mundo faz</label>
                    <label><input type="radio" name="q3" value="c"> Apenas um mal-entendido</label>
                </div>

                <div class="quiz-box">
                    <p><strong>4. Qual atitude estimula um ambiente escolar respeitoso?</strong></p>
                    <label><input type="radio" name="q4" value="a"> Ouvir a opinião do outro com empatia</label>
                    <label><input type="radio" name="q4" value="b"> Rir quando alguém comete um erro em sala</label>
                    <label><input type="radio" name="q4" value="c"> Inventar histórias sobre pessoas que não gosta</label>
                </div>

                <div class="quiz-box">
                    <p><strong>5. Se você estiver passando por bullying, o ideal é:</strong></p>
                    <label><input type="radio" name="q5" value="a"> Sofrer em silêncio até passar</label>
                    <label><input type="radio" name="q5" value="b"> Conversar com um responsável ou profissional</label>
                    <label><input type="radio" name="q5" value="c"> Responder com agressão física</label>
                </div>

                <button type="button" onclick="calcularQuiz()" class="btn-action" style="background: var(--primary-grad); color: white;">Finalizar Quiz</button>
            </form>

            <div id="resultado-quiz" class="alert-box hidden"></div>
        </section>

        <section id="referencias" class="tab-content">
            <h2>Fontes e Referências</h2>
            <p style="color: var(--text-muted); margin-bottom: 1.5rem;">Conteúdo elaborado com base nas orientações das seguintes instituições oficiais:</p>

            <div class="grid-cards">
                <div class="card">
                    <h3>Ministério da Educação (MEC)</h3>
                    <p>Programas de prevenção e diretrizes de combate à violência escolar.</p>
                </div>
                <div class="card">
                    <h3>SaferNet Brasil</h3>
                    <p>Guias educativos de segurança na internet e combate ao cyberbullying.</p>
                </div>
                <div class="card">
                    <h3>CVV — Centro de Valorização da Vida</h3>
                    <p>Atendimento voluntário e gratuito de apoio emocional (Disque 188).</p>
                </div>
            </div>
        </section>

    </main>

    <button id="btn-top" onclick="scrollToTop()">↑</button>

    <footer>
        <p>&copy; Portal de Apoio ao Estudante — Projeto Educativo Individual</p>
    </footer>

    <script>
        // Navegação entre Abas
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.nav-link').forEach(link => link.classList.remove('active'));
            
            document.getElementById(tabId).classList.add('active');
            
            // Marca menu ativo
            const activeLink = Array.from(document.querySelectorAll('.nav-link'))
                .find(a => a.getAttribute('onclick').includes(tabId));
            if (activeLink) activeLink.classList.add('active');

            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // Modo Escuro
        document.getElementById('btn-theme').addEventListener('click', () => {
            document.body.classList.toggle('dark-mode');
        });

        // Controle de Fonte
        let fontSize = 100;
        document.getElementById('btn-font-inc').addEventListener('click', () => {
            if (fontSize < 125) { fontSize += 5; document.body.style.fontSize = fontSize + '%'; }
        });
        document.getElementById('btn-font-dec').addEventListener('click', () => {
            if (fontSize > 85) { fontSize -= 5; document.body.style.fontSize = fontSize + '%'; }
        });

        // Botão Voltar ao Topo
        window.addEventListener('scroll', () => {
            const btnTop = document.getElementById('btn-top');
            btnTop.style.display = window.scrollY > 200 ? 'block' : 'none';
        });

        function scrollToTop() {
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // Form de Escuta Simulado
        document.getElementById('form-escuta').addEventListener('submit', (e) => {
            e.preventDefault();
            const msgBox = document.getElementById('mensagem-acolhimento');
            msgBox.classList.remove('hidden');
            msgBox.innerHTML = `
                <h3>Obrigado por compartilhar! 💙</h3>
                <p>Sua voz importa. Lembre-se de que você não precisa carregar tudo sozinho(a). Procure um adulto de confiança na escola ou em casa.</p>
                <small><em>*Esta é uma demonstração. Nenhuma informação foi salva.</em></small>
            `;
            document.getElementById('form-escuta').reset();
        });

        // Resolução do Quiz
        function calcularQuiz() {
            const gabarito = { q1: 'b', q2: 'c', q3: 'a', q4: 'a', q5: 'b' };
            let pontos = 0;
            const form = document.getElementById('quiz-form');

            for (let q in gabarito) {
                const checked = form.querySelector(`input[name="${q}"]:checked`);
                if (checked && checked.value === gabarito[q]) {
                    pontos++;
                }
            }

            const resBox = document.getElementById('resultado-quiz');
            resBox.classList.remove('hidden');
            resBox.innerHTML = `
                <h3>Resultado do Quiz</h3>
                <p>Você acertou <strong>${pontos}</strong> de 5 perguntas.</p>
                <p>${pontos === 5 ? 'Excelente! Você compreende muito bem como promover o respeito na escola! 🎉' : 'Bom trabalho! Continue aprendendo e praticando a empatia no dia a dia. 👍'}</p>
            `;
        }
    </script>
</body>
</html>