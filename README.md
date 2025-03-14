
<html lang="vi">
  <head>
    <meta charset="UTF-8" />
    <title>3 Máy Tính Tích Hợp</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <!-- Import phông chữ Lobster -->
    <link
      href="https://fonts.googleapis.com/css2?family=Lobster&display=swap"
      rel="stylesheet"
    />
    <!-- Include Nerdamer cho Máy Tính Toán Học -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/nerdamer/1.1.9/nerdamer.core.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/nerdamer/1.1.9/Algebra.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/nerdamer/1.1.9/Solve.js"></script>
    <style>
      /* =================== PHẦN CHUNG =================== */
      * {
        box-sizing: border-box;
      }
      body {
        margin: 0;
        font-family: "Lobster", cursive;
        background: linear-gradient(120deg, #ffe2f2, #e1fffe);
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        background-attachment: fixed;
      }
      /* Thanh điều hướng (topBar) chứa 3 nút */
      .topBar {
        width: 100%;
        text-align: center;
        padding: 15px 0;
        margin-bottom: 20px;
      }
      .topBar button {
        border: 3px dashed #ff6f91; /* viền nét đứt màu hồng */
        border-radius: 20px;
        padding: 20px 40px;
        margin: 0 10px;
        color: #ff6f91;
        font-size: 1.8rem;
        cursor: pointer;
        background: #fff;
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
        transition: background 0.3s, color 0.3s;
      }
      .topBar button:hover {
        background: #ffe2f2;
        color: #ff4f7f;
      }
      /* Container chung cho mỗi máy tính */
      .container {
        max-width: 900px;
        width: 90%;
        background: #fff;
        border-radius: 14px;
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
        padding: 20px 30px;
        margin-bottom: 30px;
        display: none;
      }
      /* =================== 1) MÁY TÍNH TOÁN HỌC (calcMath) =================== */
      #calcMath {
        display: block; /* Mặc định hiển thị Máy Tính Toán Học */
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
        text-align: center;
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
      .calcBtn {
        width: 100%;
        padding: 20px;
        font-size: 2rem;
        background: linear-gradient(135deg, #ff8a65, #ff7043);
        color: #fff;
        border: none;
        border-radius: 10px;
        cursor: pointer;
        transition: background 0.3s, box-shadow 0.3s;
        margin-bottom: 30px;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
      }
      .calcBtn:hover {
        background: linear-gradient(135deg, #ff7043, #ff8a65);
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
      }
      .resultMath {
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
      /* =================== 2) MÁY TÍNH TAM GIÁC VUÔNG (calcTriangle) =================== */
      #calcTriangle {
        background: linear-gradient(135deg, #ff4b2b, #ffcc00);
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
      #canvasContainer {
        display: inline-block;
        padding: 10px;
        background-color: #fcebd0;
        border: 2px solid #d32f2f;
        border-radius: 15px;
        margin: 10px auto;
      }
      .angleCheckContainer {
        display: flex;
        align-items: center;
        margin-bottom: 10px;
      }
      .angleCheckContainer label {
        margin-right: 10px;
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
      /* =================== 3) MÁY TÍNH TAM GIÁC TRUNG ĐIỂM (calcMidpoint) =================== */
      #calcMidpoint {
      }
      .input-fields {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
        gap: 10px;
        margin-bottom: 15px;
      }
      .input-field label {
        display: inline-block;
        width: 40px;
        font-weight: 600;
        color: #444;
      }
      .input-field input[type="number"] {
        width: 70px;
        text-align: right;
        padding: 3px 6px;
        border: 1px solid #ccc;
        border-radius: 6px;
      }
      #message {
        margin-top: 10px;
        color: red;
        font-weight: bold;
      }
      .result-values {
        margin-top: 10px;
        padding: 10px;
        background: #f3f7ff;
        border-radius: 8px;
      }
      .formula {
        margin-top: 20px;
        padding: 10px;
        background: #faf0ff;
        border-radius: 8px;
      }
      #canvasMidpoint {
        background: #fafafa;
        border-radius: 10px;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
      }
    </style>
  </head>
  <body>
    <!-- Thanh điều hướng -->
    <div class="topBar">
      <button id="btnCalcMath">Máy Tính Toán Học</button>
      <button id="btnCalcTriangle">Tam Giác Vuông</button>
      <button id="btnCalcMidpoint">Tam Giác Trung Điểm</button>
    </div>

    <!-- 1) Máy tính Toán Học -->
    <div class="container" id="calcMath">
      <h1>Máy Tính Toán Học</h1>
      <div id="expression" contenteditable="true"></div>
      <div id="keyboard" class="keyboard"></div>
      <button class="calcBtn" id="calculateBtn">Tính Toán</button>
      <div class="resultMath">Kết quả: <span id="result"></span></div>
      <div class="explanation">
        <strong>Giải thích:</strong>
        <div id="explanation"></div>
      </div>
    </div>

    <!-- 2) Máy tính Tam Giác Vuông -->
    <div class="container" id="calcTriangle">
      <h2>Máy Tính Tam Giác Vuông</h2>
      <p>
        Nhập 2 hoặc 3 cạnh (có thể nhập cạnh huyền). Tam giác được vẽ với góc
        vuông ở đỉnh V1.
      </p>
      <label>Cạnh ngang (W):</label>
      <input type="number" id="sideB" placeholder="Ví dụ: 4" step="any" /><br />
      <label>Cạnh dọc (L):</label>
      <input type="number" id="sideC" placeholder="Ví dụ: 3" step="any" /><br />
      <label>Cạnh huyền (tùy chọn):</label>
      <input type="number" id="sideA" placeholder="Ví dụ: 5" step="any" /><br />
      <h2>Nhãn Góc</h2>
      <p>
        Mặc định: V1 = góc vuông, V2, V3. Nhấn ô vuông bên cạnh V2 hoặc V3 để
        hoán đổi.
      </p>
      <div class="angleCheckContainer">
        <label for="labelA">Góc V1:</label>
        <input type="text" id="labelA" value="A" maxlength="10" />
        <div class="checkSquare" id="checkA">✓</div>
      </div>
      <div class="angleCheckContainer">
        <label for="labelB">Góc V2:</label>
        <input type="text" id="labelB" value="B" maxlength="10" />
        <div class="checkSquare" id="checkB"></div>
      </div>
      <div class="angleCheckContainer">
        <label for="labelC">Góc V3:</label>
        <input type="text" id="labelC" value="C" maxlength="10" />
        <div class="checkSquare" id="checkC"></div>
      </div>
      <button class="calcBtn" onclick="calculateTriangle()">Tính Toán</button>
      <div id="triangleResult"></div>
      <div id="canvasContainer">
        <canvas id="triangleCanvas" width="400" height="400"></canvas>
      </div>
    </div>

    <!-- 3) Máy tính Tam Giác Trung Điểm -->
    <div class="container" id="calcMidpoint">
      <h1>Máy Tính Tam Giác Trung Điểm</h1>
      <p>
        Nhập 8 giá trị: <strong>AB, AD, BD, BC, BE, EC, AC, DE</strong>.<br />
        (Bạn có thể nhập một vài ô; chương trình sẽ tự tính các giá trị còn
        thiếu theo ràng buộc:
        <br />– D là trung điểm AB (⇒ AD = BD, AB = 2×AD) <br />– E là trung
        điểm BC (⇒ BE = EC, BC = 2×BE) <br />– DE = AC/2)
      </p>
      <div class="input-fields">
        <div class="input-field">
          <label for="AB">AB:</label>
          <input type="number" id="AB" placeholder="..." step="any" />
        </div>
        <div class="input-field">
          <label for="AD">AD:</label>
          <input type="number" id="AD" placeholder="..." step="any" />
        </div>
        <div class="input-field">
          <label for="BD">BD:</label>
          <input type="number" id="BD" placeholder="..." step="any" />
        </div>
        <div class="input-field">
          <label for="BC">BC:</label>
          <input type="number" id="BC" placeholder="..." step="any" />
        </div>
        <div class="input-field">
          <label for="BE">BE:</label>
          <input type="number" id="BE" placeholder="..." step="any" />
        </div>
        <div class="input-field">
          <label for="EC">EC:</label>
          <input type="number" id="EC" placeholder="..." step="any" />
        </div>
        <div class="input-field">
          <label for="AC">AC:</label>
          <input type="number" id="AC" placeholder="..." step="any" />
        </div>
        <div class="input-field">
          <label for="DE">DE:</label>
          <input type="number" id="DE" placeholder="..." step="any" />
        </div>
      </div>
      <button onclick="xuLy()">Tính &amp; Vẽ</button>
      <div id="message"></div>
      <div class="result-values">
        <p><strong>Kết quả tính được:</strong></p>
        <p id="ketQua"></p>
      </div>
      <div style="display: flex; justify-content: center; margin-top: 20px">
        <canvas id="canvasMidpoint" width="600" height="400"></canvas>
      </div>
      <div class="formula">
        <h3>Các ràng buộc</h3>
        <ul>
          <li>D là trung điểm AB ⇒ AD = BD, AB = 2×AD</li>
          <li>E là trung điểm BC ⇒ BE = EC, BC = 2×BE</li>
          <li>DE = AC/2 (đường trung bình, song song AC)</li>
        </ul>
      </div>
    </div>

    <!-- ====================== Mã JavaScript ====================== -->
    <!-- 1) Mã cho Máy Tính Toán Học -->
    <script>
      // Các hàm xử lý con trỏ và bàn phím
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
          (k) => diffCoefficients[k] !== 0
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
          let msg = "Phương trình có nhiều biến: ";
          nonZeroVars.forEach(function (varName) {
            msg += varName + " (hệ số: " + diffCoefficients[varName] + "), ";
          });
          msg +=
            "với số hạng tự do: " +
            totalConstant +
            ".<br>Không thể giải được duy nhất.";
          return msg;
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
          explanation +=
            "+ Số dương nhân số âm (hoặc ngược lại) cho ra số âm.<br>";
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
      document
        .getElementById("calculateBtn")
        .addEventListener("click", calculate);
      renderKeyboard();
    </script>

    <!-- 2) Mã cho Máy Tính Tam Giác Vuông -->
    <script>
      // --- Máy Tính Tam Giác Vuông ---
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
      checkA.addEventListener("click", () => {});
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
        let W = parseFloat(document.getElementById("sideB").value);
        let L = parseFloat(document.getElementById("sideC").value);
        let hyp = parseFloat(document.getElementById("sideA").value);
        let providedW = !isNaN(W),
          providedL = !isNaN(L),
          providedH = !isNaN(hyp);
        let countProvided =
          (providedW ? 1 : 0) + (providedL ? 1 : 0) + (providedH ? 1 : 0);
        if (countProvided < 2) {
          document.getElementById("triangleResult").innerHTML =
            "<p>Vui lòng nhập ít nhất 2 giá trị (W, L, hoặc cạnh huyền).</p>";
          clearCanvasTriangle();
          return;
        }
        if (countProvided === 2) {
          if (!providedH) {
            hyp = Math.sqrt(W * W + L * L);
          } else if (!providedW) {
            let temp = hyp * hyp - L * L;
            if (temp < 0) {
              document.getElementById("triangleResult").innerHTML =
                "<p>Dữ liệu không hợp lệ: Cạnh huyền phải > cạnh dọc.</p>";
              clearCanvasTriangle();
              return;
            }
            W = Math.sqrt(temp);
          } else if (!providedL) {
            let temp = hyp * hyp - W * W;
            if (temp < 0) {
              document.getElementById("triangleResult").innerHTML =
                "<p>Dữ liệu không hợp lệ: Cạnh huyền phải > cạnh ngang.</p>";
              clearCanvasTriangle();
              return;
            }
            L = Math.sqrt(temp);
          }
        } else {
          let diff = Math.abs(W * W + L * L - hyp * hyp);
          let eps = 1e-6;
          if (diff > eps) {
            document.getElementById("triangleResult").innerHTML =
              "<p>Dữ liệu không hợp lệ: W² + L² không bằng cạnh huyền².</p>";
            clearCanvasTriangle();
            return;
          }
        }
        let angleV2 = (Math.atan(L / W) * 180) / Math.PI;
        let angleV3 = 90 - angleV2;
        let resHTML = `<p>Góc vuông: ${v1_label} = 90°</p>`;
        resHTML += `<p>Các góc còn lại: ${v2_label} = ${angleV2.toFixed(
          2
        )}°, ${v3_label} = ${angleV3.toFixed(2)}°</p>`;
        resHTML += `<p>Các cạnh: Huyền (đối ${v1_label}) = ${hyp.toFixed(
          2
        )}, Ngang (${v1_label}-${v2_label}) = ${W.toFixed(
          2
        )}, Dọc (${v1_label}-${v3_label}) = ${L.toFixed(2)}</p>`;
        document.getElementById("triangleResult").innerHTML = resHTML;
        drawTriangle(W, L);
      }
      function drawTriangle(W, L) {
        const margin = 50,
          scale = 50;
        let canvas = document.getElementById("triangleCanvas");
        let ctx = canvas.getContext("2d");
        let width = Math.max(400, margin + W * scale + margin);
        let height = Math.max(400, margin + L * scale + margin);
        canvas.width = width;
        canvas.height = height;
        document.getElementById("canvasContainer").style.width = width + "px";
        document.getElementById("canvasContainer").style.height = height + "px";
        ctx.clearRect(0, 0, width, height);
        let V1 = { x: margin, y: margin + L * scale };
        let V2 = { x: margin + W * scale, y: margin + L * scale };
        let V3 = { x: margin, y: margin };
        ctx.beginPath();
        ctx.moveTo(V1.x, V1.y);
        ctx.lineTo(V2.x, V2.y);
        ctx.lineTo(V3.x, V3.y);
        ctx.closePath();
        ctx.lineWidth = 2;
        ctx.strokeStyle = "#333";
        ctx.stroke();
        let marker = 20;
        ctx.beginPath();
        ctx.moveTo(V1.x + marker, V1.y);
        ctx.lineTo(V1.x + marker, V1.y - marker);
        ctx.lineTo(V1.x, V1.y - marker);
        ctx.stroke();
        ctx.font = "18px 'Lobster', cursive";
        ctx.fillStyle = "#d32f2f";
        ctx.fillText(v1_label, V1.x - 30, V1.y + 25);
        ctx.fillText(v2_label, V2.x + 10, V2.y + 25);
        ctx.fillText(v3_label, V3.x - 30, V3.y - 10);
        ctx.fillStyle = "#1976d2";
        let midV1V2 = { x: (V1.x + V2.x) / 2, y: (V1.y + V2.y) / 2 };
        let midV1V3 = { x: (V1.x + V3.x) / 2, y: (V1.y + V3.y) / 2 };
        let midV2V3 = { x: (V2.x + V3.x) / 2, y: (V2.y + V3.y) / 2 };
        ctx.fillText(W.toFixed(2), midV1V2.x, midV1V2.y + 25);
        ctx.fillText(L.toFixed(2), midV1V3.x - 35, midV1V3.y);
        ctx.fillText(
          Math.sqrt(W * W + L * L).toFixed(2),
          midV2V3.x + 10,
          midV2V3.y
        );
      }
      function clearCanvasTriangle() {
        let canvas = document.getElementById("triangleCanvas");
        let ctx = canvas.getContext("2d");
        ctx.clearRect(0, 0, canvas.width, canvas.height);
      }
      calculateTriangle();
    </script>

    <!-- 3) Máy Tính Tam Giác Trung Điểm -->
    <script>
      let vals = {
        AB: null,
        AD: null,
        BD: null,
        BC: null,
        BE: null,
        EC: null,
        AC: null,
        DE: null,
      };
      function readVal(id) {
        const v = document.getElementById(id).value.trim();
        return v === "" ? null : parseFloat(v);
      }
      function fmt(v) {
        return v == null ? "—" : v.toFixed(2);
      }
      function showMessage(msg) {
        document.getElementById("message").textContent = msg;
      }
      function clearCanvasDE() {
        const canvas = document.getElementById("canvasMidpoint");
        const ctx = canvas.getContext("2d");
        ctx.clearRect(0, 0, canvas.width, canvas.height);
      }
      function xuLy() {
        clearCanvasDE();
        showMessage("");
        vals.AB = readVal("AB");
        vals.AD = readVal("AD");
        vals.BD = readVal("BD");
        vals.BC = readVal("BC");
        vals.BE = readVal("BE");
        vals.EC = readVal("EC");
        vals.AC = readVal("AC");
        vals.DE = readVal("DE");
        let changed = true;
        let loopCount = 0;
        while (changed && loopCount < 10) {
          changed = false;
          loopCount++;
          if (vals.AB != null && vals.AB > 0) {
            if (vals.AD == null) {
              vals.AD = vals.AB / 2;
              changed = true;
            }
            if (vals.BD == null) {
              vals.BD = vals.AB / 2;
              changed = true;
            }
          }
          if (vals.AD != null && vals.AD > 0) {
            if (vals.AB == null) {
              vals.AB = 2 * vals.AD;
              changed = true;
            }
            if (vals.BD == null) {
              vals.BD = vals.AD;
              changed = true;
            }
          }
          if (vals.BD != null && vals.BD > 0) {
            if (vals.AB == null) {
              vals.AB = 2 * vals.BD;
              changed = true;
            }
            if (vals.AD == null) {
              vals.AD = vals.BD;
              changed = true;
            }
          }
          if (vals.AD != null && vals.BD != null) {
            if (Math.abs(vals.AD - vals.BD) > 1e-9) {
              showMessage("Mâu thuẫn: AD phải = BD (D là trung điểm AB)!");
              return;
            }
            if (vals.AB != null && Math.abs(vals.AB - 2 * vals.AD) > 1e-9) {
              showMessage("Mâu thuẫn: AB phải = 2×AD!");
              return;
            }
          }
          if (vals.BC != null && vals.BC > 0) {
            if (vals.BE == null) {
              vals.BE = vals.BC / 2;
              changed = true;
            }
            if (vals.EC == null) {
              vals.EC = vals.BC / 2;
              changed = true;
            }
          }
          if (vals.BE != null && vals.BE > 0) {
            if (vals.BC == null) {
              vals.BC = 2 * vals.BE;
              changed = true;
            }
            if (vals.EC == null) {
              vals.EC = vals.BE;
              changed = true;
            }
          }
          if (vals.EC != null && vals.EC > 0) {
            if (vals.BC == null) {
              vals.BC = 2 * vals.EC;
              changed = true;
            }
            if (vals.BE == null) {
              vals.BE = vals.EC;
              changed = true;
            }
          }
          if (vals.BE != null && vals.EC != null) {
            if (Math.abs(vals.BE - vals.EC) > 1e-9) {
              showMessage("Mâu thuẫn: BE phải = EC (E là trung điểm BC)!");
              return;
            }
            if (vals.BC != null && Math.abs(vals.BC - 2 * vals.BE) > 1e-9) {
              showMessage("Mâu thuẫn: BC phải = 2×BE!");
              return;
            }
          }
          if (vals.AC != null && vals.AC > 0) {
            if (vals.DE == null) {
              vals.DE = vals.AC / 2;
              changed = true;
            } else if (Math.abs(vals.DE - vals.AC / 2) > 1e-9) {
              showMessage("Mâu thuẫn: DE phải = AC/2!");
              return;
            }
          }
          if (vals.DE != null && vals.DE > 0) {
            if (vals.AC == null) {
              vals.AC = 2 * vals.DE;
              changed = true;
            } else if (Math.abs(vals.AC - 2 * vals.DE) > 1e-9) {
              showMessage("Mâu thuẫn: AC phải = 2×DE!");
              return;
            }
          }
        }
        let html = "";
        html += "AB = " + fmt(vals.AB) + "<br/>";
        html += "AD = " + fmt(vals.AD) + "<br/>";
        html += "BD = " + fmt(vals.BD) + "<br/>";
        html += "BC = " + fmt(vals.BC) + "<br/>";
        html += "BE = " + fmt(vals.BE) + "<br/>";
        html += "EC = " + fmt(vals.EC) + "<br/>";
        html += "AC = " + fmt(vals.AC) + "<br/>";
        html += "DE = " + fmt(vals.DE) + "<br/>";
        document.getElementById("ketQua").innerHTML = html;
        if (
          vals.AB != null &&
          vals.AB > 0 &&
          vals.BC != null &&
          vals.BC > 0 &&
          vals.AC != null &&
          vals.AC > 0
        ) {
          if (
            vals.AB + vals.BC <= vals.AC ||
            vals.AB + vals.AC <= vals.BC ||
            vals.BC + vals.AC <= vals.AB
          ) {
            showMessage("Không thoả mãn bất đẳng thức tam giác!");
            return;
          }
          drawTriangleMidpoint();
        } else {
          showMessage("Cần AB, BC, AC > 0 để vẽ tam giác!");
        }
      }
      function drawTriangleMidpoint() {
        const canvas = document.getElementById("canvasMidpoint");
        const ctx = canvas.getContext("2d");
        const A = { x: 0, y: 0 };
        const B = { x: vals.AB, y: 0 };
        const xC =
          (vals.AB * vals.AB + vals.AC * vals.AC - vals.BC * vals.BC) /
          (2 * vals.AB);
        let tmp = vals.AC * vals.AC - xC * xC;
        if (tmp < 0) tmp = 0;
        const yC = Math.sqrt(tmp);
        const C = { x: xC, y: yC };
        const D = { x: (A.x + B.x) / 2, y: (A.y + B.y) / 2 };
        const E = { x: (B.x + C.x) / 2, y: (B.y + C.y) / 2 };
        const pts = [A, B, C, D, E];
        let minX = Math.min(...pts.map((p) => p.x));
        let maxX = Math.max(...pts.map((p) => p.x));
        let minY = Math.min(...pts.map((p) => p.y));
        let maxY = Math.max(...pts.map((p) => p.y));
        let rangeX = maxX - minX;
        let rangeY = maxY - minY;
        if (rangeX < 1) rangeX = 1;
        if (rangeY < 1) rangeY = 1;
        let dynamicWidth = Math.round(rangeX * 40 + 200);
        let dynamicHeight = Math.round(rangeY * 40 + 200);
        dynamicWidth = Math.max(dynamicWidth, 300);
        dynamicHeight = Math.max(dynamicHeight, 300);
        dynamicWidth = Math.min(dynamicWidth, 1200);
        dynamicHeight = Math.min(dynamicHeight, 800);
        canvas.width = dynamicWidth;
        canvas.height = dynamicHeight;
        const padding = 20;
        const w = canvas.width - 2 * padding;
        const h = canvas.height - 2 * padding;
        const scale = Math.min(w / rangeX, h / rangeY);
        function toCanvasX(x) {
          return padding + (x - minX) * scale;
        }
        function toCanvasY(y) {
          return canvas.height - padding - (y - minY) * scale;
        }
        function distance(p1, p2) {
          return Math.sqrt((p1.x - p2.x) ** 2 + (p1.y - p2.y) ** 2);
        }
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        function drawLine(p1, p2, color = "black") {
          ctx.beginPath();
          ctx.moveTo(toCanvasX(p1.x), toCanvasY(p1.y));
          ctx.lineTo(toCanvasX(p2.x), toCanvasY(p2.y));
          ctx.strokeStyle = color;
          ctx.lineWidth = 2;
          ctx.stroke();
        }
        function drawPoint(p, label) {
          const cx = toCanvasX(p.x);
          const cy = toCanvasY(p.y);
          ctx.fillStyle = "blue";
          ctx.beginPath();
          ctx.arc(cx, cy, 4, 0, 2 * Math.PI);
          ctx.fill();
          ctx.fillStyle = "black";
          ctx.font = "14px Arial";
          ctx.fillText(label, cx + 8, cy - 8);
        }
        function drawEdgeLabel(p1, p2, lengthVal) {
          const t = 0.55;
          const midX = p1.x + t * (p2.x - p1.x);
          const midY = p1.y + t * (p2.y - p1.y);
          const cx = toCanvasX(midX);
          const cy = toCanvasY(midY);
          const dx = (p2.x - p1.x) * scale;
          const dy = (p2.y - p1.y) * scale;
          const segLen = Math.sqrt(dx * dx + dy * dy);
          if (segLen < 1e-9) return;
          const offset = 25;
          const perpX = -dy / segLen;
          const perpY = dx / segLen;
          const labelX = cx + perpX * offset;
          const labelY = cy + perpY * offset;
          ctx.fillStyle = "red";
          ctx.font = "13px Arial";
          ctx.fillText(lengthVal.toFixed(2), labelX, labelY);
        }
        drawLine(A, B);
        drawLine(B, C);
        drawLine(C, A);
        drawLine(D, E, "red");
        drawPoint(A, "A");
        drawPoint(B, "B");
        drawPoint(C, "C");
        drawPoint(D, "D");
        drawPoint(E, "E");
        drawEdgeLabel(A, B, distance(A, B));
        drawEdgeLabel(B, C, distance(B, C));
        drawEdgeLabel(C, A, distance(C, A));
        drawEdgeLabel(A, D, distance(A, D));
        drawEdgeLabel(B, D, distance(B, D));
        drawEdgeLabel(B, E, distance(B, E));
        drawEdgeLabel(E, C, distance(E, C));
        drawEdgeLabel(D, E, distance(D, E));
      }
    </script>

    <!-- Script chuyển đổi giữa 3 máy tính -->
    <script>
      const calcMath = document.getElementById("calcMath");
      const calcTriangle = document.getElementById("calcTriangle");
      const calcMidpoint = document.getElementById("calcMidpoint");
      const btnCalcMath = document.getElementById("btnCalcMath");
      const btnCalcTriangle = document.getElementById("btnCalcTriangle");
      const btnCalcMidpoint = document.getElementById("btnCalcMidpoint");
      calcMath.style.display = "block";
      calcTriangle.style.display = "none";
      calcMidpoint.style.display = "none";
      btnCalcMath.addEventListener("click", () => {
        calcMath.style.display = "block";
        calcTriangle.style.display = "none";
        calcMidpoint.style.display = "none";
      });
      btnCalcTriangle.addEventListener("click", () => {
        calcMath.style.display = "none";
        calcTriangle.style.display = "block";
        calcMidpoint.style.display = "none";
      });
      btnCalcMidpoint.addEventListener("click", () => {
        calcMath.style.display = "none";
        calcTriangle.style.display = "none";
        calcMidpoint.style.display = "block";
      });
    </script>
  </body>
</html>
