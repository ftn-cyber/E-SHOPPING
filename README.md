<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E-Shopping - Belanja Murah</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f4f4f4; margin: 0; padding: 0; }
        header { background-color: #232f3e; color: white; padding: 15px; display: flex; justify-content: space-between; align-items: center; }
        .logo { font-size: 24px; font-weight: bold; }
        .nav-btn { background: #febd69; border: none; padding: 10px 20px; cursor: pointer; font-weight: bold; margin-left: 10px; border-radius: 3px; }
        
        /* Container */
        .container { max-width: 200px; margin: 0 auto; padding: 20px; text-align: center; }
        .products-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 20px; padding: 20px; max-width: 1200px; margin: auto; }
        
        /* Product Card */
        .card { background: white; padding: 15px; border-radius: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); cursor: pointer; transition: transform 0.2s; text-align: left; }
        .card:hover { transform: scale(1.02); }
        .card img { width: 100%; height: 150px; object-fit: cover; background: #ddd; }
        .price { color: #b12704; font-size: 18px; font-weight: bold; margin: 10px 0; }
        .meta { font-size: 12px; color: #555; display: flex; justify-content: space-between; }
        
        /* Forms */
        .form-box { background: white; padding: 30px; max-width: 400px; margin: 50px auto; border-radius: 8px; box-shadow: 0 4px 10px rgba(0,0,0,0.2); text-align: center; }
        input { width: 90%; padding: 10px; margin: 10px 0; border: 1px solid #ccc; border-radius: 4px; }
        
        /* Admin Panel */
        .admin-panel { background: white; max-width: 800px; margin: 20px auto; padding: 20px; display: none; }
        table { width: 100%; border-collapse: collapse; margin-top: 20px; }
        th, td { border: 1px solid #ddd; padding: 8px; text-align: center; }
        th { background-color: #f2f2f2; }

        /* Utility */
        .hidden { display: none; }
    </style>
</head>
<body>

    <!-- Header -->
    <header>
        <div class="logo">E-Shopping</div>
        <div>
            <button class="nav-btn" onclick="showLogin()">Login</button>
            <button class="nav-btn" onclick="showSignup()">Sign Up</button>
        </div>
    </header>

    <!-- Halaman Utama (Produk) -->
    <div id="main-page">
        <h2 style="text-align:center; margin-top:20px;">Rekomendasi Produk</h2>
        <div class="products-grid" id="product-list">
            <!-- Produk akan digenerate oleh JS -->
        </div>
    </div>

    <!-- Form Sign Up -->
    <div id="signup-page" class="container hidden">
        <div class="form-box">
            <h2>Sign Up</h2>
            <input type="text" placeholder="Username">
            <input type="email" placeholder="Email">
            <button class="nav-btn" style="width:95%" onclick="handleSignup()">Daftar Sekarang</button>
        </div>
    </div>

    <!-- Form Login -->
    <div id="login-page" class="container hidden">
        <div class="form-box">
            <h2>Login Member</h2>
            <input type="text" id="username" placeholder="Username (Contoh: root@...)">
            <input type="password" id="password" placeholder="Password">
            <button class="nav-btn" style="width:95%" onclick="handleLogin()">Masuk</button>
        </div>
    </div>

    <!-- Admin Panel -->
    <div id="admin-page" class="container hidden">
        <h2>Admin Dashboard</h2>
        <p>Selamat datang, Root.</p>
        
        <div style="background: #e3f2fd; padding: 15px; border-radius: 5px;">
            <h3>Fitur Transaksi: Biner Decode</h3>
            <p>Mengarahkan otomatis...</p>
            <div id="redirect-timer">Redirecting in 3 seconds...</div>
        </div>

        <table>
            <thead>
                <tr>
                    <th>ID</th>
                    <th>User</th>
                    <th>Item</th>
                    <th>Harga</th>
                    <th>Status</th>
                </tr>
            </thead>
            <tbody id="transaction-body">
                <!-- 30 Transaksi akan digenerate -->
            </tbody>
        </table>
    </div>

    <script>
        // --- DATA PRODUK (Palsu) ---
        const products = [
            { name: "iPhone 15 Pro Max (KW)", price: "Rp 5.000.000", sold: 120, reviews: 5 },
            { name: "Samsung Galaxy S24 Ultra (KW)", price: "Rp 4.500.000", sold: 89, reviews: 4 },
            { name: "MacBook Air M3 (KW)", price: "Rp 7.000.000", sold: 45, reviews: 5 },
            { name: "AirPods Pro Gen 2 (KW)", price: "Rp 800.000", sold: 300, reviews: 4 },
            { name: "PlayStation 5 Slim (KW)", price: "Rp 6.500.000", sold: 210, reviews: 5 },
            { name: "Nike Air Jordan (KW)", price: "Rp 350.000", sold: 500, reviews: 4 },
            { name: "Laptop Gaming RTX 4090 (KW)", price: "Rp 12.000.000", sold: 15, reviews: 5 },
            { name: "Kopi Susu Gula Aren (Botol)", price: "Rp 15.000", sold: 1000, reviews: 5 }
        ];

        // Render Produk
        const productContainer = document.getElementById('product-list');
        products.forEach(p => {
            let stars = "★".repeat(p.reviews) + "☆".repeat(5 - p.rereviews);
            let html = `
                <div class="card" onclick="triggerXSS()">
                    <img src="https://via.placeholder.com/200x150?text=${encodeURIComponent(p.name)}" alt="${p.name}">
                    <h3>${p.name}</h3>
                    <div class="price">${p.price}</div>
                    <div class="meta">
                        <span>${p.sold} Terjual</span>
                        <span style="color:gold">${stars}</span>
                    </div>
                    <div style="margin-top:10px; font-size:12px; color:#333;">
                        Komentar: "Barang bagus, cepet sampainya!" 
                        <br><i>Ketik komentar:</i> <input type="text" style="width:80%; margin-top:5px;" placeholder="Tulis review...">
                    </div>
                </div>
            `;
            productContainer.innerHTML += html;
        });

        // --- FUNGSI NAVIGASI ---
        function hideAll() {
            document.getElementById('main-page').classList.add('hidden');
            document.getElementById('login-page').classList.add('hidden');
            document.getElementById('signup-page').classList.add('hidden');
            document.getElementById('admin-page').classList.add('hidden');
        }

        function showSignup() {
            hideAll();
            document.getElementById('signup-page').classList.remove('hidden');
        }

        function showLogin() {
            hideAll();
            document.getElementById('login-page').classList.remove('hidden');
        }

        // --- LOGIKA SIGN UP (Alert) ---
        function handleSignup() {
            alert("Wkwkwk, data kamu sudah masuk! Mau daftar kok?");
            showLogin();
        }

        // --- LOGIKA LOGIN (SQL Injection) ---
        function handleLogin() {
            const user = document.getElementById('username').value;
            const pass = document.getElementById('password').value;

            // SQL Injection Logic: Jika username mengandung string spesifik, abaikan password
            if (user.includes("root@e-shopping.com'or 1=1 ---+")) {
                openAdminPanel();
            } else {
                alert("Login Gagal! (Coba pakai user: root@e-shopping.com'or 1=1 ---+)");
            }
        }

        // --- LOGIKA ADMIN PANEL & REDIRECT ---
        function openAdminPanel() {
            hideAll();
            document.getElementById('admin-page').classList.remove('hidden');
            
            // Generate 30 Transaksi Palsu
            const tbody = document.getElementById('transaction-body');
            for(let i=1; i<=30; i++) {
                let row = `<tr>
                    <td>#${i}</td>
                    <td>User_${i}@gmail.com</td>
                    <td>Item Palsu ${i}</td>
                    <td>Rp 100.000</td>
                    <td>Selesai</td>
                </tr>`;
                tbody.innerHTML += row;
            }

            // Redirect Otomatis ke Link Biner
            setTimeout(() => {
                window.location.href = "https://ftn-cyber.github.io/Biner-code/";
            }, 3000); // Redirect setelah 3 detik
        }

        // --- LOGIKA XSS (Command Injection) ---
        function triggerXSS() {
            // Command yang diminta: <img src=# onerror='alert(document.cookie)'/>
            const command = "<img src=# onerror='alert(document.cookie)'/>";
            
            // Eksekusi Alert
            alert(command);

            // Redirect ke Link Base64
            window.location.href = "https://ftn-cyber.github.io/Base64/";
        }

    </script>
</body>
</html>
