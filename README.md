<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Máy Tính Toán Học & Tam Giác Vuông</title>
  <!-- Import phông chữ Lobster -->
  <link
    href="https://fonts.googleapis.com/css2?family=Lobster&display=swap"
    rel="stylesheet"
  />
  <!-- Include Nerdamer cho giải phương trình (Máy Tính Toán Học) -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/nerdamer/1.1.9/nerdamer.core.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/nerdamer/1.1.9/Algebra.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/nerdamer/1.1.9/Solve.js"></script>

  <style>
    /* ------------------ CSS CHUNG ------------------ */
    * {
      box-sizing: border-box;
    }
    body {
      margin: 0;
      padding: 0;
      background: linear-gradient(135deg, #ece9e6, #ffffff);
      font-family: "Lobster", cursive;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start; /* Để thanh trên cùng ở đầu trang */
      min-height: 100vh;
      background-attachment: fixed;
    }
    h1 {
      text-align: center;
      font-size: 3rem;
      margin-bottom: 20px;
      color: #5a5a5a;
    }
    /* Thanh trên cùng: 1 nút toggleCalcBtn */
    .topBar {
      width: 100%;
      background: linear-gradient(135deg, #4caf50, #66bb6a);
      text-align: center;
      padding: 10px 0;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    }
    .topBar button {
      border: none;
      border-radius: 10px;
      font-size: 1.8rem;
      padding: 10px 20px;
      background: transparent;
      color: #fff;
      cursor: pointer;
      font-family: "Lobster", cursive;
    }
    .container {
      border-radius: 20px;
      padding: 40px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
      max-width: 600px;
      width: 90%;
      animation: fadeIn 1.5s ease-out;
      margin-bottom: 20px;
    }
    @keyframes fadeIn {
      from {
        opacity: 0;
        transform: translateY(30px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    /* ------------------ CSS Máy Tính Toán Học (originalCalc) ------------------ */
    #originalCalc {
      background: rgba(255, 255, 255, 0.85);
      backdrop-filter: blur(10px);
      border-radius: 20px;
      padding: 40px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
      max-width: 600px;
      width: 90%;
      margin-bottom: 20px;
    }
    #expression {
      width: 100%;
      min-height: 60px;
      padding: 20px;
      font-size: 2rem;
      text-align: right;
      margin-bottom: 30px;
      border: none;
      border-radius: 10px;
      background: rgba(255, 255, 255, 0.7);
      box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.1);
      outline: none;
    }
    .keyboard {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 15px;
      margin-bottom: 15px;
    }
    .key {
      padding: 20px;
      font-size: 1.8rem;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: transform 0.2s, box-shadow 0.2s;
      background: linear-gradient(145deg, #e0e0e0, #ffffff);
      box-shadow: 5px 5px 10px #bebebe, -5px -5px 10px #ffffff;
      user-select: none;
    }
    .key:hover {
      transform: scale(1.05);
      box-shadow: 2px 2px 5px #bebebe, -2px -2px 5px #ffffff;
    }
    .key.operator {
      background: linear-gradient(145deg, #d1c4e9, #b39ddb);
      color: #3a1e2d;
      font-weight: bold;
    }
    .key.clear {
      background: linear-gradient(145deg, #ffcdd2, #ef9a9a);
      color: #b71c1c;
      font-weight: bold;
    }
    .key.exit {
      background: linear-gradient(145deg, #c8e6c9, #a5d6a7);
      color: #1b5e20;
      font-weight: bold;
    }
    .btn {
      width: 100%;
      padding: 20px;
      font-size: 2rem;
      font-family: "Lobster", cursive;
      background: linear-gradient(135deg, #ff8a65, #ff7043);
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: background 0.3s, box-shadow 0.3s;
      margin-bottom: 30px;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    }
    .btn:hover {
      background: linear-gradient(135deg, #ff7043, #ff8a65);
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
    }
    .result {
      font-size: 2rem;
      font-weight: bold;
      margin-bottom: 20px;
      text-align: center;
      color: #424242;
    }
    .explanation {
      background: rgba(255, 255, 255, 0.85);
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
      font-size: 1.6rem;
      line-height: 1.6;
      color: #555;
    }

    /* ------------------ CSS Máy Tính Tam Giác Vuông (triangleCalc) ------------------ */
    #triangleCalc {
      display: none;
      /* Nền gradient đẹp */
      background: linear-gradient(135deg, #ff4b2b, #ffcc00);
      border-radius: 20px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
      padding: 40px;
      max-width: 600px;
      width: 90%;
      margin-bottom: 20px;
    }
    .angleCheckContainer {
      display: flex;
      align-items: center;
      margin-bottom: 15px;
    }
    .checkSquare {
      width: 20px;
      height: 20px;
      border: 2px solid #333;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      margin-left: 8px;
      cursor: pointer;
      user-select: none;
      font-family: "Lobster", cursive;
      font-size: 16px;
    }
    #canvasContainer {
      display: inline-block;
      padding: 10px;
      background-color: #fcebd0;
      border: 2px solid #d32f2f;
      border-radius: 15px;
      margin: 10px auto;
    }
    canvas {
      display: block;
      background: #fff;
    }
    #triangleResult {
      font-family: "Lobster", cursive;
      margin-top: 20px;
      background: rgba(255, 255, 255, 0.85);
      padding: 15px;
      border-radius: 10px;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
      max-width: 600px;
      margin: 20px auto 0 auto;
      text-align: center;
    }
  </style>
</head>
<body>
  <!-- Thanh trên cùng: 1 nút duy nhất toggleCalcBtn -->
  <div class="topBar">
    <button id="toggleCalcBtn">Chuyển sang Máy Tính Tam Giác Vuông</button>
  </div>

  <!-- Máy tính Toán Học (originalCalc) -->
  <div class="container" id="originalCalc">
    <h1>Máy Tính Toán Học</h1>
    <div id="expression" class="expression-input" contenteditable="true"></div>
    <div id="keyboard" class="keyboard"></div>
    <button class="btn" id="calculateBtn">Tính Toán</button>
    <div class="result">
      Kết quả: <span id="result"></span>
    </div>
    <div class="explanation">
      <strong>Giải thích:</strong>
      <div id="explanation"></div>
    </div>
  </div>

  <!-- Máy tính Tam Giác Vuông (triangleCalc) -->
  <div class="container" id="triangleCalc">
    <h2>Máy Tính Tam Giác Vuông</h2>
    <p style="font-family:'Lobster', cursive;">
      Nhập ít nhất 2 giá trị (W, L, hoặc cạnh huyền). Tam giác được vẽ với góc vuông ở góc dưới bên trái (V1).
    </p>
    <!-- Nhập các cạnh -->
    <label for="sideB">Cạnh ngang (W):</label>
    <input type="number" id="sideB" placeholder="Ví dụ: 4" step="any" /><br />
    <label for="sideC">Cạnh dọc (L):</label>
    <input type="number" id="sideC" placeholder="Ví dụ: 3" step="any" /><br />
    <label for="sideA">Cạnh huyền (tùy chọn):</label>
    <input type="number" id="sideA" placeholder="Ví dụ: 5" step="any" /><br />

    <h2>Nhãn Góc</h2>
    <p style="font-family:'Lobster', cursive;">
      Mặc định: V1 (góc vuông), V2, V3. Nhấn ô vuông bên cạnh V2 hoặc V3 để hoán đổi nhãn với V1.
    </p>
    <div class="angleCheckContainer">
      <label for="labelA">Góc V1:</label>
      <input type="text" id="labelA" placeholder="A" maxlength="10" />
      <div class="checkSquare" id="checkA">✓</div>
    </div>
    <div class="angleCheckContainer">
      <label for="labelB">Góc V2:</label>
      <input type="text" id="labelB" placeholder="B" maxlength="10" />
      <div class="checkSquare" id="checkB"></div>
    </div>
    <div class="angleCheckContainer">
      <label for="labelC">Góc V3:</label>
      <input type="text" id="labelC" placeholder="C" maxlength="10" />
      <div class="checkSquare" id="checkC"></div>
    </div>
    <button class="btn calcButton" onclick="calculateTriangle()">
      Tính Toán
    </button>
    <div id="canvasContainer">
      <canvas id="triangleCanvas"></canvas>
    </div>
    <div id="triangleResult"></div>
  </div>

  <!-- ----------------- Mã JavaScript ----------------- -->
  <!-- Mã cho Máy Tính Toán Học (originalCalc) -->
  <script>
    /*******************************************************
     *            CODE CHO MÁY TÍNH TOÁN HỌC
     *******************************************************/
    let currentMode = "numeric";
    let savedRange = null;
    const expressionDiv = document.getElementById("expression");

    function insertAtCursorElement(element) {
      const sel = window.getSelection();
      let range =
        sel.rangeCount > 0
          ? sel.getRangeAt(0)
          : savedRange || document.createRange();
      range.deleteContents();
      range.insertNode(element);
      range.selectNodeContents(element);
      range.collapse(false);
      sel.removeAllRanges();
      sel.addRange(range);
      savedRange = range;
    }

    function insertAtCursor(html) {
      const sel = window.getSelection();
      let range =
        sel.rangeCount > 0
          ? sel.getRangeAt(0)
          : savedRange || document.createRange();
      range.deleteContents();
      const el = document.createElement("div");
      el.innerHTML = html;
      const frag = document.createDocumentFragment();
      let node, lastNode;
      while ((node = el.firstChild)) {
        lastNode = frag.appendChild(node);
      }
      range.insertNode(frag);
      if (lastNode) {
        range.setStartAfter(lastNode);
        range.collapse(true);
      }
      sel.removeAllRanges();
      sel.addRange(range);
      savedRange = range;
    }

    function exitSuperscript() {
      const sel = window.getSelection();
      if (sel.rangeCount === 0) return;
      let range = sel.getRangeAt(0);
      let node = range.startContainer;
      while (node && node !== expressionDiv) {
        if (node.nodeName.toLowerCase() === "sup") {
          let newRange = document.createRange();
          newRange.setStartAfter(node);
          newRange.collapse(true);
          sel.removeAllRanges();
          sel.addRange(newRange);
          savedRange = newRange;
          break;
        }
        node = node.parentNode;
      }
    }

    function saveSelection() {
      const sel = window.getSelection();
      if (sel.rangeCount > 0) {
        savedRange = sel.getRangeAt(0);
      }
    }
    expressionDiv.addEventListener("mouseup", saveSelection);
    expressionDiv.addEventListener("keyup", saveSelection);
    expressionDiv.addEventListener("focus", saveSelection);

    function renderKeyboard() {
      const keyboard = document.getElementById("keyboard");
      let layout;
      if (currentMode === "numeric") {
        layout = [
          ["Var", "π", "=", "C"],
          ["7", "8", "9", "÷"],
          ["4", "5", "6", "×"],
          ["1", "2", "3", "-"],
          ["0", ".", "(", ")"],
          ["√", "xⁿ", "+", "↘ Thoát số mũ"],
          ["x mũ -n"],
        ];
      } else {
        layout = [
          ["Var", "π", "=", "C"],
          ["x", "y", "z", "÷"],
          ["a", "b", "c", "×"],
          ["d", "v", "t", "-"],
          ["s", ".", "(", ")"],
          ["√", "xⁿ", "+", "↘ Thoát số mũ"],
          ["x mũ -n"],
        ];
      }
      let html = "";
      layout.forEach((row) => {
        row.forEach((key) => {
          let dataValue = key;
          if (key === "Var") dataValue = "toggleVar";
          if (key === "=") dataValue = "=";
          if (key === "C") dataValue = "clear";
          if (key === "xⁿ") dataValue = "power";
          if (key === "↘ Thoát số mũ") dataValue = "exitSup";
          if (key === "x mũ -n") dataValue = "xpowerNeg";

          let extraClass = "";
          if (["÷", "×", "-", "+", "√", "=", "xⁿ", "x mũ -n"].includes(key))
            extraClass = " operator";
          if (key === "C") extraClass = " clear";
          if (key === "↘ Thoát số mũ") extraClass = " exit";

          if (row.length === 1) {
            html += `<div class="key${extraClass}" style="grid-column: span 4;" data-value="${dataValue}">${key}</div>`;
          } else {
            html += `<div class="key${extraClass}" data-value="${dataValue}">${key}</div>`;
          }
        });
      });
      keyboard.innerHTML = html;
      attachKeyListeners();
    }

    function attachKeyListeners() {
      const keys = document.querySelectorAll(".key");
      keys.forEach((key) => {
        key.addEventListener("mousedown", (e) => {
          e.preventDefault();
        });
        key.addEventListener("click", () => {
          const value = key.getAttribute("data-value");
          if (value === "toggleVar") {
            currentMode = currentMode === "numeric" ? "variable" : "numeric";
            renderKeyboard();
          } else if (value === "clear") {
            expressionDiv.innerHTML = "";
            savedRange = null;
          } else if (value === "exitSup") {
            exitSuperscript();
          } else if (value === "power") {
            let sup = document.createElement("sup");
            sup.innerHTML = "";
            insertAtCursorElement(sup);
          } else if (value === "xpowerNeg") {
            let sup = document.createElement("sup");
            sup.innerHTML = "-";
            insertAtCursorElement(sup);
          } else {
            insertAtCursor(value);
          }
          expressionDiv.focus();
        });
      });
    }

    function getExpressionPlainText() {
      let html = expressionDiv.innerHTML;
      let text = html.replace(/<sup>(.*?)<\/sup>/g, function (match, p1) {
        let cleaned = p1.replace(/\u200B|&#8203;/g, "").trim();
        return cleaned ? "^" + cleaned : "";
      });
      return text.replace(/<[^>]*>/g, "");
    }

    function convertExpression(expr) {
      let compExpr = expr;
      compExpr = compExpr.replace(/π/g, "Math.PI");
      compExpr = compExpr.replace(/×/g, "*").replace(/÷/g, "/");
      compExpr = compExpr.replace(/\^/g, "**");
      compExpr = compExpr.replace(/√\(/g, "Math.sqrt(");
      return compExpr;
    }

    function parseSide(side) {
      side = side.replace(/\s+/g, "");
      if (side[0] !== "+" && side[0] !== "-") {
        side = "+" + side;
      }
      let regex = /([+-])(\d*\.?\d*)([xyzabcdvts]?)/g;
      let match;
      let coefficients = {};
      let constant = 0;
      while ((match = regex.exec(side)) !== null) {
        let sign = match[1];
        let numberStr = match[2];
        let variable = match[3];
        let num = numberStr === "" ? 1 : parseFloat(numberStr);
        if (sign === "-") num = -num;
        if (variable) {
          coefficients[variable] = (coefficients[variable] || 0) + num;
        } else {
          constant += num;
        }
      }
      return { coefficients, constant };
    }

    function solveEquationManual(equation) {
      let parts = equation.split("=");
      if (parts.length !== 2) return "Định dạng sai";
      let left = parseSide(parts[0]);
      let right = parseSide(parts[1]);
      let diffCoefficients = {};
      let keys = new Set([
        ...Object.keys(left.coefficients),
        ...Object.keys(right.coefficients),
      ]);
      keys.forEach(function (key) {
        diffCoefficients[key] =
          (left.coefficients[key] || 0) - (right.coefficients[key] || 0);
      });
      let totalConstant = left.constant - right.constant;
      let nonZeroVars = Object.keys(diffCoefficients).filter(
        (key) => diffCoefficients[key] !== 0
      );
      if (nonZeroVars.length === 0) {
        if (totalConstant === 0) return "Vô số nghiệm";
        else return "Vô nghiệm";
      } else if (nonZeroVars.length === 1) {
        let variable = nonZeroVars[0];
        let coef = diffCoefficients[variable];
        let value = -totalConstant / coef;
        return variable + " = " + value.toFixed(2);
      } else {
        let message = "Phương trình có nhiều biến: ";
        nonZeroVars.forEach(function (varName) {
          message +=
            varName + " (hệ số: " + diffCoefficients[varName] + "), ";
        });
        message +=
          "với số hạng tự do: " + totalConstant + ".<br>Không thể giải được duy nhất.";
        return message;
      }
    }

    function solveEquationNerdamer(equation) {
      let vars = extractVariables(equation);
      if (vars.length !== 1) {
        return "Phương trình có nhiều biến, không thể giải được duy nhất.";
      }
      let variable = vars[0];
      try {
        let solutions = nerdamer.solve(equation, variable);
        if (solutions.length === 0) return "Không có nghiệm";
        return solutions.map((s) => s.toString()).join(", ");
      } catch (error) {
        return "Lỗi trong việc giải phương trình: " + error.message;
      }
    }

    function extractVariables(expr) {
      let regex = /[xyzabcdvts]/g;
      let matches = expr.match(regex);
      return matches ? [...new Set(matches)] : [];
    }

    function extractVariable(expr) {
      let vars = extractVariables(expr);
      return vars.length > 0 ? vars[0] : "x";
    }

    function solveEquation(equation) {
      if (equation.indexOf("^") !== -1) {
        return solveEquationNerdamer(equation);
      } else {
        return solveEquationManual(equation);
      }
    }

    function generateDetailedExplanation(expr, result) {
      expr = expr.trim();
      if (/^-?\d+(\.\d+)?$/.test(expr)) {
        return `Giải thích:<br><br>
- Mỗi số đứng đơn lẽ được hiểu là chính nó.<br><br>
<strong>Kết quả của biểu thức "<em>${expr}</em>" là:</strong> <span style="font-size:1.8em;">${result}</span>.`;
      }
      let explanation = "Giải thích:<br><br>";
      explanation += "- Nguyên tắc: Tính từ trái sang phải.<br><br>";
      if (expr.includes("(") && expr.includes(")")) {
        explanation +=
          "- Các phép toán trong dấu ngoặc được tính trước, sau đó tính từ trái sang phải.<br><br>";
      }
      if (expr.includes("^")) {
        let expMatch = expr.match(/(\d+)\^(-?\d+)/);
        if (expMatch) {
          let base = expMatch[1];
          let exp = parseInt(expMatch[2]);
          if (exp === 0) {
            if (base === "0") {
              explanation +=
                "- 0^0 là bất quy tắc, kết quả được coi là Infinity.<br><br>";
            } else {
              explanation +=
                "- Bất kỳ số nào mũ 0 đều bằng 1 (trừ 0^0).<br><br>";
            }
          } else if (exp < 0) {
            explanation += `- Số mũ âm: Với ${base}^${exp}, nghĩa là lấy 1 chia cho ${base} được nhân ${Math.abs(
              exp
            )} lần, tức là 1/(${base}^${Math.abs(exp)}).<br><br>`;
          } else {
            explanation += `- Số mũ dương: Hệ số ${base} được nhân với chính nó ${exp} lần.<br><br>`;
          }
        }
      }
      if (/(^|[×\*])0|0([×\*]|$)/.test(expr)) {
        explanation += "- Bất kỳ số nào nhân với 0 đều bằng 0.<br><br>";
      }
      if (/([÷\\/])0(?!\d)/.test(expr)) {
        explanation +=
          "- Bất kỳ số nào chia cho 0 đều không hợp lý (Infinity).<br><br>";
      }
      if (expr.includes("π")) {
        explanation +=
          "- Với số π: Công thức hình tròn: Chu vi = 2πr, Diện tích = πr².<br><br>";
      }
      let binarySubtractionMatch = expr.match(/(\d+)\s*\-\s*(\d+)/);
      if (binarySubtractionMatch) {
        explanation += "- Giải thích về phép trừ (nếu kết quả âm):<br>";
        explanation +=
          "+ So sánh hai số, lấy số lớn trừ số bé, rồi thêm dấu trừ của số lớn vào kết quả.<br>";
        explanation += "+ Ví dụ:<br>";
        explanation +=
          "+ • 7 và 15: số lớn là 15, 15 - 7 = 8, thêm dấu trừ => -8 (7 - 15 = -8).<br>";
        explanation +=
          "+ • 20 và 50: số lớn là 50, 50 - 20 = 30, thêm dấu trừ => -30 (20 - 50 = -30).<br><br>";
      } else if (expr.includes("-") && /[×\*\/÷]/.test(expr)) {
        explanation += "- Giải thích về dấu âm (trong nhân/chia):<br>";
        explanation += "+ Số dương nhân số âm (hoặc ngược lại) cho ra số âm.<br>";
        explanation += "+ Số âm nhân số âm cho ra số dương.<br><br>";
      }
      explanation += `<strong>Kết quả của biểu thức "<em>${expr}</em>" là:</strong> <span style="font-size:1.8em;">${result}</span>.`;
      return explanation;
    }

    function calculate() {
      let expression = getExpressionPlainText();
      if (expression.includes("=")) {
        let solution = solveEquation(expression);
        document.getElementById("result").innerText = solution;
        document.getElementById("explanation").innerHTML =
          "Phương trình được giải: " +
          solution +
          "<br><br>" +
          generateDetailedExplanation(expression, solution);
        return;
      }
      expression = convertExpression(expression);
      try {
        const result = eval(expression);
        document.getElementById("result").innerText = result;
        document.getElementById("explanation").innerHTML =
          generateDetailedExplanation(getExpressionPlainText(), result);
      } catch (error) {
        document.getElementById("result").innerText = "Lỗi!";
        document.getElementById("explanation").innerText =
          "Có lỗi trong quá trình tính toán. Vui lòng kiểm tra lại biểu thức.";
      }
    }

    document.getElementById("calculateBtn").addEventListener("click", calculate);
    renderKeyboard();
  </script>

  <!-- Mã cho Máy Tính Tam Giác Vuông (triangleCalc) -->
  <script>
    /*******************************************************
     *       CODE CHO MÁY TÍNH TAM GIÁC VUÔNG
     *******************************************************/
    let v1_label = "A",
      v2_label = "B",
      v3_label = "C";

    function updateLabelInputs() {
      document.getElementById("labelA").value = v1_label;
      document.getElementById("labelB").value = v2_label;
      document.getElementById("labelC").value = v3_label;
    }
    function initLabels() {
      v1_label = document.getElementById("labelA").value || "A";
      v2_label = document.getElementById("labelB").value || "B";
      v3_label = document.getElementById("labelC").value || "C";
      updateLabelInputs();
    }
    initLabels();

    const checkA = document.getElementById("checkA");
    const checkB = document.getElementById("checkB");
    const checkC = document.getElementById("checkC");
    checkA.textContent = "✓";
    checkB.textContent = "";
    checkC.textContent = "";

    checkA.addEventListener("click", () => {
      // V1 đã là góc vuông, không làm gì
    });
    checkB.addEventListener("click", () => {
      [v1_label, v2_label] = [v2_label, v1_label];
      checkA.textContent = "✓";
      checkB.textContent = "";
      checkC.textContent = "";
      updateLabelInputs();
      calculateTriangle();
    });
    checkC.addEventListener("click", () => {
      [v1_label, v3_label] = [v3_label, v1_label];
      checkA.textContent = "✓";
      checkB.textContent = "";
      checkC.textContent = "";
      updateLabelInputs();
      calculateTriangle();
    });

    function calculateTriangle() {
      // Đọc 3 giá trị từ input
      let W = parseFloat(document.getElementById("sideB").value);  // cạnh ngang
      let L = parseFloat(document.getElementById("sideC").value);  // cạnh dọc
      let hyp = parseFloat(document.getElementById("sideA").value); // cạnh huyền

      // Kiểm tra số cạnh được nhập
      let providedW = !isNaN(W);
      let providedL = !isNaN(L);
      let providedH = !isNaN(hyp);
      let countProvided = (providedW ? 1 : 0) + (providedL ? 1 : 0) + (providedH ? 1 : 0);

      // Cần ít nhất 2 giá trị
      if (countProvided < 2) {
        document.getElementById("triangleResult").innerHTML =
          "<p>Vui lòng nhập ít nhất 2 giá trị (W, L, hoặc cạnh huyền).</p>";
        clearCanvasTriangle();
        return;
      }

      // Nếu chỉ có 2 giá trị => tính giá trị còn lại
      if (countProvided === 2) {
        // Thiếu hyp
        if (!providedH) {
          hyp = Math.sqrt(W * W + L * L);
        }
        // Thiếu W
        else if (!providedW) {
          let temp = hyp * hyp - L * L;
          if (temp < 0) {
            document.getElementById("triangleResult").innerHTML =
              "<p>Dữ liệu không hợp lệ: Cạnh huyền phải lớn hơn cạnh dọc.</p>";
            clearCanvasTriangle();
            return;
          }
          W = Math.sqrt(temp);
        }
        // Thiếu L
        else if (!providedL) {
          let temp = hyp * hyp - W * W;
          if (temp < 0) {
            document.getElementById("triangleResult").innerHTML =
              "<p>Dữ liệu không hợp lệ: Cạnh huyền phải lớn hơn cạnh ngang.</p>";
            clearCanvasTriangle();
            return;
          }
          L = Math.sqrt(temp);
        }
      } 
      // Nếu nhập đủ 3 => kiểm tra nhất quán
      else {
        let diff = Math.abs(W * W + L * L - hyp * hyp);
        let eps = 1e-6;
        if (diff > eps) {
          document.getElementById("triangleResult").innerHTML =
            "<p>Dữ liệu không hợp lệ: W² + L² không bằng cạnh huyền².</p>";
          clearCanvasTriangle();
          return;
        }
      }

      // ----- Tính góc -----
      let angleV2 = Math.atan(L / W) * 180 / Math.PI; // góc tại V2
      let angleV3 = 90 - angleV2; // góc tại V3

      // Hiển thị kết quả
      let resHTML = `<p>Góc vuông: ${v1_label} = 90°</p>`;
      resHTML += `<p>Các góc còn lại: ${v2_label} = ${angleV2.toFixed(2)}°, ${v3_label} = ${angleV3.toFixed(2)}°</p>`;
      resHTML += `<p>Các cạnh: Huyền (đối ${v1_label}) = ${hyp.toFixed(2)}, Ngang (${v1_label}-${v2_label}) = ${W.toFixed(2)}, Dọc (${v1_label}-${v3_label}) = ${L.toFixed(2)}</p>`;
      document.getElementById("triangleResult").innerHTML = resHTML;

      // Vẽ tam giác
      drawTriangle(W, L);
    }

    function drawTriangle(W, L) {
      const margin = 50;
      const scale = 50;
      let canvas = document.getElementById("triangleCanvas");
      let ctx = canvas.getContext("2d");

      // Tính kích thước canvas
      let width = Math.max(400, margin + W * scale + margin);
      let height = Math.max(400, margin + L * scale + margin);
      canvas.width = width;
      canvas.height = height;
      document.getElementById("canvasContainer").style.width = width + "px";
      document.getElementById("canvasContainer").style.height = height + "px";

      ctx.clearRect(0, 0, width, height);

      // Định nghĩa 3 đỉnh vật lý (V1, V2, V3)
      // V1 (góc vuông) ở (margin, margin + L*scale)
      let V1 = { x: margin, y: margin + L * scale };
      // V2 ở (margin + W*scale, margin + L*scale)
      let V2 = { x: margin + W * scale, y: margin + L * scale };
      // V3 ở (margin, margin)
      let V3 = { x: margin, y: margin };

      // Vẽ tam giác
      ctx.beginPath();
      ctx.moveTo(V1.x, V1.y);
      ctx.lineTo(V2.x, V2.y);
      ctx.lineTo(V3.x, V3.y);
      ctx.closePath();
      ctx.lineWidth = 2;
      ctx.strokeStyle = "#333";
      ctx.stroke();

      // Vẽ ký hiệu góc vuông tại V1
      let marker = 20;
      ctx.beginPath();
      ctx.moveTo(V1.x + marker, V1.y);
      ctx.lineTo(V1.x + marker, V1.y - marker);
      ctx.lineTo(V1.x, V1.y - marker);
      ctx.stroke();

      // Vẽ nhãn đỉnh
      ctx.font = "18px 'Lobster', cursive";
      ctx.fillStyle = "#d32f2f";
      ctx.fillText(v1_label, V1.x - 30, V1.y + 25);
      ctx.fillText(v2_label, V2.x + 10, V2.y + 25);
      ctx.fillText(v3_label, V3.x - 30, V3.y - 10);

      // Ghi chú độ dài (màu xanh)
      ctx.fillStyle = "#1976d2";
      let midV1V2 = { x: (V1.x + V2.x) / 2, y: (V1.y + V2.y) / 2 };
      let midV1V3 = { x: (V1.x + V3.x) / 2, y: (V1.y + V3.y) / 2 };
      let midV2V3 = { x: (V2.x + V3.x) / 2, y: (V2.y + V3.y) / 2 };
      ctx.fillText(W.toFixed(2), midV1V2.x, midV1V2.y + 25);
      ctx.fillText(L.toFixed(2), midV1V3.x - 35, midV1V3.y);
      ctx.fillText(Math.sqrt(W * W + L * L).toFixed(2), midV2V3.x + 10, midV2V3.y);
    }

    function clearCanvasTriangle() {
      let canvas = document.getElementById("triangleCanvas");
      let ctx = canvas.getContext("2d");
      ctx.clearRect(0, 0, canvas.width, canvas.height);
    }
  </script>

  <!-- Mã chuyển đổi (nút trên cùng) -->
  <script>
    const originalCalc = document.getElementById("originalCalc");
    const triangleCalc = document.getElementById("triangleCalc");
    const toggleBtn = document.getElementById("toggleCalcBtn");

    // Mặc định đang hiển thị máy tính Toán Học
    let showingOriginal = true;

    toggleBtn.addEventListener("click", () => {
      if (showingOriginal) {
        // Đang ở Toán Học => chuyển sang Tam Giác
        originalCalc.style.display = "none";
        triangleCalc.style.display = "block";
        toggleBtn.textContent = "Trở về Máy Tính Toán Học";
      } else {
        // Đang ở Tam Giác => quay lại Toán Học
        triangleCalc.style.display = "none";
        originalCalc.style.display = "block";
        toggleBtn.textContent = "Chuyển sang Máy Tính Tam Giác Vuông";
      }
      showingOriginal = !showingOriginal;
    });
  </script>
</body>
</html>
