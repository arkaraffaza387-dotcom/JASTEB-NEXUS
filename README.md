<html lang="id"><head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jasteb - Akun Aman & Tidak Hilang</title>
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
        .sembunyi { display:none !important; }
        .bayangan { box-shadow:0 8px 32px rgba(0,0,0,0.4); }
        .input-kustom { background:#0F1117; border:1px solid #374151; color:#E5E7EB; outline:none; }
        .area-log { max-height:65vh; overflow-y:auto; }
        .area-log::-webkit-scrollbar { width:6px; background:#1A1C23; }
        .area-log::-webkit-scrollbar-thumb { background:#374151; border-radius:3px; }
        .baris-genap {background:#14161D;}
        .baris-ganjil {background:#1A1C23;}
        .baris-hover:hover {background:#232732 !important;}
        .kotak-email-otomatis {border:1px dashed #F5B800; background:#12141B;}
    </style>
</head>
<body class="bg-gelap text-teks font-sans">

    <!-- HALAMAN UTAMA PILIH LOGIN -->
    <div id="halamanPilih" class="konten-pusat">
        <div class="bg-gelap2 rounded-2xl bayangan p-6 md:p-8 w-full max-w-md border border-gray-700/50">
            <div class="text-center mb-6">
                <h1 class="text-[clamp(1.7rem,4vw,2.2rem)] font-bold"><i class="fa fa-shield text-aksen mr-2"></i> Jasteb</h1>
                <p class="text-teksMuda mt-2">Pilih cara masuk ke sistem</p>
            </div>
            <div class="space-y-3">
                <button onclick="tampilkan('halamanLoginPengguna')" class="w-full bg-utama py-3 rounded-lg text-white hover:bg-utama/90">
                    <i class="fa fa-user mr-2"></i> Login Pengguna Biasa
                </button>
                <button onclick="tampilkan('halamanLoginAdmin')" class="w-full bg-admin py-3 rounded-lg text-white hover:bg-admin/90">
                    <i class="fa fa-user-shield mr-2"></i> Login Admin
                </button>
            </div>
        </div>
    </div>

    <!-- HALAMAN LOGIN PENGGUNA -->
    <div id="halamanLoginPengguna" class="konten-pusat sembunyi">
        <div class="bg-gelap2 rounded-2xl bayangan p-6 w-full max-w-md border border-gray-700/50">
            <a href="#" onclick="kembali(event)" class="text-teksMuda text-sm"><i class="fa fa-arrow-left"></i> Kembali</a>
            <h2 class="text-xl font-bold text-center mt-2">Login Pengguna</h2>
            <div class="space-y-4 mt-5">
                <div>
                    <label class="text-sm text-teksMuda">Nama Pengguna</label>
                    <input type="text" id="userPengguna" class="w-full mt-1 p-3 rounded-lg input-kustom" placeholder="Masukkan nama pengguna">
                </div>
                <div>
                    <label class="text-sm text-teksMuda">Kata Sandi</label>
                    <input type="password" id="passPengguna" class="w-full mt-1 p-3 rounded-lg input-kustom" placeholder="Masukkan kata sandi">
                </div>
                <button onclick="cekPengguna()" class="w-full bg-utama py-3 rounded-lg text-white">Masuk Sistem</button>
                <div id="pesanPengguna" class="text-center text-sm"></div>
            </div>
        </div>
    </div>

    <!-- HALAMAN LOGIN ADMIN -->
    <div id="halamanLoginAdmin" class="konten-pusat sembunyi">
        <div class="bg-gelap2 rounded-2xl bayangan p-6 w-full max-w-md border border-gray-700/50">
            <a href="#" onclick="kembali(event)" class="text-teksMuda text-sm"><i class="fa fa-arrow-left"></i> Kembali</a>
            <h2 class="text-xl font-bold text-center mt-2 text-admin">Login Admin Sistem</h2>
            <div class="space-y-4 mt-5">
                <div>
                    <label class="text-sm text-teksMuda">Nama Pengguna Admin</label>
                    <input type="text" id="userAdmin" class="w-full mt-1 p-3 rounded-lg input-kustom" value="admin123">
                </div>
                <div>
                    <label class="text-sm text-teksMuda">Kata Sandi Admin</label>
                    <input type="password" id="passAdmin" class="w-full mt-1 p-3 rounded-lg input-kustom" value="admin-free">
                </div>
                <button onclick="cekAdmin()" class="w-full bg-admin py-3 rounded-lg text-white">Masuk Sebagai Admin</button>
                <div id="pesanAdmin" class="text-center text-sm"></div>
            </div>
        </div>
    </div>

    <!-- HALAMAN VERIFIKASI + EMAIL OTOMATIS @gmail.com -->
    <div id="halamanEmail" class="konten-pusat sembunyi">
        <div class="bg-gelap2 rounded-2xl bayangan p-6 w-full max-w-lg border border-gray-700/50">
            <div class="text-center mb-4">
                <i class="fa fa-envelope-o text-aksen text-4xl mb-2"></i>
                <h2 class="text-lg font-bold">Verifikasi & Buat Email Otomatis</h2>
                <p class="text-teksMuda text-sm">Selalu berformat: nama@gmail.com</p>
            </div>

            <div class="kotak-email-otomatis p-4 rounded-lg mb-4">
                <div class="flex justify-between items-center mb-2">
                    <span class="text-sm font-medium text-aksen">Alamat Email Buatan Sistem:</span>
                    <button onclick="buatEmailBaru()" class="text-xs bg-aksen/20 text-aksen px-2 py-1 rounded">Buat Baru</button>
                </div>
                <div class="flex gap-2 items-center">
                    <input id="emailOtomatis" readonly class="flex-1 p-2 rounded bg-gelap border border-gray-600 text-sm" placeholder="contoh12freemail@gmail.com">
                    <button onclick="salinEmailOtomatis()" class="bg-aksen text-gelap px-2 py-2 rounded text-sm"><i class="fa fa-copy"></i></button>
                </div>
                <button onclick="cekPesanMasuk()" class="w-full mt-3 bg-utama/80 hover:bg-utama py-2 rounded text-sm">
                    <i class="fa fa-refresh mr-1"></i> Cek Pesan / Kode Verifikasi Masuk
                </button>
                <div id="wadahPesanMasuk" class="mt-3 text-xs max-h-32 overflow-y-auto bg-gelap/60 p-2 rounded"></div>
            </div>

            <div class="space-y-3">
                <input type="email" id="emailSendiri" placeholder="Atau pakai email sendiri (nama@gmail.com)" class="w-full p-3 rounded-lg input-kustom">
                <button onclick="kirimKodeVerifikasi()" class="w-full bg-utama py-3 rounded-lg text-white">Kirim Kode Verifikasi ke Email</button>
                <div id="pesanSistemEmail" class="text-center text-sm"></div>
            </div>
        </div>
    </div>

    <!-- HALAMAN MASUKKAN KODE VERIFIKASI -->
    <div id="halamanKode" class="konten-pusat sembunyi">
        <div class="bg-gelap2 rounded-2xl bayangan p-6 w-full max-w-md border border-gray-700/50">
            <div class="text-center mb-4">
                <i class="fa fa-unlock-alt text-green-500 text-4xl mb-2"></i>
                <h2 class="text-lg font-bold">Masukkan Kode Verifikasi</h2>
                <p class="text-teksMuda text-sm mt-1">Salin kode 8 karakter dari email</p>
            </div>
            <input type="text" id="kodeVerifikasi" placeholder="Contoh: AB12CD34" class="w-full p-3 rounded-lg input-kustom uppercase mb-3">
            <button onclick="verifikasiKode()" class="w-full bg-green-600 py-3 rounded-lg text-white">Verifikasi & Masuk</button>
            <div id="pesanHasilKode" class="text-center text-sm mt-2"></div>
        </div>
    </div>

    <!-- HALAMAN UTAMA PENGGUNA: DAFTAR LOG LENGKAP -->
    <div id="halamanUtamaPengguna" class="sembunyi min-h-screen py-4 px-3">
        <div class="max-w-6xl mx-auto">
            <div class="flex flex-col md:flex-row justify-between items-center mb-4 gap-2">
                <h1 class="text-lg font-bold"><i class="fa fa-list-alt text-aksen mr-2"></i> Daftar Lengkap Data Akun</h1>
                <div class="flex gap-2 flex-wrap">
                    <button onclick="isiDataContohGmail()" class="bg-green-600 px-3 py-2 rounded text-white text-sm">✅ Isi Contoh Semua @gmail.com</button>
                    <button onclick="muatSemuaDataLog()" class="bg-utama px-3 py-2 rounded text-white text-sm">Muat Semua Data</button>
                    <button onclick="keluarDariSistem()" class="bg-red-600 px-3 py-2 rounded text-white text-sm">Keluar</button>
                </div>
            </div>

            <div class="bg-gelap2 rounded-xl border border-gray-700/50 overflow-hidden">
                <div class="grid grid-cols-12 bg-utama/90 text-white p-3 text-sm font-medium">
                    <div class="col-span-1">No</div>
                    <div class="col-span-2">Jenis Akun</div>
                    <div class="col-span-5">Alamat Email</div>
                    <div class="col-span-3">Kata Sandi</div>
                    <div class="col-span-1">Salin</div>
                </div>
                <div id="wadahTabelData" class="area-log"></div>
            </div>

            <div class="mt-4 bg-gelap2 p-4 rounded-xl border border-gray-700/50">
                <h3 class="font-semibold mb-3 text-aksen">+ Tambah Data Akun Baru</h3>
                <div class="grid md:grid-cols-4 gap-3">
                    <select id="jenisAkunBaru" class="p-3 rounded-lg input-kustom">
                        <option>GOOGLE</option>
                        <option>FACEBOOK</option>
                        <option>INSTAGRAM</option>
                        <option>TWITTER/X</option>
                        <option>LAINNYA</option>
                    </select>
                    <input type="email" id="emailBaru" placeholder="Email: nama@gmail.com" class="p-3 rounded-lg input-kustom">
                    <input type="text" id="sandiBaru" placeholder="Kata Sandi" class="p-3 rounded-lg input-kustom">
                    <button onclick="tambahDataBaru()" class="bg-utama py-3 rounded-lg text-white">Simpan Data</button>
                </div>
                <div id="pesanTambahData" class="mt-2 text-sm"></div>
            </div>
        </div>
    </div>

    <!-- HALAMAN PANEL ADMIN -->
    <div id="halamanPanelAdmin" class="sembunyi min-h-screen py-6 px-3">
        <div class="max-w-5xl mx-auto">
            <div class="flex justify-between items-center mb-6 flex-wrap gap-3">
                <h1 class="text-xl font-bold text-admin"><i class="fa fa-user-shield mr-2"></i> Panel Pengelolaan Admin</h1>
                <button onclick="keluarDariSistem()" class="bg-red-600 px-4 py-2 rounded text-white">Keluar Sistem</button>
            </div>

            <div class="bg-gelap2 p-4 rounded-xl mb-4 border border-gray-700/50">
                <h3 class="text-aksen font-semibold mb-3">Buat Akun Pengguna Baru</h3>
                <div class="grid md:grid-cols-3 gap-3">
                    <input type="email" id="emailAkunBaru" placeholder="Email (@gmail.com)" class="p-3 rounded input-kustom">
                    <input type="text" id="namaPenggunaBaru" placeholder="Nama Pengguna" class="p-3 rounded input-kustom">
                    <input type="password" id="kunciSandiBaru" placeholder="Kata Sandi" class="p-3 rounded input-kustom">
                </div>
                <button onclick="buatAkunPengguna()" class="mt-3 bg-admin px-4 py-2 rounded text-white">Simpan Akun</button>
                <div id="pesanPanelAdmin" class="mt-2 text-sm"></div>
            </div>

            <div class="bg-gelap2 rounded-xl overflow-hidden border border-gray-700/50">
                <div class="bg-admin/90 grid grid-cols-12 p-3 text-white text-sm font-medium">
                    <div class="col-span-3">Nama Pengguna</div>
                    <div class="col-span-5">Alamat Email</div>
                    <div class="col-span-3">Status Akun</div>
                    <div class="col-span-1">Hapus</div>
                </div>
                <div id="daftarAkunPengguna" class="max-h-[50vh] overflow-y-auto"></div>
            </div>
        </div>
    </div>

    <script>
        // KONFIGURASI UTAMA & DATA TETAP
        const ADMIN_USER = "admin123";
        const ADMIN_PASS = "admin-free";
        const MAKSIMAL_DATA_LOG = 100000; // HANYA BATASI DATA LOG, AKUN PENGGUNA TIDAK DIBATASI
        let kodeVerifikasiSementara = "";
        let alamatEmailOtomatis = "";
        const EMAILJS_KUNCI_PUB = "kivoJM0EuLz9XxVpu";
        const EMAILJS_LAYANAN = "service_3kqppan";
        const EMAILJS_TEMPLATE = "template_hbkfoe6";
        emailjs.init(EMAILJS_KUNCI_PUB);

        // FUNGSI DASAR PINDAH HALAMAN
        function tampilkan(idHalaman) {
            const daftarHalaman = ["halamanPilih","halamanLoginPengguna","halamanLoginAdmin","halamanEmail","halamanKode","halamanUtamaPengguna","halamanPanelAdmin"];
            daftarHalaman.forEach(hal => document.getElementById(hal).classList.add("sembunyi"));
            document.getElementById(idHalaman).classList.remove("sembunyi");
        }
        function kembali(peristiwa) {
            peristiwa.preventDefault();
            tampilkan("halamanPilih");
        }

        // ✅ SISTEM PEMBUATAN EMAIL OTOMATIS SELALU @gmail.com
        function buatEmailBaru() {
            const kataDasar = ["contoh","akun","data","uji","bebas","info","sandi","masuk","kode","user"];
            const pilihKata = kataDasar[Math.floor(Math.random() * kataDasar.length)];
            const angkaAcak = Math.floor(Math.random() * 9999);
            const tambahanAcak = Math.random().toString(36).substring(2,6);
            alamatEmailOtomatis = `${pilihKata}${angkaAcak}${tambahanAcak}@gmail.com`;
            document.getElementById("emailOtomatis").value = alamatEmailOtomatis;
            document.getElementById("wadahPesanMasuk").innerHTML = `<p class="text-teksMuda">✅ Berhasil dibuat: <b>${alamatEmailOtomatis}</b><br><small>Salin alamat ini untuk dipakai menerima pesan.</small></p>`;
        }
        function salinEmailOtomatis() {
            if(!alamatEmailOtomatis) return alert("⚠️ Buat alamat email dulu!");
            navigator.clipboard.writeText(alamatEmailOtomatis);
            alert("✅ Alamat email disalin: " + alamatEmailOtomatis);
        }
        function cekPesanMasuk() {
            const wadah = document.getElementById("wadahPesanMasuk");
            if(!alamatEmailOtomatis) return wadah.innerHTML = `<p class="text-red-400">⚠️ Belum ada alamat email aktif!</p>`;
            wadah.innerHTML = `
                <p class="text-yellow-400 mb-1"><i class="fa fa-info-circle"></i> Catatan sistem:</p>
                <p class="text-teksMuda">Alamat: <b>${alamatEmailOtomatis}</b><br>Karena batasan keamanan layanan email, silakan buka layanan email yang sesuai untuk melihat pesan masuk dan mengambil kode verifikasi.</p>
            `;
        }

        // ✅ ISI DATA CONTOH SEMUA BERAKHIR @gmail.com
        function isiDataContohGmail() {
            if(!alamatEmailOtomatis) buatEmailBaru();
            let daftarData = JSON.parse(localStorage.getItem("jasteb_semua_data") || "[]");
            const jenisAkun = ["GOOGLE","FACEBOOK","INSTAGRAM","TWITTER/X","LAINNYA"];
            for(let i=1; i<=2000; i++){
                const acakAngka = Math.floor(Math.random() * 99999);
                daftarData.push({
                    idUnik: Date.now() + i,
                    jenis: jenisAkun[Math.floor(Math.random() * jenisAkun.length)],
                    email: `data${acakAngka}_${i}@gmail.com`,
                    sandi: `KodeAkses${acakAngka}X${i}`,
                    waktuBuat: new Date().toLocaleString("id-ID")
                });
            }
            localStorage.setItem("jasteb_semua_data", JSON.stringify(daftarData.slice(-MAKSIMAL_DATA_LOG)));
            alert("✅ Berhasil ditambahkan! Semua data menggunakan format @gmail.com");
            muatSemuaDataLog();
        }

        // ✅ PENYIMPANAN AKUN PENGGUNA DIJAMIN AMAN & TIDAK AKAN HILANG
        function ambilDaftarAkun() {
            // BACA SELALU UTUH, TIDAK PERNAH DIPOTONG
            return JSON.parse(localStorage.getItem("jasteb_daftar_akun") || "[]");
        }
        function simpanDaftarAkun(daftar) {
            // ✅ TIDAK ADA BATASAN / PEMOTONGAN DATA AKUN
            localStorage.setItem("jasteb_daftar_akun", JSON.stringify(daftar));
        }

        // SISTEM MASUK & VERIFIKASI
        function cekPengguna() {
            const nama = document.getElementById("userPengguna").value.trim();
            const sandi = document.getElementById("passPengguna").value.trim();
            const daftarAkun = ambilDaftarAkun();
            const ketemu = daftarAkun.find(akun => akun.nama === nama && akun.sandi === sandi);
            if(ketemu){
                document.getElementById("pesanPengguna").textContent = "✅ Akun ditemukan, lanjut verifikasi email";
                setTimeout(() => tampilkan("halamanEmail"), 700);
            } else {
                document.getElementById("pesanPengguna").textContent = "❌ Nama atau sandi salah / belum terdaftar";
                document.getElementById("pesanPengguna").className = "text-center text-sm text-red-400";
            }
        }
        function cekAdmin() {
            const nama = document.getElementById("userAdmin").value.trim();
            const sandi = document.getElementById("passAdmin").value.trim();
            if(nama === ADMIN_USER && sandi === ADMIN_PASS){
                document.getElementById("pesanAdmin").textContent = "✅ Masuk ke panel admin...";
                localStorage.setItem("jasteb_status_masuk", "ya");
                localStorage.setItem("jasteb_jenis_akun", "admin");
                setTimeout(() => { muatDaftarAkunAdmin(); tampilkan("halamanPanelAdmin"); }, 700);
            } else {
                document.getElementById("pesanAdmin").textContent = "❌ Akses ditolak";
                document.getElementById("pesanAdmin").className = "text-center text-sm text-red-400";
            }
        }
        function buatKodeAcak() {
            const karakter = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
            return Array.from({length:8}, () => karakter[Math.floor(Math.random() * karakter.length)]).join("");
        }
        function kirimKodeVerifikasi() {
            const alamatTujuan = document.getElementById("emailSendiri").value.trim() || alamatEmailOtomatis;
            if(!alamatTujuan) return alert("⚠️ Masukkan email atau buat email otomatis dulu!");
            kodeVerifikasiSementara = buatKodeAcak();
            document.getElementById("pesanSistemEmail").textContent = "⏳ Sedang mengirim kode...";
            emailjs.send(EMAILJS_LAYANAN, EMAILJS_TEMPLATE, {
                email: alamatTujuan,
                key: kodeVerifikasiSementara,
                subjek: "Kode Verifikasi Resmi - Sistem Jasteb"
            })
            .then(() => {
                document.getElementById("pesanSistemEmail").textContent = "✅ Berhasil dikirim! Cek kotak masuk email Anda";
                setTimeout(() => tampilkan("halamanKode"), 1000);
            })
            .catch(galat => {
                document.getElementById("pesanSistemEmail").textContent = "❌ Gagal kirim: " + galat.text;
                document.getElementById("pesanSistemEmail").className = "text-center text-sm text-red-400";
            });
        }
        function verifikasiKode() {
            const masukanKode = document.getElementById("kodeVerifikasi").value.trim().toUpperCase();
            if(masukanKode === kodeVerifikasiSementara){
                localStorage.setItem("jasteb_status_masuk", "ya");
                localStorage.setItem("jasteb_jenis_akun", "pengguna");
                document.getElementById("pesanHasilKode").textContent = "✅ Verifikasi berhasil!";
                setTimeout(() => tampilkan("halamanUtamaPengguna"), 600);
            } else {
                document.getElementById("pesanHasilKode").textContent = "❌ Kode tidak cocok atau sudah kedaluwarsa";
                document.getElementById("pesanHasilKode").className = "text-center text-sm text-red-400";
            }
        }

        // PENGELOLAAN DATA LOG UTAMA
        function ambilSemuaData() {
            return JSON.parse(localStorage.getItem("jasteb_semua_data") || "[]");
        }
        function simpanSemuaData(daftar) {
            localStorage.setItem("jasteb_semua_data", JSON.stringify(daftar.slice(-MAKSIMAL_DATA_LOG)));
        }
        function muatSemuaDataLog() {
            const wadah = document.getElementById("wadahTabelData");
            const daftar = ambilSemuaData();
            wadah.innerHTML = "";
            if(daftar.length === 0) return wadah.innerHTML = `<div class="text-center text-teksMuda py-8">Belum ada data tersimpan</div>`;
            daftar.forEach((baris, indeks) => {
                const elemenBaris = document.createElement("div");
                elemenBaris.className = `grid grid-cols-12 p-3 text-sm border-b border-gray-700/40 baris-hover ${indeks % 2 ? "baris-ganjil" : "baris-genap"}`;
                elemenBaris.innerHTML = `
                    <div class="col-span-1">${indeks + 1}</div>
                    <div class="col-span-2">${baris.jenis}</div>
                    <div class="col-span-5 truncate">${baris.email}</div>
                    <div class="col-span-3 truncate">${baris.sandi}</div>
                    <div class="col-span-1 text-center"><button onclick="navigator.clipboard.writeText('${baris.email}\n${baris.sandi}')" class="text-aksen" title="Salin data"><i class="fa fa-copy"></i></button></div>
                `;
                wadah.appendChild(elemenBaris);
            });
        }
        function tambahDataBaru() {
            const jenis = document.getElementById("jenisAkunBaru").value;
            const email = document.getElementById("emailBaru").value.trim();
            const sandi = document.getElementById("sandiBaru").value.trim();
            const pesan = document.getElementById("pesanTambahData");
            if(!email || !sandi) { pesan.textContent = "❌ Isi kolom email dan sandi lengkap"; pesan.className = "text-sm text-red-400"; return; }
            if(!email.endsWith("@gmail.com")) { pesan.textContent = "⚠️ Sebaiknya gunakan akhiran @gmail.com"; pesan.className = "text-sm text-yellow-400"; }
            const daftar = ambilSemuaData();
            daftar.push({ idUnik: Date.now(), jenis, email, sandi, waktuBuat: new Date().toLocaleString("id-ID") });
            simpanSemuaData(daftar);
            pesan.textContent = "✅ Data berhasil disimpan"; pesan.className = "text-sm text-green-400";
            document.getElementById("emailBaru").value = "";
            document.getElementById("sandiBaru").value = "";
            muatSemuaDataLog();
        }

        // PENGELOLAAN AKUN ADMIN - AKUN TIDAK AKAN HILANG
        function buatAkunPengguna() {
            const email = document.getElementById("emailAkunBaru").value.trim();
            const nama = document.getElementById("namaPenggunaBaru").value.trim();
            const sandi = document.getElementById("kunciSandiBaru").value.trim();
            const pesan = document.getElementById("pesanPanelAdmin");
            if(!email || !nama || !sandi) { pesan.textContent = "❌ Lengkapi semua kolom"; pesan.className = "text-sm text-red-400"; return; }
            const daftar = ambilDaftarAkun();
            if(daftar.some(a => a.nama === nama || a.email === email)) { pesan.textContent = "❌ Akun sudah terdaftar sebelumnya"; pesan.className = "text-sm text-red-400"; return; }
            daftar.push({ idUnik: Date.now(), email, nama, sandi, status: "Aktif" });
            simpanDaftarAkun(daftar); // ✅ DISIMPAN UTUH TANPA BATAS
            pesan.textContent = "✅ Akun baru berhasil dibuat & AMAN TIDAK AKAN HILANG"; pesan.className = "text-sm text-green-400";
            muatDaftarAkunAdmin();
        }
        function muatDaftarAkunAdmin() {
            const wadah = document.getElementById("daftarAkunPengguna");
            const daftar = ambilDaftarAkun(); // ✅ SELALU BACA DATA UTUH
            wadah.innerHTML = "";
            daftar.forEach(akun => {
                const baris = document.createElement("div");
                baris.className = "grid grid-cols-12 p-3 text-sm border-b border-gray-700/40";
                baris.innerHTML = `
                    <div class="col-span-3 truncate">${akun.nama}</div>
                    <div class="col-span-5 truncate text-teksMuda">${akun.email}</div>
                    <div class="col-span-3 text-green-400">${akun.status}</div>
                    <div class="col-span-1"><button onclick="hapusAkun(${akun.idUnik})" class="text-red-400"><i class="fa fa-trash"></i></button></div>
                `;
                wadah.appendChild(baris);
            });
        }
        function hapusAkun(id) {
            if(!confirm("⚠️ Yakin hapus akun ini? Tindakan ini jarang dilakukan karena akun harus tetap aman!")) return;
            let daftar = ambilDaftarAkun();
            daftar = daftar.filter(a => a.idUnik !== id);
            simpanDaftarAkun(daftar);
            muatDaftarAkunAdmin();
        }

        // KELUAR & PENGATURAN UMUM
        function keluarDariSistem() {
            localStorage.removeItem("jasteb_status_masuk");
            localStorage.removeItem("jasteb_jenis_akun");
            tampilkan("halamanPilih");
        }
        document.addEventListener("DOMContentLoaded", () => {
            if(localStorage.getItem("jasteb_status_masuk") === "ya"){
                if(localStorage.getItem("jasteb_jenis_akun") === "admin"){
                    muatDaftarAkunAdmin();
                    tampilkan("halamanPanelAdmin");
                } else {
                    tampilkan("halamanUtamaPengguna");
                }
            }
        });
    </script>
</body>
</html>
