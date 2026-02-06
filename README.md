<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Color Bet Games</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Orbitron', sans-serif;
            text-align: center;
            background: linear-gradient(135deg, #0f0f23, #1a1a2e);
            color: #fff;
            margin: 0;
            padding: 20px;
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }
        body::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle, rgba(0, 255, 255, 0.1) 0%, transparent 70%);
            animation: float 10s ease-in-out infinite;
            pointer-events: none;
        }
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }
        .game-container {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            margin: 0 auto;
            max-width: 800px;
            box-shadow: 0 0 40px rgba(0, 255, 255, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.2);
            display: flex;
            flex-direction: column;
        }
        .tabs {
            display: flex;
            justify-content: center;
            margin-bottom: 20px;
        }
        .tab {
            padding: 10px 20px;
            margin: 0 10px;
            background: rgba(0, 0, 0, 0.3);
            color: #ccc;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .tab.active {
            background: rgba(0, 255, 255, 0.3);
            color: #fff;
            box-shadow: 0 0 20px rgba(0, 255, 255, 0.5);
        }
        .tab:hover {
            transform: scale(1.05);
        }
        .game-section {
            display: none;
        }
        .game-section.active {
            display: block;
        }
        h1 {
            font-size: 3rem;
            text-shadow: 0 0 20px #00ffff;
            margin-bottom: 10px;
        }
        p {
            font-size: 1.2rem;
            margin-bottom: 30px;
        }
        .colors {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            margin: 20px 0;
        }
        .color-btn {
            width: 120px;
            height: 120px;
            margin: 15px;
            border: none;
            border-radius: 50%;
            cursor: pointer;
            font-size: 18px;
            font-weight: bold;
            color: white;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.8);
            transition: all 0.3s ease;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
            position: relative;
        }
        .color-btn:hover {
            transform: scale(1.1);
            box-shadow: 0 0 30px rgba(255, 255, 255, 0.8);
        }
        .red { background: radial-gradient(circle, #ff0000, #cc0000); }
        .blue { background: radial-gradient(circle, #0000ff, #0000cc); }
        .green { background: radial-gradient(circle, #00ff00, #00cc00); }
        .yellow { background: radial-gradient(circle, #ffff00, #cccc00); color: black; }
        .purple { background: radial-gradient(circle, #800080, #660066); }
        .orange { background: radial-gradient(circle, #ff6600, #cc5500); }
        .selected {
            animation: pulse 1s infinite;
            box-shadow: 0 0 40px rgba(255, 255, 255, 1);
        }
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        #pull-btn, #spin-btn, #customize-btn {
            padding: 15px 30px;
            font-size: 20px;
            background: linear-gradient(45deg, #ff0080, #8000ff);
            color: white;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            margin: 10px;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.8);
            box-shadow: 0 0 20px rgba(255, 0, 128, 0.5);
            transition: all 0.3s ease;
            font-family: 'Orbitron', sans-serif;
            font-weight: bold;
        }
        #pull-btn:hover, #spin-btn:hover, #customize-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 0 30px rgba(255, 0, 128, 0.8);
        }
        #results, #wheel-results {
            margin-top: 30px;
            font-size: 1.5rem;
            min-height: 200px;
        }
        .dice {
            display: inline-block;
            width: 100px;
            height: 100px;
            margin: 15px;
            border-radius: 15px;
            font-size: 24px;
            font-weight: bold;
            color: white;
            line-height: 100px;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.8);
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
            transition: all 0.5s ease;
        }
        .rolling {
            animation: roll 0.3s infinite linear;
        }
        @keyframes roll {
            0% { transform: rotate(0deg) scale(1); background: radial-gradient(circle, #ff0000, #cc0000); }
            16% { transform: rotate(60deg) scale(1.1); background: radial-gradient(circle, #0000ff, #0000cc); }
            33% { transform: rotate(120deg) scale(1); background: radial-gradient(circle, #00ff00, #00cc00); }
            50% { transform: rotate(180deg) scale(0.9); background: radial-gradient(circle, #ffff00, #cccc00); }
            66% { transform: rotate(240deg) scale(1); background: radial-gradient(circle, #800080, #660066); }
            83% { transform: rotate(300deg) scale(1.1); background: radial-gradient(circle, #ff6600, #cc5500); }
            100% { transform: rotate(360deg) scale(1); background: radial-gradient(circle, #ff0000, #cc0000); }
        }
        .flash {
            animation: flash 0.2s infinite alternate;
        }
        @keyframes flash {
            0% { opacity: 1; }
            100% { opacity: 0.5; }
        }
        .win {
            color: #00ff00;
            text-shadow: 0 0 20px #00ff00;
            animation: confetti 1s ease-out;
        }
        .lose {
            color: #ff0000;
            text-shadow: 0 0 20px #ff0000;
        }
        @keyframes confetti {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); }
            100% { transform: scale(1); }
        }
        #countdown {
            font-size: 2rem;
            color: #ffff00;
            text-shadow: 0 0 20px #ffff00;
            margin: 20px 0;
        }
        #wheel-container {
            position: relative;
            margin: 20px auto;
            width: 300px;
            height: 300px;
        }
        #wheel-canvas {
            border-radius: 50%;
            box-shadow: 0 0 30px rgba(0, 255, 255, 0.5);
        }
        #wheel-pointer {
            position: absolute;
            top: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 0;
            height: 0;
            border-left: 10px solid transparent;
            border-right: 10px solid transparent;
            border-top: 20px solid #ffff00;
            filter: drop-shadow(0 0 10px #ffff00);
        }
        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(10px);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            background: rgba(15, 15, 35, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            max-width: 600px;
            width: 90%;
            box-shadow: 0 0 50px rgba(0, 255, 255, 0.5);
            border: 1px solid rgba(0, 255, 255, 0.3);
            position: relative;
            animation: modalSlideIn 0.3s ease-out;
        }
        @keyframes modalSlideIn {
            from {
                opacity: 0;
                transform: translateY(-50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        .modal-content h2 {
            color: #00ffff;
            text-shadow: 0 0 20px #00ffff;
            margin-bottom: 20px;
            font-size: 2rem;
        }
        .modal-content .close {
            position: absolute;
            top: 15px;
            right: 20px;
            font-size: 28px;
            color: #fff;
            cursor: pointer;
            transition: all 0.3s ease;
            width: 30px;
            height: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
        }
        .modal-content .close:hover {
            color: #ff0000;
            background: rgba(255, 0, 0, 0.1);
            text-shadow: 0 0 10px #ff0000;
            transform: rotate(90deg);
        }
        .modal-content label {
            display: block;
            margin: 15px 0 10px 0;
            font-size: 1rem;
            color: #00ffff;
            text-shadow: 0 0 10px rgba(0, 255, 255, 0.5);
        }
        .modal-content input {
            width: calc(50% - 15px);
            padding: 10px;
            margin: 5px;
            background: rgba(0, 0, 0, 0.4);
            color: white;
            border: 1px solid rgba(0, 255, 255, 0.3);
            border-radius: 10px;
            font-family: 'Orbitron', sans-serif;
            font-size: 0.9rem;
            transition: all 0.3s ease;
            box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.3);
        }
        .modal-content input:focus {
            outline: none;
            border-color: #00ffff;
            box-shadow: 0 0 15px rgba(0, 255, 255, 0.5), inset 0 0 10px rgba(0, 255, 255, 0.1);
        }
        .modal-content input::placeholder {
            color: rgba(255, 255, 255, 0.4);
        }
        .modal-content button {
            padding: 12px 25px;
            background: linear-gradient(45deg, #00ff00, #008000);
            color: white;
            border: none;
            border-radius: 15px;
            cursor: pointer;
            margin-top: 20px;
            font-family: 'Orbitron', sans-serif;
            font-weight: bold;
            font-size: 1rem;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.8);
            box-shadow: 0 0 20px rgba(0, 255, 0, 0.3);
            transition: all 0.3s ease;
        }
        .modal-content button:hover {
            transform: scale(1.05);
            box-shadow: 0 0 30px rgba(0, 255, 0, 0.6);
        }
        .modal-content button:active {
            transform: scale(0.98);
        }
        /* Admin Panel as Footer */
        .admin-footer {
            margin-top: auto;
            padding: 10px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            background: rgba(0, 0, 0, 0.2);
            border-radius: 0 0 20px 20px;
            font-size: 0.8rem;
            color: #aaa;
        }
    </style>
</head>
<body>
    <div class="game-container">
        <div class="tabs">
            <button class="tab active" data-game="color">Color Game</button>
            <button class="tab" data-game="wheel">Spin the Wheel</button>
        </div>

        <div id="color-game" class="game-section active">
            <h1>Color Bet Game</h1>
            <p>Choose a color to bet on, then pull the lever for the ultimate roll!</p>
            <div class="colors">
                <button class="color-btn red" data-color="red">Red</button>
                <button class="color-btn blue" data-color="blue">Blue</button>
                <button class="color-btn green" data-color="green">Green</button>
                <button class="color-btn yellow" data-color="yellow">Yellow</button>
                <button class="color-btn purple" data-color="purple">Purple</button>
                <button class="color-btn orange" data-color="orange">Orange</button>
            </div>
            <button id="pull-btn">Pull Lever</button>
            <div id="countdown"></div>
            <div id="results"></div>
        </div>

        <div id="wheel-game" class="game-section">
            <h1>Spin the Wheel</h1>
            <p>Customize and spin for prizes!</p>
            <button id="customize-btn">Customize Wheel</button>
            <div id="wheel-container">
                <canvas id="wheel-canvas" width="300" height="300"></canvas>
                <div id="wheel-pointer"></div>
            </div>
            <button id="spin-btn">Spin Wheel</button>
            <div id="wheel-results"></div>
        </div>

        <div id="customize-modal" class="modal">
            <div class="modal-content">
                <span class="close">&times;</span>
                <h2>Customize Wheel Segments</h2>
                <label>Enter up to 10 segments:</label>
                <input type="text" id="segment1" placeholder="Segment 1">
                <input type="text" id="segment2" placeholder="Segment 2">
                <input type="text" id="segment3" placeholder="Segment 3">
                <input type="text" id="segment4" placeholder="Segment 4">
                <input type="text" id="segment5" placeholder="Segment 5">
                <input type="text" id="segment6" placeholder="Segment 6">
                <input type="text" id="segment7" placeholder="Segment 7">
                <input type="text" id="segment8" placeholder="Segment 8">
                <input type="text" id="segment9" placeholder="Segment 9">
                <input type="text" id="segment10" placeholder="Segment 10">
                <button id="update-wheel">Update Wheel</button>
            </div>
        </div>

        <div class="admin-footer">
            <p>© 2023 Color Games</p>
        </div>
    </div>

    <script>
        const colors = ['red', 'blue', 'green', 'yellow', 'purple', 'orange'];
        const colorHex = { red: '#ff0000', blue: '#0000ff', green: '#00ff00', yellow: '#ffff00', purple: '#800080', orange: '#ff6600' };
        let selectedColor = null;
        let adminGame = 'color';
        let excludedColor = { color: null, wheel: null };
        let forceWin = { color: false, wheel: false };
        let wheelSegments = ['Win $10', 'Lose', 'Bonus', 'Try Again', 'Jackpot', 'Nothing']; // Default
        let isSpinning = false;
        let adminWindow = null; // To keep track of the admin window

        // Tab switching
        document.querySelectorAll('.tab').forEach(tab => {
            tab.addEventListener('click', () => {
                document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
                document.querySelectorAll('.game-section').forEach(s => s.classList.remove('active'));
                tab.classList.add('active');
                document.getElementById(tab.dataset.game + '-game').classList.add('active');
                adminGame = tab.dataset.game;
            });
        });

        // Color selection
        document.querySelectorAll('.color-btn').forEach(btn => {
            btn.addEventListener('click', () => {
                document.querySelectorAll('.color-btn').forEach(b => b.classList.remove('selected'));
                btn.classList.add('selected');
                selectedColor = btn.dataset.color;
            });
        });

        // Color Game Logic
        document.getElementById('pull-btn').addEventListener('click', () => {
            if (!selectedColor) {
                alert('Please select a color first!');
                return;
            }

            const resultsDiv = document.getElementById('results');
            const countdownDiv = document.getElementById('countdown');

            resultsDiv.innerHTML = '';
            countdownDiv.textContent = '3';
            document.body.classList.add('flash');

            let count = 3;
            const countdownInterval = setInterval(() => {
                count--;
                if (count > 0) {
                    countdownDiv.textContent = count;
                } else {
                    clearInterval(countdownInterval);
                    countdownDiv.textContent = '';
                    document.body.classList.remove('flash');

                    resultsDiv.innerHTML = '<h2>Rolling...</h2>';
                    const diceElements = [];
                    for (let i = 0; i < 3; i++) {
                        const diceDiv = document.createElement('div');
                        diceDiv.className = 'dice rolling';
                        diceDiv.textContent = '?';
                        resultsDiv.appendChild(diceDiv);
                        diceElements.push(diceDiv);
                    }

                    setTimeout(() => {
                        diceElements.forEach(dice => dice.classList.remove('rolling'));

                        let availableColors = colors.filter(c => c !== excludedColor.color);
                        const rolledColors = [];

                        if (forceWin.color) {
                            // NEW "SUBTLE WIN" LOGIC
                            // 1. Decide which one is the guaranteed win (0, 1, or 2)
                            const winIndex = Math.floor(Math.random() * 3);
                            
                            // 2. Decide if we allow 'Jackpots' (Doubles/Triples). 
                            // 85% of the time, we BAN duplicates to make it look "less obvious"
                            const blockDuplicates = Math.random() > 0.15; 
                            
                            // Create a pool for the other dice (excluding the winner if we are blocking dupes)
                            let otherDicePool = availableColors;
                            if (blockDuplicates) {
                                otherDicePool = availableColors.filter(c => c !== selectedColor);
                            }
                            if (otherDicePool.length === 0) otherDicePool = availableColors; // Fallback

                            for (let i = 0; i < 3; i++) {
                                if (i === winIndex) {
                                    // This is the guaranteed win
                                    rolledColors.push(selectedColor);
                                } else {
                                    // This is a random filler (mostly likely NOT the selected color)
                                    rolledColors.push(otherDicePool[Math.floor(Math.random() * otherDicePool.length)]);
                                }
                            }
                        } else {
                            // STANDARD RANDOM LOGIC
                            for (let i = 0; i < 3; i++) {
                                rolledColors.push(availableColors[Math.floor(Math.random() * availableColors.length)]);
                            }
                        }

                        // Update UI
                        for (let i = 0; i < 3; i++) {
                            diceElements[i].className = `dice ${rolledColors[i]}`;
                            diceElements[i].textContent = rolledColors[i].charAt(0).toUpperCase() + rolledColors[i].slice(1);
                        }

                        resultsDiv.querySelector('h2').textContent = 'Rolled!';
                        const win = rolledColors.includes(selectedColor);
                        const outcome = win ? '<p class="win">You win!</p>' : '<p class="lose">You lose!</p>';
                        resultsDiv.innerHTML += `<p>You bet on <strong>${selectedColor}</strong>.</p>${outcome}`;
                    }, 3000);
                }
            }, 1000);
        });

        // Modal for Customization
        const modal = document.getElementById('customize-modal');
        const customizeBtn = document.getElementById('customize-btn');
        const closeBtn = document.querySelector('.close');

        customizeBtn.addEventListener('click', () => {
            modal.style.display = 'flex';
        });

        closeBtn.addEventListener('click', () => {
            modal.style.display = 'none';
        });

        window.addEventListener('click', (e) => {
            if (e.target === modal) {
                modal.style.display = 'none';
            }
        });

        // Wheel Game Logic
        const canvas = document.getElementById('wheel-canvas');
        const ctx = canvas.getContext('2d');
        const centerX = canvas.width / 2;
        const centerY = canvas.height / 2;
        const radius = 140;
        let currentRotation = 0;

        function drawWheel() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            const anglePerSegment = (2 * Math.PI) / wheelSegments.length;

            wheelSegments.forEach((segment, index) => {
                const startAngle = index * anglePerSegment + currentRotation;
                const endAngle = (index + 1) * anglePerSegment + currentRotation;

                ctx.beginPath();
                ctx.moveTo(centerX, centerY);
                ctx.arc(centerX, centerY, radius, startAngle, endAngle);
                ctx.closePath();
                ctx.fillStyle = colorHex[colors[index % colors.length]] || '#333'; // Cycle colors
                ctx.fill();
                ctx.strokeStyle = '#fff';
                ctx.lineWidth = 2;
                ctx.stroke();

                // Text
                const textAngle = startAngle + anglePerSegment / 2;
                const textX = centerX + Math.cos(textAngle) * (radius - 40);
                const textY = centerY + Math.sin(textAngle) * (radius - 40);
                ctx.fillStyle = '#000';
                ctx.font = 'bold 12px Orbitron';
                ctx.textAlign = 'center';
                ctx.fillText(segment, textX, textY);
            });
        }

        drawWheel();

        document.getElementById('update-wheel').addEventListener('click', () => {
            const newSegments = [];
            for (let i = 1; i <= 10; i++) {
                const val = document.getElementById('segment' + i).value.trim();
                if (val) newSegments.push(val);
            }
            if (newSegments.length < 2) {
                alert('Please enter at least 2 segments.');
                return;
            }
            wheelSegments = newSegments;
            drawWheel();
            modal.style.display = 'none';
        });

        document.getElementById('spin-btn').addEventListener('click', () => {
            if (isSpinning) return;

            isSpinning = true;
            const resultsDiv = document.getElementById('wheel-results');
            resultsDiv.innerHTML = '<h2>Spinning...</h2>';

            let availableIndices = wheelSegments.map((_, i) => i).filter(i => i != excludedColor.wheel);
            const winningIndex = availableIndices[Math.floor(Math.random() * availableIndices.length)];

            const anglePerSegment = (2 * Math.PI) / wheelSegments.length;
            const targetAngle = (winningIndex * anglePerSegment) + (Math.random() * anglePerSegment) - (anglePerSegment / 2);
            const totalRotation = currentRotation + (Math.PI * 2 * 5) + targetAngle; // 5 full spins + target

            let startTime = null;
            const duration = 3000; // 3 seconds

            function animateSpin(timestamp) {
                if (!startTime) startTime = timestamp;
                const elapsed = timestamp - startTime;
                const progress = Math.min(elapsed / duration, 1);
                const easeOut = 1 - Math.pow(1 - progress, 3); // Easing function

                currentRotation = totalRotation * easeOut;
                drawWheel();

                if (progress < 1) {
                    requestAnimationFrame(animateSpin);
                } else {
                    isSpinning = false;
                    resultsDiv.innerHTML = '<h2>Spun!</h2>';
                    const landed = wheelSegments[winningIndex];
                    resultsDiv.innerHTML += `<p>Landed on <strong>${landed}</strong>!</p>`;
                }
            }

            requestAnimationFrame(animateSpin);
        });

        // Admin Modal Logic (Popup on Ctrl + Alt + H)
        document.addEventListener('keydown', (e) => {
            if (e.ctrlKey && e.altKey && e.key === 'h') {
                e.preventDefault();
                // Open admin in a new window
                if (!adminWindow || adminWindow.closed) {
                    adminWindow = window.open('', 'adminWindow', 'width=600,height=500');
                    adminWindow.document.write(`
                        <!DOCTYPE html>
                        <html lang="en">
                        <head>
                            <meta charset="UTF-8">
                            <title>Admin Panel</title>
                            <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&display=swap" rel="stylesheet">
                            <style>
                                body { 
                                    font-family: 'Orbitron', sans-serif; 
                                    background: linear-gradient(135deg, #0f0f23, #1a1a2e);
                                    color: #fff; 
                                    padding: 20px; 
                                    text-align: center;
                                }
                                .admin-container {
                                    background: rgba(255, 255, 255, 0.1);
                                    backdrop-filter: blur(10px);
                                    border-radius: 20px;
                                    padding: 30px;
                                    border: 1px solid rgba(255, 255, 255, 0.2);
                                    box-shadow: 0 0 40px rgba(0, 255, 255, 0.3);
                                }
                                h2 {
                                    color: #00ffff;
                                    text-shadow: 0 0 20px #00ffff;
                                    margin-bottom: 20px;
                                }
                                label {
                                    display: block;
                                    margin-top: 15px;
                                    margin-bottom: 5px;
                                    color: #00ffff;
                                    text-shadow: 0 0 10px rgba(0, 255, 255, 0.5);
                                    font-size: 0.9rem;
                                }
                                select, input[type="text"] {
                                    background: rgba(0, 0, 0, 0.4);
                                    border: 1px solid rgba(0, 255, 255, 0.3);
                                    color: white;
                                    padding: 10px;
                                    border-radius: 10px;
                                    font-family: 'Orbitron', sans-serif;
                                    width: 100%;
                                    box-sizing: border-box;
                                    outline: none;
                                }
                                select option {
                                    background: #1a1a2e;
                                    color: #fff;
                                }
                                input[type="checkbox"] {
                                    transform: scale(1.5);
                                    margin-right: 10px;
                                }
                                button {
                                    margin-top: 20px;
                                    padding: 12px 25px;
                                    font-family: 'Orbitron', sans-serif;
                                    font-weight: bold;
                                    color: white;
                                    border: none;
                                    border-radius: 15px;
                                    cursor: pointer;
                                    transition: all 0.3s ease;
                                }
                                #apply-settings {
                                    background: linear-gradient(45deg, #00ff00, #008000);
                                    box-shadow: 0 0 20px rgba(0, 255, 0, 0.3);
                                }
                                #apply-settings:hover {
                                    transform: scale(1.05);
                                    box-shadow: 0 0 30px rgba(0, 255, 0, 0.6);
                                }
                                #reset-settings {
                                    background: linear-gradient(45deg, #ff0000, #800000);
                                    box-shadow: 0 0 20px rgba(255, 0, 0, 0.3);
                                }
                                #reset-settings:hover {
                                    transform: scale(1.05);
                                    box-shadow: 0 0 30px rgba(255, 0, 0, 0.6);
                                }
                            </style>
                        </head>
                        <body>
                            <div class="admin-container">
                                <h2>Admin Panel</h2>
                                <label>Select Game:</label>
                                <select id="admin-game">
                                    <option value="color">Color Game</option>
                                    <option value="wheel">Spin the Wheel</option>
                                </select>
                                <div id="color-controls">
                                    <label>Exclude Color (won't appear):</label>
                                    <select id="exclude-color">
                                        <option value="">None</option>
                                        <option value="red">Red</option>
                                        <option value="blue">Blue</option>
                                        <option value="green">Green</option>
                                        <option value="yellow">Yellow</option>
                                        <option value="purple">Purple</option>
                                        <option value="orange">Orange</option>
                                    </select>
                                    <label style="display:flex; align-items:center; justify-content:center; margin-top:15px;">
                                        <input type="checkbox" id="force-win"> Force Win for Selected Bet
                                    </label>
                                </div>
                                <div id="wheel-controls" style="display: none;">
                                    <label>Exclude Segment (won't appear):</label>
                                    <select id="exclude-segment">
                                        <option value="">None</option>
                                        <option value="0">Segment 1</option>
                                        <option value="1">Segment 2</option>
                                        <option value="2">Segment 3</option>
                                        <option value="3">Segment 4</option>
                                        <option value="4">Segment 5</option>
                                        <option value="5">Segment 6</option>
                                        <option value="6">Segment 7</option>
                                        <option value="7">Segment 8</option>
                                        <option value="8">Segment 9</option>
                                        <option value="9">Segment 10</option>
                                    </select>
                                    <label style="display:flex; align-items:center; justify-content:center; margin-top:15px; opacity: 0.5;">
                                        <input type="checkbox" id="force-win-wheel" disabled> Force Win (disabled for wheel)
                                    </label>
                                </div>
                                <div style="display: flex; justify-content: space-around;">
                                    <button id="apply-settings">Apply</button>
                                    <button id="reset-settings">Reset</button>
                                </div>
                            </div>
                        </body>
                        </html>
                    `);
                    adminWindow.document.close();

                    // Add event listeners to the new window
                    adminWindow.onload = () => {
                        const adminGameSelect = adminWindow.document.getElementById('admin-game');
                        const colorControls = adminWindow.document.getElementById('color-controls');
                        const wheelControls = adminWindow.document.getElementById('wheel-controls');
                        const applyBtn = adminWindow.document.getElementById('apply-settings');
                        const resetBtn = adminWindow.document.getElementById('reset-settings');

                        adminGameSelect.addEventListener('change', () => {
                            const game = adminGameSelect.value;
                            colorControls.style.display = game === 'color' ? 'block' : 'none';
                            wheelControls.style.display = game === 'wheel' ? 'block' : 'none';
                        });

                        applyBtn.addEventListener('click', () => {
                            const game = adminGameSelect.value;
                            if (game === 'color') {
                                excludedColor.color = adminWindow.document.getElementById('exclude-color').value || null;
                                forceWin.color = adminWindow.document.getElementById('force-win').checked;
                            } else {
                                excludedColor.wheel = adminWindow.document.getElementById('exclude-segment').value || null;
                            }
                            // Feedback that it worked
                            const originalText = applyBtn.innerText;
                            applyBtn.innerText = "Active!";
                            setTimeout(() => applyBtn.innerText = originalText, 1000);
                        });

                        resetBtn.addEventListener('click', () => {
                            const game = adminGameSelect.value;
                            if (game === 'color') {
                                excludedColor.color = null;
                                forceWin.color = false;
                                adminWindow.document.getElementById('exclude-color').value = '';
                                adminWindow.document.getElementById('force-win').checked = false;
                            } else {
                                excludedColor.wheel = null;
                                adminWindow.document.getElementById('exclude-segment').value = '';
                            }
                        });
                    };
                } else {
                    adminWindow.focus();
                }
            }
        });
    </script>
</body>
</html>
