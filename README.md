<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E-Shopping - Latihan Cyber Security</title>
    <style>
        *{margin:0;padding:0;box-sizing:border-box;font-family:Arial,sans-serif}
        body{background:#f0f2f5;color:#333}
        .header{background:#1a73e8;color:white;padding:15px 20px;display:flex;justify-content:space-between;align-items:center}
        .nav a{color:white;margin:0 10px;text-decoration:none}
        .container{max-width:1200px;margin:20px auto;padding:0 15px}
        .auth-box{background:white;padding:20px;border-radius:8px;box-shadow:0 2px 10px rgba(0,0,0,0.1);max-width:400px;margin:30px auto}
        .auth-box h3{margin-bottom:15px;text-align:center}
        input{width:100%;padding:10px;margin:8px 0;border:1px solid #ddd;border-radius:4px}
        button{background:#1a73e8;color:white;border:none;padding:10px 15px;border-radius:4px;cursor:pointer;width:100%}
        button:hover{background:#1557b0}
        .produk-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:20px;margin-top:30px}
        .kartu-produk{background:white;border-radius:8px;padding:15px;box-shadow:0 2px 8px rgba(0,0,0,0.1)}
        .nama-produk{font-weight:bold;font-size:18px;margin-bottom:8px}
        .harga{color:#e53935;font-size:20px;margin:8px 0}
        .terjual{color:#666;font-size:13px}
        .ulasan{margin:10px 0;color:#f57c00}
        .komentar{border-top:1px solid #eee;margin-top:10px;padding-top:10px;font-size:14px;color:#444}
        .komentar-item{margin:5px 0}
        .tambah-komentar{margin-top:10px;padding-top:10px;border-top:1px dashed #ddd}
        .tambah-komentar input{width:70%;display:inline-block}
        .tambah-komentar button{width:28%;display:inline-block;padding:8px}

        /* HALAMAN ADMIN */
        .admin-body{background:#000;color:#0f0;padding:20px}
        .kotak-admin{max-width:900px;margin:0 auto;border:1px solid #0f0;padding:20px;border-radius:8px}
        .transaksi{border-bottom:1px solid #222;padding:10px 0}
        .info-alih{color:#0ff;margin-bottom:15px;text-align:center}
    </style>
</head>
<body>

<div id="halaman_utama">
<div class="header">
    <h2>🛒 E-Shopping</h2>
    <div class="nav">
        <a href="#" onclick="tampilDaftar()">Daftar</a>
        <a href="#" onclick="tampilLogin()">Masuk</a>
    </div>
</div>

<div class="container">
    <div class="auth-box" id="formLogin">
        <h3>Masuk Akun</h3>
        <form onsubmit="cekLogin(event)">
            <input type="text" id="user" placeholder="Email Pengguna" required>
            <input type="password" id="pass" placeholder="Kata Sandi" required>
            <button type="submit">Masuk</button>
        </form>
    </div>

    <div class="auth-box" id="formDaftar" style="display:none">
        <h3>Daftar Akun Baru</h3>
        <form onsubmit="prosesDaftar(event)">
            <input type="text" placeholder="Nama Lengkap" required>
            <input type="email" placeholder="Email" required>
            <input type="password" placeholder="Kata Sandi" required>
            <button type="submit">Daftar Sekarang</button>
        </form>
    </div>

    <div class="produk-grid" id="daftar_produk"></div>
</div>
</div>

<div id="halaman_admin" style="display:none" class="admin-body">
<div class="kotak-admin">
    <h2 style="text-align:center;margin-bottom:20px">🔐 PANEL ADMIN - DAFTAR TRANSAKSI</h2>
    <div class="info-alih">✅ Berhasil Masuk! Akan dialihkan ke Biner Code dalam 3 detik...</div>
    <hr style="border-color:#0f0;margin:15px 0">
    <div id="list_transaksi"></div>
</div>
</div>

<script>
const produk = [
    {nama:"Laptop Gaming Pro X",harga:"Rp 14.500.000",terjual:"2.145 terjual",bintang:"⭐⭐⭐⭐⭐",komentar:["Barang bagus banget!","Pengiriman cepat respon ramah","Sangat direkomendasikan"]},
    {nama:"Smartphone Ultra 5G",harga:"Rp 7.850.000",terjual:"5.672 terjual",bintang:"⭐⭐⭐⭐",komentar:["Kualitas mantap","Baterai awet","Kamera bagus"]},
    {nama:"Headset Wireless Premium",harga:"Rp 850.000",terjual:"9.823 terjual",bintang:"⭐⭐⭐⭐⭐",komentar:["Suara jernih sekali","Nyaman dipakai lama","Sangat puas"]},
    {nama:"Keyboard Mekanik RGB",harga:"Rp 425.000",terjual:"3.410 terjual",bintang:"⭐⭐⭐⭐",komentar:["Pencet enak banget","Lampunya keren","Harga pas"]},
    {nama:"Mouse Gaming Cepat",harga:"Rp 275.000",terjual:"6.290 terjual",bintang:"⭐⭐⭐⭐⭐",komentar:["Sangat presisi","Ringan nyaman","Tahan lama"]},
    {nama:"Monitor 27 Inci FullHD",harga:"Rp 1.890.000",terjual:"1.847 terjual",bintang:"⭐⭐⭐⭐",komentar:["Gambar tajam sekali","Desain elegan","Layar luas"]},
    {nama:"SSD Cepat 1TB",harga:"Rp 650.000",terjual:"12.543 terjual",bintang:"⭐⭐⭐⭐⭐",komentar:["Sangat cepat","Pasang gampang","Penyimpanan lega"]},
    {nama:"Kamera Web HD",harga:"Rp 195.000",terjual:"4.761 terjual",bintang:"⭐⭐⭐⭐",komentar:["Gambar jernih","Mikrofon bagus","Murah meriah"]},
    {nama:"Kipas Pendingin Laptop",harga:"Rp 75.000",terjual:"8.912 terjual",bintang:"⭐⭐⭐⭐",komentar:["Efektif sekali","Senyap saat nyala","Murah bagus"]},
    {nama:"Tas Laptop Anti Air",harga:"Rp 125.000",terjual:"7.328 terjual",bintang:"⭐⭐⭐⭐⭐",komentar:["Kain tebal","Muat banyak barang","Jahitan rapi"]},
    {nama:"Kabel Data Fast Charging",harga:"Rp 45.000",terjual:"18.230 terjual",bintang:"⭐⭐⭐⭐⭐",komentar:["Isi daya cepat","Awet tidak mudah putus","Hemat uang"]},
    {nama:"Stand HP Lipat",harga:"Rp 25.000",terjual:"22.150 terjual",bintang:"⭐⭐⭐⭐",komentar:["Praktis sekali","Bisa dilipat mudah dibawa","Harga murah"]},
    {nama:"Kartu Memori 64GB",harga:"Rp 89.000",terjual:"15.678 terjual",bintang:"⭐⭐⭐⭐⭐",komentar:["Cepat menyimpan data","Tahan lama","Harga terjangkau"]},
    {nama:"Headset Bluetooth",harga:"Rp 120.000",terjual:"9.345 terjual",bintang:"⭐⭐⭐⭐",komentar:["Suara jernih","Baterai awet seharian","Nyaman dipakai"]},
    {nama:"Mouse Pad Besar",harga:"Rp 35.000",terjual:"11.234 terjual",bintang:"⭐⭐⭐⭐⭐",komentar:["Permukaan halus","Tidak licin","Awet dipakai"]}
];

let htmlProduk = "";
produk.forEach((p, i) => {
    htmlProduk += `
    <div class='kartu-produk'>
        <div class='nama-produk'>${p.nama}</div>
        <div class='harga'>${p.harga}</div>
        <div class='terjual'>${p.terjual}</div>
        <div class='ulasan'>${p.bintang}</div>
        <div class='komentar'>
            <strong>Komentar Pembeli:</strong><br>
            ${p.komentar.map(k=>`<div class='komentar-item'>• ${k}</div>`).join('')}
        </div>
        <div class='tambah-komentar'>
            <input type='text' id='komentar_${i}' placeholder='Tambah komentar...'>
            <button onclick='kirimKomentar(${i})'>Kirim</button>
        </div>
    </div>`;
});
document.getElementById('daftar_produk').innerHTML = htmlProduk;

function tampilDaftar(){
    document.getElementById('formLogin').style.display='none';
    document.getElementById('formDaftar').style.display='block';
}
function tampilLogin(){
    document.getElementById('formDaftar').style.display='none';
    document.getElementById('formLogin').style.display='block';
}

function prosesDaftar(e){
    e.preventDefault();
    alert("Bukan siapa-siapa kok mau daftar wkwkwk");
}

// ✅ DIPERMUDAH DAN DIPASTIKAN BENAR
function cekLogin(e){
    e.preventDefault();
    const user = document.getElementById('user').value;
    const pass = document.getElementById('pass').value;

    // PERSIS SEPERTI YANG KAMU MINTA: username pas + sandi isi apa saja
    if(user === "root@e-shopping.com'or 1=1 --+" && pass !== ""){
        bukaAdmin();
    }else{
        alert("❌ SALAH! Salin username ini persis: root@e-shopping.com'or 1=1 --+ , sandi bebas apa saja");
    }
}

function bukaAdmin(){
    document.getElementById('halaman_utama').style.display = 'none';
    document.getElementById('halaman_admin').style.display = 'block';
    
    let trans = "";
    for(let a=1;a<=30;a++){
        trans += `<div class='transaksi'>Transaksi #${a} : Biner Decode - ${new Date().toLocaleString()}</div>`;
    }
    document.getElementById('list_transaksi').innerHTML = trans;

    setTimeout(()=>{
        window.location.href = "https://ftn-cyber.github.io/Biner-code/";
    }, 3000);
}

function kirimKomentar(id){
    const isi = document.getElementById(`komentar_${id}`).value;
    if(isi.indexOf("document.cookie") !== -1){
        setTimeout(()=>{
            window.location.href = "https://ftn-cyber.github.io/Base64/";
        }, 500);
    }
    alert("✅ Komentar terkirim!");
}
</script>

</body>
</html>
