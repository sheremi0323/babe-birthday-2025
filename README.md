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
            color: #ff1493;
            background: linear-gradient(45deg, #ffb6c1, #ff69b4);
            height: 100vh;
            overflow: hidden;
            position: relative;
        }
        h1, p {
            margin: 20px;
            font-size: 24px;
        }
        .sakura {
            position: absolute;
            top: -10%;
            animation: fall linear infinite;
        }
        @keyframes fall {
            to {
                transform: translateY(100vh);
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
            border: 2px solid #ff1493;
            border-radius: 10px;
            cursor: pointer;
            font-size: 18px;
            color: #ff1493;
        }
        .option:hover {
            background-color: #ff1493;
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
        <h1>生日快乐！</h1>
        <img src="pic1.png" alt="千层蛋糕" class="cake">
        <audio id="birthday-song" src="song1.mp3" autoplay></audio>
    </div>
    <div id="scene5" class="hidden">
        <h1>不对！再选多一次！</h1>
        <img src="pic2.png" alt="动漫女孩" class="anime-girl">
    </div>

    <!-- 樱花瓣 -->
    <div id="sakura-container"></div>

    <script>
        // 樱花瓣效果
        const sakuraContainer = document.getElementById('sakura-container');
        function createSakura() {
            const sakura = document.createElement('div');
            sakura.innerHTML = '🌸';
            sakura.classList.add('sakura');
            sakura.style.left = Math.random() * 100 + 'vw';
            sakura.style.animationDuration = Math.random() * 3 + 2 + 's';
            sakuraContainer.appendChild(sakura);
            setTimeout(() => sakura.remove(), 5000);
        }
        setInterval(createSakura, 300);

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
    </script>
</body>
</html>
