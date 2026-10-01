<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>计算器</title>
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
            background: #1a1a2e;
            font-family: 'Segoe UI', sans-serif;
        }
        .calculator {
            background: #16213e;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            width: 320px;
        }
        .display {
            background: #0f3460;
            color: #e94560;
            font-size: 2.5rem;
            padding: 20px;
            text-align: right;
            border-radius: 10px;
            margin-bottom: 15px;
            min-height: 80px;
            word-wrap: break-word;
            overflow-wrap: break-word;
        }
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }
        button {
            padding: 20px;
            font-size: 1.3rem;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.2s;
            color: #fff;
        }
        button:hover {
            transform: translateY(-2px);
            opacity: 0.9;
        }
        button:active {
            transform: translateY(0);
        }
        .num {
            background: #533483;
        }
        .operator {
            background: #e94560;
        }
        .func {
            background: #0f3460;
        }
        .equal {
            background: #e94560;
            grid-column: span 2;
        }
        .zero {
            grid-column: span 2;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="buttons">
            <button class="func" onclick="clearAll()">AC</button>
            <button class="func" onclick="clearEntry()">CE</button>
            <button class="func" onclick="appendOperator('%')">%</button>
            <button class="operator" onclick="appendOperator('/')">÷</button>
            
            <button class="num" onclick="appendNum('7')">7</button>
            <button class="num" onclick="appendNum('8')">8</button>
            <button class="num" onclick="appendNum('9')">9</button>
            <button class="operator" onclick="appendOperator('*')">×</button>
            
            <button class="num" onclick="appendNum('4')">4</button>
            <button class="num" onclick="appendNum('5')">5</button>
            <button class="num" onclick="appendNum('6')">6</button>
            <button class="operator" onclick="appendOperator('-')">−</button>
            
            <button class="num" onclick="appendNum('1')">1</button>
            <button class="num" onclick="appendNum('2')">2</button>
            <button class="num" onclick="appendNum('3')">3</button>
            <button class="operator" onclick="appendOperator('+')">+</button>
            
            <button class="num zero" onclick="appendNum('0')">0</button>
            <button class="num" onclick="appendNum('.')">.</button>
            <button class="equal" onclick="calculate()">=</button>
        </div>
    </div>

    <script>
        let display = document.getElementById('display');
        let current = '0';
        let shouldReset = false;

        function updateDisplay() {
            display.textContent = current;
        }

        function appendNum(n) {
            if (shouldReset) {
                current = '0';
                shouldReset = false;
            }
            if (current === '0' && n !== '.') {
                current = n;
            } else if (n === '.' && current.includes('.')) {
                return;
            } else {
                current += n;
            }
            updateDisplay();
        }

        function appendOperator(op) {
            shouldReset = false;
            const last = current.slice(-1);
            if ('+-*/%'.includes(last)) {
                current = current.slice(0, -1) + op;
            } else {
                current += op;
            }
    更新显示();
        }

    函数 清除所有() {
    当前 = '0';
    更新显示();
        }

        function clearEntry() {
    当前 = '0';
    更新显示();
        }

    函数 calculate() {
    尝试 {
    当前值 = String(eval(当前值));
    应重置 = 真；
    } 捕获 {
    当前值 = '错误'。
    应重置 = 真；
            }
    更新显示();
        }

        // 键盘支持
        document.addEventListener('keydown', (e) => {
            if (e.key >= '0' && e.key <= '9') appendNum(e.key);
    否则如果(e.key === '.') 追加数字('.');
            else if (e.key === '+') appendOperator('+');
            else if (e.key === '-') appendOperator('-');
    否则如果(e.key === '*') appendOperator('*');
    否则如果(e.key === '/') { e.preventDefault(); appendOperator('/'); }
    否则如果(e.key === '%') appendOperator('%');
    否则如果(e.key === 'Enter' || e.key === '=') calculate();
    否则如果(e.key === 'Escape') 清除全部();
    否则如果(e.key === 'Backspace') {
    当前值 = 当前值长度大于1时，取前一个元素；否则为'0'。
    更新显示();
            }
        });
    </script>
</body>
</html>

