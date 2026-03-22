<!DOCTYPE html>
<html>
<head>
  <title>Water Magics App</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
</head>

<body style="margin:0;font-family:Arial;">

<div id="app"></div>

<script>
let role = null;
let screen = "dashboard";

function render() {
  const app = document.getElementById("app");

  // LOGIN
  if (!role) {
    app.innerHTML = `
      <div style="display:flex;flex-direction:column;align-items:center;justify-content:center;height:100vh;background:linear-gradient(#0f172a,#1d4ed8,#22d3ee);color:white;">
        <h1 style="font-size:48px;font-weight:900;letter-spacing:3px;">⛲ WATER MAGICS ⛲</h1>
        ${["Management","Marketing","Execution","Dealer","Customer","Accounts"].map(r => 
          `<button onclick="selectRole('${r}')" style="padding:12px;margin:6px;border-radius:12px;">${r}</button>`
        ).join("")}
      </div>
    `;
    return;
  }

  // ANALYTICS
  let analytics = `
    <h3>Analytics</h3>

    <div>
      <h4>📊 Marketing</h4>
      <p>Today Leads: 8</p>
      <p>This Month: 120</p>
      <p>Positive: 60 | Converted: 25 | Lost: 10</p>
    </div>

    <div>
      <h4>💰 Accounts</h4>
      <p>Today Income: ₹20,000 | Expenses: ₹8,000</p>
      <p>This Month vs Last Month Growth: +19%</p>
    </div>

    <div>
      <h4>🛠️ Execution</h4>
      <p>Running Projects: 6</p>
      <p>Project: Crown Fountain (70%)</p>
    </div>
  `;

  // ADD ENQUIRY
  let addEnquiry = `
    <h3>Add Enquiry</h3>
    <input placeholder="Name"/><br/>
    <input placeholder="Phone"/><br/>
    <input placeholder="Location"/><br/>
    <input placeholder="Fountain Type"/><br/>
    <input placeholder="Budget"/><br/><br/>

    <button style="background:green;color:white;">Qualified</button>
    <button style="background:orange;color:white;">Follow Later</button>
    <button style="background:red;color:white;">Not Interested</button>
  `;

  // BALANCE SHEET
  let balanceSheet = `
    <h3>Balance Sheet</h3>
    <p>Income</p>
    <p>Expenses</p>
    <p>Balance</p>
  `;

  // DASHBOARD
  let dashboard = "";

  if (role === "Marketing") {
    dashboard = `
      <button onclick="setScreen('addenquiry')">Add Enquiry</button>
      <button>Follow Ups</button>
    `;
  }

  if (role === "Management") {
    dashboard = `
      <button onclick="setScreen('analytics')">Analytics</button>
      <button onclick="setScreen('balancesheet')">Accounts</button>
    `;
  }

  if (role === "Accounts") {
    dashboard = `
      <button onclick="setScreen('balancesheet')">Balance Sheet</button>
    `;
  }

  app.innerHTML = `
    <div style="padding:20px;">
      <h2>${role} PANEL</h2>

      <button onclick="setScreen('dashboard')">Dashboard</button>

      <div style="margin-top:20px;">
        ${screen === "dashboard" ? dashboard : ""}
        ${screen === "analytics" ? analytics : ""}
        ${screen === "addenquiry" ? addEnquiry : ""}
        ${screen === "balancesheet" ? balanceSheet : ""}
      </div>

      <button onclick="logout()" style="margin-top:20px;background:red;color:white;">Logout</button>
    </div>
  `;
}

function selectRole(r) {
  role = r;
  screen = "dashboard";
  render();
}

function setScreen(s) {
  screen = s;
  render();
}

function logout() {
  role = null;
  render();
}

render();
</script>

</body>
</html>
