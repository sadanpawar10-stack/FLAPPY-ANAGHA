# FLAPPY-ANAGHA
A flappy bird like game based on school teacher named ANAGHA who always targets a bay named amogh and says KAYYYY AMOGH and if anyone is laughing in the class she says her famous dialogue WHAT MAKES YOU 😂 
<!DOCTYPE html>
<html>
<head>
    <title>Flappy ANAGHA</title>
    <style>
        /* CSS Keyframes for the background color animation */
        @keyframes backgroundAnimation {
            0%   { background-color: #70c5ce; } /* Light blue */
            25%  { background-color: #94d8b2; } /* Light green */
            50%  { background-color: #f7b2c6; } /* Light pink */
            75%  { background-color: #ffe6aa; } /* Light yellow */
            100% { background-color: #70c5ce; } /* Back to blue */
        }

        /* CSS Keyframes for the RGB text loop animation */
        @keyframes rgbLoop {
            0%   { color: #ff0000; } /* Red */
            16%  { color: #ff7f00; } /* Orange */
            33%  { color: #ffff00; } /* Yellow */
            50%  { color: #00ff00; } /* Green */
            66%  { color: #0000ff; } /* Blue */
            83%  { color: #4b0082; } /* Indigo */
            100% { color: #9400d3; } /* Violet */
        }

        /* Keyframes for diamond rotation */
        @keyframes rotateDiamond {
            0% { transform: translate(-50%, -50%) rotate(0deg); }
            100% { transform: translate(-50%, -50%) rotate(360deg); }
        }

        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #eee;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
        }
        .game-container {
            width: 400px;
            height: 600px;
            /* Apply the animation to the game container */
            animation: backgroundAnimation 20s infinite alternate; 
            border: 5px solid black;
            position: relative;
            overflow: hidden;
            /* Prevent text selection */
            user-select: none; 
            -webkit-user-select: none; /* Safari */
            -moz-user-select: none; /* Firefox */
            -ms-user-select: none; /* IE/Edge */
        }
        .bird {
            position: absolute;
            width: 40px;
            height: 30px;
            top: 250px;
            left: 50px;
            /* Added smooth rotation transition */
            transition: transform 0.1s; 
        }
        .pipe {
            position: absolute;
            width: 60px;
            background-color: #74bf2e;
            border: 2px solid #543847;
            box-sizing: border-box;
        }
        /* Style for the collectible diamond emoji */
        .diamond {
            position: absolute;
            width: 40px; 
            height: 40px;
            font-size: 30px; 
            display: flex;
            justify-content: center;
            align-items: center;
            top: 50%;
            left: 50%; 
            transform: translate(-50%, -50%); 
            pointer-events: none; /* Ignore clicks */
            animation: rotateDiamond 3s infinite linear;
        }
        /* Updated keyframes for div element that uses CSS transform property */
        @keyframes rotateDiamond {
            0% { transform: translate(-50%, -50%) rotate(0deg); }
            100% { transform: translate(-50%, -50%) rotate(360deg); }
        }
        /* Common styles for score boards */
        .score-board {
            position: absolute;
            transform: none; 
            color: white;
            text-shadow: 2px 2px 0 #333, -2px -2px 0 #333, 2px -2px 0 #333, -2px 2px 0 #333;
            z-index: 10;
            pointer-events: none; 
            white-space: nowrap; /* Keep content on one line */
        }
        /* Specific position and size for coins */
        #coin-board {
            top: 10px; 
            left: 10px; 
            font-size: 32px; 
        }
        /* Specific position and size for diamonds (below coins) */
        #diamond-board {
            top: 50px; /* Positioned just below the coin board */
            left: 10px;
            font-size: 24px; /* Slightly smaller font for secondary score */
        }

        .overlay-screen {
            display: none;
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            color: white;
            z-index: 20;
        }
        .overlay-screen p {
            font-size: 1em;
            margin: 5px 0;
        }
        /* Applied to the start button and restart button */
        .menu-button {
            cursor: pointer;
            height: auto;
            margin-top: 15px;
            display: inline-block;
            background-color: black;
            border: 2px solid white;
            padding: 10px 20px; 
            font-size: 1.2em;
            font-weight: bold;
            border-radius: 10px;
            animation: rgbLoop 5s infinite linear;
            text-decoration: none; 
            color: inherit; 
            pointer-events: auto; /* Ensure buttons are clickable */
        }
        #pauseButton {
            position: absolute;
            top: 10px;
            right: 10px;
            width: 40px;
            height: 40px;
            cursor: pointer;
            display: none;
            z-index: 15;
            background-color: rgba(0, 0, 0, 0.5); 
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 1.5em; 
            padding: 0;
            line-height: 40px; 
            pointer-events: auto; /* Ensure the pause button is clickable */
        }
        #lossMessage {
            font-size: 1.5em;
            color: #FF4136;
            font-weight: bold;
            margin-bottom: 10px;
        }
        .instruction-box {
            background-color: rgba(255, 255, 255, 0.3); 
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            max-width: 80%;
            margin-top: 20px;
            color: #333;
        }
        .instruction-box p {
            color: inherit;
        }
        .instruction-box strong {
            color: #d9534f;
        }
        /* Specific background for the Start Screen */
        #startScreen {
            background: linear-gradient(to bottom, #4a7d96, #70c5ce); 
            color: white;
        }
        #startScreen h1 {
             color: white;
             text-shadow: 2px 2px 0 #000;
        }
        #gameOverScreen {
            background-color: rgba(0, 0, 0, 0.75); 
        }
        #pauseScreen {
            background-color: rgba(0, 0, 0, 0.6); 
        }
        /* New style for content containers within overlay screens */
        .menuContent {
            background: linear-gradient(to bottom, #4a7d96, #70c5ce); 
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.5);
            max-width: 80%;
            color: white;
            display: flex;
            flex-direction: column;
            align-items: center;
            text-shadow: 2px 2px 0 #000;
        }
        .menuContent p {
            color: inherit;
            text-shadow: none; /* Remove extra shadow from these <p> tags */
        }
        /* Style for the resume button specifically */
        #resumeButton {
            background-color: #28a745;
            border: 2px solid white;
            color: white;
            animation: none; 
        }
        #highScoreText {
            font-size: 1.2em;
            color: #FFD700;
            margin-top: 10px;
            display: none;
            text-shadow: none; 
        }
        /* Specific styles for the Game Over stats */
        #diamondScoreText {
            font-size: 1em;
            color: #b9f2ff; /* Light blue/diamond color */
            margin-top: 5px;
        }
    </style>
</head>
<body>

    <div class="game-container">
        <!-- Coin Board - Top Left -->
        <div class="score-board" id="coin-board">0 🪙</div>
        <!-- Diamond Board - Top Left (below coins) -->
        <div class="score-board" id="diamond-board">0 💎</div>

        <img src="bird.png" class="bird" id="bird" alt="Flappy Bird">
        
        <button id="pauseButton" onclick="pauseGame()">⏸️</button>

        <div class="overlay-screen" id="startScreen">
            <h1>Flappy ANAGHA</h1>
            <div class="menuContent">
                <p><strong>Instructions:</strong> Tap the screen or press 'Space' to jump.</p>
                <p>Avoid pipes and obstacles!</p>
                <p>Press 'P' to pause/resume.</p>
                <button class="menu-button" onclick="startGame()">START</button>
                <p><small>Tap the button or screen to begin.</small></p>
            </div>
        </div>

        <div class="overlay-screen" id="pauseScreen">
            <div class="menuContent">
                <h1>Paused</h1>
                <button id="resumeButton" class="menu-button" onclick="resumeGame()">RESUME</button>
                <p>Tap the button or press 'P' to resume</p>
            </div>
        </div>

        <div class="overlay-screen" id="gameOverScreen">
            <div class="menuContent">
                <div id="lossMessage">WHAT MAKES YOU LAUGH</div> 
                <p>Coins Collected (Current Game): <span id="finalCoins">0</span> 🪙</p>
                <p id="diamondScoreText">Diamonds Collected (Current Game): <span id="finalDiamonds">0</span> 💎</p>
                <p id="highScoreText">Most Coins (Lifetime): <span id="highScoreDisplay">0</span> 🪙</p>
                <button class="menu-button" onclick="startGame()">RESTART</button>
                <p>Tap the button or screen to restart</p>
            </div>
        </div>
    </div>

    <script>
        // Ensure you have these audio files in the same directory for them to work
        // const gameOverSound = new Audio('gameover.wav'); 
        // const jumpSound = new Audio('jump.wav'); 
        // 'bird.png' is required.

        const gameContainer = document.querySelector('.game-container');
        const birdEl = document.getElementById('bird');
        const coinBoardEl = document.getElementById('coin-board'); 
        const diamondBoardEl = document.getElementById('diamond-board'); 
        const finalCoinsEl = document.getElementById('finalCoins'); 
        const finalDiamondsEl = document.getElementById('finalDiamonds');
        const highScoreDisplayEl = document.getElementById('highScoreDisplay');
        const highScoreTextEl = document.getElementById('highScoreText');
        const startScreen = document.getElementById('startScreen');
        const pauseScreen = document.getElementById('pauseScreen');
        const gameOverScreen = document.getElementById('gameOverScreen');
        const pauseButton = document.getElementById('pauseButton');

        // Game state variables that reset every game
        let birdTop;
        let velocity;
        let pipes;
        let diamonds; 
        let currentRunCoins;
        let currentRunDiamonds;
        let gameState;
        let gameIntervalId;
        let pipeIntervalId;
        let pipeSpeed;
        const gravity = 0.5;
        let highScore = 0; // Tracks maximum coins in a single run
        const jumpForce = -7; 
        const pipeGap = 180; 
        
        // **PERSISTENT VARIABLES:** These are NOT reset in resetGame()
        let coins = 0; // Lifetime total coins
        let diamondsCollected = 0; // Lifetime total diamonds

        // Function to reset game variables *for a new game run* (temporary score for current run)
        function resetGame() {
            birdTop = 250;
            velocity = 0;
            pipes = [];
            diamonds = []; 
            currentRunCoins = 0; 
            currentRunDiamonds = 0;

            pipeSpeed = 3;
            gameState = 'running';
            
            // Update the live scoreboards with current lifetime totals
            coinBoardEl.textContent = coins + ' 🪙'; 
            diamondBoardEl.textContent = diamondsCollected + ' 💎';

            birdEl.style.top = birdTop + 'px';
            birdEl.style.transform = 'rotate(0deg)'; 

            document.querySelectorAll('.pipe').forEach(el => el.remove());
            document.querySelectorAll('.diamond').forEach(el => el.remove());

            if (gameIntervalId) clearInterval(gameIntervalId);
            if (pipeIntervalId) clearInterval(pipeIntervalId);
        }
        
        function startGame() {
            resetGame();
            startScreen.style.display = 'none';
            gameOverScreen.style.display = 'none';
            pauseButton.style.display = 'block';

            gameIntervalId = setInterval(gameLoop, 20); 
            pipeIntervalId = setInterval(createPipes, 2000);
        }

        // --- Core Game Logic Functions ---

        function gameLoop() {
            velocity += gravity;
            birdTop += velocity;
            
            if (birdTop < 0) {
                birdTop = 0;
                velocity = 0;
            }

            birdEl.style.transform = `rotate(${Math.min(velocity * 3, 90)}deg)`;
            birdEl.style.top = birdTop + 'px';

            movePipes();
            moveDiamonds(); 
            checkCollision();
            
            if (birdTop > gameContainer.clientHeight - birdEl.clientHeight) {
                gameOver();
            }
        }

        function jump() {
            velocity = jumpForce;
        }

        function createPipes() {
            const containerHeight = gameContainer.clientHeight;
            const minHeight = 50;
            const maxHeight = containerHeight - pipeGap - minHeight;
            const topPipeHeight = Math.floor(Math.random() * (maxHeight - minHeight + 1)) + minHeight;
            const bottomPipeHeight = containerHeight - topPipeHeight - pipeGap;
            const startLeft = gameContainer.clientWidth;

            const topPipe = document.createElement('div');
            const bottomPipe = document.createElement('div');
            topPipe.classList.add('pipe');
            bottomPipe.classList.add('pipe');
            topPipe.style.height = topPipeHeight + 'px';
            topPipe.style.top = '0px';
            topPipe.style.left = startLeft + 'px';
            bottomPipe.style.height = bottomPipeHeight + 'px';
            bottomPipe.style.bottom = '0px';
            bottomPipe.style.left = startLeft + 'px';
            gameContainer.appendChild(topPipe);
            gameContainer.appendChild(bottomPipe);

            pipes.push({ top: topPipe, bottom: bottomPipe, passed: false });

            // Make diamonds rare (approx 10% chance)
            if (Math.random() < 0.1) { 
                createDiamond(startLeft, topPipeHeight, pipeGap);
            }
        }

        function createDiamond(leftPos, topHeight, gap) {
            const diamondEl = document.createElement('div'); 
            diamondEl.textContent = '💎'; 
            diamondEl.classList.add('diamond');
            
            diamondEl.style.top = (topHeight + gap / 2) + 'px';
            diamondEl.style.left = leftPos + 'px'; 

            gameContainer.appendChild(diamondEl);
            diamonds.push({ element: diamondEl });
        }

        function movePipes() {
            for (let i = 0; i < pipes.length; i++) {
                const pipe = pipes[i];
                let leftPos = parseInt(pipe.top.style.left);

                leftPos -= pipeSpeed;
                pipe.top.style.left = leftPos + 'px';
                pipe.bottom.style.left = leftPos + 'px';

                if (leftPos + pipe.top.clientWidth < 0) {
                    pipe.top.remove();
                    pipe.bottom.remove();
                    pipes.splice(i, 1);
                    i--; 
                }
                
                if (leftPos < 50 && !pipe.passed) {
                    // Update lifetime total AND current run score
                    coins++; 
                    currentRunCoins++;
                    coinBoardEl.textContent = coins + ' 🪙'; 
                    pipe.passed = true; 
                }
            }
        }

        function moveDiamonds() {
            for (let i = 0; i < diamonds.length; i++) {
                const diamond = diamonds[i];
                let leftPos = parseInt(diamond.element.style.left);
                leftPos -= pipeSpeed;
                diamond.element.style.left = leftPos + 'px';

                if (leftPos + diamond.element.clientWidth < 0) {
                    diamond.element.remove();
                    diamonds.splice(i, 1);
                    i--;
                }
            }
        }

        function collectDiamond(diamondIndex) {
            diamonds[diamondIndex].element.remove();
            diamonds.splice(diamondIndex, 1);
            // Update lifetime total AND current run score
            diamondsCollected++; 
            currentRunDiamonds++;
            diamondBoardEl.textContent = diamondsCollected + ' 💎'; // Update the live diamond board
        }

        function checkCollision() {
            const birdRect = birdEl.getBoundingClientRect();
            const containerRect = gameContainer.getBoundingClientRect();
            
            const birdLeft = birdRect.left - containerRect.left;
            const birdTopPos = birdRect.top - containerRect.top;
            const birdRight = birdLeft + birdRect.width;
            const birdBottom = birdTopPos + birdRect.height;

            for (let i = 0; i < pipes.length; i++) {
                const pipe = pipes[i];
                const topPipeRect = pipe.top.getBoundingClientRect();
                const bottomPipeRect = pipe.bottom.getBoundingClientRect();
                const topPipeLeft = topPipeRect.left - containerRect.left;
                const topPipeRight = topPipeLeft + topPipeRect.width;
                const topPipeBottom = topPipeRect.bottom - containerRect.top;
                const bottomPipeLeft = bottomPipeRect.left - containerRect.left;
                const bottomPipeRight = bottomPipeLeft + bottomPipeRect.width;
                const bottomPipeTop = bottomPipeRect.top - containerRect.top;

                const horizontalOverlap = birdRight > topPipeLeft && birdLeft < topPipeRight;
                const verticalOverlapTop = birdTopPos < topPipeBottom;
                const verticalOverlapBottom = birdBottom > bottomPipeTop;

                if (horizontalOverlap && (verticalOverlapTop || verticalOverlapBottom)) {
                    gameOver();
                    return; 
                }
            }

            for (let i = 0; i < diamonds.length; i++) {
                const diamondEl = diamonds[i].element;
                const diamondRect = diamondEl.getBoundingClientRect();
                const dLeft = diamondRect.left - containerRect.left;
                const dTop = diamondRect.top - containerRect.top;
                const dRight = dLeft + diamondRect.width;
                const dBottom = dTop + diamondRect.height;

                if (birdRight > dLeft && birdLeft < dRight && birdBottom > dTop && birdTopPos < dBottom) {
                    collectDiamond(i);
                    i--; 
                }
            }
        }

        function gameOver() {
            gameState = 'gameOver';
            // gameOverSound.play(); 
            clearInterval(gameIntervalId);
            clearInterval(pipeIntervalId);
            pauseButton.style.display = 'none';
            gameOverScreen.style.display = 'flex';
            
            // Display final stats for the *current run*
            finalCoinsEl.textContent = currentRunCoins;
            finalDiamondsEl.textContent = currentRunDiamonds;

            if (currentRunCoins > highScore) {
                highScore = currentRunCoins;
                highScoreDisplayEl.textContent = highScore;
            }
            highScoreTextEl.style.display = 'block';
        }

        function pauseGame() {
            if (gameState === 'running') {
                gameState = 'paused';
                clearInterval(gameIntervalId);
                clearInterval(pipeIntervalId);
                pauseScreen.style.display = 'flex';
                pauseButton.textContent = '▶️'; 
            } else if (gameState === 'paused') {
                resumeGame();
            }
        }

        function resumeGame() {
            if (gameState === 'paused') {
                gameState = 'running';
                gameIntervalId = setInterval(gameLoop, 20); 
                pipeIntervalId = setInterval(createPipes, 2000); 
                pauseScreen.style.display = 'none';
                pauseButton.textContent = '⏸️'; 
            }
        }

        // --- Event Listeners ---
        document.addEventListener('keydown', function(e) {
            if (e.code === 'Space' && gameState === 'running') {
                jump();
            } else if (e.key === 'p' || e.key === 'P') {
                if (gameState === 'running' || gameState === 'paused') {
                    pauseGame();
                }
            }
        });

        gameContainer.addEventListener('click', function(e) {
            if (e.target.closest('.overlay-screen')) return;
            if (gameState === 'running') {
                jump();
            }
        });
        
        // Initial setup
        startScreen.style.display = 'flex';
        gameState = 'start';
        // Ensure initial persistent counters are displayed on load
        coinBoardEl.textContent = coins + ' 🪙';
        diamondBoardEl.textContent = diamondsCollected + ' 💎';
    </script>
</body>
</html>
