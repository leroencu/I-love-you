# I-love-you
Котику
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>I Love You</title>
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
        }
        #canvas-container {
            position: relative;
            width: 100%;
            height: 100%;
            filter: blur(0.4px);
        }
        .small-text {
            position: absolute;
            color: #ff1a1a;
            font-size: 13px;
            font-weight: bold;
            white-space: nowrap;
            opacity: 0;
            transform: translate(-50%, -50%);
            text-shadow: 0 0 5px rgba(255, 0, 0, 0.8), 0 0 10px rgba(255, 0, 0, 0.4);
            transition: opacity 0.8s ease-in-out;
        }
        /* Белая надпись, которая будет в ЦЕНТРЕ СЕРДЦА, а не экрана */
        .center-text {
            position: absolute;
            /* Координаты left и top будут установлены через JS */
            transform: translate(-50%, -50%);
            font-size: 70px;
            font-weight: 900;
            color: #ffffff;
            opacity: 0;
            text-align: center;
            white-space: nowrap;
            z-index: 100;
            text-shadow: 0 0 15px rgba(255, 255, 255, 0.7);
            transition: opacity 1.5s ease-in-out;
        }
    </style>
</head>
<body>
    <div id="canvas-container">
        <div id="center-text" class="center-text">I love you</div>
    </div>
    <script>
        const container = document.getElementById('canvas-container');
        const centerTextEl = document.getElementById('center-text');
        const width = window.innerWidth;
        const height = window.innerHeight;
        const centerX = width / 2;
        const centerY = height / 2;
        const scale = Math.min(width, height) / 22;
        const elements = [];
        // Точки контура
        const totalPoints = 250;
        const copiesPerPoint = 2;
        // Переменные для вычисления визуального центра сердца
        let minX = Infinity, maxX = -Infinity;
        let minY = Infinity, maxY = -Infinity;
        for (let i = 0; i < totalPoints; i++) {
            let t = (i / totalPoints) * Math.PI * 2;           
            let x = 16 * Math.pow(Math.sin(t), 3);
            let y = 13 * Math.cos(t) - 5 * Math.cos(2 * t) - 2 * Math.cos(3 * t) - Math.cos(4 * t);
            let baseX = centerX + x * scale;
            let baseY = centerY - y * scale;
            // Отслеживаем крайние точки сердца, чтобы найти его визуальный центр
            if (baseX < minX) minX = baseX;
            if (baseX > maxX) maxX = baseX;
            if (baseY < minY) minY = baseY;
            if (baseY > maxY) maxY = baseY;
            for (let j = 0; j < copiesPerPoint; j++) {
                let offsetAlong = (j - copiesPerPoint / 2) * 8; 
                let randomOffsetX = (Math.random() - 0.5) * 12;
                let randomOffsetY = (Math.random() - 0.5) * 12;
                let posX = baseX + offsetAlong + randomOffsetX;
                let posY = baseY + randomOffsetY;
                const span = document.createElement('span');
                span.className = 'small-text';
                span.innerText = 'I love you';
                span.style.left = posX + 'px';
                span.style.top = posY + 'px';
                const delay = Math.random() * 1.2;
                span.style.transitionDelay = delay + 's';
                container.appendChild(span);
                elements.push(span);
            }
        }
        // Вычисляем центр сердца
        // По X он совпадает с центром экрана
        // По Y — это середина между верхней и нижней точкой сердца
        const heartCenterX = (minX + maxX) / 2;
        const heartCenterY = (minY + maxY) / 2;
        // Устанавливаем координаты для белой надписи ИМЕННО В ЦЕНТР СЕРДЦА
        centerTextEl.style.left = heartCenterX + 'px';
        // Немного опускаем вниз, так как верхняя часть сердца "пустее", а визуально центр ниже
        centerTextEl.style.top = (heartCenterY + 15) + 'px';
        // Запускаем появление всех красных надписей
        setTimeout(() => {
            elements.forEach(el => {
                el.style.opacity = '1';
            });
        }, 100);
        // Через 15 секунд появляется большая белая надпись в центре сердца
        setTimeout(() => {
            centerTextEl.style.opacity = '1';
        }, 15000);
    </script>
</body>
</html>
