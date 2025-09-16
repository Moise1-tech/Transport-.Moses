# Transport-.Moses
Tis is my project that  aim to help in transport easly which can be used by trasport company and increas custom3
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Transport Connect</title>
  <style>
    /* General styles */
    body { font-family: Arial, sans-serif; margin: 0; padding: 0; }
    header { background: #333; color: #fff; padding: 10px; text-align: center; }
    nav a { color: white; margin: 0 15px; text-decoration: none; font-weight: bold; }
    section { padding: 20px; min-height: 80vh; }

    /* Backgrounds */
    #home { background: #FFD54F; }
    #about { background: #0EA5E9; color: white; }
    #account { background: #f3f3f3; }
    #database { background: #fff8e1; }
    #help { background: #4CAF50; color: white; }

    /* Forms */
    form { margin-top: 15px; }
    input, select, button, textarea {
      padding: 8px; margin: 5px 0; width: 100%; max-width: 400px;
      border: 1px solid #ccc; border-radius: 5px;
    }
    button { background: #333; color: #fff; cursor: pointer; }

    table { border-collapse: collapse; margin-top: 15px; }
    th, td { border: 1px solid #333; padding: 8px; text-align: left; }

    footer { text-align: center; padding: 15px; background: #333; color: white; }

    /* Chat button */
    #chatBtn {
      position: fixed; bottom: 20px; right: 20px; background: #0EA5E9;
      color: white; border: none; border-radius: 50%; width: 60px; height: 60px;
      font-size: 24px; cursor: pointer;
    }
    #chatBox {
      display: none; position: fixed; bottom: 90px; right: 20px;
      width: 300px; height: 400px; background: white; border: 1px solid #ccc;
      border-radius: 10px; box-shadow: 0 0 10px rgba(0,0,0,0.2);
      flex-direction: column;
    }
    #chatMessages { flex: 1; padding: 10px; overflow-y: auto; }
    #chatInput { display: flex; }
    #chatInput input { flex: 1; border-radius: 0; }
    #chatInput button { border-radius: 0; }
  </style>
</head>
<body>

<header>
  <h1>Transport Connect</h1>
  <nav>
    <a href="#home">Home</a>
    <a href="#about">About</a>
    <a href="#account">Account</a>
    <a href="#database">Database</a>
    <a href="#help">Help</a>
  </nav>
</header>

<section id="home">
  <h2>Welcome to Transport Connect</h2>
  <p>This platform helps connect customers with transport companies and drivers.</p>
  <p>Steps to use: create an account, login, request transport, and communicate with drivers.</p>
</section>

<section id="about">
  <h2>About</h2>
  <p>Transport Connect is a system designed to connect customers with transport companies quickly and securely.</p>
</section>

<section id="account">
  <h2>Account</h2>
  <h3>Create Account</h3>
  <form id="createAccountForm">
    <input type="text" placeholder="Name" required>
    <input type="email" placeholder="Email" required>
    <input type="password" placeholder="Password" required>
    <select>
      <option value="customer">Customer</option>
      <option value="driver">Driver</option>
    </select>
    <button type="submit">Create Account</button>
  </form>

  <h3>Login</h3>
  <form id="loginForm">
    <input type="email" placeholder="Email" required>
    <input type="password" placeholder="Password" required>
    <button type="submit">Login</button>
  </form>

  <h3>Forgot Password</h3>
  <form id="forgotPasswordForm">
    <input type="email" placeholder="Enter your email" required>
    <button type="submit">Recover Password</button>
  </form>
</section>

<section id="database">
  <h2>Database Entry</h2>
  <form id="dataForm">
    <input type="text" id="name" placeholder="Full Name" required>
    <input type="text" id="address" placeholder="Address" required>
    <input type="email" id="contact" placeholder="Email" required>
    <input type="text" id="phone" placeholder="Phone" required>
    <select id="role">
      <option value="customer">Customer</option>
      <option value="driver">Driver</option>
    </select>
    <input type="text" id="vehicle" placeholder="Vehicle (if driver)">
    <label>Payment Mode:</label>
    <select id="payment">
      <option value="visa">💳 Visa Card</option>
      <option value="momopay">📱 MomoPay</option>
      <option value="bank">🏦 Bank</option>
    </select>
    <button type="submit">Save Record</button>
  </form>

  <h3>Records</h3>
  <table id="recordsTable">
    <thead>
      <tr>
        <th>Name</th><th>Address</th><th>Email</th><th>Phone</th><th>Role</th><th>Vehicle</th><th>Payment</th><th>Action</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>
</section>

<section id="help">
  <h2>Help & Contact</h2>
  <p>Phone: +250785621733</p>
  <p>Email: moisendaruhutse77@gmail.com</p>
</section>

<footer>
  <p>Developed by NDARUHUTSE MOISE</p>
</footer>

<!-- Chat Button -->
<button id="chatBtn">💬</button>
<div id="chatBox">
  <div id="chatMessages"></div>
  <div id="chatInput">
    <input type="text" id="chatText" placeholder="Type a message...">
    <button id="sendBtn">Send</button>
  </div>
</div>

<script>
  // Database handling
  const dataForm = document.getElementById('dataForm');
  const recordsTable = document.querySelector('#recordsTable tbody');
  let records = JSON.parse(localStorage.getItem('records') || '[]');

  function renderRecords() {
    recordsTable.innerHTML = '';
    records.forEach((rec, i) => {
      const row = `<tr>
        <td>${rec.name}</td><td>${rec.address}</td><td>${rec.contact}</td>
        <td>${rec.phone}</td><td>${rec.role}</td><td>${rec.vehicle}</td><td>${rec.payment}</td>
        <td><button onclick="deleteRecord(${i})">Delete</button></td>
      </tr>`;
      recordsTable.innerHTML += row;
    });
  }
  function deleteRecord(i) {
    records.splice(i,1);
    localStorage.setItem('records', JSON.stringify(records));
    renderRecords();
  }
  dataForm.addEventListener('submit', e => {
    e.preventDefault();
    const rec = {
      name: document.getElementById('name').value,
      address: document.getElementById('address').value,
      contact: document.getElementById('contact').value,
      phone: document.getElementById('phone').value,
      role: document.getElementById('role').value,
      vehicle: document.getElementById('vehicle').value,
      payment: document.getElementById('payment').value
    };
    records.push(rec);
    localStorage.setItem('records', JSON.stringify(records));
    renderRecords();
    dataForm.reset();
  });
  renderRecords();

  // Chat system
  const chatBtn = document.getElementById('chatBtn');
  const chatBox = document.getElementById('chatBox');
  const chatMessages = document.getElementById('chatMessages');
  const chatText = document.getElementById('chatText');
  const sendBtn = document.getElementById('sendBtn');

  chatBtn.addEventListener('click', () => {
    chatBox.style.display = chatBox.style.display === 'flex' ? 'none' : 'flex';
    chatBox.style.flexDirection = 'column';
  });

  function addMessage(sender, text) {
    const p = document.createElement('p');
    p.textContent = sender + ": " + text;
    chatMessages.appendChild(p);
    chatMessages.scrollTop = chatMessages.scrollHeight;
  }

  sendBtn.addEventListener('click', () => {
    const msg = chatText.value.trim();
    if (!msg) return;
    addMessage("You", msg);
    chatText.value = "";
    setTimeout(() => addMessage("Driver", "Got your message: " + msg), 1000);
  });
</script>
</body>
</html>
