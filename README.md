<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>动物气球乐园 - 幼儿游戏</title>
    <link href="https://fonts.googleapis.com/css2?family=Comic+Neue:wght@700&display=swap" rel="stylesheet">
    <style>
        /* ========= 样式与原来完全一致，仅精简展示 ========= */
        *{margin:0;padding:0;box-sizing:border-box}
        body{font-family:'Comic Neue',cursive;background:linear-gradient(to bottom,#6ecbf5,#ff9de9);min-height:100vh;display:flex;flex-direction:column;align-items:center;padding:20px}
        .header{text-align:center;margin-bottom:20px;padding:20px;background:rgba(255,255,255,.85);border-radius:25px;box-shadow:0 8px 20px rgba(0,0,0,.15);width:90%;max-width:700px;border:5px solid #ffd166;animation:bounce 2s infinite}
        h1{color:#ff6b6b;font-size:3rem;margin-bottom:10px;text-shadow:3px 3px 0 #ffd166}
        .instructions{color:#6a0572;font-size:1.4rem;margin-bottom:15px}
        .game-container{width:90%;max-width:900px;height:65vh;background:rgba(255,255,255,.6);border-radius:30px;position:relative;overflow:hidden;box-shadow:0 12px 30px rgba(0,0,0,.2);border:10px solid #ffd166;background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100' height='100'%3E%3Ccircle cx='50' cy='50' r='40' fill='none' stroke='%23FFD166' stroke-width='2' stroke-dasharray='5,5'/%3E%3C/svg%3E")}
        .balloon{position:absolute;width:150px;height:180px;border-radius:50%;cursor:pointer;display:flex;justify-content:center;align-items:center;font-size:4rem;transition:transform .3s;animation:float 8s infinite ease-in-out;box-shadow:0 6px 15px rgba(0,0,0,.2);z-index:2}
        .balloon:nth-child(3){background:#ff6b6b;top:15%;left:10%;animation-duration:9s}
        .balloon:nth-child(4){background:#4ecdc4;top:25%;left:50%;animation-duration:11s}
        .balloon:nth-child(5){background:#ffd166;top:55%;left:20%;animation-duration:8s}
        .balloon:nth-child(6){background:#6a0572;top:35%;left:75%;animation-duration:10s}
        .balloon:nth-child(7){background:#f75c03;top:65%;left:60%;animation-duration:12s}
        .balloon:nth-child(8){background:#1a936f;top:10%;left:80%;animation-duration:7s}
        .balloon:hover{transform:scale(1.15)}
        @keyframes float{0%,100%{transform:translateY(0) rotate(0)}25%{transform:translateY(-20px) rotate(3deg)}50%{transform:translateY(0) rotate(0)}75%{transform:translateY(15px) rotate(-3deg)}}
        .controls{margin-top:30px;display:flex;gap:20px;flex-wrap:wrap;justify-content:center}
        .btn{padding:18px 35px;font-size:1.4rem;border:none;border-radius:60px;cursor:pointer;background:linear-gradient(to bottom,#ff6b6b,#ff4f4f);color:#fff;font-weight:bold;box-shadow:0 6px 15px rgba(0,0,0,.25);transition:all .3s;text-shadow:1px 1px 2px rgba(0,0,0,.3)}
        .btn:hover{transform:scale(1.08) translateY(-5px);box-shadow:0 10px 20px rgba(0,0,0,.3)}
        .btn:active{transform:scale(.98) translateY(2px);box-shadow:0 3px 8px rgba(0,0,0,.2)}
        .btn-music{background:linear-gradient(to bottom,#4ecdc4,#2fa99e)}
        .btn-animals{background:linear-gradient(to bottom,#6a0572,#4d0370)}
        .btn-reset{background:linear-gradient(to bottom,#f75c03,#d14a02)}
        .score{font-size:1.8rem;color:#6a0572;background:#fff;padding:15px 35px;border-radius:60px;box-shadow:0 6px 15px rgba(0,0,0,.15);margin-top:25px;border:4px solid #ffd166;font-weight:bold}
        .animal{font-size:6rem;position:absolute;animation:popIn .5s forwards,bounce 1s infinite .5s;z-index:3;text-shadow:3px 3px 5px rgba(0,0,0,.3);filter:drop-shadow(0 0 8px rgba(255,255,255,.8))}
        @keyframes popIn{0%{transform:scale(0);opacity:0}70%{transform:scale(1.2)}100%{transform:scale(1);opacity:1}}
        @keyframes bounce{0%,100%{transform:translateY(0)}50%{transform:translateY(-25px)}}
        .cloud{position:absolute;background:#fff;border-radius:50%;opacity:.7;z-index:1}
        .cloud::before,.cloud::after{content:'';position:absolute;background:#fff;border-radius:50%}
        .cloud1{width:120px;height:60px;top:15%;left:5%;animation:drift 25s linear infinite}
        .cloud1::before{width:60px;height:60px;top:-30px;left:15px}
        .cloud1::after{width:80px;height:80px;top:-20px;right:15px}
        .cloud2{width:150px;height:70px;top:25%;right:5%;animation:drift 30s linear infinite reverse}
        .cloud2::before{width:70px;height:70px;top:-35px;left:20px}
        .cloud2::after{width:90px;height:90px;top:-30px;right:20px}
        @keyframes drift{from{transform:translateX(-100px)}to{transform:translateX(calc(100vw + 100px))}}
        .ground{position:absolute;bottom:0;left:0;width:100%;height:80px;background:linear-gradient(to bottom,#8bc34a,#4caf50);border-top-left-radius:40% 30px;border-top-right-radius:40% 30px;z-index:1}
        @media (max-width:768px){h1{font-size:2.2rem}.instructions{font-size:1.2rem}.balloon{width:120px;height:150px;font-size:3.5rem}.btn{padding:15px 30px;font-size:1.2rem}.score{font-size:1.5rem;padding:12px 25px}.animal{font-size:5rem}}
        @media (max-width:480px){h1{font-size:1.8rem}.game-container{height:55vh}.balloon{width:100px;height:130px;font-size:3rem}.controls{flex-direction:column;align-items:center}.btn{width:80%}.animal{font-size:4rem}}
    </style>
</head>
<body>
    <div class="header">
        <h1>🎈 动物气球乐园 🎈</h1>
        <p class="instructions">点击气球，听听小动物的叫声，看看会出现什么可爱的小动物！</p>
    </div>

    <div class="game-container" id="gameContainer">
        <div class="cloud cloud1"></div>
        <div class="cloud cloud2"></div>

        <!-- 6 个气球 -->
        <div class="balloon">🎈</div>
        <div class="balloon">🎈</div>
        <div class="balloon">🎈</div>
        <div class="balloon">🎈</div>
        <div class="balloon">🎈</div>
        <div class="balloon">🎈</div>

        <div class="ground"></div>
    </div>

    <div class="score">点击计数: <span id="scoreCount">0</span></div>

    <div class="controls">
        <button class="btn btn-music" id="musicBtn">🎵 播放音乐</button>
        <button class="btn btn-animals" id="animalBtn">🐻 更多动物</button>
        <button class="btn btn-reset" id="resetBtn">🔄 重新开始</button>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const gameContainer = document.getElementById('gameContainer');
            const scoreCount    = document.getElementById('scoreCount');
            const musicBtn      = document.getElementById('musicBtn');
            const animalBtn     = document.getElementById('animalBtn');
            const resetBtn      = document.getElementById('resetBtn');
            const balloons      = document.querySelectorAll('.balloon');

            let score = 0, musicPlaying = false, audioContext, backgroundMusic;

            /* =========  关键：文件名与仓库完全一致  ========= */
            const animals = [
                { emoji: '🐔', name: '公鸡', sound: '公鸡叫.mp3' },
                { emoji: '🐱', name: '小猫', sound: '猫叫.mp3'   },
                { emoji: '🐶', name: '小狗', sound: '狗叫.mp3'   },
                { emoji: '🐮', name: '奶牛', sound: '牛叫.mp3'   },
                { emoji: '🐸', name: '青蛙', sound: '青蛙叫.mp3' }
            ];

            /* ---------- 播放声音 ---------- */
            function playSound(soundFile) {
                const url = new URL(soundFile, location.href).href; // 绝对路径
                const audio = new Audio(url);
                audio.play().catch(e => console.error('播放失败', e));
                return audio;
            }

            /* ---------- 背景音乐 ---------- */
            function playBackgroundMusic() {
                const notes = [392, 440, 493.88, 523.25, 587.33];
                let i = 0;
                backgroundMusic = setInterval(() => {
                    if (!audioContext) return;
                    const osc = audioContext.createOscillator();
                    const g   = audioContext.createGain();
                    osc.type = 'sine';
                    osc.frequency.value = notes[i % notes.length];
                    g.gain.setValueAtTime(0.1, audioContext.currentTime);
                    g.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.5);
                    osc.connect(g).connect(audioContext.destination);
                    osc.start();
                    osc.stop(audioContext.currentTime + 0.5);
                    i++;
                }, 500);
            }
            function stopBackgroundMusic() {
                clearInterval(backgroundMusic);
            }

            /* ---------- 气球点击 ---------- */
            balloons.forEach(balloon => {
                balloon.addEventListener('click', function () {
                    score++;
                    scoreCount.textContent = score;

                    const pick = animals[Math.floor(Math.random() * animals.length)];
                    const audio = playSound(pick.sound);
                    setTimeout(() => { audio.pause(); audio.currentTime = 0; }, 3000);

                    setTimeout(() => {
                        this.style.backgroundColor = getRandomColor();
                        this.innerHTML = pick.emoji;
                        this.style.fontSize = '4.5rem';
                        this.style.zIndex = '10';

                        const label = document.createElement('div');
                        label.textContent = pick.name;
                        Object.assign(label.style, {
                            position: 'absolute', bottom: '-30px', left: '50%',
                            transform: 'translateX(-50%)', background: 'rgba(255,255,255,.8)',
                            padding: '5px 10px', borderRadius: '10px', fontSize: '1rem',
                            fontWeight: 'bold', color: '#6A0572'
                        });
                        this.appendChild(label);

                        setTimeout(() => {
                            this.innerHTML = '🎈';
                            this.style.fontSize = '4rem';
                            this.style.backgroundColor = '';
                            this.style.zIndex = '2';
                        }, 2000);
                    }, 500);
                });
            });

            function getRandomColor() {
                const colors = ['#FF6B6B','#4ECDC4','#FFD166','#6A0572','#F75C03','#1A936F','#118AB2'];
                return colors[Math.floor(Math.random() * colors.length)];
            }

            /* ---------- 按钮事件 ---------- */
            musicBtn.addEventListener('click', () => {
                if (!audioContext) {
                    audioContext = new (window.AudioContext || window.webkitAudioContext)();
                }
                if (!musicPlaying) {
                    playBackgroundMusic();
                    musicBtn.textContent = '🎵 暂停音乐';
                    musicBtn.style.background = 'linear-gradient(to bottom, #ff6b6b, #ff4f4f)';
                } else {
                    stopBackgroundMusic();
                    musicBtn.textContent = '🎵 播放音乐';
                    musicBtn.style.background = 'linear-gradient(to bottom, #4ECDC4, #2fa99e)';
                }
                musicPlaying = !musicPlaying;
            });

            animalBtn.addEventListener('click', () => {
                const pick = animals[Math.floor(Math.random() * animals.length)];
                const animal = document.createElement('div');
                animal.className = 'animal';
                animal.textContent = pick.emoji;
                animal.style.left = Math.random() * 80 + 10 + '%';
                animal.style.top  = Math.random() * 80 + 10 + '%';

                const label = document.createElement('div');
                label.textContent = pick.name;
                Object.assign(label.style, {
                    position: 'absolute', bottom: '-35px', left: '50%',
                    transform: 'translateX(-50%)', background: 'rgba(255,255,255,.8)',
                    padding: '5px 10px', borderRadius: '10px', fontSize: '1rem',
                    fontWeight: 'bold', color: '#6A0572'
                });
                animal.appendChild(label);
                gameContainer.appendChild(animal);

                playSound(pick.sound);
                setTimeout(() => animal.remove(), 3000);
            });

            resetBtn.addEventListener('click', () => {
                score = 0;
                scoreCount.textContent = score;
                balloons.forEach(b => {
                    b.innerHTML = '🎈';
                    b.style.backgroundColor = '';
                    b.style.fontSize = '4rem';
                    b.style.zIndex = '2';
                });
                if (musicPlaying) {
                    stopBackgroundMusic();
                    musicPlaying = false;
                    musicBtn.textContent = '🎵 播放音乐';
                    musicBtn.style.background = 'linear-gradient(to bottom, #4ECDC4, #2fa99e)';
                }
            });

            /* ---------- 页面加载后送 3 个小动物 ---------- */
            for (let i = 0; i < 3; i++) setTimeout(() => animalBtn.click(), i * 1000);
        });
    </script>
</body>
</html>
