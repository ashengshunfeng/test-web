<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Editable Transaction Agreement — Goldman Sachs</title>
  <style>
    /* A4 Portrait settings */
    @page { size: A4 portrait; margin: 20mm; }
    @media print { html, body { width: 210mm; height: 297mm; } }
    body { margin: 0; padding: 0; font-family: 'Segoe UI', sans-serif; background: #f4f4f4; color: #2c3e50; }
    .page { width: 210mm; min-height: 297mm; margin: 0 auto; padding: 20mm; background: #fff; box-sizing: border-box; position: relative; }
    /* Modal overlay */
    #loginModal { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.6); display: flex; align-items: center; justify-content: center; z-index: 1000; }
    #loginModal .modal { background: #fff; padding: 20px; border-radius: 8px; width: 320px; box-shadow: 0 2px 10px rgba(0,0,0,0.3); }
    #authTabs { text-align: center; margin-bottom: 10px; }
    #authTabs button { padding: 6px 12px; border: none; border-radius: 4px; margin: 0 4px; cursor: pointer; }
    #showLogin { background: #0052cc; color: #fff; }
    #showRegister { background: #ddd; color: #333; }
    .modal h3 { margin-top: 0; }
    .modal input { width: 100%; padding: 8px; margin: 8px 0; box-sizing: border-box; }
    .modal button { width: 100%; padding: 8px; margin-top: 8px; background: #0052cc; color: #fff; border: none; border-radius: 4px; cursor: pointer; }
    /* Editable content */
    .header-frame { background: #e9f3ff; border-radius: 6px; padding: 5px 20px; text-align: center; width: calc(100% - 10mm); margin: 0 auto 6mm auto; }
    .header-frame h1, .header-frame h2, .tags span { cursor: text; }
    .tags span { display: inline-block; margin: 0 4px; padding: 2px 4px; border: 1px solid #0052cc; border-radius: 6px; background: #f0f8ff; }
    .content { display: flex; flex-direction: column; gap: 6mm; font-size: 10pt; line-height: 1.5; }
    .section h3, .section p, .section ol { cursor: text; }
    .section ol { padding-left: 12mm; }
    .footer { display: flex; flex-direction: column; gap: 2.5mm; font-size: 10pt; }
    .sign-grid { display: grid; grid-template-columns: 1fr 1fr; align-items: flex-end; column-gap: 6mm; }
    .sign-block { position: relative; text-align: center; }
    .sign-block .line { border-top: 1px solid #555; margin-top: 2.5mm; width: 80%; margin: 0 auto; }
    .party-b .seal { position: absolute; width: 38mm; bottom: 10mm; left: 0mm; z-index: 3; cursor: move; }
    .party-b .signature { width: 60mm; margin: 0 auto 2.5mm; position: relative; z-index: 1; }
  </style>
</head>
<body>
  <div id="loginModal">
    <div class="modal">
      <div id="authTabs">
        <button id="showLogin">Đăng nhập</button>
        <button id="showRegister">Đăng ký</button>
      </div>
      <div id="loginForm">
        <h3>Đăng nhập</h3>
        <input type="text" id="username" placeholder="Tên đăng nhập" />
        <input type="password" id="password" placeholder="Mật khẩu" />
        <button id="loginBtn">Đăng nhập</button>
      </div>
      <div id="registerForm" style="display:none;">
        <h3>Đăng ký</h3>
        <input type="text" id="regUsername" placeholder="Tên đăng ký" />
        <input type="password" id="regPassword" placeholder="Mật khẩu" />
        <input type="password" id="regConfirm" placeholder="Xác nhận mật khẩu" />
        <button id="registerBtn">Đăng ký</button>
      </div>
    </div>
  </div>

  <div class="page" id="editor" contenteditable="false">
    <div class="header-frame">
      <h1 contenteditable="true">GOLDMAN SACHS GROUP</h1>
      <div class="tags">
        <span contenteditable="true">Golden Age</span>
        <span contenteditable="true">Safe</span>
        <span contenteditable="true">Legitimate</span>
      </div>
      <h2 contenteditable="true">Transaction Agreement</h2>
    </div>
    <div class="content">
      <div class="section">
        <h3 contenteditable="true">Article 1: Security & Fund Management</h3>
        <p contenteditable="true">Party B will execute combined orders based on Party A’s actual account balance, ensuring precise execution and optimized returns. Party B guarantees a 100% refund for all completed orders; incomplete orders are non-refundable. All funds remain fully secure within Party A’s account.</p>
      </div>
      <!-- Repeat for other articles with contenteditable elements -->
    </div>
    <div class="footer">
      <div class="date" contenteditable="true"><strong>Date:</strong> __________</div>
      <div class="sign-grid">
        <div class="sign-block party-a">
          <div class="line"></div>
          <div contenteditable="true">Signature of Party A (Trading Party)</div>
        </div>
        <div class="sign-block party-b">
          <img class="seal" src="https://i.imgur.com/7vNny0K.png" alt="Seal">
          <img class="signature" src="https://i.imgur.com/DWJ9Jj2.png" alt="Party B Signature">
          <div class="line"></div>
          <div contenteditable="true">Signature of Party B (Goldman Sachs)</div>
        </div>
      </div>
    </div>
  </div>

  <script>
    // Tab toggling
    document.getElementById('showLogin').onclick = () => {
      document.getElementById('loginForm').style.display = 'block';
      document.getElementById('registerForm').style.display = 'none';
      document.getElementById('showLogin').style.background='#0052cc';
      document.getElementById('showRegister').style.background='#ddd';
    };
    document.getElementById('showRegister').onclick = () => {
      document.getElementById('loginForm').style.display = 'none';
      document.getElementById('registerForm').style.display = 'block';
      document.getElementById('showRegister').style.background='#0052cc';
      document.getElementById('showLogin').style.background='#ddd';
    };
    // Simple auth & enable editing
    document.getElementById('loginBtn').onclick = () => {
      const u = document.getElementById('username').value;
      const p = document.getElementById('password').value;
      if(u==='admin' && p==='password'){
        document.getElementById('loginModal').style.display='none';
        document.getElementById('editor').setAttribute('contenteditable','true');
      } else alert('Invalid credentials');
    };
    // Drag & drop seal
    const seal = document.querySelector('.seal');
    seal.setAttribute('draggable','true');
    document.getElementById('editor').addEventListener('dragover', e=> e.preventDefault());
    document.getElementById('editor').addEventListener('drop', e=> {
      e.preventDefault();
      const x = e.offsetX - seal.width/2;
      const y = e.offsetY - seal.height/2;
      seal.style.left = x + 'px';
      seal.style.bottom = (document.getElementById('editor').clientHeight - y - seal.height) + 'px';
    });
  </script>
</body>
</html>
Update README.md
