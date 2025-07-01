<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Editable Transaction Agreement — Goldman Sachs</n  <style>
    /* A4 Portrait settings */
    @page { size: A4 portrait; margin: 20mm; }
    @media print { html, body { width: 210mm; height: 297mm; } }
    body { margin:0; padding:0; font-family:'Segoe UI',sans-serif; background:#f4f4f4; color:#2c3e50; }
    .page { width:210mm; min-height:297mm; margin:40px auto; padding:20mm; background:#fff; box-sizing:border-box;
             position: relative; }
    /* Login Modal */
    #loginModal { position: absolute; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.6);
                  display:flex; align-items:center; justify-content:center; z-index:1000; }
    #loginModal .modal { background:#fff; padding:20px; border-radius:8px; width:300px; box-shadow:0 2px 10px rgba(0,0,0,0.3); }
    #loginModal input { width:100%; padding:8px; margin:8px 0; }
    #loginModal button { width:100%; padding:8px; margin-top:8px; background:#0052cc; color:#fff; border:none; border-radius:4px; }
    /* Header */
    .header-frame { background:#e9f3ff; border-radius:6px; padding:5px 20px;
                     text-align:center; width:calc(100% - 10mm); margin:0 auto 6mm auto; }
    .header-frame h1, .header-frame h2, .tags span { cursor:text; }
    .tags span { display:inline-block; margin:0 4px; padding:2px 4px; border:1px solid #0052cc; border-radius:6px; background:#f0f8ff; }
    /* Content */
    .content { display:flex; flex-direction:column; gap:6mm; font-size:10pt; line-height:1.5; }
    .section h3, .section p, .section ol { cursor:text; }
    .section ol { padding-left:12mm; }
    /* Footer */
    .footer { display:flex; flex-direction:column; gap:2.5mm; font-size:10pt; }
    .sign-grid { display:grid; grid-template-columns:1fr 1fr; align-items:flex-end; column-gap:6mm; width:100%; }
    .sign-block { position:relative; text-align:center; }
    .sign-block .line { border-top:1px solid #555; margin:2.5mm auto 0; width:80%; }
    /* Seal draggable overlay */
    .party-b .seal { position:absolute; width:38mm; bottom:10mm; left:0; z-index:3; cursor:move; }
    .party-b .signature { width:60mm; margin:2.5mm auto 2.5mm; position:relative; z-index:1; }
  </style>
</head>
<body>
  <div id="loginModal">
    <div class="modal">
      <div id="authTabs">
        <button id="showLogin" style="background:#0052cc;color:#fff;border:none;padding:5px 10px;border-radius:4px;">Đăng nhập</button>
        <button id="showRegister" style="background:#ddd;color:#333;border:none;padding:5px 10px;border-radius:4px;margin-left:4px;">Đăng ký</button>
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
  <script>
    // Simple login validation (hard-coded for demo)
    document.getElementById('loginBtn').onclick = () => {
      const u = document.getElementById('username').value;
      const p = document.getElementById('password').value;
      if(u==='admin' && p==='password'){
        document.getElementById('loginModal').style.display='none';
        // Enable editing
        document.querySelectorAll('[contenteditable]').forEach(el=> el.setAttribute('contenteditable','true'));
        // Make seal draggable
        const seal = document.querySelector('.seal');
        seal.addEventListener('dragstart', e => {
          e.dataTransfer.setData('text/plain', null);
        });
        document.getElementById('editor').addEventListener('dragover', e=> e.preventDefault());
        document.getElementById('editor').addEventListener('drop', e=> {
          e.preventDefault();
          const x = e.offsetX - seal.width/2;
          const y = e.offsetY - seal.height/2;
          seal.style.left = x + 'px';
          seal.style.bottom = (document.getElementById('editor').clientHeight - y - seal.height) + 'px';
        });
      } else alert('Invalid credentials');
    };
  </script>
</body>
</html>
