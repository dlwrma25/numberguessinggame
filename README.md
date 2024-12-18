<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Number Guessing Game</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #fcefe3;
            color: #4b3832;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-image: radial-gradient(rgba(0, 0, 0, 0.05) 1px, transparent 5px);
            background-size: 10px 10px;
        }

        .container {
            background-color: #ffd5c2;
            border: 3px solid #4b3832;
            border-radius: 15px;
            padding: 20px 30px;
            text-align: center;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            max-width: 400px;
        }

        h1 {
            font-size: 2rem;
            color: #4b3832;
            margin-bottom: 15px;
        }

        input[type="number"] {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            font-size: 1rem;
            border: 2px solid #4b3832;
            border-radius: 5px;
        }

        button {
            background-color: #e5989b;
            color: #fff;
            border: none;
            padding: 10px 20px;
            font-size: 1rem;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 10px;
        }

        button:hover {
            background-color: #b5838d;
        }

        .message {
            margin-top: 15px;
            font-size: 1.2rem;
        }

        .attempts {
            margin-top: 10px;
            font-size: 1rem;
            color: #6d6875;
        }

    </style>
</head>
<body>
    <div class="container">
        <h1>Guess the Number!</h1>
        <p>I'm thinking of a number between <strong>1</strong> and <strong>100</strong>. Can you guess it?</p>

        <input type="number" id="guessInput" placeholder="Enter your guess here" />
        <button id="submitGuess">Submit Guess</button>
        <button id="retryButton" style="display:none;">Retry</button>

        <div class="message" id="message"></div>
        <div class="attempts" id="attempts"></div>
    </div>

    <script>
        let randomNumber = Math.floor(Math.random() * 100) + 1;
        let attempts = 0;

        const submitButton = document.getElementById('submitGuess');
        const retryButton = document.getElementById('retryButton');
        const message = document.getElementById('message');
        const attemptsDisplay = document.getElementById('attempts');
        const guessInput = document.getElementById('guessInput');

        function resetGame() {
            randomNumber = Math.floor(Math.random() * 100) + 1;
            attempts = 0;
            message.textContent = '';
            attemptsDisplay.textContent = '';
            guessInput.value = '';
            submitButton.disabled = false;
            retryButton.style.display = 'none';
        }

        submitButton.addEventListener('click', () => {
            const userGuess = parseInt(guessInput.value);
            attempts++;

            if (isNaN(userGuess) || userGuess < 1 || userGuess > 100) {
                message.textContent = 'Please enter a valid number between 1 and 100!';
                message.style.color = '#b5838d';
            } else if (userGuess < randomNumber) {
                message.textContent = 'Too low! Try again.';
                message.style.color = '#6a994e';
            } else if (userGuess > randomNumber) {
                message.textContent = 'Too high! Try again.';
                message.style.color = '#bc4749';
            } else {
                message.textContent = `🎉 Correct! The number was ${randomNumber}. You guessed it in ${attempts} attempts!`;
                message.style.color = '#f08080';
                submitButton.disabled = true;
                retryButton.style.display = 'block';
            }

            attemptsDisplay.textContent = `Attempts: ${attempts}`;

            if (attempts === 3 && userGuess !== randomNumber) {
                message.textContent = `❌ Game over! The correct number was ${randomNumber}.`;
                message.style.color = '#d62828';
                submitButton.disabled = true;
                retryButton.style.display = 'block';
            }
        });

        retryButton.addEventListener('click', resetGame);
    </script>
</body>
</html>

