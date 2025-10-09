---
layout: default
title: "Random Tên - Tuổi - Pass"
permalink: /
---

<!doctype html>

<html lang="vi">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Random Tên - Tuổi - Pass</title>
  <style>
    :root{--bg:#f6f8fa;--card:#fff;--accent:#2563eb}
    body{font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,'Helvetica Neue',Arial;margin:0;background:var(--bg);color:#111}
    .container{max-width:760px;margin:48px auto;padding:20px}
    header{display:flex;align-items:center;gap:12px}
    h1{margin:0;font-size:20px}
    .card{background:var(--card);padding:18px;border-radius:12px;box-shadow:0 6px 18px rgba(22,31,41,.06);margin-top:18px}
    .grid{display:grid;grid-template-columns:1fr 120px;gap:12px;align-items:center}
    .value{padding:14px;border-radius:8px;background:#f3f6fb;font-weight:600}
    .label{font-size:13px;color:#475569;margin-bottom:6px}
    button{padding:10px 12px;border-radius:8px;border:0;background:var(--accent);color:#fff;cursor:pointer}
    .btn-ghost{background:transparent;color:var(--accent);border:1px solid rgba(37,99,235,.12)}
    .controls{display:flex;gap:8px;align-items:center;margin-top:12px;flex-wrap:wrap}
    input[type=number]{width:74px;padding:8px;border-radius:8px;border:1px solid #e6eef8}
    footer{margin-top:18px;color:#6b7280;font-size:13px;text-align:center}
    .small{font-size:13px;color:#6b7280}
    .toplink{text-align:center;margin-bottom:12px}
    .toplink a{color:#2563eb;text-decoration:none;font-weight:600}
  </style>
</head>
<body>
  <div class="container">

<!-- Link truy cập TempMail -->
<div class="toplink">
  🔗 <a href="https://tempmail.vn/" target="_blank" rel="noopener">Truy cập website TempMail.vn</a>
</div>

<!-- Link truy cập Instagram (ngay dưới link mail) -->
<div class="toplink">
  📸 <a href="https://www.instagram.com/" target="_blank" rel="noopener">Truy cập Instagram</a>
</div>

<header>
  <svg width="36" height="36" viewBox="0 0 24 24" fill="none" aria-hidden><rect width="24" height="24" rx="6" fill="#2563eb"/><path d="M7 12h10M7 8h10M7 16h6" stroke="#fff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg>
  <div>
    <h1>Trình tạo ngẫu nhiên — Tên · Tuổi · Mật khẩu</h1>
    <div class="small">Tạo thông tin chỉ với 1 click.</div>
  </div>
</header>

<div class="card" style="margin-top:20px">
  <div style="display:grid;gap:18px">
    <div>
      <div class="label">Tên</div>
      <div class="grid">
        <div id="name" class="value">—</div>
        <div><button id="copyName" type="button">Sao chép</button></div>
      </div>
    </div>

    <div>
      <div class="label">Tuổi</div>
      <div class="grid">
        <div id="age" class="value">—</div>
        <div><button id="copyAge" type="button" class="btn-ghost">Sao chép</button></div>
      </div>
    </div>

    <div>
      <div class="label">Mật khẩu</div>
      <div class="grid">
        <div id="pass" class="value">—</div>
        <div style="display:flex;flex-direction:column;gap:6px">
          <button id="generatePass" class="btn-ghost" type="button">Tạo pass</button>
          <button id="copyPass" type="button">Sao chép</button>
        </div>
      </div>
    </div>

    <div style="display:flex;flex-direction:column;gap:8px">
      <div class="controls">
        <button id="generate" type="button">Tạo mới</button>
        <button id="download" class="btn-ghost" type="button">Tải xuống (.txt)</button>
        <label style="display:flex;align-items:center;gap:8px" class="small">
          Độ dài pass:
          <input id="length" type="number" min="6" max="64" value="12">
        </label>
      </div>
      <div class="small">Gợi ý: Bấm 'Sao chép' để copy từng mục. Bạn có thể điều chỉnh độ dài mật khẩu.</div>
    </div>
  </div>
</div>

<footer class="small">tạo bởi theanh</footer>

  </div>

  <script>
    const firstNames=['An','Bảo','Chi','Dũng','Em','Giang','Hà','Hải','Hưng','Khanh','Lan','Linh','Minh','Ngân','Ngọc','Phong','Quân','Trang','Tuấn','Vy'];
    const lastNames=['Nguyễn','Trần','Lê','Phạm','Hoàng','Vũ','Đặng','Bùi','Đỗ','Hà'];
    const randFrom=arr=>arr[Math.floor(Math.random()*arr.length)];
    const randRange=(min,max)=>Math.floor(Math.random()*(max-min+1))+min;
    function generateName(){
      const family=randFrom(lastNames);
      if(Math.random()<0.3)return `${family} ${randFrom(firstNames)} ${randFrom(firstNames)}`;
      return `${family} ${randFrom(firstNames)}`;
    }
    function generateAge(){return randRange(18,80);}
    function generatePassword(len){
      const chars='abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
      let pw='';
      for(let i=0;i<len;i++)pw+=chars.charAt(Math.floor(Math.random()*chars.length));
      return pw;
    }
    const elName=document.getElementById('name');
    const elAge=document.getElementById('age');
    const elPass=document.getElementById('pass');
    function populate(){elName.textContent=generateName();elAge.textContent=generateAge();}
    document.getElementById('generate').addEventListener('click',()=>{populate();});
    document.getElementById('generatePass').addEventListener('click',()=>{elPass.textContent=generatePassword(parseInt(document.getElementById('length').value)||12);});
    function copyText(t,b){if(!t||t==='—')return;navigator.clipboard.writeText(t).then(()=>{b.textContent='Đã copy';setTimeout(()=>b.textContent='Sao chép',700);});}
    document.getElementById('copyName').addEventListener('click',()=>copyText(elName.textContent,document.getElementById('copyName')));
    document.getElementById('copyAge').addEventListener('click',()=>copyText(elAge.textContent,document.getElementById('copyAge')));
    document.getElementById('copyPass').addEventListener('click',()=>copyText(elPass.textContent,document.getElementById('copyPass')));
    document.getElementById('download').addEventListener('click',()=>{
      const txt=`Tên: ${elName.textContent}\nTuổi: ${elAge.textContent}\nMật khẩu: ${elPass.textContent}\n`;
      const blob=new Blob([txt],{type:'text/plain;charset=utf-8'});
      const a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download='random_profile.txt';a.click();
    });
    populate();
  </script>

</body>
</html>