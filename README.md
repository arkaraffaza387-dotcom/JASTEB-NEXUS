<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jasteb - Sistem Log Data Lengkap</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css">
    <script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        utama: '#165DFF',
                        gelap: '#0F1117',
                        gelap2: '#1A1C23',
                        aksen: '#F5B800',
                        teks: '#E5E7EB',
                        teksMuda: '#9CA3AF',
                        admin: '#7C3AED',
                        barisGenap: '#14161D',
                        barisGanjil: '#1A1C23'
                    }
                }
            }
        }
    </script>
    <style>
        .konten-pusat { display:flex !important; align-items:center !important; justify-content:center !important; min-height:100vh !important; padding:1rem !important; }
        .sembunyi { display: none !important; }
        .bayangan { box-shadow:0 8px 32px rgba(0,0,0,0.4); }
        .input-kustom { background-color: #0F1117; border:1px solid #374151; color:#E5E7EB; outline:none; }
        .area-log { max-height: 72vh; overflow-y: auto; }
        .area-log::-webkit-scrollbar { width: 7px; }
        .area-log::-webkit-scrollbar-track { background: #1A1C23; }
        .area-log::-webkit-scrollbar-thumb { background: #374151; border-radius:4px; }
        .baris-genap { background-color: #14161D; }
        .baris-ganjil { background-color: #1A1C23; }
        .baris-hover:hover { background-color: #232732 !important; }
    </style>
</head>
<body class="bg-gelap text-teks font-sans">

    <!-- HALAMAN UTAMA PILIH LOGIN -->
    <div id="halamanPilih" class="konten-pusat">
        <div class="bg-gelap2 rounded-2xl bayangan p-6 md:p-8 w-full max-w-md border border-gray-700/50">
            <div class="text-center mb-6 md:mb-8">
                <h1 class="text-[clamp(1.7rem,4vw,2.2rem)] font-bold">
                    <i class="fa fa-shield text-aksen mr-2"></i> Jasteb
                </h1>
                <p class="text-teksMuda mt-2 text-sm md:text-base">Pilih akses masuk sistem</p>
            </div>
            <div class="space-y-3 md:space-y-4">
                <button onclick="tampilkan('halamanLoginPengguna')" 
                    class="w-full bg-utama hover:bg-utama/90 py-2.5 md:py-3 rounded-lg text-white font-medium">
                    <i class="fa fa-user mr-2"></i> Login Pengguna Biasa
                </button>
                <button onclick="tampilkan('halamanLoginAdmin')" 
                    class="w-full bg-admin hover:bg-admin/90 py-2.5 md:py-3 rounded-lg text-white font-medium">
                    <i class="fa fa-user-shield mr-2"></i> Login Admin
                </button>
            </div>
        </div>
    </div>

    <!-- HALAMAN LOGIN PENGGUNA -->
    <div id="halamanLoginPengguna" class="konten-pusat sembunyi">
        <div class="bg-gelap2 rounded-2xl bayangan p-6 md:p-8 w-full max-w-md border border-gray-700/50">
            <a href="#" onclick="kembali(event)" class="text-teksMuda text-sm">
                <i class="fa fa-arrow-left"></i> Kembali
            </a>
            <h2 class="text-lg md:text-xl font-bold text-center mt-2">Login Pengguna</h2>
            <div class="space-y-3 md:space-y-4 mt-4 md:mt-6">
                <div>
                    <label class="block text-sm text-teksMuda mb-1">Username</label>
                    <input type="text" id="userPengguna" class="w-full p-3 rounded-lg input-kustom">
                </div>
                <div>
                    <label class="block text-sm text-teksMuda mb-1">Kata Sandi</label>
                    <input type="password" id="passPengguna" class="w-full p-3 rounded-lg input-kustom">
                </div>
                <button onclick="cekPengguna()" class="w-full bg-utama py-3 rounded-lg text-white font-medium">
                    Masuk
                </button>
                <div id="pesanPengguna" class="text-center text-sm"></div>
            </div>
        </div>
    </div>

    <!-- HALAMAN LOGIN ADMIN -->
    <div id="halamanLoginAdmin" class="konten-pusat sembunyi">
        <div class="bg-gelap2 rounded-2xl bayangan p-6 md:p-8 w-full max-w-md border border-gray-700/50">
            <a href="#" onclick="kembali(event)" class="text-teksMuda text-sm">
                <i class="fa fa-arrow-left"></i> Kembali
            </a>
            <h2 class="text-lg md:text-xl font-bold text-center mt-2 text-admin">Login Admin</h2>
            <div class="space-y-3 md:space-y-4 mt-4 md:mt-6">
                <div>
                    <label class="block text-sm text-teksMuda mb-1">Username Admin</label>
                    <input type="text" id="userAdmin" class="w-full p-3 rounded-lg input-kustom" value="admin123">
                </div>
                <div>
                    <label class="block text-sm text-teksMuda mb-1">Kata Sandi Admin</label>
                    <input type="password" id="passAdmin" class="w-full p-3 rounded-lg input-kustom" value="admin-free">
                </div>
                <button onclick="cekAdmin()" class="w-full bg-admin py-3 rounded-lg text-white font-medium">
                    Masuk Sebagai Admin
                </button>
                <div id="pesanAdmin" class="text-center text-sm"></div>
            </div>
        </div>
    </div>

    <!-- HALAMAN VERIFIKASI EMAIL -->
    <div id="halamanEmail" class="konten-pusat sembunyi">
        <div class="bg-gelap2 rounded-2xl bayangan p-6 md:p-8 w-full max-w-md border border-gray-700/50">
            <div class="text-center mb-6">
                <i class="fa fa-envelope-o text-aksen text-4xl mb-3"></i>
                <h2 class="text-lg font-bold">Verifikasi Email</h2>
                <p class="text-teksMuda text-sm mt-1">Kode dikirim ke alamat Anda</p>
            </div>
            <div class="space-y-4">
                <input type="email" id="emailTujuan" placeholder="contoh@gmail.com" class="w-full p-3 rounded-lg input-kustom">
                <button onclick="kirimKode()" class="w-full bg-utama py-3 rounded-lg text-white">Kirim Kode</button>
                <div id="pesanEmail" class="text-center text-sm"></div>
            </div>
        </div>
    </div>

    <!-- HALAMAN MASUKKAN KODE -->
    <div id="halamanKode" class="konten-pusat sembunyi">
        <div class="bg-gelap2 rounded-2xl bayangan p-6 md:p-8 w-full max-w-md border border-gray-700/50">
            <div class="text-center mb-6">
                <i class="fa fa-unlock-alt text-green-500 text-4xl mb-3"></i>
                <h2 class="text-lg font-bold">Masukkan Kode Verifikasi</h2>
                <p class="text-teksMuda text-sm mt-1">Salin kode dari pesan email</p>
            </div>
            <div class="space-y-4">
                <input type="text" id="kodeVerif" placeholder="8 Karakter" class="w-full p-3 rounded-lg input-kustom uppercase">
                <button onclick="cekKode()" class="w-full bg-green-600 py-3 rounded-lg text-white">Verifikasi & Masuk</button>
                <div id="pesanKode" class="text-center text-sm"></div>
            </div>
        </div>
    </div>

    <!-- HALAMAN UTAMA PENGGUNA: DAFTAR LOG EMAIL & SANDI (SAMPAI 100.000) -->
    <div id="halamanUtamaPengguna" class="sembunyi min-h-screen py-4 px-3 md:px-4">
        <div class="max-w-6xl mx-auto">
            <div class="flex flex-col md:flex-row justify-between items-center mb-4 gap-3">
                <h1 class="text-lg md:text-xl font-bold"><i class="fa fa-list-alt text-aksen mr-2"></i> Daftar Lengkap Data Akun</h1>
                <div class="flex gap-2 flex-wrap">
                    <button onclick="isiDataOtomatis()" class="bg-green-600 px-3 py-2 rounded-lg text-white text-sm">Isi Contoh</button>
                    <button onclick="muatSemuaLog()" class="bg-utama px-3 py-2 rounded-lg text-white text-sm">Muat Semua Data</button>
                    <button onclick="hapusSemuaLog()" class="bg-orange-600 px-3 py-2 rounded-lg text-white text-sm">Kosongkan</button>
                    <button onclick="keluar()" class="bg-red-600 hover:bg-red-700 px-3 py-2 rounded-lg text-white text-sm">Keluar</button>
                </div>
            </div>

            <!-- TABEL DATA LENGKAP -->
            <div class="bg-gelap2 rounded-xl border border-gray-700/50 overflow-hidden">
                <div class="grid grid-cols-12 bg-utama/90 text-white font-medium p-3 text-sm">
                    <div class="col-span-1">No</div>
                    <div class="col-span-2">Jenis Akun</div>
                    <div class="col-span-5">Alamat Email</div>
                    <div class="col-span-3">Kata Sandi</div>
                    <div class="col-span-1">Salin</div>
                </div>
                <div id="wadahLogData" class="area-log">
                    <div class="text-center text-teksMuda py-10">Tekan tombol <b>"Isi Contoh"</b> atau <b>"Muat Semua Data"</b> untuk menampilkan daftar lengkap</div>
                </div>
            </div>

            <!-- FORM TAMBAH DATA BARU -->
            <div class="mt-4 bg-gelap2 p-4 rounded-xl border border-gray-700/50">
                <h3 class="font-semibold mb-3 text-aksen">+ Tambah Data Akun Baru</h3>
                <div class="grid md:grid-cols-4 gap-3">
                    <select id="jenisAkun" class="p-3 rounded-lg input-kustom">
                        <option>GOOGLE</option>
                        <option>FACEBOOK</option>
                        <option>INSTAGRAM</option>
                        <option>TWITTER/X</option>
                        <option>LAINNYA</option>
                    </select>
                    <input type="email" id="emailBaruLog" placeholder="Alamat Email" class="p-3 rounded-lg input-kustom">
                    <input type="text" id="sandiBaruLog" placeholder="Kata Sandi" class="p-3 rounded-lg input-kustom">
                    <button onclick="tambahDataLog()" class="bg-utama py-3 rounded-lg text-white">Simpan Data</button>
                </div>
                <div id="pesanLog" class="mt-2 text-sm"></div>
            </div>
        </div>
    </div>

    <!-- HALAMAN ADMIN PANEL -->
    <div id="halamanPanelAdmin" class="sembunyi min-h-screen py-6 px-3 md:px-4">
        <div class="max-w-5xl mx-auto">
            <div class="flex flex-col md:flex-row justify-between items-center mb-8 gap-4">
                <h1 class="text-xl md:text-2xl font-bold text-admin text-center"><i class="fa fa-user-shield mr-2"></i> Panel Pengelolaan Admin</h1>
                <button onclick="keluar()" class="bg-red-600 hover:bg-red-700 px-4 py-2 rounded-lg text-white">Keluar</button>
            </div>

            <!-- Form Buat Akun Pengguna -->
            <div class="bg-gelap2 p-4 md:p-6 rounded-xl mb-6 border border-gray-700/50">
                <h3 class="font-semibold mb-4 text-aksen">Buat Akun Pengguna Baru</h3>
                <div class="grid md:grid-cols-2 gap-4">
                    <input type="email" id="newEmail" placeholder="Email Pengguna" class="p-3 rounded-lg input-kustom">
                    <input type="text" id="newUser" placeholder="Username" class="p-3 rounded-lg input-kustom">
                    <input type="password" id="newPass" placeholder="Kata Sandi" class="p-3 rounded-lg input-kustom">
                    <button onclick="tambahAkun()" class="bg-admin py-3 rounded-lg text-white">Simpan Akun</button>
                </div>
                <div id="pesanPanel" class="mt-3 text-sm"></div>
            </div>

            <!-- Daftar Pengguna Terdaftar -->
            <div class="bg-gelap2 rounded-xl overflow-hidden border border-gray-700/50">
                <div class="bg-admin/90 grid grid-cols-12 p-3 text-sm font-medium text-white">
                    <div class="col-span-3">Username</div>
                    <div class="col-span-5">Email</div>
                    <div class="col-span-3">Status</div>
                    <div class="col-span-1">Hapus</div>
                </div>
                <div id="daftarAkunAdmin" class="max-h-[55vh] overflow-y-auto"></div>
            </div>
        </div>
    </div>

    <script>
        // KONFIGURASI UTAMA
        const ADMIN_USER = "admin123";
        const ADMIN_PASS = "admin-free";
        const MAKSIMAL_DATA_LOG = 100000; // ✅ BATAS PENUH 100.000 CATATAN
        let kodeSementara = "";
        let akunAktif = {};

        // Pengaturan EmailJS
        emailjs.init("kivoJM0EuLz9XxVpu");
        const EMAIL_SERVICE = "service_3kqppan";
        const EMAIL_TEMPLATE = "template_hbkfoe6";

        // FUNGSI UTAMA PINDAH HALAMAN
        function tampilkan(idHalaman) {
            const semuaHalaman = ["halamanPilih","halamanLoginPengguna","halamanLoginAdmin","halamanEmail","halamanKode","halamanUtamaPengguna","halamanPanelAdmin"];
            semuaHalaman.forEach(id => document.getElementById(id).classList.add("sembunyi"));
            document.getElementById(idHalaman).classList.remove("sembunyi");
        }
        function kembali(e) {
            e.preventDefault();
            tampilkan("halamanPilih");
        }

        // PROSES LOGIN
        function cekPengguna() {
            const u = document.getElementById("userPengguna").value.trim();
            const p = document.getElementById("passPengguna").value.trim();
            const pesan = document.getElementById("pesanPengguna");
            const daftar = JSON.parse(localStorage.getItem("jasteb_akun") || "[]");
            const ketemu = daftar.find(a => a.user === u && a.pass === p);
            if (ketemu) {
                pesan.textContent = "✅ Akun ditemukan, lanjut verifikasi";
                akunAktif = ketemu;
                setTimeout(() => tampilkan("halamanEmail"), 800);
            } else {
                pesan.textContent = "❌ Username atau sandi salah/belum terdaftar";
                pesan.className = "text-center text-sm text-red-400";
            }
        }
        function cekAdmin() {
            const u = document.getElementById("userAdmin").value.trim();
            const p = document.getElementById("passAdmin").value.trim();
            const pesan = document.getElementById("pesanAdmin");
            if (u === ADMIN_USER && p === ADMIN_PASS) {
                pesan.textContent = "✅ Masuk ke panel admin...";
                localStorage.setItem("jasteb_login", "ya");
                localStorage.setItem("jasteb_jenis", "admin");
                setTimeout(() => { muatDaftarAdmin(); tampilkan("halamanPanelAdmin"); }, 800);
            } else {
                pesan.textContent = "❌ Akses ditolak";
                pesan.className = "text-center text-sm text-red-400";
            }
        }

        // SISTEM VERIFIKASI EMAIL
        function buatKode() {
            const kodeDasar = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
            let hasil = "";
            for (let i=0; i<8; i++) hasil += kodeDasar[Math.floor(Math.random()*kodeDasar.length)];
            return hasil;
        }
        function kirimKode() {
            const email = document.getElementById("emailTujuan").value.trim();
            const pesan = document.getElementById("pesanEmail");
            if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) { pesan.textContent = "❌ Format email salah"; return; }
            kodeSementara = buatKode();
            pesan.textContent = "⏳ Sedang mengirim...";
            emailjs.send(EMAIL_SERVICE, EMAIL_TEMPLATE, {email: email, key: kodeSementara})
            .then(() => { pesan.textContent = "✅ Berhasil dikirim, cek kotak masuk"; setTimeout(() => tampilkan("halamanKode"), 1000); })
            .catch(e => pesan.textContent = "❌ Gagal: " + e.text);
        }
        function cekKode() {
            const k = document.getElementById("kodeVerif").value.trim();
            if (k === kodeSementara) {
                localStorage.setItem("jasteb_login", "ya");
                localStorage.setItem("jasteb_jenis", "pengguna");
                tampilkan("halamanUtamaPengguna");
            } else {
                document.getElementById("pesanKode").textContent = "❌ Kode verifikasi tidak cocok";
            }
        }

        // ✅ SISTEM PENYIMPANAN & TAMPILAN LOG EMAIL + SANDI - PENUH 100.000
        function ambilSemuaLog() {
            let dataMentah = localStorage.getItem("jasteb_log_data");
            return dataMentah ? JSON.parse(dataMentah) : [];
        }
        function simpanSemuaLog(daftarData) {
            // Otomatis batasi agar tidak melebihi 100.000 data
            localStorage.setItem("jasteb_log_data", JSON.stringify(daftarData.slice(-MAKSIMAL_DATA_LOG)));
        }
        function tambahDataLog() {
            const jenis = document.getElementById("jenisAkun").value;
            const email = document.getElementById("emailBaruLog").value.trim();
            const sandi = document.getElementById("sandiBaruLog").value.trim();
            const pesan = document.getElementById("pesanLog");
            if (!email || !sandi) { pesan.textContent = "❌ Isi email dan sandi lengkap"; pesan.className = "text-sm text-red-400"; return; }
            if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) { pesan.textContent = "❌ Alamat email tidak sah"; pesan.className = "text-sm text-red-400"; return; }
            
            let daftar = ambilSemuaLog();
            daftar.push({
                id: Date.now() + Math.floor(Math.random()*1000),
                jenis: jenis,
                email: email,
                sandi: sandi,
                waktu: new Date().toLocaleString("id-ID")
            });
            simpanSemuaLog(daftar);
            pesan.textContent = "✅ Data berhasil disimpan";
            pesan.className = "text-sm text-green-400";
            document.getElementById("emailBaruLog").value = "";
            document.getElementById("sandiBaruLog").value = "";
            muatSemuaLog();
        }
        function muatSemuaLog() {
            const wadah = document.getElementById("wadahLogData");
            const daftar = ambilSemuaLog();
            wadah.innerHTML = "";
            if (daftar.length === 0) { wadah.innerHTML = `<div class="text-center text-teksMuda py-10">Belum ada data tersimpan</div>`; return; }

            // Muat bertahap (500 baris sekali) agar HP tidak macet
            let indeks = 0;
            function tampilBagian() {
                let potongan = daftar.slice(indeks, indeks + 500);
                potongan.forEach((data, urut) => {
                    let nomorUrut = indeks + urut + 1;
                    let baris = document.createElement("div");
                    baris.className = `grid grid-cols-12 p-3 text-sm border-b border-gray-700/40 baris-hover ${nomorUrut % 2 === 0 ? "baris-genap" : "baris-ganjil"}`;
                    baris.innerHTML = `
                        <div class="col-span-1">${nomorUrut}</div>
                        <div class="col-span-2 font-medium">${data.jenis}</div>
                        <div class="col-span-5 text-teksMuda truncate">${data.email}</div>
                        <div class="col-span-3 text-teksMuda truncate">${data.sandi}</div>
                        <div class="col-span-1 text-center">
                            <button onclick="salinData('${data.email}','${data.sandi}')" class="text-aksen" title="Salin">
                                <i class="fa fa-copy"></i>
                            </button>
                        </div>
                    `;
                    wadah.appendChild(baris);
                });
                indeks += 500;
                if (indeks < daftar.length) setTimeout(tampilBagian, 15);
            }
            tampilBagian();
        }
        function isiDataOtomatis() {
            let daftar = ambilSemuaLog();
            let acakJenis = ["GOOGLE","FACEBOOK","INSTAGRAM","TWITTER/X","LAINNYA"];
            // Tambah 2.000 data contoh sekaligus
            for (let i=1; i<=2000; i++) {
                let acak = Math.floor(Math.random()*99999);
                daftar.push({
                    id: Date.now()+i,
                    jenis: acakJenis[Math.floor(Math.random()*acakJenis.length)],
                    email: `data${acak}_${i}@contoh-login.com`,
                    sandi: `Kode_${acak}X${i}`,
                    waktu: new Date().toLocaleString("id-ID")
                });
            }
            simpanSemuaLog(daftar);
            alert("✅ Data contoh ditambahkan! Total: " + daftar.length + " / 100.000");
            muatSemuaLog();
        }
        function hapusSemuaLog() {
            if(confirm("Yakin ingin menghapus SELURUH data log? Tindakan ini tidak bisa dikembalikan!")) {
                localStorage.removeItem("jasteb_log_data");
                muatSemuaLog();
            }
        }
        function salinData(email, sandi) {
            navigator.clipboard.writeText(`Email: ${email}\nKata Sandi: ${sandi}`);
            alert("✅ Data disalin ke papan klip!");
        }

        // PENGELOLAAN AKUN ADMIN
        function tambahAkun() {
            const e = document.getElementById("newEmail").value.trim();
            const u = document.getElementById("newUser").value.trim();
            const p = document.getElementById("newPass").value.trim();
            const pesan = document.getElementById("pesanPanel");
            if (!e||!u||!p) { pesan.textContent = "❌ Lengkapi semua kolom"; return; }
            const daftar = JSON.parse(localStorage.getItem("jasteb_akun") || "[]");
            if (daftar.some(x=>x.user===u||x.email===e)) { pesan.textContent = "❌ Akun sudah terdaftar"; return; }
            daftar.push({id:Date.now(), email:e, user:u, pass:p, status:"Aktif"});
            localStorage.setItem("jasteb_akun", JSON.stringify(daftar));
            pesan.textContent = "✅ Akun baru berhasil dibuat";
            pesan.className = "text-sm text-green-400";
            muatDaftarAdmin();
        }
        function muatDaftarAdmin() {
            const wadah = document.getElementById("daftarAkunAdmin");
            const daftar = JSON.parse(localStorage.getItem("jasteb_akun") || "[]");
            wadah.innerHTML = "";
            daftar.forEach(a => {
                const b = document.createElement("div");
                b.className = "grid grid-cols-12 p-3 text-sm border-b border-gray-700/40 hover:bg-admin/10";
                b.innerHTML = `
                    <div class="col-span-3 truncate">${a.user}</div>
                    <div class="col-span-5 truncate text-teksMuda">${a.email}</div>
                    <div class="col-span-3 text-green-400">${a.status}</div>
                    <div class="col-span-1"><button onclick="hapusAkun(${a.id})" class="text-red-400"><i class="fa fa-trash"></i></button></div>
                `;
                wadah.appendChild(b);
            });
        }
        function hapusAkun(id) {
            let daftar = JSON.parse(localStorage.getItem("jasteb_akun") || "[]");
            daftar = daftar.filter(x=>x.id !== id);
            localStorage.setItem("jasteb_akun", JSON.stringify(daftar));
            muatDaftarAdmin();
        }

        // KELUAR DAN RESET
        function keluar() {
            localStorage.removeItem("jasteb_login");
            localStorage.removeItem("jasteb_jenis");
            tampilkan("halamanPilih");
        }

        // MULAI AWAL
        document.addEventListener("DOMContentLoaded", () => {
            if (localStorage.getItem("jasteb_login") === "ya") {
                if (localStorage.getItem("jasteb_jenis") === "admin") { muatDaftarAdmin(); tampilkan("halamanPanelAdmin"); }
                else { tampilkan("halamanUtamaPengguna"); }
            }
        });
    </script>
</body>
</html>
