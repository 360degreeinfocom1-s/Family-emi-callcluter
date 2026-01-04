<!DOCTYPE html>
<html>
<head>
  <title>Family Loan EMI Calculator</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #4e54c8, #8f94fb);
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #333;
    }

    .card {
      background: #ffffff;
      padding: 25px;
      border-radius: 15px;
      width: 350px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.2);
    }

    .logo {
      text-align: center;
      font-size: 26px;
      font-weight: bold;
      color: #4e54c8;
      margin-bottom: 10px;
    }

    h3 {
      text-align: center;
      margin-bottom: 20px;
    }

    input {
      width: 100%;
      padding: 10px;
      margin: 8px 0;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-size: 15px;
    }

    button {
      width: 100%;
      padding: 12px;
      background: #4e54c8;
      color: white;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      cursor: pointer;
      margin-top: 10px;
    }

    button:hover {
      background: #3c40a4;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 15px;
      font-size: 13px;
    }

    th, td {
      border: 1px solid #ddd;
      padding: 6px;
      text-align: center;
    }

    th {
      background: #f2f2f2;
    }

    .emi {
      text-align: center;
      font-size: 18px;
      margin-top: 15px;
      color: #4e54c8;
      font-weight: bold;
    }
  </style>
</head>
<body>

<div class="card">
  <div class="logo">🏠 Family Finance</div>
  <h3>Family Loan EMI Calculator</h3>

  <input id="loan" type="number" placeholder="Loan Amount (₹)" value="5000">
  <input id="rate" type="number" placeholder="Interest Rate (%)" value="4">
  <input id="months" type="number" placeholder="Tenure (Months)" value="12">

  <button onclick="calculate()">Calculate EMI</button>

  <div id="result"></div>
</div>

<script>
function calculate() {
  let P = Number(document.getElementById("loan").value);
  let R = Number(document.getElementById("rate").value) / 12 / 100;
  let N = Number(document.getElementById("months").value);

  let EMI = (P * R * Math.pow(1 + R, N)) / (Math.pow(1 + R, N) - 1);
  let balance = P;

  let html = `<div class="emi">Monthly EMI: ₹${EMI.toFixed(2)}</div>`;
  html += "<table><tr><th>Month</th><th>Interest</th><th>Principal</th><th>Balance</th></tr>";

  for (let i = 1; i <= N; i++) {
    let interest = balance * R;
    let principal = EMI - interest;
    balance -= principal;

    html += `<tr>
      <td>${i}</td>
      <td>${interest.toFixed(2)}</td>
      <td>${principal.toFixed(2)}</td>
      <td>${balance > 0 ? balance.toFixed(2) : 0}</td>
    </tr>`;
  }

  html += "</table>";
  document.getElementById("result").innerHTML = html;
}
</script>

</body>
</html>
