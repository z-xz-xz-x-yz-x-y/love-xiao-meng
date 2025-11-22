# love-xiao-meng
lovey
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>专属温馨提醒</title>
    <style>
        * {margin: 0; padding: 0; box-sizing: border-box;}
        body {
            margin: 0; 
            padding: 20px; 
            background: linear-gradient(135deg, #fdf2f8, #ffe6f2);
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            overflow: hidden;
            height: 100vh;
        }
        #startBtn {
            background: linear-gradient(45deg, #ff4d6d, #ff8fa3);
            color: white;
            border: none;
            padding: 16px 28px;
            border-radius: 25px;
            font-size: 18px;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(255,77,109,0.4);
            display: block;
            margin: 0 auto 20px;
            font-weight: bold;
            transition: all 0.3s ease;
        }
        #startBtn:active {
            transform: scale(0.95);
            box-shadow: 0 2px 8px rgba(255,77,109,0.4);
        }
        .tip {
            position: absolute;
            padding: 12px 18px;
            border-radius: 20px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            font-size: 16px;
            animation: pop 0.2s ease, float 2s ease-in-out;
            font-weight: 500;
            max-width: 200px;
            text-align: center;
            z-index: 10;
        }
        @keyframes pop {
            from {opacity: 0; transform: scale(0.7);}
            to {opacity: 1; transform: scale(1);}
        }
        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-5px); }
        }
        #tipArea {
            position: relative;
            width: 100%;
            height: calc(100vh - 100px);
            overflow: hidden;
        }
        .heart {
            position: absolute;
            font-size: 20px;
            animation: float 2s ease-in-out infinite;
            z-index: 5;
        }
    </style>
</head>
<body>
    <audio id="bgm" loop preload="auto">
        <source src="https://cdn.jsdelivr.net/gh/BobLChen/CDN@master/music/01.mp3" type="audio/mpeg">
    </audio>

    <button id="startBtn">开启温馨提醒</button>
    <div id="tipArea"></div>

    <script>
        // 温馨提醒内容
        const texts = [
            "💖 亲爱的小梦，天冷加衣别着凉",
            "💖 亲爱的小梦，好好吃饭长肉肉",
            "💖 亲爱的小梦，记得想我呀",
            "💖 亲爱的小梦，保持甜甜的心情",
            "💖 亲爱的小梦，今天也要顺顺利利",
            "💖 亲爱的小梦，每天都要开开心心",
            "💖 亲爱的小梦，我超想你",
            "💖 亲爱的小梦，我爱你呀",
            "💖 亲爱的小梦，我好想你",
            "💖 亲爱的小梦，一直爱你不改变",
            "💖 亲爱的小梦，多喝水呀",
            "💖 亲爱的小梦，别熬夜早点休息",
            "💖 亲爱的小梦，今天也要元气满满",
            "💖 亲爱的小梦，你最可爱啦",
            "💖 亲爱的小梦，要照顾好自己",
            "💖 亲爱的小梦，愿你事事顺心",
            "💖 亲爱的小梦，和你在一起超幸福",
            "💖 亲爱的小梦，记得补充能量",
            "💖 亲爱的小梦，笑容要一直灿烂",
            "💖 亲爱的小梦，永远喜欢你呀",
            "💖 亲爱的小梦，出门注意安全",
            "💖 亲爱的小梦，累了就歇一歇",
            "💖 亲爱的小梦，被你治愈的一天",
            "💖 亲爱的小梦，顺顺利利每一天"
        ];
        
        const colors = ["#ffe6f2", "#fff0f5", "#ffe0e9", "#fce4ec", "#f8d7da", "#f9f0ff", "#f0f8ff"];
        const area = document.getElementById("tipArea");
        const bgm = document.getElementById("bgm");
        let timer;

        function createTip() {
            const tip = document.createElement("div");
            tip.className = "tip";
            tip.textContent = texts[Math.floor(Math.random() * texts.length)];
            tip.style.background = colors[Math.floor(Math.random() * colors.length)];
            tip.style.left = Math.random() * 80 + "%";
            tip.style.top = Math.random() * 80 + "%";
            tip.style.color = "#e91e63";
            area.appendChild(tip);
            
            // 创建小心心
            if (Math.random() > 0.7) {
                const heart = document.createElement("div");
                heart.className = "heart";
                heart.textContent = "💕";
                heart.style.left = Math.random() * 90 + "%";
                heart.style.top = Math.random() * 90 + "%";
                area.appendChild(heart);
                setTimeout(() => heart.remove(), 2000);
            }
            
            setTimeout(() => tip.remove(), 2000);
        }

        document.getElementById("startBtn").onclick = () => {
            // 微信自动播放处理
            bgm.play().catch(err => {
                // 微信中需要用户交互才能播放音乐
                document.body.onclick = () => {
                    bgm.play();
                    document.body.onclick = null;
                };
            });
            
            if (timer) clearInterval(timer);
            timer = setInterval(createTip, 200);
            
            // 按钮点击后改变样式
            const btn = document.getElementById("startBtn");
            btn.textContent = "温馨提醒进行中...";
            btn.style.background = "linear-gradient(45deg, #ff8fa3, #ffb3c1)";
            btn.disabled = true;
        };

        // 防止微信下拉刷新
        document.addEventListener('touchmove', function(e) {
            e.preventDefault();
        }, { passive: false });
    </script>
</body>
</html>
