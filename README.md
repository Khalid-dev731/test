<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Simple Calculator</title>
  <style>
    body {
      background: #f4f4f4;
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .calculator {
      background: #222;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 8px 24px rgba(0,0,0,0.3);
      width: 260px;
    }
    .display {
      background: #111;
      color: #fff;
      font-size: 2em;
      padding: 15px;
      border-radius: 5px;
      margin-bottom: 15px;
      text-align: right;
      overflow-x: auto;
    }
    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }
    .buttons button {
      padding: 20px;
      font-size: 1.1em;
      border: none;
      border-radius: 5px;
      background: #333;
      color: #fff;
      cursor: pointer;
      transition: background 0.2s;
    }
    .buttons button:active {
      background: #555;
    }
    .buttons .operator {
      background: #ff9500;
      color: #fff;
    }
    .buttons .operator:active {
      background: #cc7a00;
    }
    .buttons .equals {
      background: #34c759;
      color: #fff;
      grid-column: span 2;
    }
    .buttons .equals:active {
      background: #28a745;
    }
    .buttons .clear {
      background: #ff3b30;
      color: #fff;
    }
    .buttons .clear:active {
      background: #c1271a;
    }
  </style>
</head>
<body>
  <div class="calculator">
    <div class="display" id="display">0</div>
    <div class="buttons">
      <button class="clear" onclick="clearDisplay()">C</button>
      <button onclick="appendValue('(')">(</button>
      <button onclick="appendValue(')')">)</button>
      <button class="operator" onclick="appendValue('/')">÷</button>
      <button onclick="appendValue('7')">7</button>
      <button onclick="appendValue('8')">8</button>
      <button onclick="appendValue('9')">9</button>
      <button class="operator" onclick="appendValue('*')">×</button>
      <button onclick="appendValue('4')">4</button>
      <button onclick="appendValue('5')">5</button>
      <button onclick="appendValue('6')">6</button>
      <button class="operator" onclick="appendValue('-')">−</button>
      <button onclick="appendValue('1')">1</button>
      <button onclick="appendValue('2')">2</button>
      <button onclick="appendValue('3')">3</button>
      <button class="operator" onclick="appendValue('+')">+</button>
      <button onclick="appendValue('0')">0</button>
      <button onclick="appendValue('.')">.</button>
      <button class="equals" onclick="calculateResult()">=</button>
    </div>
  </div>
  <script>
    let display = document.getElementById('display');
    let currentInput = '';

    function appendValue(value) {
      if (currentInput === '' && (value === '+' || value === '*' || value === '/' || value === ')')) {
        return;
      }
      if (currentInput === '0' && value !== '.') {
        currentInput = value;
      } else {
        currentInput += value;
      }
      display.textContent = currentInput;
    }

    function clearDisplay() {
      currentInput = '';
      display.textContent = '0';
    }

    function calculateResult() {
      try {
        // eslint-disable-next-line no-eval
        let result = eval(currentInput.replace(/÷/g, '/').replace(/×/g, '*'));
        if (result === undefined) result = 0;
        display.textContent = result;
        currentInput = result.toString();
      } catch (e) {
        display.textContent = 'Error';
        currentInput = '';
      }
    }
  </script>
</body>
</html>
