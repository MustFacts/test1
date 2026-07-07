<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MUSTFACTS — Гайд по скаму в Discord</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Inter:wght@400;600;700;900&display=swap');

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --yellow: #FFD700;
            --yellow-dark: #B8960C;
            --black: #0a0a0a;
            --dark: #1a1a1a;
            --gray: #2a2a2a;
            --light: #e0e0e0;
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            font-family: 'Inter', sans-serif;
            background: var(--black);
            color: var(--light);
            overflow-x: hidden;
            min-height: 100vh;
        }

        /* ===== SPLASH SCREEN ===== */
        #splash {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--black);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 10000;
            transition: opacity 0.8s ease, transform 0.8s ease;
        }

        #splash.hide {
            opacity: 0;
            transform: scale(1.1);
            pointer-events: none;
        }

        .splash-logo {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 5rem;
            letter-spacing: 8px;
            margin-bottom: 20px;
            opacity: 0;
            animation: logoAppear 1s ease forwards 0.3s;
        }

        .splash-logo .must {
            color: #fff;
            text-shadow: 0 0 20px rgba(255,255,255,0.3);
        }

        .splash-logo .facts {
            color: var(--yellow);
            text-shadow: 0 0 30px rgba(255, 215, 0, 0.5);
        }

        .splash-welcome {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 2.5rem;
            color: var(--yellow);
            letter-spacing: 6px;
            opacity: 0;
            animation: welcomeAppear 1s ease forwards 1s;
        }

        .splash-subtitle {
            font-size: 1rem;
            color: #888;
            margin-top: 15px;
            opacity: 0;
            animation: subtitleAppear 1s ease forwards 1.5s;
        }

        .splash-loader {
            margin-top: 40px;
            width: 200px;
            height: 3px;
            background: var(--gray);
            border-radius: 3px;
            overflow: hidden;
            opacity: 0;
            animation: loaderAppear 0.5s ease forwards 2s;
        }

        .splash-loader-bar {
            height: 100%;
            width: 0%;
            background: linear-gradient(90deg, var(--yellow), #fff, var(--yellow));
            border-radius: 3px;
            animation: loadBar 1.5s ease forwards 2s;
        }

        @keyframes logoAppear {
            0% { opacity: 0; transform: translateY(-30px) scale(0.8); }
            100% { opacity: 1; transform: translateY(0) scale(1); }
        }

        @keyframes welcomeAppear {
            0% { opacity: 0; transform: translateY(20px); }
            100% { opacity: 1; transform: translateY(0); }
        }

        @keyframes subtitleAppear {
            0% { opacity: 0; }
            100% { opacity: 1; }
        }

        @keyframes loaderAppear {
            0% { opacity: 0; }
            100% { opacity: 1; }
        }

        @keyframes loadBar {
            0% { width: 0%; }
            100% { width: 100%; }
        }

        /* ===== PARTICLES ===== */
        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
            overflow: hidden;
        }

        .particle {
            position: absolute;
            width: 3px;
            height: 3px;
            background: var(--yellow);
            border-radius: 50%;
            opacity: 0;
            animation: floatParticle 6s infinite;
        }

        @keyframes floatParticle {
            0% { opacity: 0; transform: translateY(100vh) scale(0); }
            50% { opacity: 0.6; }
            100% { opacity: 0; transform: translateY(-100px) scale(1); }
        }

        /* ===== HEADER ===== */
        header {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            padding: 15px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 1000;
            background: linear-gradient(180deg, rgba(0,0,0,0.9) 0%, transparent 100%);
        }

        .header-left {
            display: flex;
            align-items: center;
            gap: 20px;
        }

        .home-btn {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            border: 2px solid var(--yellow);
            display: flex;
            align-items: center;
            justify-content: center;
            background: var(--dark);
            box-shadow: 0 0 15px rgba(255, 215, 0, 0.3);
            animation: iconPulse 3s ease infinite;
            cursor: pointer;
            transition: transform 0.3s ease;
        }

        .home-btn:hover {
            transform: scale(1.1);
        }

        .home-btn svg {
            width: 24px;
            height: 24px;
            fill: var(--yellow);
        }

        .header-logo {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 1.8rem;
            letter-spacing: 4px;
        }

        .header-logo .must { color: #fff; }
        .header-logo .facts { color: var(--yellow); }

        .menu-btn {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            border: 2px solid var(--yellow);
            display: flex;
            align-items: center;
            justify-content: center;
            background: var(--dark);
            box-shadow: 0 0 15px rgba(255, 215, 0, 0.3);
            cursor: pointer;
            transition: transform 0.3s ease;
        }

        .menu-btn:hover {
            transform: scale(1.1);
        }

        .menu-btn svg {
            width: 24px;
            height: 24px;
            stroke: var(--yellow);
            stroke-width: 2.5;
            fill: none;
        }

        @keyframes iconPulse {
            0%, 100% { box-shadow: 0 0 15px rgba(255, 215, 0, 0.3); }
            50% { box-shadow: 0 0 25px rgba(255, 215, 0, 0.6); }
        }

        /* ===== SIDE MENU ===== */
        .side-menu-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(5px);
            z-index: 1500;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.4s ease;
        }

        .side-menu-overlay.active {
            opacity: 1;
            pointer-events: all;
        }

        .side-menu {
            position: fixed;
            top: 0;
            right: -400px;
            width: 400px;
            max-width: 90vw;
            height: 100%;
            background: var(--dark);
            border-left: 2px solid var(--yellow);
            z-index: 1600;
            padding: 80px 30px 30px;
            overflow-y: auto;
            transition: right 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            box-shadow: -10px 0 30px rgba(0,0,0,0.5);
        }

        .side-menu.active {
            right: 0;
        }

        .menu-close {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--gray);
            border: none;
            color: #fff;
            font-size: 1.2rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
        }

        .menu-close:hover {
            background: #E74C3C;
            transform: rotate(90deg);
        }

        .menu-title {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 2rem;
            color: var(--yellow);
            letter-spacing: 3px;
            margin-bottom: 30px;
            border-bottom: 1px solid var(--gray);
            padding-bottom: 15px;
        }

        .menu-item {
            margin-bottom: 25px;
            padding: 20px;
            background: var(--black);
            border-radius: 15px;
            border: 1px solid var(--gray);
            transition: all 0.3s ease;
        }

        .menu-item:hover {
            border-color: var(--yellow);
            transform: translateX(-5px);
        }

        .menu-item h3 {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 1.3rem;
            color: var(--yellow);
            letter-spacing: 2px;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .menu-item p {
            color: #ccc;
            line-height: 1.6;
            font-size: 0.95rem;
        }

        .menu-item ul {
            list-style: none;
            margin-top: 10px;
        }

        .menu-item ul li {
            padding: 5px 0;
            color: #aaa;
            font-size: 0.9rem;
            position: relative;
            padding-left: 20px;
        }

        .menu-item ul li::before {
            content: '•';
            color: var(--yellow);
            position: absolute;
            left: 0;
        }

        .highlight-link {
            color: var(--yellow);
            font-weight: 600;
            text-decoration: none;
            border-bottom: 1px dashed var(--yellow);
        }

        .highlight-link:hover {
            border-bottom-style: solid;
        }

        /* ===== MAIN CONTENT ===== */
        #main-content {
            opacity: 0;
            transition: opacity 1s ease;
            position: relative;
            z-index: 2;
        }

        #main-content.show {
            opacity: 1;
        }

        /* ===== HOME SECTION ===== */
        .home-section {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 120px 20px 60px;
            text-align: center;
        }

        .home-section h1 {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 4rem;
            letter-spacing: 6px;
            margin-bottom: 20px;
        }

        .home-section h1 .highlight {
            color: var(--yellow);
        }

        .home-section p {
            font-size: 1.2rem;
            color: #999;
            max-width: 700px;
            margin: 0 auto 30px;
            line-height: 1.8;
        }

        .scroll-indicator {
            margin-top: 60px;
            animation: bounce 2s infinite;
        }

        .scroll-indicator svg {
            width: 40px;
            height: 40px;
            fill: var(--yellow);
            opacity: 0.6;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-20px); }
            60% { transform: translateY(-10px); }
        }

        /* ===== FACTS SECTION ===== */
        .facts-section {
            padding: 80px 30px;
            max-width: 1200px;
            margin: 0 auto;
        }

        .section-title {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 2.5rem;
            color: var(--yellow);
            letter-spacing: 4px;
            text-align: center;
            margin-bottom: 50px;
        }

        .facts-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 30px;
        }

        .fact-card {
            background: var(--dark);
            border-radius: 20px;
            padding: 30px;
            border: 2px solid var(--gray);
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .fact-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at center, rgba(255,215,0,0.1) 0%, transparent 70%);
            opacity: 0;
            transition: opacity 0.4s ease;
        }

        .fact-card:hover {
            transform: translateY(-8px) scale(1.02);
            border-color: var(--yellow);
            box-shadow: 0 20px 40px rgba(255, 215, 0, 0.15);
        }

        .fact-card:hover::before {
            opacity: 1;
        }

        .fact-card:active {
            transform: scale(0.95);
        }

        .fact-number {
            position: absolute;
            top: 15px;
            right: 20px;
            font-family: 'Bebas Neue', sans-serif;
            font-size: 3rem;
            color: var(--yellow);
            opacity: 0.2;
        }

        .fact-icon {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 20px;
            font-size: 1.8rem;
        }

        .fact-icon.nitro { background: linear-gradient(135deg, #5865F2, #7B68EE); }
        .fact-icon.giveaway { background: linear-gradient(135deg, #FF6B6B, #FF8E53); }
        .fact-icon.impersonation { background: linear-gradient(135deg, #E74C3C, #C0392B); }
        .fact-icon.middleman { background: linear-gradient(135deg, #F39C12, #E67E22); }
        .fact-icon.malware { background: linear-gradient(135deg, #8E44AD, #9B59B6); }
        .fact-icon.oauth { background: linear-gradient(135deg, #1ABC9C, #16A085); }
        .fact-icon.buy { background: linear-gradient(135deg, #FFD700, #FFA500); }
        .fact-icon.age { background: linear-gradient(135deg, #9B59B6, #8E44AD); }
        .fact-icon.security { background: linear-gradient(135deg, #2ECC71, #27AE60); }
        .fact-icon.voice { background: linear-gradient(135deg, #3498DB, #2980B9); }
        .fact-icon.boost { background: linear-gradient(135deg, #E91E63, #C2185B); }
        .fact-icon.tags { background: linear-gradient(135deg, #00BCD4, #0097A7); }

        .fact-title {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 1.5rem;
            letter-spacing: 3px;
            margin-bottom: 15px;
            position: relative;
            z-index: 1;
        }

        .fact-desc {
            color: #aaa;
            line-height: 1.6;
            font-size: 0.95rem;
            position: relative;
            z-index: 1;
        }

        /* ===== MODAL ===== */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.85);
            backdrop-filter: blur(10px);
            z-index: 5000;
            display: flex;
            align-items: center;
            justify-content: center;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.4s ease;
        }

        .modal-overlay.active {
            opacity: 1;
            pointer-events: all;
        }

        .modal {
            background: var(--dark);
            border-radius: 25px;
            padding: 40px;
            max-width: 650px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
            border: 2px solid var(--yellow);
            transform: scale(0.7) translateY(50px);
            transition: transform 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            position: relative;
        }

        .modal-overlay.active .modal {
            transform: scale(1) translateY(0);
        }

        .modal-close {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--gray);
            border: none;
            color: #fff;
            font-size: 1.2rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
        }

        .modal-close:hover {
            background: #E74C3C;
            transform: rotate(90deg);
        }

        .modal-header {
            display: flex;
            align-items: center;
            gap: 20px;
            margin-bottom: 30px;
        }

        .modal-icon {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            flex-shrink: 0;
        }

        .modal-title {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 2rem;
            letter-spacing: 3px;
        }

        .modal-body h3 {
            color: var(--yellow);
            font-size: 1.1rem;
            margin: 25px 0 12px;
            font-family: 'Bebas Neue', sans-serif;
            letter-spacing: 2px;
        }

        .modal-body p {
            color: #ccc;
            line-height: 1.7;
            font-size: 0.95rem;
        }

        .modal-body ul {
            list-style: none;
            padding: 0;
        }

        .modal-body ul li {
            padding: 10px 0 10px 30px;
            position: relative;
            color: #ccc;
            line-height: 1.6;
            border-bottom: 1px solid var(--gray);
        }

        .modal-body ul li:last-child {
            border-bottom: none;
        }

        .modal-body ul li::before {
            content: '⚠';
            position: absolute;
            left: 0;
            top: 10px;
        }

        .modal-body .ok-box {
            background: rgba(46, 204, 113, 0.1);
            border: 1px solid #2ECC71;
            border-radius: 12px;
            padding: 15px 20px;
            margin-top: 20px;
        }

        .modal-body .ok-box p {
            color: #2ECC71;
            font-weight: 600;
        }

        /* ===== CLICK ANIMATION ===== */
        .click-ripple {
            position: fixed;
            border-radius: 50%;
            background: rgba(255, 215, 0, 0.4);
            transform: scale(0);
            animation: ripple 0.6s ease-out;
            pointer-events: none;
            z-index: 9999;
        }

        @keyframes ripple {
            to {
                transform: scale(4);
                opacity: 0;
            }
        }

        /* ===== SCROLLBAR ===== */
        ::-webkit-scrollbar {
            width: 8px;
        }

        ::-webkit-scrollbar-track {
            background: var(--black);
        }

        ::-webkit-scrollbar-thumb {
            background: var(--yellow-dark);
            border-radius: 4px;
        }

        /* ===== RESPONSIVE ===== */
        @media (max-width: 768px) {
            .splash-logo { font-size: 3rem; }
            .splash-welcome { font-size: 1.5rem; }
            .home-section h1 { font-size: 2.5rem; }
            .home-section p { font-size: 1rem; }
            .facts-grid { grid-template-columns: 1fr; }
            .modal { padding: 25px; }
            .modal-title { font-size: 1.5rem; }
            .side-menu { width: 100%; max-width: 100%; }
        }

        /* ===== FOOTER ===== */
        footer {
            text-align: center;
            padding: 40px 30px;
            color: #555;
            font-size: 0.85rem;
            border-top: 1px solid var(--gray);
            margin-top: 60px;
        }

        footer a {
            color: var(--yellow);
            text-decoration: none;
        }

        footer a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>

    <!-- PARTICLES -->
    <div class="particles" id="particles"></div>

    <!-- SPLASH SCREEN -->
    <div id="splash">
        <div class="splash-logo">
            <span class="must">MUST</span><span class="facts">FACTS</span>
        </div>
        <div class="splash-welcome">ДОБРО ПОЖАЛОВАТЬ</div>
        <div class="splash-subtitle">Гайд по распознаванию скама в Discord</div>
        <div class="splash-loader">
            <div class="splash-loader-bar"></div>
        </div>
    </div>

    <!-- HEADER -->
    <header>
        <div class="header-left">
            <div class="home-btn" onclick="scrollToHome()" title="На главную">
                <svg viewBox="0 0 24 24"><path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"/></svg>
            </div>
            <div class="header-logo">
                <span class="must">MUST</span><span class="facts">FACTS</span>
            </div>
        </div>
        <div class="menu-btn" onclick="toggleMenu()" title="Меню">
            <svg viewBox="0 0 24 24"><line x1="4" y1="6" x2="20" y2="6"></line><line x1="4" y1="12" x2="20" y2="12"></line><line x1="4" y1="18" x2="20" y2="18"></line></svg>
        </div>
    </header>

    <!-- SIDE MENU -->
    <div class="side-menu-overlay" id="menu-overlay" onclick="toggleMenu()"></div>
    <div class="side-menu" id="side-menu">
        <button class="menu-close" onclick="toggleMenu()">✕</button>
        <div class="menu-title">ДОПОЛНИТЕЛЬНЫЕ ФАКТЫ</div>
        
        <div class="menu-item">
            <h3>🇷🇺 Как купить Nitro в России (2026)</h3>
            <p>Прямая оплата картами РФ не работает. Используй проверенные площадки:</p>
            <ul>
                <li><a href="https://playerok.com" target="_blank" class="highlight-link">Playerok.com</a> — маркетплейс игровых товаров</li>
                <li><a href="https://ggsel.com" target="_blank" class="highlight-link">Ggsel.com</a> — цифровые ключи и подписки</li>
                <li><a href="https://funpay.com" target="_blank" class="highlight-link">Funpay.com</a> — биржа игровых услуг</li>
                <li>Подарочные карты Discord Gift (покупай коды, а не аккаунты!)</li>
            </ul>
            <p style="margin-top: 10px; font-size: 0.85rem; color: #888;">️ Никогда не передавай логин/пароль от своего аккаунта продавцу.</p>
        </div>

        <div class="menu-item">
            <h3>🔍 Как понять, что человек врёт про возраст</h3>
            <p>Признаки несоответствия заявленному возрасту:</p>
            <ul>
                <li>Слишком «взрослая» лексика или сленг для заявленного возраста</li>
                <li>Знание событий/мемов, которые были популярны задолго до его рождения</li>
                <li>Неспособность объяснить простые вещи, которые должен знать ровесник</li>
                <li>Противоречия в биографии (например, «учусь в 5 классе», но говорит о работе)</li>
                <li>Отказ от видеозвонков или голосовых сообщений без веской причины</li>
            </ul>
            <p style="margin-top: 10px; font-size: 0.85rem; color: #888;">💡 Помни: даже если возраст настоящий, это не гарантирует безопасность.</p>
        </div>

        <div class="menu-item">
            <h3>🛡️ Безопасность аккаунта</h3>
            <p>Базовые правила защиты:</p>
            <ul>
                <li>Включи двухфакторную аутентификацию (2FA)</li>
                <li>Не переходи по ссылкам от незнакомцев</li>
                <li>Проверяй URL перед вводом данных</li>
                <li>Используй уникальный пароль для Discord</li>
            </ul>
        </div>
    </div>

    <!-- MAIN CONTENT -->
    <div id="main-content">
        <!-- HOME SECTION -->
        <section class="home-section" id="home">
            <h1>ТЫ СЕЙЧАС В <span class="highlight">ХОМ</span></h1>
            <p>Добро пожаловать в MUSTFACTS — твой гид по безопасности в Discord.<br>
            Здесь ты узнаешь о всех типах скам-схем и как их распознать.<br>
            Листай вниз, чтобы увидеть факты.</p>
            <div class="scroll-indicator">
                <svg viewBox="0 0 24 24"><path d="M7.41 8.59L12 13.17l4.59-4.58L18 10l-6 6-6-6 1.41-1.41z"/></svg>
            </div>
        </section>

        <!-- FACTS SECTION -->
        <section class="facts-section" id="facts">
            <h2 class="section-title">ФАКТЫ О DISCORD</h2>
            
            <div class="facts-grid">
                <!-- NITRO SCAM -->
                <div class="fact-card" onclick="openModal('nitro')">
                    <div class="fact-number">01</div>
                    <div class="fact-icon nitro">🎁</div>
                    <div class="fact-title">NITRO — Фейковая раздача</div>
                    <div class="fact-desc">Ссылка на «бесплатный Nitro» ведёт на клон страницы входа Discord. Введённые данные сразу уходят мошеннику.</div>
                </div>

                <!-- GIVEAWAY -->
                <div class="fact-card" onclick="openModal('giveaway')">
                    <div class="fact-number">02</div>
                    <div class="fact-icon giveaway">🎰</div>
                    <div class="fact-title">GIVEAWAY — Розыгрыш с предоплатой</div>
                    <div class="fact-desc">Для «вывода выигрыша» просят перевести небольшую сумму — комиссию, налог, верификацию.</div>
                </div>

                <!-- IMPERSONATION -->
                <div class="fact-card" onclick="openModal('impersonation')">
                    <div class="fact-number">03</div>
                    <div class="fact-icon impersonation"></div>
                    <div class="fact-title">IMPERSONATION — ЛС «от админа»</div>
                    <div class="fact-desc">Пишут от имени модератора или «Discord Support» и просят код подтверждения.</div>
                </div>

                <!-- MIDDLEMAN -->
                <div class="fact-card" onclick="openModal('middleman')">
                    <div class="fact-number">04</div>
                    <div class="fact-icon middleman">🤝</div>
                    <div class="fact-title">MIDDLEMAN — Подставной посредник</div>
                    <div class="fact-desc">«Проверенный» посредник забирает предмет или деньги и исчезает.</div>
                </div>

                <!-- MALWARE -->
                <div class="fact-card" onclick="openModal('malware')">
                    <div class="fact-number">05</div>
                    <div class="fact-icon malware">🦠</div>
                    <div class="fact-title">MALWARE-LINK — Файл с вредоносом</div>
                    <div class="fact-desc">Под видом читов или кряков присылают файл, который крадёт токены сессии.</div>
                </div>

                <!-- OAUTH -->
                <div class="fact-card" onclick="openModal('oauth')">
                    <div class="fact-number">06</div>
                    <div class="fact-icon oauth">🔗</div>
                    <div class="fact-title">OAUTH-PHISH — Поддельная авторизация</div>
                    <div class="fact-desc">Сайт запрашивает лишние права при входе через Discord.</div>
                </div>

                <!-- BUY NITRO RUSSIA -->
                <div class="fact-card" onclick="openModal('buy')">
                    <div class="fact-number">07</div>
                    <div class="fact-icon buy">🇺</div>
                    <div class="fact-title">Как купить Nitro в России (2026)</div>
                    <div class="fact-desc">Playerok, Ggsel, Funpay — рабочие способы покупки Nitro для РФ.</div>
                </div>

                <!-- AGE CHECK -->
                <div class="fact-card" onclick="openModal('age')">
                    <div class="fact-number">08</div>
                    <div class="fact-icon age">🔍</div>
                    <div class="fact-title">Как понять, что врут про возраст</div>
                    <div class="fact-desc">Признаки несоответствия: лексика, знания, противоречия в биографии.</div>
                </div>

                <!-- SECURITY -->
                <div class="fact-card" onclick="openModal('security')">
                    <div class="fact-number">09</div>
                    <div class="fact-icon security">🛡️</div>
                    <div class="fact-title">Безопасность аккаунта</div>
                    <div class="fact-desc">2FA, уникальные пароли, проверка URL — базовые правила защиты.</div>
                </div>

                <!-- VOICE SCAM -->
                <div class="fact-card" onclick="openModal('voice')">
                    <div class="fact-number">10</div>
                    <div class="fact-icon voice">🎤</div>
                    <div class="fact-title">Голосовой скам</div>
                    <div class="fact-desc">«Зайди в голосовой канал» — там бот записывает твой голос для обхода верификации.</div>
                </div>

                <!-- BOOST SCAM -->
                <div class="fact-card" onclick="openModal('boost')">
                    <div class="fact-number">11</div>
                    <div class="fact-icon boost">⚡</div>
                    <div class="fact-title">Фейковый буст сервера</div>
                    <div class="fact-desc">«Забусти наш сервер — получишь Nitro» — после буста тебя кидают.</div>
                </div>

                <!-- TAGS SCAM -->
                <div class="fact-card" onclick="openModal('tags')">
                    <div class="fact-number">12</div>
                    <div class="fact-icon tags">🏷️</div>
                    <div class="fact-title">Скам с тегами</div>
                    <div class="fact-desc">«Отметь 10 друзей — получишь приз» — массовый спам и взлом аккаунтов.</div>
                </div>
            </div>
        </section>

        <footer>
            <p>Не публикует и не хранит личные данные — только паттерны поведения.</p>
            <p>Подозрительную активность сообщайте через <a href="https://discord.com/safety" target="_blank">Discord Trust & Safety</a></p>
            <p style="margin-top: 10px;">© 2026 MUSTFACTS</p>
        </footer>
    </div>

    <!-- MODAL -->
    <div class="modal-overlay" id="modal-overlay" onclick="closeModal(event)">
        <div class="modal" onclick="event.stopPropagation()">
            <button class="modal-close" onclick="closeModal()">✕</button>
            <div class="modal-header">
                <div class="modal-icon" id="modal-icon"></div>
                <div class="modal-title" id="modal-title"></div>
            </div>
            <div class="modal-body" id="modal-body"></div>
        </div>
    </div>

    <script>
        // ===== PARTICLES =====
        const particlesContainer = document.getElementById('particles');
        for (let i = 0; i < 30; i++) {
            const particle = document.createElement('div');
            particle.className = 'particle';
            particle.style.left = Math.random() * 100 + '%';
            particle.style.animationDelay = Math.random() * 6 + 's';
            particle.style.animationDuration = (4 + Math.random() * 4) + 's';
            particlesContainer.appendChild(particle);
        }

        // ===== SPLASH SCREEN =====
        setTimeout(() => {
            document.getElementById('splash').classList.add('hide');
            setTimeout(() => {
                document.getElementById('main-content').classList.add('show');
            }, 400);
        }, 3800);

        // ===== SCROLL TO HOME =====
        function scrollToHome() {
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // ===== CLICK RIPPLE =====
        document.addEventListener('click', (e) => {
            if (e.target.closest('.home-btn') || e.target.closest('.menu-btn') || e.target.closest('.side-menu') || e.target.closest('.modal')) return;
            const ripple = document.createElement('div');
            ripple.className = 'click-ripple';
            ripple.style.left = e.clientX - 25 + 'px';
            ripple.style.top = e.clientY - 25 + 'px';
            ripple.style.width = '50px';
            ripple.style.height = '50px';
            document.body.appendChild(ripple);
            setTimeout(() => ripple.remove(), 600);
        });

        // ===== MENU FUNCTIONS =====
        function toggleMenu() {
            const menu = document.getElementById('side-menu');
            const overlay = document.getElementById('menu-overlay');
            menu.classList.toggle('active');
            overlay.classList.toggle('active');
            
            if (menu.classList.contains('active')) {
                document.body.style.overflow = 'hidden';
            } else {
                document.body.style.overflow = '';
            }
        }

        // Close menu on Escape
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape') {
                const menu = document.getElementById('side-menu');
                if (menu.classList.contains('active')) toggleMenu();
                closeModal();
            }
        });

        // ===== MODAL DATA =====
        const modalData = {
            nitro: {
                icon: '🎁',
                iconBg: 'linear-gradient(135deg, #5865F2, #7B68EE)',
                title: 'NITRO — Фейковая раздача',
                content: `
                    <h3>КАК РАБОТАЕТ СХЕМА</h3>
                    <p>Сообщение или ЛС с ссылкой на «бесплатный Nitro» ведёт на сайт-клон страницы входа Discord. Введённые логин и пароль (или токен) сразу уходят мошеннику.</p>
                    
                    <h3>ПРИЗНАКИ СКАМА</h3>
                    <ul>
                        <li>Домен похож на discord.com, но не совпадает точно (discorcl, dlscord и т.п.)</li>
                        <li>Срочность: «осталось 3 подарка», обратный отсчёт на странице</li>
                        <li>Ссылку прислал только что добавленный «друг» или взломанный знакомый</li>
                    </ul>

                    <div class="ok-box">
                        <p>Nitro активируется только через discord.com или discord.gift — открывай такие ссылки, вбивая адрес вручную, а не по клику.</p>
                    </div>
                `
            },
            giveaway: {
                icon: '🎰',
                iconBg: 'linear-gradient(135deg, #FF6B6B, #FF8E53)',
                title: 'GIVEAWAY — Розыгрыш с предоплатой',
                content: `
                    <h3>КАК РАБОТАЕТ СХЕМА</h3>
                    <p>Канал якобы разыгрывает крупный приз (скины, крипту, подписку), но для «участия» или «вывода выигрыша» просят сначала перевести небольшую сумму — комиссию, налог, верификацию.</p>
                    
                    <h3>ПРИЗНАКИ СКАМА</h3>
                    <ul>
                        <li>Победитель объявляется подозрительно быстро после старта</li>
                        <li>Оплата принимается только в крипте или через подарочные карты</li>
                        <li>Организатор — новый аккаунт без истории на сервере</li>
                    </ul>

                    <div class="ok-box">
                        <p>Ни одна легитимная раздача не требует денег для получения приза. Просьба оплаты — сама по себе стоп-сигнал.</p>
                    </div>
                `
            },
            impersonation: {
                icon: '🎭',
                iconBg: 'linear-gradient(135deg, #E74C3C, #C0392B)',
                title: 'IMPERSONATION — ЛС «от админа»',
                content: `
                    <h3>КАК РАБОТАЕТ СХЕМА</h3>
                    <p>В личку пишет аккаунт с ником и аватаром модератора или «Discord Support» — сообщает о нарушении и просит перейти по ссылке «для апелляции» или назвать код из письма.</p>
                    
                    <h3>ПРИЗНАКИ СКАМА</h3>
                    <ul>
                        <li>Discord Support никогда не пишет первым в личные сообщения</li>
                        <li>Просьба продиктовать код подтверждения из email или SMS</li>
                        <li>Профиль без роли на сервере, хотя выглядит как «Staff»</li>
                    </ul>

                    <div class="ok-box">
                        <p>Проверяй роль отправителя на самом сервере и никогда не называй коды подтверждения — их не спрашивает ни один настоящий сотрудник.</p>
                    </div>
                `
            },
            middleman: {
                icon: '🤝',
                iconBg: 'linear-gradient(135deg, #F39C12, #E67E22)',
                title: 'MIDDLEMAN — Подставной посредник',
                content: `
                    <h3>КАК РАБОТАЕТ СХЕМА</h3>
                    <p>При обмене скинами, аккаунтами или валютой одна сторона предлагает «своего проверенного» посредника, который должен подстраховать обе стороны — но забирает предмет или деньги и исчезает.</p>
                    
                    <h3>ПРИЗНАКИ СКАМА</h3>
                    <ul>
                        <li>Посредника предложила только одна сторона сделки</li>
                        <li>У «проверенного» аккаунта нет отзывов за пределами этой сделки</li>
                        <li>Настаивает на переписке вне сервера, где нет модерации</li>
                    </ul>

                    <div class="ok-box">
                        <p>Используй посредника, которого предлагает нейтральная сторона — например, официальный escrow-бот сервера с публичной репутацией.</p>
                    </div>
                `
            },
            malware: {
                icon: '🦠',
                iconBg: 'linear-gradient(135deg, #8E44AD, #9B59B6)',
                title: 'MALWARE-LINK — Файл с вредоносом',
                content: `
                    <h3>КАК РАБОТАЕТ СХЕМА</h3>
                    <p>Под видом читов, кряков или «показать скриншот» присылают исполняемый файл. После запуска он ворует сохранённые токены сессии из браузера и Discord-клиента.</p>
                    
                    <h3>ПРИЗНАКИ СКАМА</h3>
                    <ul>
                        <li>Архив с паролом «чтобы антивирус не ругался»</li>
                        <li>.exe замаскирован под изображение (двойное расширение файла)</li>
                        <li>Просьба отключить антивирус перед запуском</li>
                    </ul>

                    <div class="ok-box">
                        <p>Просьба отключить защиту перед запуском файла — гарантированный признак вредоноса. Не открывай такие файлы вообще.</p>
                    </div>
                `
            },
            oauth: {
                icon: '',
                iconBg: 'linear-gradient(135deg, #1ABC9C, #16A085)',
                title: 'OAUTH-PHISH — Поддельная авторизация',
                content: `
                    <h3>КАК РАБОТАЕТ СХЕМА</h3>
                    <p>Сайт (например, «проверка возраста» или «бот статистики») просит «войти через Discord» и запрашивает разрешения, которые обычному сервису не нужны — вроде управления сервером или чтения сообщений.</p>
                    
                    <h3>ПРИЗНАКИ СКАМА</h3>
                    <ul>
                        <li>Список запрашиваемых прав шире, чем нужно для функции сайта</li>
                        <li>Сайт создан недавно, нет отзывов или упоминаний за пределами одного сервера</li>
                        <li>После входа сразу начинается рассылка спама от твоего имени</li>
                    </ul>

                    <div class="ok-box">
                        <p>Перед подтверждением OAuth-доступа читай список запрашиваемых прав — и отзывай подозрительные авторизации в настройках Discord → «Авторизации».</p>
                    </div>
                `
            },
            buy: {
                icon: '🇷🇺',
                iconBg: 'linear-gradient(135deg, #FFD700, #FFA500)',
                title: 'Как купить Nitro в России (2026)',
                content: `
                    <h3>ПОЧЕМУ НЕЛЬЗЯ КУПИТЬ НАПРЯМУЮ</h3>
                    <p>С 2022 года Discord приостановил приём российских карт. Прямая оплата через сайт недоступна для пользователей из РФ.</p>
                    
                    <h3>РАБОЧИЕ СПОСОБЫ</h3>
                    <ul>
                        <li><strong>Playerok.com</strong> — маркетплейс игровых товаров, много продавцов Nitro</li>
                        <li><strong>Ggsel.com</strong> — цифровые ключи и подписки, быстрая доставка</li>
                        <li><strong>Funpay.com</strong> — биржа игровых услуг, безопасные сделки</li>
                        <li>Подарочные карты Discord Gift — покупай коды на маркетплейсах</li>
                        <li>Через друга из другой страны — он покупает и дарит тебе подписку</li>
                    </ul>

                    <div class="ok-box">
                        <p>Никогда не вводи данные своей учётной записи на сторонних сайтах «покупки Nitro». Покупай только коды/гифты и активируй их вручную на discord.gift</p>
                    </div>
                `
            },
            age: {
                icon: '🔍',
                iconBg: 'linear-gradient(135deg, #9B59B6, #8E44AD)',
                title: 'Как понять, что человек врёт про возраст',
                content: `
                    <h3>ПРИЗНАКИ НЕСООТВЕТСТВИЯ</h3>
                    <p>Даже если человек кажется взрослым, это не гарантирует безопасность. Но есть признаки лжи:</p>
                    
                    <h3>ЧТО ПРОВЕРЯТЬ</h3>
                    <ul>
                        <li>Слишком «взрослая» лексика или сленг для заявленного возраста</li>
                        <li>Знание событий/мемов, которые были популярны задолго до его рождения</li>
                        <li>Неспособность объяснить простые вещи, которые должен знать ровесник</li>
                        <li>Противоречия в биографии (например, «учусь в 5 классе», но говорит о работе)</li>
                        <li>Отказ от видеозвонков или голосовых сообщений без веской причины</li>
                        <li>Слишком идеальная история без обычных подростковых проблем</li>
                    </ul>

                    <div class="ok-box">
                        <p>Помни: даже если возраст настоящий, это не гарантирует безопасность. Всегда будь осторожен при общении с незнакомцами.</p>
                    </div>
                `
            },
            security: {
                icon: '️',
                iconBg: 'linear-gradient(135deg, #2ECC71, #27AE60)',
                title: 'Безопасность аккаунта',
                content: `
                    <h3>БАЗОВЫЕ ПРАВИЛА ЗАЩИТЫ</h3>
                    <p>Эти простые правила спасут твой аккаунт от взлома:</p>
                    
                    <h3>ЧТО ДЕЛАТЬ</h3>
                    <ul>
                        <li>Включи двухфакторную аутентификацию (2FA) в настройках Discord</li>
                        <li>Не переходи по ссылкам от незнакомцев</li>
                        <li>Проверяй URL перед вводом данных — discord.com, а не discorcl.com</li>
                        <li>Используй уникальный пароль для Discord (не такой же, как на других сайтах)</li>
                        <li>Не сохраняй пароль в браузере на общественных компьютерах</li>
                        <li>Регулярно проверяй активные сессии в настройках</li>
                    </ul>

                    <div class="ok-box">
                        <p>2FA — самая важная защита. Даже если украдут пароль, без кода из приложения никто не войдёт.</p>
                    </div>
                `
            },
            voice: {
                icon: '🎤',
                iconBg: 'linear-gradient(135deg, #3498DB, #2980B9)',
                title: 'Голосовой скам',
                content: `
                    <h3>КАК РАБОТАЕТ СХЕМА</h3>
                    <p>«Зайди в голосовой канал — там розыгрыш/важная информация». Там стоит бот, который записывает твой голос.</p>
                    
                    <h3>ДЛЯ ЧЕГО ЭТО</h3>
                    <ul>
                        <li>Запись голоса для обхода голосовой верификации на других серверах</li>
                        <li>Создание deepfake-аудио для мошенничества с твоими друзьями</li>
                        <li>Сбор биометрических данных</li>
                    </ul>

                    <div class="ok-box">
                        <p>Не заходи в подозрительные голосовые каналы от незнакомцев. Если канал создан только что и там нет модераторов — это опасно.</p>
                    </div>
                `
            },
            boost: {
                icon: '⚡',
                iconBg: 'linear-gradient(135deg, #E91E63, #C2185B)',
                title: 'Фейковый буст сервера',
                content: `
                    <h3>КАК РАБОТАЕТ СХЕМА</h3>
                    <p>«Забусти наш сервер — получишь Nitro/деньги/привилегии». После буста тебя кидают или банят.</p>
                    
                    <h3>ПРИЗНАКИ СКАМА</h3>
                    <ul>
                        <li>Обещают вернуть деньги или дать Nitro после буста</li>
                        <li>Сервер создан недавно, мало участников</li>
                        <li>Нет официальной верификации сервера</li>
                        <li>Давят на срочность: «только сегодня», «последние места»</li>
                    </ul>

                    <div class="ok-box">
                        <p>Буст — это пожертвование серверу. Никто не обязан тебе ничего возвращать. Не верь обещаниям «вернуть деньги».</p>
                    </div>
                `
            },
            tags: {
                icon: '🏷️',
                iconBg: 'linear-gradient(135deg, #00BCD4, #0097A7)',
                title: 'Скам с тегами',
                content: `
                    <h3>КАК РАБОТАЕТ СХЕМА</h3>
                    <p>«Отметь 10 друзей — получишь Nitro/приз». Ты массово тегаешь людей, создаёшь спам, а приз не получаешь.</p>
                    
                    <h3>ЧЕМ ЭТО ОПАСНО</h3>
                    <ul>
                        <li>Твой аккаунт могут заблокировать за спам</li>
                        <li>Друзья получат уведомления от твоего имени</li>
                        <li>Если аккаунт взломан — так распространяют вирусы</li>
                        <li>Массовые упоминания = нарушение правил Discord</li>
                    </ul>

                    <div class="ok-box">
                        <p>Ни одна легитимная раздача не требует массового упоминания друзей. Это всегда спам или скам.</p>
                    </div>
                `
            }
        };

        // ===== MODAL FUNCTIONS =====
        function openModal(type) {
            const data = modalData[type];
            if (!data) return;

            document.getElementById('modal-icon').textContent = data.icon;
            document.getElementById('modal-icon').style.background = data.iconBg;
            document.getElementById('modal-title').textContent = data.title;
            document.getElementById('modal-body').innerHTML = data.content;

            document.getElementById('modal-overlay').classList.add('active');
            document.body.style.overflow = 'hidden';
        }

        function closeModal(e) {
            if (e && e.target !== e.currentTarget && !e.target.classList.contains('modal-close')) return;
            document.getElementById('modal-overlay').classList.remove('active');
            document.body.style.overflow = '';
        }
    </script>
</body>
</html>
