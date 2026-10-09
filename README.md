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
            font-size: 13px;
            font-weight: bold;
            white-space: nowrap;
            opacity: 0;
            transform: translate(-50%, -50%);
            text-shadow: 0 0 6px rgba(255, 0, 0, 0.9);
            transition: opacity 0.6s ease-in-out;
        }
        .center-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 65px;
            font-weight: 900;
            color: #ffffff;
            opacity: 0;
            text-align: center;
            white-space: nowrap;
            z-index: 100;
            text-shadow: 0 0 20px rgba(255, 255, 255, 0.9);
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
        const width = window.innerWidth;
        const height = window.innerHeight;
        const centerX = width / 2;
        const centerY = height / 2;
        const scale = Math.min(width, height) / 26;
        const elements = [];
        // Функция проверки, находится ли точка внутри сердца
        function isInsideHeart(x, y) {
            // Нормализуем координаты (приводим к системе формулы сердца)
            let nx = (x - centerX) / scale;
            let ny = -(y - centerY) / scale; // Инвертируем Y
            // Формула сердца: (x^2 + y^2 - 1)^3 - x^2 * y^3 <= 0
            let a = nx * nx + ny * ny - 1;
            let formula = a * a * a - nx * nx * ny * ny * ny;
            return formula <= 0;
        }
        // Заполняем всё пространство сердца надписями
        // Проходим по всей площади экрана с шагом, проверяем — внутри ли сердца
        const step = 18; // Чем меньше шаг, тем плотнее надписи
        for (let y = 0; y < height; y += step) {
            for (let x = 0; x < width; x += step) {
                // Небольшое случайное смещение, чтобы сетка не была идеально ровной
                let px = x + (Math.random() - 0.5) * step;
                let py = y + (Math.random() - 0.5) * step;
                if (isInsideHeart(px, py)) {
                    const span = document.createElement('span');
                    span.className = 'small-text';
                    span.innerText = 'I love you';
                    span.style.left = px + 'px';
                    span.style.top = py + 'px';                    
                    // Небольшая случайная задержка, чтобы они появлялись волной
                    const delay = Math.random() * 1.5;
                    span.style.transitionDelay = delay + 's';
                    container.appendChild(span);
                    elements.push(span);
                }
            }
        }
        // Все надписи загораются
        setTimeout(() => {
            elements.forEach(el => {
                el.style.opacity = '1';
            });
        }, 200);
        // Через 15 секунд появляется большая белая надпись по центру
        setTimeout(() => {
            centerTextEl.style.opacity = '1';
        }, 15000);
    </script>
</body>
</html>
