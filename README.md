# cheerup-na-hehe
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Digital Letter for Niks</title>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;700&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 50%, #fecfef 100%);
            font-family: 'Poppins', sans-serif;
            overflow: hidden;
            position: relative;
        }

        body::before {
            content: '';
            position: absolute;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 1px, transparent 1px);
            background-size: 50px 50px;
            animation: float 20s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translate(-50%, -50%) rotate(0deg); }
            50% { transform: translate(-50%, -50%) rotate(180deg); }
        }

        .envelope {
            position: relative;
            width: 300px;
            height: 200px;
            background: linear-gradient(135deg, #ff6b6b 0%, #ff8787 100%);
            cursor: pointer;
            transition: all 0.5s ease;
            box-shadow: 0 10px 30px rgba(255, 107, 107, 0.3);
            border-radius: 10px;
            overflow: hidden;
        }

        .envelope:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(255, 107, 107, 0.4);
        }

        .envelope.flap-open .flap {
            transform: rotateX(-180deg);
        }

        .envelope-body {
            position: absolute;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #ff6b6b 0%, #ff8787 100%);
            clip-path: polygon(0% 0%, 100% 0%, 100% 85%, 50% 100%, 0% 85%);
            z-index: 1;
            border-radius: 10px;
        }

        .flap {
            position: absolute;
            top: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #ff5252 0%, #ff6b6b 100%);
            clip-path: polygon(0% 0%, 50% 50%, 100% 0%);
            transform-origin: top;
            transition: transform 0.6s ease;
            z-index: 2;
            border-radius: 10px 10px 0 0;
        }

        .heart {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 0;
            transition: all 0.5s ease;
        }

        .heart svg {
            width: 80px;
            height: 80px;
            fill: #fff;
            filter: drop-shadow(0 0 10px rgba(255, 255, 255, 0.5));
            animation: heartbeat 2s ease-in-out infinite;
        }

        @keyframes heartbeat {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }

        .letter {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0);
            background: white;
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            width: 90%;
            max-width: 500px;
            max-height: 80vh;
            overflow-y: auto;
            opacity: 0;
            transition: all 0.5s ease;
            z-index: 3;
        }

        .letter::-webkit-scrollbar {
            width: 8px;
        }

        .letter::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 10px;
        }

        .letter::-webkit-scrollbar-thumb {
            background: #ff6b6b;
            border-radius: 10px;
        }

        .letter.show {
            transform: translate(-50%, -50%) scale(1);
            opacity: 1;
        }

        .letter h2 {
            color: #ff6b6b;
            margin-bottom: 20px;
            font-family: 'Dancing Script', cursive;
            font-size: 2.5em;
            text-align: center;
            background: linear-gradient(45deg, #ff6b6b, #ff8787);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .letter p {
            color: #333;
            line-height: 2;
            margin-bottom: 15px;
            font-size: 1.1em;
            animation: fadeInUp 0.6s ease forwards;
            opacity: 0;
            transform: translateY(20px);
        }

        @keyframes fadeInUp {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .letter p:nth-child(3) { animation-delay: 0.1s; }
        .letter p:nth-child(4) { animation-delay: 0.2s; }
        .letter p:nth-child(5) { animation-delay: 0.3s; }
        .letter p:nth-child(6) { animation-delay: 0.4s; }
        .letter p:nth-child(7) { animation-delay: 0.5s; }

        .signature {
            text-align: right;
            font-style: italic;
            color: #ff6b6b;
            font-weight: bold;
            font-family: 'Dancing Script', cursive;
            font-size: 1.3em;
            margin-top: 30px;
        }

        .close-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            background: #ff6b6b;
            color: white;
            border: none;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            font-size: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 2px 10px rgba(255, 107, 107, 0.3);
        }

        .close-btn:hover {
            background: #ff5252;
            transform: rotate(90deg);
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.5);
        }

        .floating-hearts {
            position: absolute;
            width: 100%;
            height: 100%;
            overflow: hidden;
            pointer-events: none;
        }

        .floating-heart {
            position: absolute;
            color: #ff6b6b;
            font-size: 20px;
            animation: floatUp 15s linear infinite;
            opacity: 0.7;
        }

        @keyframes floatUp {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 0;
            }
            10% {
                opacity: 0.7;
            }
            90% {
                opacity: 0.7;
            }
            100% {
                transform: translateY(-100vh) rotate(360deg);
                opacity: 0;
            }
        }

        @media (max-width: 600px) {
            .letter {
                padding: 30px 20px;
                width: 95%;
            }

            .letter h2 {
                font-size: 2em;
            }

            .letter p {
                font-size: 1em;
            }
        }
    </style>
