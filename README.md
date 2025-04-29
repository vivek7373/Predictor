# Predictor<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Big-Small Predictor Simulator</title>
  <style>
    body { font-family: Arial; background: #121212; color: #fff; text-align: center; padding: 20px; }
    .box { background: #1e1e1e; padding: 20px; border-radius: 10px; margin: auto; max-width: 400px; }
    button { margin: 10px; padding: 10px 20px; border: none; border-radius: 5px; background: #2196F3; color: white; font-size: 16px; }
    .result { font-size: 24px; margin-top: 20px; }
    .history { font-size: 14px; margin-top: 10px; color: #ccc; }
  </style>
</head>
<body>
  <div class="box">
    <h2>Big-Small Result Simulator</h2><div>
  <label><strong>Mode:</strong></label><br>
  <button onclick="setMode('auto')">AI Prediction</button>
  <button onclick="setMode('manual')">Manual Set</button>
</div>

<div id="manualControls" style="display:none;">
  <label>Set Next Result:</label><br>
  <button onclick="manualSet('Big')">Big</button>
  <button onclick="manualSet('Small')">Small</button>
</div>

<button onclick="generateResult()">Generate Result</button>

<div class="result" id="result"></div>
<div class="history" id="history"></div>

  </div>  <script>
    let mode = 'auto';
    let manualResult = '';
    let history = [];

    function setMode(m) {
      mode = m;
      document.getElementById('manualControls').style.display = (m === 'manual') ? 'block' : 'none';
    }

    function manualSet(value) {
      manualResult = value;
    }

    function generateResult() {
      let result = '';

      if (mode === 'manual') {
        result = manualResult || 'Not Set';
      } else {
        // Count Big and Small in history
        let bigs = history.filter(r => r === 'Big').length;
        let smalls = history.filter(r => r === 'Small').length;

        let probabilitySmall = 50;
        if (bigs > smalls) probabilitySmall = 60;
        else if (smalls > bigs) probabilitySmall = 40;

        let rand = Math.random() * 100;
        result = rand < probabilitySmall ? 'Small' : 'Big';
      }

      history.unshift(result);
      if (history.length > 10) history.pop();

      document.getElementById('result').innerText = "Result: " + result;
      document.getElementById('history').innerText = "History: " + history.join(', ');
    }
  </script></body>
</html>
