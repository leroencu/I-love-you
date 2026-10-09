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
        }
        /* Маленькие красные надписи */
        .small-text {
            position: absolute;
            color: #ff1a1a;
            font-size: 14px;
            font-weight: bold;
            white-space: nowrap;
            opacity: 0;
            transform: translate(-50%, -50%);
            text-shadow: 0 0 8px rgba(255, 0, 0, 0.9);
            transition: opacity 0.5s ease-in-out; /* Плавное появление */
        }
        /* Большая белая надпись по центру */
        .center-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 70px;
            font-weight: 900;
            color: #ffffff;
            opacity: 0;
            text-align: center;
            white-space: nowrap;
            z-index: 100;
            text-shadow: 0 0 20px rgba(255, 255, 255, 0.8);
            transition: opacity 1s ease-in-out;
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
        // Количество надписей по контуру сердца
        const totalPoints = 200; 
        const width = window.innerWidth;
        const height = window.innerHeight;
        const centerX = width / 2;
        const centerY = height / 2;
        const scale = Math.min(width, height) / 25;
        const elements = []; // Массив для хранения всех надписей
        // 1. Создаем МНОГО надписей по контуру сердца
        for (let i = 0; i < totalPoints; i++) {
            let t = (i / totalPoints) * Math.PI * 2;            
            // Формула сердца
            let x = 16 * Math.pow(Math.sin(t), 3);
            let y = 13 * Math.cos(t) - 5 * Math.cos(2 * t) - 2 * Math.cos(3 * t) - Math.cos(4 * t);
            let posX = centerX + x * scale;
            let posY = centerY - y * scale;
            const span = document.createElement('span');
            span.className = 'small-text';
            span.innerText = 'I love you';            
            // Случайное смещение, чтобы надписи были похожи на живой рой
            let randomOffsetX = (Math.random() - 0.5) * 35;
            let randomOffsetY = (Math.random() - 0.5) * 35;
            span.style.left = (posX + randomOffsetX) + 'px';
            span.style.top = (posY + randomOffsetY) + 'px';
            container.appendChild(span);
            elements.push(span);
        }
        // 2. Все надписи загораются одна за другой и остаются гореть
        elements.forEach((el, index) => {
            // Задержка для каждой надписи, чтобы они появлялись волной, но не слишком долго
            // 200 надписей * 50мс = 10 секунд на полное появление. 
            // К 15 секунде все точно будут гореть.
            setTimeout(() => {
                el.style.opacity = '1';
            }, index * 50); 
        });
        // 3. Через 15 секунд показываем большую надпись по центру
        setTimeout(() => {
            centerTextEl.style.opacity = '1';
        }, 15000);
    </script>
</body>
</html>
