<!DOCTYPE html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>Secret Santa 🎅</title>  
    <style>  
        * {  
            margin: 0;  
            padding: 0;  
            box-sizing: border-box;  
        }  
  
        body {  
            font-family: 'Georgia', serif;  
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);  
            min-height: 100vh;  
            display: flex;  
            justify-content: center;  
            align-items: center;  
            padding: 20px;  
            overflow-x: hidden;  
        }  
  
        /* Snowfall background effect */  
        .snowflake {  
            position: fixed;  
            top: -10px;  
            z-index: 1;  
            color: white;  
            font-size: 1em;  
            font-family: Arial, sans-serif;  
            text-shadow: 0 0 5px #000;  
            animation: fall linear infinite;  
            opacity: 0.8;  
        }  
  
        @keyframes fall {  
            to {  
                transform: translateY(100vh);  
            }  
        }  
  
        .container {  
            background: white;  
            padding: 40px;  
            border-radius: 20px;  
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);  
            max-width: 600px;  
            width: 100%;  
            position: relative;  
            z-index: 10;  
        }  
  
        h1 {  
            text-align: center;  
            color: #667eea;  
            font-size: 2.5em;  
            margin-bottom: 10px;  
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);  
        }  
  
        .subtitle {  
            text-align: center;  
            color: #764ba2;  
            font-size: 1.2em;  
            margin-bottom: 30px;  
            font-style: italic;  
        }  
  
        .form-group {  
            margin-bottom: 20px;  
        }  
  
        label {  
            display: block;  
            margin-bottom: 8px;  
            color: #333;  
            font-weight: bold;  
            font-size: 1.1em;  
        }  
  
        select, input {  
            width: 100%;  
            padding: 15px;  
            font-size: 1.1em;  
            border: 2px solid #e0e0e0;  
            border-radius: 10px;  
            transition: border-color 0.3s;  
            font-family: inherit;  
        }  
  
        select:focus, input:focus {  
            outline: none;  
            border-color: #667eea;  
        }  
  
        .reveal-btn {  
            width: 100%;  
            padding: 18px;  
            font-size: 1.3em;  
            font-weight: bold;  
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);  
            color: white;  
            border: none;  
            border-radius: 15px;  
            cursor: pointer;  
            transition: transform 0.2s, box-shadow 0.2s;  
            margin-top: 20px;  
            text-transform: uppercase;  
            letter-spacing: 1px;  
        }  
  
        .reveal-btn:hover {  
            transform: translateY(-2px);  
            box-shadow: 0 10px 25px rgba(102, 126, 234, 0.4);  
        }  
  
        .reveal-btn:active {  
            transform: translateY(0);  
        }  
  
        .reveal-btn:disabled {  
            opacity: 0.6;  
            cursor: not-allowed;  
        }  
  
        /* Animation Container */  
        .animation-container {  
            display: none;  
            margin-top: 40px;  
            position: relative;  
            min-height: 400px;  
        }  
  
        .animation-container.active {  
            display: block;  
        }  
  
        /* ============================================ */  
        /* SNOW GLOBE ANIMATION */  
        /* ============================================ */  
        .snow-globe {  
            width: 250px;  
            height: 300px;  
            margin: 0 auto 40px;  
            position: relative;  
            opacity: 0;  
            transform: scale(0.8);  
            transition: opacity 0.5s, transform 0.5s;  
        }  
  
        .snow-globe.active {  
            opacity: 1;  
            transform: scale(1);  
        }  
  
        .globe {  
            width: 250px;  
            height: 250px;  
            border-radius: 50%;  
            background: linear-gradient(135deg, rgba(255,255,255,0.3) 0%, rgba(255,255,255,0.1) 100%);  
            border: 3px solid #ccc;  
            position: relative;  
            overflow: hidden;  
            box-shadow:   
                inset 0 0 30px rgba(255,255,255,0.5),  
                0 10px 30px rgba(0,0,0,0.2);  
        }  
  
        .globe-base {  
            width: 200px;  
            height: 50px;  
            background: linear-gradient(135deg, #8B4513 0%, #654321 100%);  
            border-radius: 10px;  
            margin: 0 auto;  
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);  
        }  
  
        .snow-particle {  
            position: absolute;  
            background: white;  
            border-radius: 50%;  
            opacity: 0.8;  
            animation: snowfall 3s linear infinite;  
        }  
  
        @keyframes snowfall {  
            0% {  
                transform: translateY(-10px) translateX(0);  
                opacity: 0;  
            }  
            10% {  
                opacity: 1;  
            }  
            90% {  
                opacity: 1;  
            }  
            100% {  
                transform: translateY(260px) translateX(20px);  
                opacity: 0;  
            }  
        }  
  
        .globe-content {  
            position: absolute;  
            top: 50%;  
            left: 50%;  
            transform: translate(-50%, -50%);  
            text-align: center;  
            z-index: 10;  
        }  
  
        .recipient-name {  
            font-size: 2em;  
            font-weight: bold;  
            color: #667eea;  
            text-shadow: 2px 2px 4px rgba(255,255,255,0.8);  
            opacity: 0;  
            transition: opacity 1s;  
        }  
  
        .recipient-name.revealed {  
            opacity: 1;  
        }  
  
        /* ============================================ */  
        /* GIFT BOX ANIMATION */  
        /* ============================================ */  
        .gift-box-container {  
            width: 250px;  
            height: 300px;  
            margin: 0 auto;  
            position: relative;  
            perspective: 1000px;  
            opacity: 0;  
            transform: scale(0.8);  
            transition: opacity 0.5s, transform 0.5s;  
        }  
  
        .gift-box-container.active {  
            opacity: 1;  
            transform: scale(1);  
        }  
  
        .gift-box {  
            width: 200px;  
            height: 200px;  
            margin: 0 auto;  
            position: relative;  
            transform-style: preserve-3d;  
        }  
  
        .box-bottom {  
            width: 200px;  
            height: 200px;  
            background: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%);  
            border-radius: 10px;  
            position: relative;  
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);  
        }  
  
        .box-lid {  
            width: 200px;  
            height: 60px;  
            background: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%);  
            border-radius: 10px 10px 5px 5px;  
            position: absolute;  
            top: -60px;  
            left: 0;  
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);  
            transform-origin: bottom;  
            transition: transform 1s ease-in-out;  
        }  
  
        .gift-box.opening .box-lid {  
            transform: rotateX(-120deg) translateY(-20px);  
        }  
  
        .ribbon-vertical {  
            width: 30px;  
            height: 200px;  
            background: linear-gradient(90deg, #f1c40f 0%, #f39c12 100%);  
            position: absolute;  
            top: 0;  
            left: 50%;  
            transform: translateX(-50%);  
            z-index: 1;  
        }  
  
        .ribbon-horizontal {  
            width: 200px;  
            height: 30px;  
            background: linear-gradient(180deg, #f1c40f 0%, #f39c12 100%);  
            position: absolute;  
            top: 50%;  
            left: 0;  
            transform: translateY(-50%);  
            z-index: 1;  
        }  
  
        .bow {  
            width: 60px;  
            height: 60px;  
            background: radial-gradient(circle, #f1c40f 0%, #f39c12 100%);  
            border-radius: 50%;  
            position: absolute;  
            top: -90px;  
            left: 50%;  
            transform: translateX(-50%);  
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);  
            z-index: 2;  
        }  
  
        .bow::before,  
        .bow::after {  
            content: '';  
            position: absolute;  
            width: 40px;  
            height: 40px;  
            background: #f1c40f;  
            border-radius: 50% 50% 0 50%;  
            top: 10px;  
        }  
  
        .bow::before {  
            left: -30px;  
            transform: rotate(-45deg);  
        }  
  
        .bow::after {  
            right: -30px;  
            transform: rotate(45deg);  
        }  
  
        .gift-content {  
            position: absolute;  
            top: 50%;  
            left: 50%;  
            transform: translate(-50%, -50%);  
            font-size: 2em;  
            font-weight: bold;  
            color: white;  
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);  
            opacity: 0;  
            transition: opacity 1s;  
            z-index: 0;  
        }  
  
        .gift-content.revealed {  
            opacity: 1;  
        }  
  
        /* Confetti effect */  
        .confetti {  
            position: fixed;  
            width: 10px;  
            height: 10px;  
            background: #f1c40f;  
            position: absolute;  
            animation: confetti-fall 3s linear;  
        }  
  
        @keyframes confetti-fall {  
            to {  
                transform: translateY(400px) rotate(360deg);  
                opacity: 0;  
            }  
        }  
  
        .result-text {  
            text-align: center;  
            margin-top: 30px;  
            font-size: 1.2em;  
            color: #333;  
        }  
  
        .success-message {  
            background: #d4edda;  
            border: 2px solid #c3e6cb;  
            color: #155724;  
            padding: 20px;  
            border-radius: 10px;  
            margin-top: 20px;  
            text-align: center;  
        }  
  
        .error-message {  
            background: #f8d7da;  
            border: 2px solid #f5c6cb;  
            color: #721c24;  
            padding: 20px;  
            border-radius: 10px;  
            margin-top: 20px;  
            text-align: center;  
        }  
  
        .loading {  
            text-align: center;  
            margin-top: 20px;  
            font-size: 1.2em;  
            color: #667eea;  
        }  
  
        @media (max-width: 600px) {  
            .container {  
                padding: 20px;  
            }  
  
            h1 {  
                font-size: 2em;  
            }  
  
            .snow-globe,  
            .gift-box-container {  
                width: 200px;  
                height: 250px;  
            }  
  
            .globe {  
                width: 200px;  
                height: 200px;  
            }  
  
            .gift-box,  
            .box-bottom {  
                width: 160px;  
                height: 160px;  
            }  
  
            .box-lid {  
                width: 160px;  
            }  
        }  
    </style>  
</head>  
<body>  
    <!-- Falling snowflakes background -->  
    <div id="snowfall"></div>  
  
    <div class="container">  
        <h1>🎅 Secret Santa 🎄</h1>  
        <p class="subtitle">Discover your gift recipients!</p>  
  
        <!-- Form Section -->  
        <div id="form-section">  
            <div class="form-group">  
                <label for="name-select">Select Your Name:</label>  
                <select id="name-select">  
                    <option value="">-- Choose your name --</option>  
                </select>  
            </div>  
  
            <div class="form-group">  
                <label for="email-input">Enter Your Email:</label>  
                <input type="email" id="email-input" placeholder="your.email@example.com">  
            </div>  
  
            <button class="reveal-btn" id="reveal-btn">  
                🎁 Reveal My Secret Santa! 🎁  
            </button>  
        </div>  
  
        <!-- Animation Section -->  
        <div class="animation-container" id="animation-container">  
            <div class="result-text">  
                <h2>Your Recipients Are...</h2>  
            </div>  
  
            <!-- Snow Globe for First Recipient -->  
            <div class="snow-globe" id="snow-globe">  
                <div class="globe">  
                    <div class="globe-content">  
                        <div class="recipient-name" id="recipient1"></div>  
                    </div>  
                </div>  
                <div class="globe-base"></div>  
            </div>  
  
            <!-- Gift Box for Second Recipient -->  
            <div class="gift-box-container" id="gift-box-container">  
                <div class="gift-box" id="gift-box">  
                    <div class="bow"></div>  
                    <div class="box-lid"></div>  
                    <div class="box-bottom">  
                        <div class="ribbon-vertical"></div>  
                        <div class="ribbon-horizontal"></div>  
                        <div class="gift-content" id="recipient2"></div>  
                    </div>  
                </div>  
            </div>  
        </div>  
  
        <!-- Messages -->  
        <div id="message-area"></div>  
    </div>  
  
    <script>  
        // Configuration - UPDATE THIS WITH YOUR CLOUDFLARE WORKER URL  
        const API_URL = 'https://your-worker.your-subdomain.workers.dev';  
  
        // Create snowfall effect  
        function createSnowfall() {  
            const snowfall = document.getElementById('snowfall');  
            for (let i = 0; i < 50; i++) {  
                const snowflake = document.createElement('div');  
                snowflake.classList.add('snowflake');  
                snowflake.innerHTML = '❄';  
                snowflake.style.left = Math.random() * 100 + '%';  
                snowflake.style.animationDuration = (Math.random() * 3 + 2) + 's';  
                snowflake.style.animationDelay = Math.random() * 5 + 's';  
                snowflake.style.fontSize = (Math.random() * 10 + 10) + 'px';  
                snowfall.appendChild(snowflake);  
            }  
        }  
  
        // Load family members  
        async function loadFamily() {  
            try {  
                const response = await fetch(`${API_URL}/api/family`);  
                const family = await response.json();  
                  
                const select = document.getElementById('name-select');  
                family.forEach(member => {  
                    const option = document.createElement('option');  
                    option.value = member.name;  
                    option.textContent = member.name;  
                    select.appendChild(option);  
                });  
            } catch (error) {  
                console.error('Error loading family:', error);  
                showMessage('Error loading family members. Please refresh the page.', 'error');  
            }  
        }  
  
        // Create snow particles in globe  
        function createSnowParticles() {  
            const globe = document.querySelector('.globe');  
            for (let i = 0; i < 30; i++) {  
                const particle = document.createElement('div');  
                particle.classList.add('snow-particle');  
                particle.style.left = Math.random() * 100 + '%';  
                particle.style.width = (Math.random() * 5 + 2) + 'px';  
                particle.style.height = particle.style.width;  
                particle.style.animationDelay = Math.random() * 3 + 's';  
                particle.style.animationDuration = (Math.random() * 2 + 2) + 's';  
                globe.appendChild(particle);  
            }  
        }  
  
        // Create confetti  
        function createConfetti() {  
            const colors = ['#f1c40f', '#e74c3c', '#3498db', '#2ecc71', '#9b59b6'];  
            for (let i = 0; i < 50; i++) {  
                const confetti = document.createElement('div');  
                confetti.classList.add('confetti');  
                confetti.style.left = Math.random() * 100 + '%';  
                confetti.style.top = '-10px';  
                confetti.style.background = colors[Math.floor(Math.random() * colors.length)];  
                confetti.style.animationDelay = Math.random() * 0.5 + 's';  
                document.body.appendChild(confetti);  
                  
                setTimeout(() => confetti.remove(), 3000);  
            }  
        }  
  
        // Show message  
        function showMessage(text, type) {  
            const messageArea = document.getElementById('message-area');  
            const div = document.createElement('div');  
            div.className = type === 'error' ? 'error-message' : 'success-message';  
            div.textContent = text;  
            messageArea.innerHTML = '';  
            messageArea.appendChild(div);  
        }  
  
        // Reveal animation sequence  
        async function revealRecipients(recipient1, recipient2) {  
            const animationContainer = document.getElementById('animation-container');  
            const formSection = document.getElementById('form-section');  
            const snowGlobe = document.getElementById('snow-globe');  
            const giftBox = document.getElementById('gift-box-container');  
            const giftBoxElement = document.getElementById('gift-box');  
            const recipient1El = document.getElementById('recipient1');  
            const recipient2El = document.getElementById('recipient2');  
  
            // Hide form  
            formSection.style.display = 'none';  
              
            // Show animation container  
            animationContainer.classList.add('active');  
  
            // Create snow particles  
            createSnowParticles();  
  
            // Step 1: Show snow globe (1 second delay)  
            await new Promise(resolve => setTimeout(resolve, 500));  
            snowGlobe.classList.add('active');  
  
            // Step 2: Let snow fall (2 seconds)  
            await new Promise(resolve => setTimeout(resolve, 2500));  
  
            // Step 3: Reveal first recipient in snow globe  
            recipient1El.textContent = recipient1;  
            recipient1El.classList.add('revealed');  
  
            // Step 4: Wait then show gift box (2 seconds)  
            await new Promise(resolve => setTimeout(resolve, 2000));  
            giftBox.classList.add('active');  
  
            // Step 5: Open gift box (1 second delay)  
            await new Promise(resolve => setTimeout(resolve, 1000));  
            giftBoxElement.classList.add('opening');  
  
            // Step 6: Reveal second recipient (wait for lid animation)  
            await new Promise(resolve => setTimeout(resolve, 1000));  
            recipient2El.textContent = recipient2;  
            recipient2El.classList.add('revealed');  
  
            // Step 7: Confetti!  
            createConfetti();  
  
            // Step 8: Show success message  
            await new Promise(resolve => setTimeout(resolve, 2000));  
            showMessage('Check your email for your assignments! 🎄', 'success');  
        }  
  
        // Handle reveal button click  
        document.getElementById('reveal-btn').addEventListener('click', async () => {  
            const name = document.getElementById('name-select').value;  
            const email = document.getElementById('email-input').value;  
  
            if (!name) {  
                showMessage('Please select your name!', 'error');  
                return;  
            }  
  
            if (!email || !email.includes('@')) {  
                showMessage('Please enter a valid email address!', 'error');  
                return;  
            }  
  
            const btn = document.getElementById('reveal-btn');  
            btn.disabled = true;  
            btn.textContent = '✨ Generating Magic... ✨';  
  
            try {  
                const response = await fetch(`${API_URL}/api/get-assignment`, {  
                    method: 'POST',  
                    headers: {  
                        'Content-Type': 'application/json'  
                    },  
                    body: JSON.stringify({ name, email })  
                });  
  
                const data = await response.json();  
  
                if (!response.ok) {  
                    throw new Error(data.error || 'Failed to get assignment');  
                }  
  
                // Start the animation sequence  
                await revealRecipients(data.recipient1, data.recipient2);  
  
            } catch (error) {  
                console.error('Error:', error);  
                showMessage('Something went wrong! Please try again.', 'error');  
                btn.disabled = false;  
                btn.textContent = '🎁 Reveal My Secret Santa! 🎁';  
            }  
        });  
  
        // Initialize  
        createSnowfall();  
        loadFamily();  
    </script>  
</body>  
</html>  
