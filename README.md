# I-love-you
Котику
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Признание</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background-color: #000;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            font-family: 'Arial', sans-serif;
            color: white;
        }
        #canvas-container {
            position: relative;
            width: 100%;
            height: 100%;
        }
        /* Стиль для маленьких надписей */
        .small-text {
            position: absolute;
            color: #ff1a1a; /* Красный цвет */
            font-size: 14px;
            font-weight: bold;
            white-space: nowrap;
            opacity: 0;
            transform: translate(-50%, -50%);
            /* Анимация появления и исчезновения */
            animation: fadeInOut 2s ease-in-out forwards;
            text-shadow: 0 0 8px rgba(255, 0, 0, 0.9);
        }
        /* Стиль для центрального текста */
        .center-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 60px;
            font-weight: 900;
            color: #ffffff;
            opacity: 0;
            text-align: center;
            white-space: nowrap;
            z-index: 100;
            /* Плавное появление и исчезновение */
            transition: opacity 1s ease-in-out;
            text-shadow: 0 0 15px rgba(255, 255, 255, 0.5);
        }
        /* Анимация мерцания для маленьких надписей */
        @keyframes fadeInOut {
            0% { opacity: 0; transform: translate(-50%, -50%) scale(0.8); }
            20% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
            80% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
            100% { opacity: 0; transform: translate(-50%, -50%) scale(1.1); }
        }
    </style>
</head>
<body>
    <div id="canvas-container">
        <div id="center-text" class="center-text"></div>
    </div>
    <script>
        const container = document.getElementById('canvas-container');
        const centerTextEl = document.getElementById('center-text');
        // 1. Функция для создания маленьких надписей по контуру сердца
        function createHeartBeat() {
            const width = window.innerWidth;
            const height = window.innerHeight;
            const centerX = width / 2;
            const centerY = height / 2;
            const scale = Math.min(width, height) / 25; 
            // Количество надписей, чтобы заполнить контур
            const totalPoints = 150; 
            for (let i = 0; i < totalPoints; i++) {
                // Параметрическое уравнение сердца
                let t = (i / totalPoints) * Math.PI * 2;             
                // Формула сердца
                let x = 16 * Math.pow(Math.sin(t), 3);
                let y = 13 * Math.cos(t) - 5 * Math.cos(2 * t) - 2 * Math.cos(3 * t) - Math.cos(4 * t);
                // Масштабируем и центрируем
                let posX = centerX + x * scale;
                // Инвертируем Y, так как в браузере ось Y идет вниз
                let posY = centerY - y * scale;
                // Создаем элемент
                const span = document.createElement('span');
                span.className = 'small-text';
                span.innerText = 'I love you';         
                // Небольшое случайное смещение, чтобы было похоже на "рой"
                let randomOffsetX = (Math.random() - 0.5) * 40;
                let randomOffsetY = (Math.random() - 0.5) * 40;
                span.style.left = (posX + randomOffsetX) + 'px';
                span.style.top = (posY + randomOffsetY) + 'px';
                // Случайная задержка появления (чтобы они появлялись не одновременно, а волной)
                const delay = Math.random() * 0.8; 
                span.style.animationDelay = delay + 's';
                container.appendChild(span);
            }
        }
        // Запускаем генерацию
        createHeartBeat();
        // --- ТАЙМИНГИ ПО ВАШЕМУ ЗАПРОСУ ---
        // 1. Держим красные надписи 15 секунд, затем они плавно исчезают (анимация 2с)
        // Ждем 15 секунд, чтобы начать исчезновение
        setTimeout(() => {
            // Принудительно скрываем все маленькие надписи
            const allSmall = document.querySelectorAll('.small-text');
            allSmall.forEach(el => {
                el.style.opacity = '0';
                el.style.transition = 'opacity 1s ease-in-out'; // Плавное затухание
            });
        }, 15000);
        // 2. Через 1 секунду после начала исчезновения (16 сек) появляется "Я люблю тебя"
        setTimeout(() => {
            centerTextEl.innerText = "Я люблю тебя";
            centerTextEl.style.fontSize = "80px"; // Чуть больше
            centerTextEl.style.opacity = "1";
        }, 16000);
        // 3. Держим "Я люблю тебя" 3 секунды (до 19 сек), затем меняем на "Ильдар"
        setTimeout(() => {
            centerTextEl.style.opacity = "0"; // Плавно скрываем         
            // Ждем завершения анимации скрытия (1 сек) и меняем текст
            setTimeout(() => {
                centerTextEl.innerText = "Ильдар";
                centerTextEl.style.fontSize = "80px";
                centerTextEl.style.opacity = "1"; // Появляемся с новым текстом
            }, 1000);
        }, 19000);
        // 4. Держим "Ильдар" 3 секунды (до 23 сек) и плавно скрываем всё
        setTimeout(() => {
            centerTextEl.style.opacity = "0";
        }, 23000);
    </script>
</body>
</html>
