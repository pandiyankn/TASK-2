# TASK-2
 CALCULATOR
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Phone-like Calculator</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="buttons">
            <button class="button" onclick="clearDisplay()">C</button>
            <button class="button" onclick="deleteLast()">DEL</button>
            <button class="button" onclick="appendOperator('/')">/</button>
            <button class="button" onclick="appendOperator('*')">*</button>
            <button class="button" onclick="appendNumber('7')">7</button>
            <button class="button" onclick="appendNumber('8')">8</button>
            <button class="button" onclick="appendNumber('9')">9</button>
            <button class="button" onclick="appendOperator('-')">-</button>
            <button class="button" onclick="appendNumber('4')">4</button>
            <button class="button" onclick="appendNumber('5')">5</button>
            <button class="button" onclick="appendNumber('6')">6</button>
            <button class="button" onclick="appendOperator('+')">+</button>
            <button class="button" onclick="appendNumber('1')">1</button>
            <button class="button" onclick="appendNumber('2')">2</button>
            <button class="button" onclick="appendNumber('3')">3</button>
            <button class="button button-equals" onclick="calculateResult()">=</button>
            <button class="button button-zero" onclick="appendNumber('0')">0</button>
            <button class="button" onclick="appendNumber('.')">.</button>
        </div>
    </div>
    <script src="scripts.js"></script>
</body>
</html>
body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background-color: #f4f4f4;
    font-family: 'Arial', sans-serif;
}

.calculator {
    background-color: #fff;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    width: 300px;
    padding: 20px;
}

.display {
    background-color: #333;
    color: white;
    font-size: 2em;
    text-align: right;
    padding: 10px;
    border-radius: 5px;
    margin-bottom: 10px;
}

.buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
}

.button {
    background-color: #e0e0e0;
    border: none;
    padding: 20px;
    font-size: 1.5em;
    border-radius: 5px;
    cursor: pointer;
}

.button:hover {
    background-color: #d0d0d0;
}

.button-equals {
    grid-column: span 2;
    background-color: #ff9500;
    color: white;
}

.button-zero {
    grid-column: span 2;
}
let display = document.getElementById('display');
let currentInput = '';
let operator = '';
let previousInput = '';

function clearDisplay() {
    currentInput = '';
    operator = '';
    previousInput = '';
    display.innerText = '0';
}

function deleteLast() {
    currentInput = currentInput.slice(0, -1);
    display.innerText = currentInput || '0';
}

function appendNumber(number) {
    currentInput += number;
    display.innerText = currentInput;
}

function appendOperator(op) {
    if (currentInput === '' && previousInput === '') return;
    if (currentInput === '' && operator !== '') {
        operator = op;
        return;
    }
    if (previousInput !== '' && currentInput !== '') {
        calculateResult();
    }
    operator = op;
    previousInput = currentInput;
    currentInput = '';
}

function calculateResult() {
    let result;
    const prev = parseFloat(previousInput);
    const current = parseFloat(currentInput);
    if (isNaN(prev) || isNaN(current)) return;
    switch (operator) {
        case '+':
            result = prev + current;
            break;
        case '-':
            result = prev - current;
            break;
        case '*':
            result = prev * current;
            break;
        case '/':
            result = prev / current;
            break;
        default:
            return;
    }
    currentInput = result;
    operator = '';
    previousInput = '';
    display.innerText = result;
}
