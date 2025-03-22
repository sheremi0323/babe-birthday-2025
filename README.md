<html>
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
        .message {
            max-width: 600px;
            margin: 20px auto;
            font-size: 20px; /* 恢复字体大小 */
            line-height: 1.6;
            color: #8b4513;
            text-align: left;
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
    </div>
    <div id="scene4-1" class="hidden">
        <div class="message" id="message-container"></div>
    </div>
    <div id="scene5" class="hidden">
        <h1>什么啦！再选多一次！</h1>
        <img src="pic2.png" alt="动漫女孩" class="anime-girl">
    </div>

    <!-- 秋叶 -->
    <div id="leaf-container"></div>

    <!-- 音频 -->
    <audio id="song1" src="song1.mp3"></audio>
    <audio id="song2" src="song2.mp3"></audio>

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

            // 播放第一首歌
            const song1 = document.getElementById('song1');
            song1.play();
        });

        // 点击 scene4 的任意位置显示长篇大论
        const messageContainer = document.getElementById('message-container');
        const messages = [
            "宝宝19岁生日快乐鸭🦆~！这一天又又又来咯~虽然宝宝讲不要庆祝什么的。。不过我尊重你的选择咯~只限今年哦！有没有惊喜呀今年生日是两个link没有长篇大论？看宝宝将期待那现在开始咯~",
            "这些年确确实实发生很多事情啦有好有坏（我觉得好的事情还是比较多的~）经历事情就是给我们的考验！看我们是不是真心相爱还是像f4 yt跟我讲的我们3个月后就会分（这句话到现在差不多要3年咯~）",
            "知道宝宝最近很迷茫，觉得自己的存在的意义是什么。。这个世界会变好吗？等通知。不过我要讲的依然是！宝宝做的任何决定，我都会站在你旁边。没有特地站在你前面挡着光，也没有特地跟在你身后保护影子。“先去做，做成一堆狗屎，再慢慢去改，一个粗糙的开始，就是最好的开始” 享受过程，丰收结果~",
            "祝宝宝+1岁 = +健康 +幸福 +学业 +友情 = 一帆风顺+学业有成+前程似锦 = 未来可期~！宝宝累了想休息就看看身边所有的美好人事物吧~生活不是为了赶路啊~你不需要向别人证明自己，因为我相信你可以的~！（超级真诚的眼神）"
        ];
        let messageIndex = 0;
        let typingInterval;

        document.getElementById('scene4').addEventListener('click', () => {
            document.getElementById('scene4').classList.add('hidden');
            document.getElementById('scene4-1').classList.remove('hidden');

            // 停止第一首歌，播放第二首歌并设置音量为 0.3
            const song1 = document.getElementById('song1');
            const song2 = document.getElementById('song2');
            song1.pause();
            song2.volume = 0.3; // 设置音量为 30%
            song2.play();

            showNextMessage();
        });

        document.getElementById('scene4-1').addEventListener('click', () => {
            showNextMessage();
        });

        function showNextMessage() {
            if (messageIndex < messages.length) {
                // 清空当前内容
                messageContainer.innerHTML = '';

                // 开始打字机效果
                typeMessage(messages[messageIndex]);
                messageIndex++;
            } else {
                // 如果已经是最后一段，可以做一些其他操作，比如回到主页面
                alert("已经是最后一段啦~");
            }
        }

        function typeMessage(message) {
            let charIndex = 0;
            clearInterval(typingInterval); // 清除之前的定时器

            typingInterval = setInterval(() => {
                if (charIndex < message.length) {
                    // 逐字显示
                    messageContainer.innerHTML += message.charAt(charIndex);
                    charIndex++;
                } else {
                    // 停止打字机效果
                    clearInterval(typingInterval);
                }
            }, 50); // 每 50 毫秒显示一个字
        }

        document.getElementById('dont-know').addEventListener('click', () => {
            document.getElementById('scene3').classList.add('hidden');
            document.getElementById('scene5').classList.remove('hidden');
            currentScene = 5;
        });

        // 点击 scene5 的任意位置返回 scene3
        document.getElementById('scene5').addEventListener('click', () => {
            document.getElementById('scene5').classList.add('hidden');
            document.getElementById('scene3').classList.remove('hidden');
            currentScene = 3;
        });
    </script>
</body>
</html>