</head>
<body>
<div class="floating-hearts" id="floatingHearts"></div>

<div class="envelope" id="envelope">
    <div class="envelope-body"></div>
    <div class="flap"></div>
    <div class="heart">
        <svg viewBox="0 0 32 32">
            <path d="M16,28.261c0,0-14-7.926-14-17.046c0-9.356,13.159-10.399,14-0.454c1.011-9.938,14-8.903,14,0.454
                C30,20.335,16,28.261,16,28.261z"/>
        </svg>
    </div>
</div>

<div class="letter" id="letter">
    <button class="close-btn" id="closeBtn">×</button>
    <h2>Cheer up na hehe</h2>
    <p>Hi Niks, I hope you're doing well right now.</p>
    <p>Wag ka na mag breakdown, the guy doesn't deserve you. You'll eventually find the guy for you, and if hindi man, magiging successful ka rin naman.</p>
    <p>I believe in you, I know this isn't much but I hope it cheers you up.</p>
    <p>Hehe, keep being you always, I'm happy to have met you and I hope we can get to know each other more hehe.</p>
    <p class="signature">Mwamwa -D</p>
</div>

<script>
    // Create floating hearts
    function createFloatingHeart() {
        const heart = document.createElement('div');
        heart.className = 'floating-heart';
        heart.innerHTML = '❤';
        heart.style.left = Math.random() * 100 + '%';
        heart.style.animationDelay = Math.random() * 15 + 's';
        heart.style.fontSize = (Math.random() * 20 + 10) + 'px';
        document.getElementById('floatingHearts').appendChild(heart);

        setTimeout(() => {
            heart.remove();
        }, 15000);
    }

    // Create initial floating hearts
    for (let i = 0; i < 5; i++) {
        setTimeout(createFloatingHeart, i * 2000);
    }

    // Continue creating hearts
    setInterval(createFloatingHeart, 3000);

    const envelope = document.getElementById('envelope');
    const letter = document.getElementById('letter');
    const closeBtn = document.getElementById('closeBtn');
    const heart = document.querySelector('.heart');

    envelope.addEventListener('click', function() {
        envelope.classList.add('flap-open');
        heart.style.transform = 'translate(-50%, -50%) scale(2)';
        heart.style.opacity = '0';

        setTimeout(() => {
            envelope.style.transform = 'translateY(100px) scale(0.5)';
            envelope.style.opacity = '0';
            letter.classList.add('show');
        }, 500);
    });

    closeBtn.addEventListener('click', function() {
        letter.classList.remove('show');

        setTimeout(() => {
            envelope.classList.remove('flap-open');
            envelope.style.transform = 'translateY(0) scale(1)';
            envelope.style.opacity = '1';
            heart.style.transform = 'translate(-50%, -50%) scale(1)';
            heart.style.opacity = '1';
        }, 500);
    });

    // Add click sound effect (optional)
    envelope.addEventListener('click', function() {
        // Create audio context for click sound
        const audioContext = new (window.AudioContext || window.webkitAudioContext)();
        const oscillator = audioContext.createOscillator();
        const gainNode = audioContext.createGain();

        oscillator.connect(gainNode);
        gainNode.connect(audioContext.destination);

        oscillator.frequency.value = 800;
        oscillator.type = 'sine';
        gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
        gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.3);

        oscillator.start(audioContext.currentTime);
        oscillator.stop(audioContext.currentTime + 0.3);
    });
</script>
</body>
</html>
