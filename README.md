<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Typing Speed Test</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: #333;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            width: 100%;
            max-width: 800px;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            padding: 30px;
        }
        
        h1 {
            text-align: center;
            margin-bottom: 20px;
            color: #2c3e50;
        }
        
        .stats {
            display: flex;
            justify-content: space-around;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .stat-box {
            background-color: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            text-align: center;
            min-width: 120px;
            margin-bottom: 10px;
        }
        
        .stat-box h3 {
            font-size: 14px;
            color: #7f8c8d;
            margin-bottom: 5px;
        }
        
        .stat-box p {
            font-size: 24px;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .text-display {
            background-color: #f8f9fa;
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 20px;
            margin-bottom: 20px;
            font-size: 18px;
            line-height: 1.6;
            min-height: 150px;
        }
        
        .text-display span {
            position: relative;
        }
        
        .text-display span.correct {
            color: #27ae60;
        }
        
        .text-display span.incorrect {
            color: #e74c3c;
            background-color: #fadbd8;
            border-radius: 3px;
        }
        
        .text-display span.current {
            background-color: #f1c40f;
            border-radius: 3px;
        }
        
        .typing-area {
            width: 100%;
            padding: 15px;
            font-size: 18px;
            border: 1px solid #ddd;
            border-radius: 8px;
            margin-bottom: 20px;
            resize: none;
            min-height: 100px;
        }
        
        .typing-area:focus {
            outline: none;
            border-color: #3498db;
            box-shadow: 0 0 5px rgba(52, 152, 219, 0.5);
        }
        
        .buttons {
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
        }
        
        button {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s;
        }
        
        button:hover {
            background-color: #2980b9;
        }
        
        button:disabled {
            background-color: #95a5a6;
            cursor: not-allowed;
        }
        
        .result-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        
        .result-content {
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            text-align: center;
            max-width: 500px;
            width: 90%;
        }
        
        .result-content h2 {
            margin-bottom: 20px;
            color: #2c3e50;
        }
        
        .result-stats {
            display: flex;
            justify-content: space-around;
            margin-bottom: 25px;
            flex-wrap: wrap;
        }
        
        .result-stat {
            text-align: center;
            margin: 10px;
        }
        
        .result-stat p {
            font-size: 14px;
            color: #7f8c8d;
        }
        
        .result-stat h3 {
            font-size: 28px;
            color: #2c3e50;
        }
        
        .close-btn {
            background-color: #e74c3c;
        }
        
        .close-btn:hover {
            background-color: #c0392b;
        }
        
        .difficulty-selector {
            margin-bottom: 20px;
            text-align: center;
        }
        
        .difficulty-selector label {
            margin-right: 10px;
            font-weight: bold;
        }
        
        .difficulty-selector select {
            padding: 8px;
            border-radius: 5px;
            border: 1px solid #ddd;
            font-size: 16px;
        }
        
        @media (max-width: 600px) {
            .container {
                padding: 20px;
            }
            
            .text-display {
                font-size: 16px;
                padding: 15px;
            }
            
            .typing-area {
                font-size: 16px;
                padding: 12px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Typing Speed Test</h1>
        
        <div class="difficulty-selector">
            <label for="difficulty">Select Difficulty:</label>
            <select id="difficulty">
                <option value="easy">Easy</option>
                <option value="medium" selected>Medium</option>
                <option value="hard">Hard</option>
            </select>
        </div>
        
        <div class="stats">
            <div class="stat-box">
                <h3>Time</h3>
                <p id="timer">60s</p>
            </div>
            <div class="stat-box">
                <h3>WPM</h3>
                <p id="wpm">0</p>
            </div>
            <div class="stat-box">
                <h3>Accuracy</h3>
                <p id="accuracy">100%</p>
            </div>
            <div class="stat-box">
                <h3>Characters</h3>
                <p id="characters">0/0</p>
            </div>
        </div>
        
        <div class="text-display" id="textDisplay">
            Click "Start Test" to begin typing...
        </div>
        
        <textarea class="typing-area" id="typingArea" placeholder="Start typing here..." disabled></textarea>
        
        <div class="buttons">
            <button id="startBtn">Start Test</button>
            <button id="resetBtn">Reset</button>
            <button id="newTextBtn">New Text</button>
        </div>
    </div>
    
    <div class="result-modal" id="resultModal">
        <div class="result-content">
            <h2>Test Complete!</h2>
            <div class="result-stats">
                <div class="result-stat">
                    <p>Words Per Minute</p>
                    <h3 id="finalWpm">0</h3>
                </div>
                <div class="result-stat">
                    <p>Accuracy</p>
                    <h3 id="finalAccuracy">0%</h3>
                </div>
                <div class="result-stat">
                    <p>Characters</p>
                    <h3 id="finalCharacters">0</h3>
                </div>
            </div>
            <button class="close-btn" id="closeModal">Close</button>
        </div>
    </div>
    
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // DOM Elements
            const textDisplay = document.getElementById('textDisplay');
            const typingArea = document.getElementById('typingArea');
            const startBtn = document.getElementById('startBtn');
            const resetBtn = document.getElementById('resetBtn');
            const newTextBtn = document.getElementById('newTextBtn');
            const timerDisplay = document.getElementById('timer');
            const wpmDisplay = document.getElementById('wpm');
            const accuracyDisplay = document.getElementById('accuracy');
            const charactersDisplay = document.getElementById('characters');
            const resultModal = document.getElementById('resultModal');
            const finalWpm = document.getElementById('finalWpm');
            const finalAccuracy = document.getElementById('finalAccuracy');
            const finalCharacters = document.getElementById('finalCharacters');
            const closeModal = document.getElementById('closeModal');
            const difficultySelector = document.getElementById('difficulty');
            
            // Sample texts for different difficulty levels
            const sampleTexts = {
                easy: [
                    "The quick brown fox jumps over the lazy dog. This simple sentence contains every letter of the alphabet.",
                    "I love to read books and learn new things every day. Knowledge is power and helps us grow.",
                    "The sun rises in the east and sets in the west. It gives us light and warmth every day."
                ],
                medium: [
                    "Technology has revolutionized the way we communicate, work, and live our daily lives. From smartphones to artificial intelligence, innovations continue to shape our future in ways we never imagined possible.",
                    "The environment is facing unprecedented challenges due to climate change, pollution, and deforestation. It is our responsibility to take action and protect our planet for future generations.",
                    "Education is the key to unlocking human potential and fostering social and economic development. By investing in quality education for all, we can create a more equitable and prosperous world."
                ],
                hard: [
                    "Quantum mechanics represents a fundamental shift in our understanding of the physical world, challenging classical notions of determinism and locality through principles such as superposition, entanglement, and wave-particle duality.",
                    "The philosophical implications of artificial intelligence extend beyond mere technical considerations, raising profound questions about consciousness, free will, and the nature of human identity in an increasingly automated world.",
                    "Sustainable development requires a delicate balance between economic growth, social inclusion, and environmental protection, necessitating innovative approaches to resource management and international cooperation."
                ]
            };
            
            // Test state variables
            let currentText = '';
            let timer = null;
            let timeLeft = 60;
            let isTestActive = false;
            let errors = 0;
            let totalTyped = 0;
            let correctChars = 0;
            
            // Initialize the test
            function initTest() {
                const difficulty = difficultySelector.value;
                const texts = sampleTexts[difficulty];
                currentText = texts[Math.floor(Math.random() * texts.length)];
                
                // Display the text with spans for each character
                textDisplay.innerHTML = '';
                for (let i = 0; i < currentText.length; i++) {
                    const span = document.createElement('span');
                    span.textContent = currentText[i];
                    textDisplay.appendChild(span);
                }
                
                // Reset the test state
                typingArea.value = '';
                typingArea.disabled = true;
                timeLeft = 60;
                timerDisplay.textContent = '60s';
                wpmDisplay.textContent = '0';
                accuracyDisplay.textContent = '100%';
                charactersDisplay.textContent = '0/0';
                isTestActive = false;
                errors = 0;
                totalTyped = 0;
                correctChars = 0;
                
                // Update the first character as current
                if (textDisplay.firstChild) {
                    textDisplay.firstChild.classList.add('current');
                }
            }
            
            // Start the test
            function startTest() {
                if (isTestActive) return;
                
                isTestActive = true;
                typingArea.disabled = false;
                typingArea.focus();
                startBtn.disabled = true;
                
                // Start the timer
                timer = setInterval(() => {
                    timeLeft--;
                    timerDisplay.textContent = timeLeft + 's';
                    
                    if (timeLeft <= 0) {
                        endTest();
                    }
                }, 1000);
            }
            
            // End the test
            function endTest() {
                clearInterval(timer);
                isTestActive = false;
                typingArea.disabled = true;
                startBtn.disabled = false;
                
                // Calculate final stats
                const wpm = Math.round((correctChars / 5) / (60 - timeLeft) * 60);
                const accuracy = Math.round((correctChars / totalTyped) * 100) || 100;
                
                // Show results
                finalWpm.textContent = wpm;
                finalAccuracy.textContent = accuracy + '%';
                finalCharacters.textContent = correctChars;
                resultModal.style.display = 'flex';
            }
            
            // Reset the test
            function resetTest() {
                clearInterval(timer);
                initTest();
                startBtn.disabled = false;
            }
            
            // Handle typing input
            function handleTyping() {
                if (!isTestActive) return;
                
                const typedText = typingArea.value;
                const textSpans = textDisplay.querySelectorAll('span');
                
                // Reset all character classes
                textSpans.forEach(span => {
                    span.classList.remove('correct', 'incorrect', 'current');
                });
                
                // Update character classes based on typing
                let newErrors = 0;
                let newCorrectChars = 0;
                
                for (let i = 0; i < textSpans.length; i++) {
                    if (i < typedText.length) {
                        if (typedText[i] === currentText[i]) {
                            textSpans[i].classList.add('correct');
                            newCorrectChars++;
                        } else {
                            textSpans[i].classList.add('incorrect');
                            newErrors++;
                        }
                    } else if (i === typedText.length) {
                        textSpans[i].classList.add('current');
                    }
                }
                
                // Update stats
                errors = newErrors;
                totalTyped = typedText.length;
                correctChars = newCorrectChars;
                
                // Calculate WPM and accuracy
                const minutesPassed = (60 - timeLeft) / 60;
                const wpm = minutesPassed > 0 ? Math.round((correctChars / 5) / minutesPassed) : 0;
                const accuracy = totalTyped > 0 ? Math.round((correctChars / totalTyped) * 100) : 100;
                
                wpmDisplay.textContent = wpm;
                accuracyDisplay.textContent = accuracy + '%';
                charactersDisplay.textContent = correctChars + '/' + currentText.length;
                
                // Check if the user has completed the text
                if (typedText.length === currentText.length) {
                    endTest();
                }
            }
            
            // Event listeners
            startBtn.addEventListener('click', startTest);
            resetBtn.addEventListener('click', resetTest);
            newTextBtn.addEventListener('click', initTest);
            typingArea.addEventListener('input', handleTyping);
            closeModal.addEventListener('click', () => {
                resultModal.style.display = 'none';
                resetTest();
            });
            difficultySelector.addEventListener('change', initTest);
            
            // Initialize the test on page load
            initTest();
        });
    </script>
</body>
</html>
