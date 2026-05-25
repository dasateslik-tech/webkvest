<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>LEGO Квест: Тайны Google | Множества и поиск</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,400;14..32,600;14..32,800&family=Fredoka+One&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(145deg, #c0e0ff 0%, #ffe0b5 100%);
            font-family: 'Inter', sans-serif;
            color: #2c1a0e;
            padding: 20px;
            min-height: 100vh;
        }

        .container {
            max-width: 1300px;
            margin: 0 auto;
            position: relative;
            z-index: 2;
        }

        .lego-header {
            background-color: #cc0f2b;
            padding: 20px 30px;
            border-radius: 50px 50px 30px 30px;
            box-shadow: 0 15px 0 #7d0a1c, 0 10px 20px rgba(0,0,0,0.2);
            text-align: center;
            margin-bottom: 30px;
            border: 2px solid #ffcd3c;
        }
        .lego-header h1 {
            font-family: 'Fredoka One', cursive;
            font-size: 2.6rem;
            color: #ffea80;
            text-shadow: 3px 3px 0 #a0001c;
            letter-spacing: 2px;
        }
        .lego-header h1 span {
            background: #ffcd3c;
            color: #cc0f2b;
            padding: 0 15px;
            border-radius: 40px;
            display: inline-block;
            margin: 0 5px;
            box-shadow: inset 0 -2px 0 #b47c00;
        }
        .lego-sub {
            background: #ffcd3c;
            display: inline-block;
            padding: 8px 24px;
            border-radius: 40px;
            font-weight: 800;
            font-size: 1.2rem;
            color: #2c1a0e;
            margin-top: 12px;
            box-shadow: 0 4px 0 #b47c00;
        }

        .story-brick {
            background: #f0f0e0;
            border-radius: 40px;
            padding: 25px;
            margin: 20px 0 35px;
            border: 3px solid #ffb347;
            box-shadow: 12px 12px 0 #c97e2a;
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            align-items: center;
        }
        .story-text {
            flex: 2;
        }
        .story-text p {
            font-size: 1.13rem;
            line-height: 1.45;
            margin-bottom: 12px;
        }
        .lego-illustration {
            flex: 1;
            background: #e3c47e;
            border-radius: 30px;
            padding: 15px;
            text-align: center;
            font-size: 4rem;
            box-shadow: inset 0 0 0 3px white, 0 8px 0 #b47c00;
        }
        .lego-illustration img {
            max-width: 100px;
            filter: drop-shadow(2px 4px 6px rgba(0,0,0,0.2));
        }

        .lego-baseplate {
            background: url('https://i.ibb.co/MDj3q34m/image.png');
            background-size: cover;
            background-position: center;
            border-radius: 48px;
            padding: 30px 20px;
            margin: 20px 0 35px;
            box-shadow: 0 18px 0 #8b5a2b, inset 0 0 0 4px #ffecb3, inset 0 0 0 8px #c29a6b;
            position: relative;
        }
        .lego-baseplate::before {
            content: "";
            font-size: 3rem;
            position: absolute;
            bottom: 10px;
            left: 15px;
            opacity: 0.4;
            transform: rotate(-15deg);
        }
        .lego-baseplate::after {
            content: "";
            font-size: 3rem;
            position: absolute;
            top: 10px;
            right: 15px;
            opacity: 0.4;
            transform: rotate(10deg);
        }
        .map-title {
            text-align: center;
            font-size: 2rem;
            font-weight: 800;
            background: #ffdd99;
            display: inline-block;
            width: auto;
            margin: 0 auto 25px;
            padding: 0 30px;
            border-radius: 60px;
            letter-spacing: 2px;
            color: #4a2a12;
            box-shadow: 0 5px 0 #b47c00;
            position: relative;
            z-index: 3;
        }
        .stations-row {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-wrap: wrap;
            gap: 30px;
            margin-bottom: 20px;
            position: relative;
            z-index: 4;
        }
        .big-lego-station {
            width: 180px;
            border-radius: 24px;
            padding: 18px 12px;
            text-align: center;
            cursor: pointer;
            transition: 0.2s ease;
            box-shadow: 0 12px 0 rgba(0,0,0,0.2), inset 0 2px 4px rgba(255,255,200,0.8);
            border: 2px solid rgba(255,255,200,0.8);
            position: relative;
        }
        .big-lego-station[data-station="1"] { background: linear-gradient(145deg, #ff4d4d, #cc0000); }
        .big-lego-station[data-station="2"] { background: linear-gradient(145deg, #ffaa33, #f57c00); }
        .big-lego-station[data-station="3"] { background: linear-gradient(145deg, #ffee55, #f9a825); }
        .big-lego-station[data-station="4"] { background: linear-gradient(145deg, #66bb6a, #2e7d32); }
        .big-lego-station[data-station="5"] { background: linear-gradient(145deg, #42a5f5, #1565c0); }
        .big-lego-station:hover {
            transform: translateY(-8px);
            box-shadow: 0 8px 0 rgba(0,0,0,0.2);
        }
        .station-number-big {
            font-size: 2.8rem;
            font-weight: 900;
            background: rgba(255,255,200,0.9);
            width: 70px;
            height: 70px;
            line-height: 70px;
            margin: 0 auto 12px;
            border-radius: 50%;
            color: #2c1a0e;
            box-shadow: inset 0 -2px 0 #c7a52b, 0 4px 8px rgba(0,0,0,0.2);
        }
        .station-name-big {
            font-weight: 800;
            font-size: 1rem;
            background: #fff9e6;
            border-radius: 40px;
            padding: 8px 4px;
            margin: 10px 0;
            color: #3b2a1f;
        }
        .big-lego-station img {
            width: 55px;
            margin-top: 5px;
            filter: drop-shadow(2px 2px 2px rgba(0,0,0,0.2));
        }
        .path-small-bricks {
            display: flex;
            justify-content: center;
            gap: 8px;
            margin: 5px 0 15px;
            flex-wrap: wrap;
        }
        .small-brick {
            width: 35px;
            height: 35px;
            background: #8a2be2;
            border-radius: 8px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            box-shadow: 0 4px 0 #53377A;
        }
        .lego-minifig {
            font-size: 2rem;
            text-align: center;
            margin-top: 25px;
            background: #f3d9b1;
            display: block;
            width: fit-content;
            margin-left: auto;
            margin-right: auto;
            padding: 8px 25px;
            border-radius: 60px;
            box-shadow: 0 6px 0 #b47c44;
        }
        .task-page {
            display: none;
            background: #fff8e7;
            border-radius: 40px;
            padding: 2rem;
            margin: 30px 0;
            border-left: 18px solid #ff9f2e;
            box-shadow: 0 10px 0 #c57f1e;
        }
        .task-page h2 {
            font-size: 2rem;
            display: flex;
            align-items: center;
            gap: 12px;
            flex-wrap: wrap;
            margin-bottom: 20px;
        }
        .lego-badge {
            background: #e34234;
            color: white;
            padding: 5px 12px;
            border-radius: 30px;
            font-size: 0.8rem;
            font-weight: bold;
        }
        .query-code {
            background: #2c3e2b;
            color: #f9f2cf;
            font-family: monospace;
            padding: 8px 15px;
            border-radius: 40px;
            display: inline-block;
            margin: 12px 0;
            font-size: 0.9rem;
            border-bottom: 3px solid #ffcd3c;
        }
        .part-input {
            background: #ebddb0;
            border-radius: 60px;
            padding: 10px 20px;
            margin-top: 15px;
            max-width: 350px;
        }
        .part-input input {
            width: 100%;
            padding: 12px 15px;
            border-radius: 40px;
            border: none;
            font-weight: bold;
            background: #ffffea;
            border: 2px solid #e3a018;
        }
        .back-button {
            background: #f0a500;
            border: none;
            padding: 10px 24px;
            font-weight: bold;
            font-size: 1rem;
            border-radius: 60px;
            cursor: pointer;
            box-shadow: 0 6px 0 #a45d00;
            transition: 0.05s linear;
            margin-top: 20px;
            display: inline-block;
        }
        .back-button:active {
            transform: translateY(3px);
            box-shadow: 0 3px 0 #a45d00;
        }
        .final-box {
            background: #fdd67a;
            border-radius: 40px;
            padding: 25px;
            text-align: center;
            box-shadow: 0 15px 0 #b45309;
            margin-top: 30px;
        }
        button {
            background: #f0a500;
            border: none;
            padding: 12px 28px;
            font-weight: bold;
            font-size: 1.1rem;
            border-radius: 60px;
            cursor: pointer;
            box-shadow: 0 6px 0 #a45d00;
            transition: 0.05s linear;
            margin: 10px;
        }
        button:active {
            transform: translateY(3px);
            box-shadow: 0 3px 0 #a45d00;
        }
        footer {
            text-align: center;
            margin-top: 45px;
            font-size: 0.85rem;
            background: #ffcd7e;
            border-radius: 50px;
            padding: 12px;
        }
        @media (max-width: 950px) {
            .big-lego-station { width: 150px; padding: 12px 6px; }
            .station-number-big { width: 55px; height: 55px; line-height: 55px; font-size: 2rem; }
            .stations-row { gap: 15px; }
        }
        @media (max-width: 750px) {
            .big-lego-station { width: 130px; }
            .station-name-big { font-size: 0.8rem; }
            .small-brick { width: 25px; height: 25px; font-size: 0.8rem; }
        }
        .query-button {
            background: linear-gradient(145deg, #4caf50, #2e7d32);
            border: none;
            padding: 12px 24px;
            font-weight: bold;
            font-size: 1.1rem;
            color: white;
            border-radius: 60px;
            cursor: pointer;
            box-shadow: 0 6px 0 #1b5e20;
            transition: 0.05s linear;
            margin: 15px 0;
            display: inline-block;
        }
        .query-button:active {
            transform: translateY(3px);
            box-shadow: 0 3px 0 #1b5e20;
        }
        .hidden-query {
            display: none;
            margin-top: 15px;
            padding: 12px;
            background: #f9f2cf;
            border-radius: 30px;
            border-left: 6px solid #ff9800;
        }
        .hidden-query.visible {
            display: block;
        }
    </style>
</head>
<body>
<div class="container">
    <div class="lego-header">
        <h1><span>МНОЖЕСТВО</span> <span>ПОИСК В СЕТИ</span></h1>
        <div class="lego-sub">🔍 ОПЕРАЦИИ: И, ИЛИ, НЕ — ДЕТЕКТИВ LEGO 🔍</div>
    </div>

    <div id="mainScreen">
        <div class="story-brick">
            <div class="story-text">
                <p><span style="background:#ffb347; padding:2px 12px; border-radius:30px;">📖 ЛЕГЕНДА LEGO</span></p>
                <p>На просторах интернета ходят удивительные слухи об одной из компаний. Один мальчик заинтересовался ими и обратился в детективное агентство, чтобы проверить пять интересных фактов.</p>
                <p><strong>Твоя миссия:</strong> пройти 5 станций, собрать ключевые слова и заполнить пропуски в итоговом тексте. Запомни, что использовать ии (даже если он встроен в браузер) категорически запрещено!</p>
            </div>
            <div class="lego-illustration">
                <img src="https://cdn-icons-png.flaticon.com/512/2620/2620983.png" alt="lego brick">
                <div style="font-size:0.7rem;">LEGO® Server</div>
            </div>
        </div>

        <div class="lego-baseplate">
            <div style="text-align: center;">
                <div class="map-title">КАРТА ПОИСКА</div>
            </div>
            <div class="stations-row">
                <div class="big-lego-station" data-station="1" data-task="task1">
                    <div class="station-number-big">①</div>
                    <div class="station-name-big">СТАНЦИЯ 1<br>Название компании</div>
                    <div style="font-size:0.7rem; background:#ffffffaa; border-radius:20px; padding:3px;">И, кавычки</div>
                </div>
                <div class="path-small-bricks"><div class="small-brick"></div><div class="small-brick"></div><div class="small-brick"></div></div>
                <div class="big-lego-station" data-station="2" data-task="task2">
                    <div class="station-number-big">②</div>
                    <div class="station-name-big">СТАНЦИЯ 2<br>Материал корпуса</div>
                    <div style="font-size:0.7rem; background:#ffffffaa; border-radius:20px; padding:3px;">НЕ (минус)</div>
                </div>
                <div class="path-small-bricks"><div class="small-brick"></div><div class="small-brick"></div><div class="small-brick"></div></div>
                <div class="big-lego-station" data-station="3" data-task="task3">
                    <div class="station-number-big">③</div>
                    <div class="station-name-big">СТАНЦИЯ 3<br>Помощники в траве</div>
                    <div style="font-size:0.7rem; background:#ffffffaa; border-radius:20px; padding:3px;">И (+), пересечение</div>
                </div>
                <div class="path-small-bricks"><div class="small-brick"></div><div class="small-brick"></div><div class="small-brick"></div></div>
                <div class="big-lego-station" data-station="4" data-task="task4">
                    <div class="station-number-big">④</div>
                    <div class="station-name-big">СТАНЦИЯ 4<br>Название сотрудников</div>
                    <div style="font-size:0.7rem; background:#ffffffaa; border-radius:20px; padding:3px;">ИЛИ + НЕ</div>
                </div>
                <div class="path-small-bricks"><div class="small-brick"></div><div class="small-brick"></div><div class="small-brick"></div></div>
                <div class="big-lego-station" data-station="5" data-task="task5">
                    <div class="station-number-big">⑤</div>
                    <div class="station-name-big">СТАНЦИЯ 5<br>Открытки Google</div>
                    <div style="font-size:0.7rem; background:#ffffffaa; border-radius:20px; padding:3px;">И, ИЛИ, НЕ</div>
                </div>
            </div>
            <div class="lego-minifig" align="center">
                Нажимай на кубики по очереди, чтобы найти слова!
            </div>
        </div>
    </div>

    <!-- СТАНЦИЯ 1 – название компании -->
    <div id="task1Page" class="task-page">
        <h2>СТАНЦИЯ 1 · НАЗВАНИЕ КОМПАНИИ <span class="lego-badge">И (+), кавычки</span></h2>
        <p><strong>Слух:</strong> самая популярная поисковая система в мире раньше называлась BackRub.</p><br>
        <p><strong>Что делать:</strong><br>
        1. Открой браузер Google Chrome. <br>
        2. В строку поиска введи точный запрос:<br>
        <code class="query-code">+"поисковая система" +"название" +"BackRub" </code><br>
        <strong>Плюс (+) </strong> и <strong> кавычки (" ")</strong> помогут найти точную информацию.<br>
        3. Найди современное название этой компании.<br>
        4. Выпиши это название. 
        <div class="part-input">
            <label>Слово №1:</label><br>
            <input type="text" id="part1" placeholder="GOOGLE">
        </div>
        <button class="back-button" data-back="main">← Вернуться к карте</button>
    </div>

    <!-- СТАНЦИЯ 2 – материал корпуса -->
    <div id="task2Page" class="task-page">
        <h2>СТАНЦИЯ 2 · МАТЕРИАЛ КОРПУСА <span class="lego-badge">И (+)</span></h2>
        <p><strong>Слух:</strong> корпус первого сервера был сделан из детского конструктора.</p>
        <p>Из какого именно? </p><br>
        <p><strong>Что делать:</strong><br>
        1. Введи запрос в поисковую строку:<br>
         <code class="query-code">+"первый" +"сервер google" +"корпус"</code><br>
        3. Найди, из какого именно конструктора собрали сервер.<br>
        4. Впиши название этого конструктора. 
        <div class="part-input">
            <label>Слово №2:</label>
            <input type="text" id="part2" placeholder="LEGO">
        </div>
        <button class="back-button" data-back="main">← Вернуться к карте</button>
    </div>

    <!-- СТАНЦИЯ 3 – помощники в траве -->
    <div id="task3Page" class="task-page">
        <h2>СТАНЦИЯ 3 · ПОМОЩНИКИ В ТРАВЕ <span class="lego-badge">И (+), НЕ (-)</span></h2>
        <p><strong>Слух:</strong> на территории штаб-квартиры Google газон стригут при помощи животных вместо бензиновых газонокосилок.</p><br>
        <p>Косить траву при помощи животных - это действительно очень экологичное решение. Однако, какие животные могут подойти лучше всех? Обрати внимание, что бензиновые газонокосилки необходимо исключить. </p><br>
        <p><strong>Что делать:</strong><br>
        1. Проанализируй задание и попробуй проверить факт самостоятельно, если не получилось, то используй готовый запрос. <br>
        
        <button class="query-button" data-target="hidden3">Показать верный запрос</button>
    <div id="hidden3" class="hidden-query">
        <code class="query-code">+"компания Google" +"животные" -бензиновые</code>
    </div><br> 
       
        2. Изучи результаты. <br>
        3. Запиши название животных ответив на вопрос: ""Кого использует руководство Google, чтобы косить траву?"
        <br>Подсказка: слово из 3 букв.
        <div class="part-input">
            <label>Слово №3:</label>
            <input type="text" id="part3" placeholder="КОЗ">
        </div>
        <button class="back-button" data-back="main">← Вернуться к карте</button>
    </div>

    <!-- СТАНЦИЯ 4 – название сотрудников -->
    <div id="task4Page" class="task-page">
        <h2>СТАНЦИЯ 4 · НАЗВАНИЕ СОТРУДНИКОВ <span class="lego-badge">И (+), НЕ (-)</span></h2>
        <p><strong>Слух:</strong> у постоянных сотрудников Google есть необычное прозвище.</p><br>
        У сотрудников Googlе действительно есть прозвище, однако, стоит учитывать, что есть новички (у них особое прозвище) и постоянные работники, название которых вам необходимо узнать. <br>
        <p><strong>Что делать:</strong><br>
        1. Проанализируй задание и попробуй самостоятельно найти прозвище сотрудников при помощи операторов +, - и "". Если не получается, то воспользуйся готовым запросом: <br>

        <button class="query-button" data-target="hidden4"> Показать верный запрос</button>
    <div id="hidden4" class="hidden-query">
        <code class="query-code">+"постоянные сотрудники" +"google" +"называют" -новички</code>
    </div><br>
        
        2. Найди, как называют себя сотрудники компании и выпиши это слово. (Обрати внимание, что оно пишется английскими буквами и во множественном числе).<br>
        <div class="part-input">
            <label>Слово №4:</label>
            <input type="text" id="part4" placeholder="GOOGLERS">
        </div>
        <button class="back-button" data-back="main">← Вернуться к карте</button>
    </div>

    <!-- СТАНЦИЯ 5 – открытки Google -->
    <div id="task5Page" class="task-page">
        <h2>СТАНЦИЯ 5 · ОТКРЫТКИ GOOGLE <span class="lego-badge">И (+), ИЛИ (OR)</span></h2>
        <p><strong>Слух:</strong> на главной странице поисковой системы Google к праздникам, знаменательным события, датам логотип компании изменяется, дополняясь забавными картинками. </p><br>
        
        <p><strong>Что делать:</strong><br>
        1. Попробуй дополнить запрос <br>
        <code class="query-code">+"логотип" +"google" +("..." OR "..." OR "...")</code><br>
        Если не получится, то воспользуйся готовым<br> 
        
        <button class="query-button" data-target="hidden5">Показать верный запрос</button>
    
    <div id="hidden5" class="hidden-query">
        <code class="query-code">+"логотип" +"google" +("событие" OR "праздник" OR "дата")</code><br></div><br>
        
        2. Выясни, как называются эти особые логотипы и выпиши слово (на английском языке и во множественном числе). <br>
        <div class="part-input">
            <label>Слово №5:</label>
            <input type="text" id="part5" placeholder="DOODLES">
        </div>
        <button class="back-button" data-back="main">← Вернуться к карте</button>
    </div>

    <!-- ФИНАЛЬНАЯ СБОРКА -->
    <div class="final-box">
        <h2>ЗАПОЛНИ ПРОПУСКИ</h2>
        <div style="background: #fff8e7; border-radius: 40px; padding: 20px; margin: 15px 0; font-size: 1.2rem; text-align: left;">
            <p><strong>___</strong> - поисковая система, корпус первого сервера которой был изготовлен из <strong>___</strong>.</p><br>
            <p>Руководство этой компании использует <strong>___</strong>, чтобы косить траву на её территории.</p><br>
            <p>Сотрудников компании называют - <strong>___</strong>.</p><br>
            <p>Поисковая система размещает на своей главной странице своеобразные открытки по случаю знаменательных событий, которые называют - <strong>___</strong>.</p>
        </div>
        <p style="font-size:1.4rem; font-weight:800; background:#ffffffba; border-radius: 50px; padding: 12px;" id="finalPreview">⬅️ Введи слова выше →</p>
        <button id="revealBtn">ПРОВЕРИТЬ ИСТИНУ</button>
        <div id="truthMessage" style="margin-top: 20px; font-weight: bold; font-size: 1.2rem;"></div>
    </div>

    <footer>
        © Кибердетектив LEGO · Операции над множествами: И (+), ИЛИ (OR), НЕ (-) помогают искать точные факты.
    </footer>
</div>

<script>
    const mainScreen = document.getElementById('mainScreen');
    const taskPages = {
        task1: document.getElementById('task1Page'),
        task2: document.getElementById('task2Page'),
        task3: document.getElementById('task3Page'),
        task4: document.getElementById('task4Page'),
        task5: document.getElementById('task5Page')
    };

    function showMainScreen() {
        mainScreen.style.display = 'block';
        for (let page in taskPages) taskPages[page].style.display = 'none';
    }

    function showTask(taskId) {
        mainScreen.style.display = 'none';
        for (let page in taskPages) taskPages[page].style.display = 'none';
        if (taskPages[taskId]) taskPages[taskId].style.display = 'block';
    }

    document.querySelectorAll('.big-lego-station').forEach(station => {
        station.addEventListener('click', (e) => {
            e.stopPropagation();
            const task = station.getAttribute('data-task');
            if (task) showTask(task);
        });
    });

    document.querySelectorAll('.back-button').forEach(btn => {
        btn.addEventListener('click', () => showMainScreen());
    });

    // Поля ввода
    const part1 = document.getElementById('part1');
    const part2 = document.getElementById('part2');
    const part3 = document.getElementById('part3');
    const part4 = document.getElementById('part4');
    const part5 = document.getElementById('part5');
    const previewSpan = document.getElementById('finalPreview');

    function updatePreview() {
        const p1 = part1.value.trim() || "___";
        const p2 = part2.value.trim() || "___";
        const p3 = part3.value.trim() || "___";
        const p4 = part4.value.trim() || "___";
        const p5 = part5.value.trim() || "___";
        previewSpan.innerText = `${p1} · ${p2} · ${p3} · ${p4} · ${p5}`;
    }

    part1.addEventListener('input', updatePreview);
    part2.addEventListener('input', updatePreview);
    part3.addEventListener('input', updatePreview);
    part4.addEventListener('input', updatePreview);
    part5.addEventListener('input', updatePreview);
    updatePreview();

    const revealBtn = document.getElementById('revealBtn');
    const truthDiv = document.getElementById('truthMessage');

    revealBtn.addEventListener('click', () => {
        let p1 = part1.value.trim().toUpperCase();
        let p2 = part2.value.trim().toUpperCase();
        let p3 = part3.value.trim().toUpperCase();
        let p4 = part4.value.trim().toUpperCase();
        let p5 = part5.value.trim().toUpperCase();

        const correct = ["GOOGLE", "LEGO", "КОЗ", "GOOGLERS", "DOODLES"];
        const user = [p1, p2, p3, p4, p5];

        let allCorrect = true;
        for (let i = 0; i < correct.length; i++) {
            if (user[i] !== correct[i]) allCorrect = false;
        }

        if (allCorrect) {
            truthDiv.innerHTML = 'Все верно! Вы правильно заполнили все факты!';
        } else {
            truthDiv.innerHTML = 'Некоторые слова введены неверно или отсутствуют. Внимательно проверь каждое слово!';
        }
    });

    // плейсхолдеры
    part1.placeholder = "Введи слово";
    part2.placeholder = "Введи слово";
    part3.placeholder = "Введи слово";
    part4.placeholder = "Введи слово";
    part5.placeholder = "Введи слово";

    showMainScreen();
    
    // Универсальный обработчик для всех кнопок "Показать запрос"
document.querySelectorAll('.query-button').forEach(button => {
    button.addEventListener('click', function() {
        const targetId = this.getAttribute('data-target');
        const hiddenBlock = document.getElementById(targetId);
        
        if (hiddenBlock) {
            hiddenBlock.classList.add('visible');
            this.style.display = 'none';   // скрываем кнопку после нажатия
        }
    });
});
</script>
</body>
</html>
