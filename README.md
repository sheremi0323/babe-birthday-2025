<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>浪漫惊喜</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: 'Comic Sans MS', cursive, sans-serif;
            text-align: center;
            color: #8b4513; /* 秋叶棕色 */
            background: linear-gradient(45deg, #ff8c00, #d2691e); /* 秋天色调 */
            height: 100vh;
            overflow: hidden;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
        }
        h1 {
            margin: 20px;
            font-size: 36px; /* 放大字体 */
        }
        p {
            margin: 20px;
            font-size: 28px; /* 放大字体 */
        }
        .leaf {
            position: absolute;
            top: -10%;
            animation: fall linear infinite;
            font-size: 24px; /* 秋叶大小 */
        }
        @keyframes fall {
            to {
                transform: translateY(100vh) rotate(360deg); /* 秋叶旋转下落 */
            }
        }
        .hidden {
            display: none;
        }
        .options {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 30px;
        }
        .option {
            padding: 10px 20px;
            background-color: #fff;
            border: 2px solid #8b4513; /* 秋叶棕色 */
            border-radius: 10px;
            cursor: pointer;
            font-size: 18px;
            color: #8b4513; /* 秋叶棕色 */
        }
        .option:hover {
            background-color: #8b4513; /* 秋叶棕色 */
            color: #fff;
        }
        .cake {
            width: 300px;
            margin-top: 20px;
        }
        .anime-girl {
            width: 200px;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div id="scene1">
        <h1>哈喽宝宝~</h1>
        <p>（嘿嘿嘿~）</p>
    </div>
    <div id="scene2" class="hidden">
        <h1>宝宝知道此时此刻是什么大日子吗~？</h1>
        <p>（装傻ing~）</p>
    </div>
    <div id="scene3" class="hidden">
        <h1>宝宝要不要猜猜看呀~？</h1>
        <div class="options">
            <div class="option" id="birthday">我的生日</div>
            <div class="option" id="dont-know">不知道</div>
        </div>
    </div>
    <div id="scene4" class="hidden">
        <h1>嘿嘿~生日快乐我的宝宝~！</h1>
        <img src="pic1.png" alt="千层蛋糕" class="cake">
        <audio id="birthday-song" src="song1.mp3" autoplay></audio>
    </div>
    <div id="scene5" class="hidden">
        <h1>什么啦！再选多一次！</h1>
        <img src="pic2.png" alt="动漫女孩" class="anime-girl">
    </div>

    <!-- 秋叶 -->
    <div id="leaf-container"></div>

    <script>
        // 秋叶飘落效果
        const leafContainer = document.getElementById('leaf-container');
        function createLeaf() {
            const leaf = document.createElement('div');
            leaf.innerHTML = '🍁'; // 秋叶
            leaf.classList.add('leaf');
            leaf.style.left = Math.random() * 100 + 'vw';
            leaf.style.animationDuration = Math.random() * 3 + 2 + 's';
            leaf.style.fontSize = Math.random() * 20 + 16 + 'px'; // 随机大小
            leafContainer.appendChild(leaf);
            setTimeout(() => leaf.remove(), 5000);
        }
        setInterval(createLeaf, 300);

        // 场景切换
        let currentScene = 1;
        document.body.addEventListener('click', () => {
            if (currentScene === 1) {
                document.getElementById('scene1').classList.add('hidden');
                document.getElementById('scene2').classList.remove('hidden');
                currentScene = 2;
            } else if (currentScene === 2) {
                document.getElementById('scene2').classList.add('hidden');
                document.getElementById('scene3').classList.remove('hidden');
                currentScene = 3;
            }
        });

        // 选项点击事件
        document.getElementById('birthday').addEventListener('click', () => {
            document.getElementById('scene3').classList.add('hidden');
            document.getElementById('scene4').classList.remove('hidden');
            currentScene = 4;
        });
        document.getElementById('dont-know').addEventListener('click', () => {
            document.getElementById('scene3').classList.add('hidden');
            document.getElementById('scene5').classList.remove('hidden');
            currentScene = 5;
        });

        // 点击 scene5 返回 scene3
        document.getElementById('scene5').addEventListener('click', () => {
            document.getElementById('scene5').classList.add('hidden');
            document.getElementById('scene3').classList.remove('hidden');
            currentScene = 3;
        });
    </script>
</body>
</html>
