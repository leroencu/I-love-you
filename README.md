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
        .small-text {
            position: absolute;
            color: #ff1a1a;
            font-size: 14px;
            font-weight: bold;
            white-space: nowrap;
            opacity: 0;
            transform: translate(-50%, -50%);
            text-shadow: 0 0 8px rgba(255, 0, 0, 0.9);
            transition: opacity 0.5s ease-in-out;
        }
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
        const totalPoints = 350; 
        const width = window.innerWidth;
        const height = window.innerHeight;
        const centerX = width / 2;
        const centerY = height / 2;
        // Немного уменьшаем масштаб, чтобы сердце точно влезло в экран и центр был свободен
        const scale = Math.min(width, height) / 28;
        const elements = []; 
        for (let i = 0; i < totalPoints; i++) {
            let t = (i / totalPoints) * Math.PI * 2;           
            let x = 16 * Math.pow(Math.sin(t), 3);
            let y = 13 * Math.cos(t) - 5 * Math.cos(2 * t) - 2 * Math.cos(3 * t) - Math.cos(4 * t);
            // Смещение ВНУТРЬ сердца (умножаем на 0.85, чтобы надписи были чуть внутри контура)
            let posX = centerX + (x * scale) * (0.85 + Math.random() * 0.15);
            let posY = centerY - (y * scale) * (0.85 + Math.random() * 0.15);
            const span = document.createElement('span');
            span.className = 'small-text';
            span.innerText = 'I love you';
            span.style.left = posX + 'px';
            span.style.top = posY + 'px';
            container.appendChild(span);
            elements.push(span);
        }
        // Все надписи загораются одновременно
        setTimeout(() => {
            elements.forEach(el => {
                el.style.opacity = '1';
            });
        }, 300);
        // Через 15 секунд появляется большая белая надпись в центре
        setTimeout(() => {
            centerTextEl.style.opacity = '1';
        }, 15000);
    </script>
</body>
</html>
