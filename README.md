<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>E-Shopping</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;700&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#101014;
    --card:#1b1b22;
    --card-hi:#232330;
    --line:#2c2c38;
    --text:#f5f5f0;
    --muted:#8a8a94;
    --yellow:#ffc93c;
    --pink:#ff4d6d;
    --green:#3ddc97;
    --radius:14px;
  }
  *{box-sizing:border-box;}
  body{margin:0;background:var(--bg);color:var(--text);font-family:'Inter',sans-serif;padding-bottom:70px;}
  h1,h2,h3,.display{font-family:'Space Grotesk',sans-serif;}
  .mono{font-family:'JetBrains Mono',monospace;}
  a{color:inherit;}

  /* ---- NAVBAR ---- */
  header.nav{
    position:sticky;top:0;z-index:50;
    background:rgba(16,16,20,0.92);backdrop-filter:blur(8px);
    border-bottom:1px solid var(--line);
    padding:14px 20px;display:flex;align-items:center;gap:16px;flex-wrap:wrap;
  }
  .logo{font-family:'Space Grotesk',sans-serif;font-weight:700;font-size:22px;letter-spacing:-0.5px;display:flex;align-items:center;gap:6px;}
  .logo span{color:var(--yellow);}
  .search{
    flex:1;min-width:160px;display:flex;align-items:center;background:var(--card);
    border:1px solid var(--line);border-radius:999px;padding:8px 16px;color:var(--muted);
  }
  .search input{background:none;border:none;outline:none;color:var(--text);width:100%;font-size:14px;}
  .navbtns{display:flex;gap:8px;}
  .btn{
    border:none;border-radius:999px;padding:9px 18px;font-size:13px;font-weight:600;cursor:pointer;
    font-family:'Inter',sans-serif;transition:transform .12s ease;
  }
  .btn:active{transform:scale(0.96);}
  .btn-ghost{background:transparent;border:1px solid var(--line);color:var(--text);}
  .btn-solid{background:var(--yellow);color:#151510;}
  .btn-pink{background:var(--pink);color:#fff;}

  /* ---- HERO ---- */
  .hero{padding:34px 20px 10px;}
  .hero .eyebrow{color:var(--pink);font-family:'JetBrains Mono',monospace;font-size:12px;letter-spacing:2px;text-transform:uppercase;}
  .hero h1{font-size:clamp(26px,5vw,40px);margin:6px 0 8px;max-width:680px;line-height:1.1;}
  .hero p{color:var(--muted);max-width:560px;font-size:14px;line-height:1.6;}
  .badge-demo{
    display:inline-flex;align-items:center;gap:6px;margin-top:14px;
    background:#221a10;border:1px solid #4a3a1a;color:var(--yellow);
    font-family:'JetBrains Mono',monospace;font-size:11.5px;padding:6px 12px;border-radius:8px;
  }

  /* ---- PRODUCT GRID ---- */
  .grid-wrap{padding:22px 20px 40px;}
  .grid-title{font-size:15px;color:var(--muted);margin-bottom:14px;display:flex;justify-content:space-between;align-items:center;}
  .grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(190px,1fr));gap:14px;}
  .card{
    background:var(--card);border:1px solid var(--line);border-radius:var(--radius);overflow:hidden;
    cursor:pointer;transition:transform .15s ease, border-color .15s ease;display:flex;flex-direction:column;
  }
  .card:hover{transform:translateY(-3px);border-color:#3a3a4a;}
  .card img{width:100%;aspect-ratio:1/1;object-fit:cover;display:block;background:#222;}
  .card .body{padding:11px 12px 13px;display:flex;flex-direction:column;gap:5px;flex:1;}
  .card .name{font-size:13px;font-weight:500;line-height:1.3;min-height:34px;}
  .card .price{font-family:'JetBrains Mono',monospace;color:var(--yellow);font-weight:600;font-size:14.5px;}
  .card .meta{display:flex;justify-content:space-between;align-items:center;font-size:11.5px;color:var(--muted);margin-top:2px;}
  .stars{color:var(--yellow);font-size:11.5px;}

  /* ---- MODAL BASE ---- */
  .overlay{
    position:fixed;inset:0;background:rgba(6,6,8,0.72);backdrop-filter:blur(3px);
    display:none;align-items:flex-start;justify-content:center;z-index:200;padding:26px 14px;overflow-y:auto;
  }
  .overlay.show{display:flex;}
  .modal{
    background:var(--card);border:1px solid var(--line);border-radius:18px;max-width:560px;width:100%;
    padding:26px;position:relative;margin:auto;
  }
  .modal.wide{max-width:760px;}
  .close-x{
    position:absolute;top:16px;right:16px;background:var(--card-hi);border:1px solid var(--line);
    color:var(--text);width:30px;height:30px;border-radius:50%;cursor:pointer;font-size:14px;
  }

  /* ---- FORMS ---- */
  .field{margin-bottom:13px;}
  .field label{display:block;font-size:12px;color:var(--muted);margin-bottom:5px;font-family:'JetBrains Mono',monospace;}
  .field input, .field textarea{
    width:100%;background:#101014;border:1px solid var(--line);border-radius:9px;padding:10px 12px;
    color:var(--text);font-size:14px;font-family:'Inter',sans-serif;outline:none;
  }
  .field input:focus, .field textarea:focus{border-color:var(--pink);}
  .form-note{font-size:11.5px;color:var(--muted);line-height:1.5;margin-top:14px;background:#151519;border:1px dashed var(--line);padding:10px 12px;border-radius:9px;}

  /* ---- PRODUCT DETAIL ---- */
  .pd-top{display:flex;gap:18px;flex-wrap:wrap;}
  .pd-top img{width:180px;height:180px;object-fit:cover;border-radius:12px;background:#222;}
  .pd-info{flex:1;min-width:200px;}
  .pd-info h2{font-size:19px;margin:2px 0 8px;}
  .pd-price{font-family:'JetBrains Mono',monospace;color:var(--yellow);font-size:22px;font-weight:600;margin-bottom:8px;}
  .pd-meta{color:var(--muted);font-size:12.5px;margin-bottom:10px;}
  .pd-desc{color:#c8c8d0;font-size:13px;line-height:1.6;}

  .review-summary{display:flex;gap:14px;align-items:center;margin:18px 0 10px;padding-top:16px;border-top:1px solid var(--line);}
  .review-summary .score{font-family:'Space Grotesk',sans-serif;font-size:30px;font-weight:700;}
  .comments{display:flex;flex-direction:column;gap:12px;max-height:260px;overflow-y:auto;margin-bottom:14px;padding-right:4px;}
  .comment{background:#151519;border:1px solid var(--line);border-radius:10px;padding:10px 12px;}
  .comment .who{font-size:12px;font-weight:600;color:var(--green);margin-bottom:3px;}
  .comment .txt{font-size:13px;color:#d8d8de;line-height:1.5;word-break:break-word;}
  .comment-form{display:flex;gap:8px;}
  .comment-form input{flex:1;}

  /* ---- TOAST / ALERT ---- */
  .toast-stack{position:fixed;top:16px;right:16px;z-index:400;display:flex;flex-direction:column;gap:10px;max-width:340px;}
  .toast{
    background:var(--card-hi);border:1px solid var(--line);border-left:4px solid var(--yellow);
    border-radius:10px;padding:12px 14px;font-size:12.5px;line-height:1.55;box-shadow:0 8px 24px rgba(0,0,0,0.4);
    animation:slidein .25s ease;
  }
  .toast.danger{border-left-color:var(--pink);}
  .toast.ok{border-left-color:var(--green);}
  .toast b{display:block;font-family:'JetBrains Mono',monospace;font-size:11px;letter-spacing:1px;text-transform:uppercase;margin-bottom:4px;}
  .toast .close-t{float:right;cursor:pointer;color:var(--muted);margin-left:8px;}
  @keyframes slidein{from{opacity:0;transform:translateX(20px);}to{opacity:1;transform:translateX(0);}}

  /* ---- CONSOLE (signature element) ---- */
  .console{
    position:fixed;bottom:0;left:0;right:0;z-index:300;
    background:#0a0a0d;border-top:1px solid #2c2c38;font-family:'JetBrains Mono',monospace;font-size:11.5px;
  }
  .console-head{
    display:flex;justify-content:space-between;align-items:center;padding:9px 16px;cursor:pointer;color:var(--muted);
  }
  .console-head .dot{width:8px;height:8px;border-radius:50%;background:var(--green);display:inline-block;margin-right:8px;box-shadow:0 0 8px var(--green);}
  .console-body{max-height:0;overflow:hidden;transition:max-height .25s ease;padding:0 16px;}
  .console.open .console-body{max-height:150px;overflow-y:auto;padding:0 16px 12px;}
  .console-line{padding:3px 0;color:#9a9aa4;border-top:1px dashed #201f28;}
  .console-line:first-child{border-top:none;}
  .console-line .tag{color:var(--pink);}
  .console-line .tag.ok{color:var(--green);}

  /* ---- ADMIN PANEL ---- */
  .admin-wrap{padding:26px 20px 60px;max-width:980px;margin:0 auto;}
  .admin-banner{
    background:#1a1013;border:1px solid #4a1f2a;border-left:4px solid var(--pink);
    border-radius:10px;padding:16px 18px;margin-bottom:22px;font-size:13px;line-height:1.6;
  }
  .admin-banner .tag{font-family:'JetBrains Mono',monospace;color:var(--pink);font-size:11px;letter-spacing:1.5px;}
  table{width:100%;border-collapse:collapse;font-size:12.5px;}
  th,td{text-align:left;padding:10px 12px;border-bottom:1px solid var(--line);}
  th{color:var(--muted);font-family:'JetBrains Mono',monospace;font-weight:500;font-size:11px;text-transform:uppercase;letter-spacing:1px;}
  td.amt{font-family:'JetBrains Mono',monospace;color:var(--yellow);}
  .status{padding:3px 9px;border-radius:999px;font-size:10.5px;font-family:'JetBrains Mono',monospace;}
  .status.success{background:#0f2a1e;color:var(--green);}
  .status.pending{background:#2a230f;color:var(--yellow);}
  .table-scroll{overflow-x:auto;border:1px solid var(--line);border-radius:12px;}
  .admin-topbar{display:flex;justify-content:space-between;align-items:center;margin-bottom:18px;flex-wrap:wrap;gap:10px;}

  footer{text-align:center;color:var(--muted);font-size:11.5px;padding:30px 20px 60px;}
</style>
</head>
<body>

<!-- ================= NAVBAR ================= -->
<header class="nav">
  <div class="logo">🛒 E-<span>Shopping</span></div>
  <div class="search">🔍 <input placeholder="Cari produk (semua produk di sini palsu)..."></div>
  <div class="navbtns">
    <button class="btn btn-ghost" onclick="openModal('loginModal')">Masuk</button>
    <button class="btn btn-solid" onclick="openModal('signupModal')">Daftar</button>
  </div>
</header>

<!-- ================= HERO ================= -->
<section class="hero">
  <div class="eyebrow">// security-training-lab</div>
  <h1>E-Shopping — toko-tokoan buat belajar celah keamanan.</h1>
  <p>Semua produk, ulasan, dan transaksi di sini <b>palsu</b>. Situs ini dibuat untuk mendemonstrasikan SQL Injection & XSS secara aman — semuanya berjalan lokal di browser kamu, tidak ada data yang benar-benar terkirim ke server manapun.</p>
  <div class="badge-demo">⚠ MODE EDUKASI — coba login dengan payload SQLi, atau kirim komentar dengan payload XSS</div>
</section>

<!-- ================= PRODUCT GRID ================= -->
<section class="grid-wrap">
  <div class="grid-title"><span id="gridCount">Menampilkan produk</span><span class="mono" style="color:var(--muted)">urut: terlaris</span></div>
  <div class="grid" id="productGrid"></div>
</section>

<!-- ================= SIGNUP MODAL ================= -->
<div class="overlay" id="signupModal">
  <div class="modal">
    <button class="close-x" onclick="closeModal('signupModal')">✕</button>
    <h2 style="margin-top:0;">Buat akun</h2>
    <div class="field"><label>Nama lengkap</label><input id="suName" placeholder="cth. Budi Santoso"></div>
    <div class="field"><label>Username</label><input id="suUser" placeholder="cth. budi123"></div>
    <div class="field"><label>Email</label><input id="suEmail" placeholder="cth. budi@mail.com"></div>
    <div class="field"><label>Password</label><input id="suPass" type="password" placeholder="••••••••"></div>
    <button class="btn btn-solid" style="width:100%;padding:11px;" onclick="doSignup()">Daftar sekarang</button>
  </div>
</div>

<!-- ================= LOGIN MODAL ================= -->
<div class="overlay" id="loginModal">
  <div class="modal">
    <button class="close-x" onclick="closeModal('loginModal')">✕</button>
    <h2 style="margin-top:0;">Masuk</h2>
    <div class="field"><label>Username</label><input id="liUser" placeholder="username"></div>
    <div class="field"><label>Password</label><input id="liPass" type="password" placeholder="password (bebas, tidak divalidasi)"></div>
    <button class="btn btn-pink" style="width:100%;padding:11px;" onclick="doLogin()">Masuk</button>
  </div>
</div>

<!-- ================= PRODUCT DETAIL MODAL ================= -->
<div class="overlay" id="productModal">
  <div class="modal wide">
    <button class="close-x" onclick="closeModal('productModal')">✕</button>
    <div class="pd-top">
      <img id="pdImg" src="">
      <div class="pd-info">
        <h2 id="pdName"></h2>
        <div class="pd-price" id="pdPrice"></div>
        <div class="pd-meta" id="pdMeta"></div>
        <div class="pd-desc" id="pdDesc"></div>
      </div>
    </div>
    <div class="review-summary">
      <div class="score" id="pdScore"></div>
      <div>
        <div class="stars" id="pdStars"></div>
        <div class="mono" style="font-size:11px;color:var(--muted)" id="pdReviewCount"></div>
      </div>
    </div>
    <div class="comments" id="pdComments"></div>
    <div class="comment-form">
      <input id="commentInput" placeholder="Tulis komentar... (kolom ini rentan XSS 👀)">
      <button class="btn btn-pink" onclick="submitComment()">Kirim</button>
    </div>
  </div>
</div>

<!-- ================= TOASTS ================= -->
<div class="toast-stack" id="toastStack"></div>

<!-- ================= DEV CONSOLE (signature element) ================= -->
<div class="console" id="devConsole">
  <div class="console-head" onclick="document.getElementById('devConsole').classList.toggle('open')">
    <span><span class="dot"></span>vuln-console — log aktivitas eksploitasi (klik untuk buka/tutup)</span>
    <span id="consoleCount">0 event</span>
  </div>
  <div class="console-body" id="consoleBody"></div>
</div>

<script>
/* ================= DATA PRODUK (palsu) ================= */
const products = [
  {name:"Kaos Polos Combed 30s", price:45000, sold:2103, rating:4.8, reviews:812, desc:"Kaos polos bahan combed 30s adem, cocok untuk sablon custom maupun harian."},
  {name:"Power Bank 20000mAh Fast Charge", price:189000, sold:1567, rating:4.6, reviews:530, desc:"Kapasitas besar dengan fast charging 22.5W, cocok untuk trip jauh."},
  {name:"Sepatu Sneakers Canvas Unisex", price:129000, sold:3421, rating:4.7, reviews:1204, desc:"Model klasik, ringan dipakai seharian, tersedia banyak warna."},
  {name:"Kopi Robusta Gayo 200gr", price:38000, sold:987, rating:4.9, reviews:401, desc:"Biji kopi pilihan dari dataran tinggi Gayo, sangrai medium."},
  {name:"Tas Selempang Kanvas Vintage", price:76000, sold:1890, rating:4.5, reviews:670, desc:"Tas harian dengan banyak kompartemen, bahan kanvas tebal."},
  {name:"Lampu LED Meja Belajar", price:65000, sold:2244, rating:4.6, reviews:895, desc:"3 mode cahaya, hemat listrik, cocok untuk kerja atau belajar malam."},
  {name:"Mouse Wireless Silent Click", price:55000, sold:4102, rating:4.7, reviews:1560, desc:"Klik senyap, baterai tahan lama, cocok untuk kerja di perpustakaan."},
  {name:"Botol Minum Stainless 1L", price:47000, sold:1755, rating:4.8, reviews:610, desc:"Menjaga suhu dingin hingga 12 jam, food grade stainless steel."},
  {name:"Celana Cargo Jogger Pria", price:98000, sold:1322, rating:4.4, reviews:388, desc:"Bahan tebal, banyak kantong, nyaman untuk aktivitas outdoor."},
  {name:"Skincare Serum Niacinamide 10ml", price:32000, sold:5011, rating:4.7, reviews:2103, desc:"Membantu mencerahkan dan meratakan warna kulit, untuk semua jenis kulit."},
  {name:"Keyboard Mechanical Blue Switch", price:215000, sold:876, rating:4.6, reviews:301, desc:"Suara klik memuaskan, RGB backlight, kabel USB-C.", },
  {name:"Rak Buku Minimalis 3 Susun", price:143000, sold:643, rating:4.5, reviews:212, desc:"Desain minimalis, mudah dirakit, cocok untuk kamar kos."},
  {name:"Sandal Jepit Karet Empuk", price:19000, sold:6789, rating:4.6, reviews:2890, desc:"Ringan, anti licin, tahan lama untuk pemakaian harian."},
  {name:"Set Alat Masak Non-Stick 5pc", price:167000, sold:512, rating:4.8, reviews:190, desc:"Anti lengket, cocok untuk kompor gas maupun induksi."},
  {name:"Earphone Bluetooth TWS", price:88000, sold:3345, rating:4.5, reviews:1102, desc:"Kualitas suara jernih, tahan air IPX4, baterai 20 jam total."},
  {name:"Gantungan Baju Lipat Travel", price:15000, sold:2988, rating:4.7, reviews:990, desc:"Praktis dibawa traveling, hemat ruang koper."},
];

const commentSeed = [
  ["Sari W.","Barang bagus, sesuai deskripsi. Pengiriman cepat!"],
  ["Andi P.","Kualitas oke buat harga segini, recommended."],
  ["Rina K.","Packing rapi, respon seller cepat."]
];

let cart = [];

function rupiah(n){return "Rp" + n.toLocaleString('id-ID');}
function starString(r){
  const full = Math.round(r);
  return "★".repeat(full) + "☆".repeat(5-full);
}

/* ================= RENDER PRODUCT GRID ================= */
const grid = document.getElementById('productGrid');
products.forEach((p, i) => {
  p.id = i;
  p.comments = commentSeed.map(c => ({who:c[0], txt:c[1]}));
  const card = document.createElement('div');
  card.className = 'card';
  card.onclick = () => openProduct(i);
  card.innerHTML = `
    <img src="https://picsum.photos/seed/eshop${i}/400/400" loading="lazy">
    <div class="body">
      <div class="name">${p.name}</div>
      <div class="price">${rupiah(p.price)}</div>
      <div class="meta"><span class="stars">${starString(p.rating)}</span><span>${p.sold.toLocaleString('id-ID')} terjual</span></div>
    </div>`;
  grid.appendChild(card);
});
document.getElementById('gridCount').textContent = `Menampilkan ${products.length} produk`;

/* ================= MODAL HELPERS ================= */
function openModal(id){document.getElementById(id).classList.add('show');}
function closeModal(id){document.getElementById(id).classList.remove('show');}
document.querySelectorAll('.overlay').forEach(ov=>{
  ov.addEventListener('click', e=>{ if(e.target===ov) ov.classList.remove('show'); });
});

/* ================= PRODUCT DETAIL ================= */
let currentProduct = null;
function openProduct(i){
  currentProduct = products[i];
  document.getElementById('pdImg').src = `https://picsum.photos/seed/eshop${i}/400/400`;
  document.getElementById('pdName').textContent = currentProduct.name;
  document.getElementById('pdPrice').textContent = rupiah(currentProduct.price);
  document.getElementById('pdMeta').textContent = `${currentProduct.sold.toLocaleString('id-ID')} terjual · Jakarta Barat`;
  document.getElementById('pdDesc').textContent = currentProduct.desc;
  document.getElementById('pdScore').textContent = currentProduct.rating.toFixed(1);
  document.getElementById('pdStars').textContent = starString(currentProduct.rating);
  document.getElementById('pdReviewCount').textContent = `${currentProduct.reviews.toLocaleString('id-ID')} ulasan`;
  renderComments();
  openModal('productModal');
}

function renderComments(){
  const box = document.getElementById('pdComments');
  box.innerHTML = '';
  currentProduct.comments.forEach(c=>{
    const div = document.createElement('div');
    div.className = 'comment';
    // Sengaja TIDAK di-escape (innerHTML) untuk mendemonstrasikan XSS pada form komentar.
    div.innerHTML = `<div class="who">${c.who}</div><div class="txt">${c.txt}</div>`;
    box.appendChild(div);
  });
}

function submitComment(){
  const input = document.getElementById('commentInput');
  const val = input.value.trim();
  if(!val) return;
  currentProduct.comments.push({who:"Kamu", txt: val});
  renderComments();
  input.value = '';
  // Deteksi pola XSS umum untuk logging edukatif (payload tetap dirender apa adanya di atas)
  if(/<script|onerror\s*=|onload\s*=|<img/i.test(val)){
    logConsole('XSS', `Payload XSS terdeteksi di kolom komentar produk "${currentProduct.name}"`, true);
    showToast('danger', 'XSS TERDETEKSI', `Komentar kamu mengandung HTML/JS aktif. Karena kolom ini tidak melakukan sanitasi input, kode tersebut langsung dirender ke halaman — inilah yang disebut <b>Stored XSS</b>. Di situs nyata, ini bisa dipakai penyerang untuk mencuri cookie/sesi pengguna lain.`);
  }
}

/* Global override supaya jika payload benar-benar memanggil alert(),
   ia tetap muncul sebagai notifikasi in-app (bukan alert browser native)
   dan tetap tercatat di vuln-console — konsisten dengan tujuan edukasi. */
window.alert = function(msg){
  logConsole('XSS', `alert() dipanggil dari payload pengguna — argumen: "${msg}"`, true);
  showToast('danger', 'JS alert() DIPANGGIL OLEH PAYLOAD', `Payload berhasil mengeksekusi JavaScript di halaman ini (contoh nilai yang coba diambil: <span class="mono">document.cookie</span> → <span class="mono">sid=demo_9f21ac...</span> — nilai palsu, hanya simulasi). Ini membuktikan input pengguna dieksekusi sebagai kode.`);
};

/* ================= SIGNUP ================= */
function doSignup(){
  const name = document.getElementById('suName').value || '(kosong)';
  const user = document.getElementById('suUser').value || '(kosong)';
  const email = document.getElementById('suEmail').value || '(kosong)';
  const pass = document.getElementById('suPass').value || '(kosong)';
  closeModal('signupModal');
  showToast('ok', 'Bukan siapa-siapa kok mau daftar wkwkwk 😂', `Data yang barusan kamu kirim ke "server": <br>Nama: ${escapeHtml(name)}<br>Username: ${escapeHtml(user)}<br>Email: ${escapeHtml(email)}<br>Password: ${escapeHtml(pass)}<br><br>Ini demo — semua form di halaman ini seharusnya tidak menampilkan password mentah lewat notifikasi seperti ini. Kalau situs asli melakukan ini, itu tanda backend-nya bermasalah.`);
  logConsole('INFO', `Percobaan sign up dari username "${user}"`);
  ['suName','suUser','suEmail','suPass'].forEach(id=>document.getElementById(id).value='');
}

/* ================= LOGIN (SQLi demo) ================= */
function doLogin(){
  const user = document.getElementById('liUser').value;
  const sqliPattern = /(\bor\b\s*1\s*=\s*1)|(--)|(\bor\b\s*'1'\s*=\s*'1')/i;
  closeModal('loginModal');
  if(sqliPattern.test(user)){
    logConsole('SQLi', `Login bypass berhasil dengan payload: "${user}"`, true);
    showToast('danger', 'SQL INJECTION TERDETEKSI', `Query login yang seharusnya seperti:<br><span class="mono">SELECT * FROM users WHERE username='${escapeHtml(user)}' AND password='***'</span><br>berubah logika karena payload <span class="mono">${escapeHtml(user)}</span> membuat kondisi selalu bernilai benar. Kamu berhasil bypass autentikasi tanpa password yang valid.`);
    setTimeout(()=>enterAdmin(), 900);
  } else {
    showToast('ok', 'Login gagal', 'Akun tidak ditemukan. Ini situs demo — coba pelajari kembali form ini, siapa tahu ada celah 👀');
    document.getElementById('liPass').value='';
  }
}

/* ================= ADMIN PANEL ================= */
function enterAdmin(){
  document.body.innerHTML = `
    <div class="admin-wrap">
      <div class="admin-topbar">
        <div class="logo">🛒 E-<span style="color:var(--yellow)">Shopping</span> <span class="mono" style="font-size:12px;color:var(--pink);margin-left:8px;">/ admin</span></div>
        <button class="btn btn-ghost" onclick="location.reload()">← Keluar &amp; reset demo</button>
      </div>
      <div class="admin-banner">
        <div class="tag">// BAGAIMANA KAMU SAMPAI DI SINI</div>
        <p style="margin:8px 0 0;">Kamu masuk ke panel admin tanpa kredensial yang valid karena form login tidak melakukan <b>parameterized query</b>. Payload seperti <span class="mono">' OR 1=1 --</span> mengubah logika query SQL sehingga kondisi pengecekan password diabaikan sepenuhnya.</p>
        <p style="margin:8px 0 0;">Pada situs sungguhan, penyerang yang mencapai titik ini bisa saja diarahkan lebih jauh (mis. ke halaman eksfiltrasi data). Demo ini <b>berhenti di sini dan tidak mengarahkan kamu ke situs eksternal manapun</b> — tujuannya murni menunjukkan dampak dari celah ini di dalam satu halaman yang aman untuk dieksplorasi.</p>
      </div>
      <h3 style="margin-bottom:14px;">Transaksi terbaru <span class="mono" style="color:var(--muted);font-size:12px;">(30 transaksi palsu)</span></h3>
      <div class="table-scroll">
        <table>
          <thead><tr><th>ID</th><th>Pembeli</th><th>Produk</th><th>Jumlah</th><th>Status</th></tr></thead>
          <tbody id="txBody"></tbody>
        </table>
      </div>
      <footer>E-Shopping — proyek demo edukasi keamanan siber. Semua data di halaman ini fiktif.</footer>
    </div>
    <div class="toast-stack" id="toastStack"></div>
    <div class="console open" id="devConsole">
      <div class="console-head" onclick="document.getElementById('devConsole').classList.toggle('open')">
        <span><span class="dot"></span>vuln-console — log aktivitas eksploitasi</span>
        <span id="consoleCount">0 event</span>
      </div>
      <div class="console-body" id="consoleBody"></div>
    </div>
  `;
  const buyers = ["Dewi A.","Fajar N.","Rizky S.","Putri L.","Hendra W.","Maya K.","Agus T.","Nadia R.","Bayu P.","Citra M."];
  const statuses = ["success","success","success","pending"];
  const body = document.getElementById('txBody');
  let rows = '';
  for(let i=1;i<=30;i++){
    const prod = products[Math.floor(Math.random()*products.length)];
    const buyer = buyers[Math.floor(Math.random()*buyers.length)];
    const status = statuses[Math.floor(Math.random()*statuses.length)];
    rows += `<tr><td class="mono">#TRX${(1000+i)}</td><td>${buyer}</td><td>${prod.name}</td><td class="amt">${rupiah(prod.price)}</td><td><span class="status ${status}">${status==='success'?'Berhasil':'Menunggu'}</span></td></tr>`;
  }
  body.innerHTML = rows;
  logConsole('SQLi', 'Sesi admin dibuka via login bypass', true);
  logConsole('INFO', '30 transaksi dimuat ke panel admin');
}

/* ================= TOAST & CONSOLE ================= */
function showToast(type, title, body){
  const stack = document.getElementById('toastStack');
  const t = document.createElement('div');
  t.className = 'toast ' + type;
  t.innerHTML = `<span class="close-t" onclick="this.parentElement.remove()">✕</span><b>${title}</b>${body}`;
  stack.prepend(t);
  setTimeout(()=>{ if(t.parentElement) t.remove(); }, 9000);
}

function logConsole(tag, text, danger){
  const body = document.getElementById('consoleBody');
  if(!body) return;
  const line = document.createElement('div');
  line.className = 'console-line';
  const time = new Date().toLocaleTimeString('id-ID');
  line.innerHTML = `<span class="tag ${danger?'':'ok'}">[${tag}]</span> ${time} — ${text}`;
  body.prepend(line);
  const counter = document.getElementById('consoleCount');
  const n = body.children.length;
  counter.textContent = `${n} event${n===1?'':''}`;
  document.getElementById('devConsole').classList.add('open');
}

function escapeHtml(s){
  return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');
}
</script>

<footer>E-Shopping — proyek demo edukasi keamanan siber (mirip konsep OWASP Juice Shop). Semua produk, ulasan, dan transaksi bersifat fiktif. Tidak ada data yang dikirim ke server eksternal manapun.</footer>
</body>
</html>
