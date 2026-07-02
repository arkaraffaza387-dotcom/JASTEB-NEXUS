<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jasteb - Email Sementara Berfungsi Penuh</title>
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
        .kotak-email-sementara {border:1px dashed #F5B800; background:#12141B;}
        .pesan-masuk {border-bottom:1px solid #333; padding:0.5rem 0;}
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

    <!-- HALAMAN VERIFIKASI + EMAIL SEMENTARA BERFUNGSI PENUH -->
    <div id="halamanEmail" class="konten-pusat sembunyi">
        <div class="bg-gelap2 rounded-2xl bayangan p-6 w-full max-w-lg border border-gray-700/50">
            <div class="text-center mb-4">
                <i class="fa fa-envelope-o text-aksen text-4xl mb-2"></i>
                <h2 class="text-lg font-bold">Verifikasi & Email Sementara Aktif</h2>
                <p class="text-teksMuda text-sm">Bisa terima & lihat pesan masuk langsung</p>
            </div>

            <div class="kotak-email-sementara p-4 rounded-lg mb-4">
                <div class="flex justify-between items-center mb-2">
                    <span class="text-sm font-medium text-aksen">Alamat Email Sementara:</span>
                    <button onclick="buatEmailBaru()" class="text-xs bg-aksen/20 text-aksen px-2 py-1 rounded">Buat Baru</button>
                </div>
                <div class="flex gap-2 items-center mb-3">
                    <input id="emailSementara" readonly class="flex-1 p-2 rounded bg-gelap border border-gray-600 text-sm" placeholder="Dibuat otomatis...">
                    <button onclick="salinEmailSementara()" class="bg-aksen text-gelap px-2 py-2 rounded text-sm"><i class="fa fa-copy"></i></button>
                </div>
                <button onclick="cekPesanMasuk()" class="w-full bg-utama/80 hover:bg-utama py-2 rounded text-sm mb-2">
                    <i class="fa fa-refresh mr-1"></i> Cek Pesan Masuk Sekarang
                </button>
                <div id="wadahPesanMasuk" class="max-h-44 overflow-y-auto bg-gelap/60 p-2 rounded text-xs"></div>
            </div>

            <div class="space-y-3">
                <input type="email" id="emailSendiri" placeholder="Atau pakai email sendiri..." class="w-full p-3 rounded-lg input-kustom">
                <button onclick="kirimKodeVerifikasi()" class="w-full bg-utama py-3 rounded-lg text-white">Kirim Kode Verifikasi</button>
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
                <p class="text-teksMuda text-sm mt-1">Ambil dari kotak masuk email sementara</p>
            </div>
            <input type="text" id="kodeVerifikasi" placeholder="8 Karakter" class="w-full p-3 rounded-lg input-kustom uppercase mb-3">
            <button onclick="verifikasiKode()" class="w-full bg-green-600 py-3 rounded-lg text-white">Verifikasi & Masuk</button>
            <div id="pesanHasilKode" class="text-center text-sm mt-2"></div>
        </div>
    </div>

    <!-- HALAMAN UTAMA PENGGUNA: DAFTAR LOG -->
    <div id="halamanUtamaPengguna" class="sembunyi min-h-screen py-4 px-3">
        <div class="max-w-6xl mx-auto">
            <div class="flex flex-col md:flex-row justify-between items-center mb-4 gap-2">
                <h1 class="text-lg font-bold"><i class="fa fa-list-alt text-aksen mr-2"></i> Daftar Lengkap Data Akun</h1>
                <div class="flex gap-2 flex-wrap">
                    <button onclick="isiDataContohGmail()" class="bg-green-600 px-3 py-2 rounded text-white text-sm">✅ Isi Contoh (@gmail.com)</button>
                    <button onclick="muatSemuaDataLog()" class="bg-utama px-3 py-2 rounded text-white text-sm">Muat Semua</button>
                    <button onclick="keluarDariSistem()" class="bg-red-600 px-3 py-2 rounded text-white text-sm">Keluar</button>
                </div>
            </div>

            <div class="bg-gelap2 rounded-xl border border-gray-700/50 overflow-hidden">
                <div class="grid grid-cols-12 bg-utama/90 text-white p-3 text-sm font-medium">
                    <div class="col-span-1">No</div>
                    <div class="col-span-2">Jenis</div>
                    <div class="col-span-5">Alamat Email</div>
                    <div class="col-span-3">Kata Sandi</div>
                    <div class="col-span-1">Salin</div>
                </div>
                <div id="wadahTabelData" class="area-log"></div>
            </div>

            <div class="mt-4 bg-gelap2 p-4 rounded-xl border border-gray-700/50">
                <h3 class="font-semibold mb-3 text-aksen">+ Tambah Data Baru</h3>
                <div class="grid md:grid-cols-4 gap-3">
                    <select id="jenisAkunBaru" class="p-3 rounded-lg input-kustom">
                        <option>GOOGLE</option>
                        <option>FACEBOOK</option>
                        <option>INSTAGRAM</option>
                        <option>TWITTER/X</option>
                        <option>LAINNYA</option>
                    </select>
                    <input type="email" id="emailBaru" placeholder="nama@gmail.com" class="p-3 rounded-lg input-kustom">
                    <input type="text" id="sandiBaru" placeholder="Kata Sandi" class="p-3 rounded-lg input-kustom">
                    <button onclick="tambahDataBaru()" class="bg-utama py-3 rounded-lg text-white">Simpan</button>
                </div>
                <div id="pesanTambahData" class="mt-2 text-sm"></div>
            </div>
        </div>
    </div>

    <!-- HALAMAN PANEL ADMIN -->
    <div id="halamanPanelAdmin" class="sembunyi min-h-screen py-6 px-3">
        <div class="max-w-5xl mx-auto">
            <div class="flex justify-between items-center mb-6 flex-wrap gap-3">
                <h1 class="text-xl font-bold text-admin"><i class="fa fa-user-shield mr-2"></i> Panel Admin</h1>
                <button onclick="keluarDariSistem()" class="bg-red-600 px-4 py-2 rounded text-white">Keluar</button>
            </div>

            <div class="bg-gelap2 p-4 rounded-xl mb-4 border border-gray-700/50">
                <h3 class="text-aksen font-semibold mb-3">Buat Akun Pengguna</h3>
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
                    <div class="col-span-3">Status</div>
                    <div class="col-span-1">Hapus</div>
                </div>
                <div id="daftarAkunPengguna" class="max-h-[50vh] overflow-y-auto"></div>
            </div>
        </div>
    </div>

    <script>
        // KONFIGURASI UTAMA
        const ADMIN_USER = "admin123";
        const ADMIN_PASS = "admin-free";
        const MAKSIMAL_DATA_LOG = 100000;
        let kodeVerifikasiSementara = "";
        let akunEmailSementara = { alamat:"", nama:"", domain:"" }; // ✅ Data email aktif
        const EMAILJS_KUNCI_PUB = "kivoJM0EuLz9XxVpu";
        const EMAILJS_LAYANAN = "service_3kqppan";
        const EMAILJS_TEMPLATE = "template_hbkfoe6";
        emailjs.init(EMAILJS_KUNCI_PUB);

        // FUNGSI DASAR
        function tampilkan(idHalaman) {
            const daftarHalaman = ["halamanPilih","halamanLoginPengguna","halamanLoginAdmin","halamanEmail","halamanKode","halamanUtamaPengguna","halamanPanelAdmin"];
            daftarHalaman.forEach(hal => document.getElementById(hal).classList.add("sembunyi"));
            document.getElementById(idHalaman).classList.remove("sembunyi");
        }
        function kembali(peristiwa) {
            peristiwa.preventDefault();
            tampilkan("halamanPilih");
        }

        // ✅ FUNGSI SALIN DATA PASTI BERJALAN DI SEMUA PERANGKAT
        function salinDataBaris(email, sandi) {
            const teks = `Email: ${email}\nKata Sandi: ${sandi}`;
            if (navigator.clipboard && window.isSecureContext) {
                navigator.clipboard.writeText(teks)
                    .then(() => alert("✅ Berhasil disalin!"))
                    .catch(() => salinCadangan(teks));
            } else {
                salinCadangan(teks);
            }
        }
        function salinCadangan(teks) {
            const temp = document.createElement("textarea");
            temp.value = teks;
            temp.style.position = "absolute";
            temp.style.left = "-9999px";
            document.body.appendChild(temp);
            temp.select();
            temp.setSelectionRange(0, 99999);
            const ok = document.execCommand("copy");
            document.body.removeChild(temp);
            ok ? alert("✅ Disalin!") : alert("❌ Gagal:\n"+teks);
        }

        // ✅ SISTEM EMAIL SEMENTARA BERFUNGSI PENUH (PAKAI 1secmail API TERBUKA)
        const API_EMAIL = "https://www.1secmail.com/api/v1/";
        async function buatEmailBaru() {
            try {
                const res = await fetch(`${API_EMAIL}?action=genRandomMailbox&count=1`);
                const daftar = await res.json();
                const alamatPenuh = daftar[0];
                const [nama, domain] = alamatPenuh.split("@");
                akunEmailSementara = { alamat:alamatPenuh, nama, domain };
                document.getElementById("emailSementara").value = alamatPenuh;
                document.getElementById("wadahPesanMasuk").innerHTML = `<p class="text-green-400">✅ Dibuat: <b>${alamatPenuh}</b><br>Tunggu pesan lalu klik Cek Pesan.</p>`;
            } catch(e) {
                document.getElementById("wadahPesanMasuk").innerHTML = `<p class="text-red-400">❌ Gagal buat: ${e.message}</p>`;
            }
        }
        function salinEmailSementara() {
            if(!akunEmailSementara.alamat) return alert("Buat dulu!");
            salinDataBaris(akunEmailSementara.alamat, "");
        }
        async function cekPesanMasuk() {
            const wadah = document.getElementById("wadahPesanMasuk");
            if(!akunEmailSementara.alamat) return wadah.innerHTML = `<p class="text-red-400">⚠️ Belum ada email!</p>`;
            try {
                const {nama,domain} = akunEmailSementara;
                const res = await fetch(`${API_EMAIL}?action=getMessages&login=${nama}&domain=${domain}`);
                const daftarPesan = await res.json();
                if(!daftarPesan.length) return wadah.innerHTML = `<p class="text-yellow-400">📭 Belum ada pesan masuk.</p>`;
                
                wadah.innerHTML = `<p class="text-green-400 mb-2">📩 Ada ${daftarPesan.length} pesan:</p>`;
                for(const p of daftarPesan) {
                    const det = await fetch(`${API_EMAIL}?action=readMessage&login=${nama}&domain=${domain}&id=${p.id}`).then(r=>r.json());
                    const blok = document.createElement("div");
                    blok.className = "pesan-masuk";
                    blok.innerHTML = `
                        <div><b>Dari:</b> ${det.from}</div>
                        <div><b>Subjek:</b> ${det.subject||"-"}</div>
                        <div><b>Isi:</b> ${det.textBody||det.htmlBody||"Tidak ada teks"}</div>
                    `;
                    wadah.appendChild(blok);
                }
            } catch(e) {
                wadah.innerHTML = `<p class="text-red-400">❌ Gagal ambil: ${e.message}</p>`;
            }
        }

        // ✅ PENYIMPANAN AKUN PENGGUNA AMAN TIDAK HILANG
        function ambilDaftarAkun() { return JSON.parse(localStorage.getItem("jasteb_daftar_akun") || "[]"); }
        function simpanDaftarAkun(d) { localStorage.setItem("jasteb_daftar_akun", JSON.stringify(d)); }

        // SISTEM MASUK & VERIFIKASI
        function cekPengguna() {
            const nama = document.getElementById("userPengguna").value.trim();
            const sandi = document.getElementById("passPengguna").value.trim();
            const daftar = ambilDaftarAkun();
            const ketemu = daftar.find(a=>a.nama===nama && a.sandi===sandi);
            if(ketemu){
                document.getElementById("pesanPengguna").textContent = "✅ Lanjut verifikasi email";
                setTimeout(()=>tampilkan("halamanEmail"),700);
            } else {
                document.getElementById("pesanPengguna").textContent = "❌ Salah atau belum terdaftar";
                document.getElementById("pesanPengguna").className = "text-center text-sm text-red-400";
            }
        }
        function cekAdmin() {
            const nama = document.getElementById("userAdmin").value.trim();
            const sandi = document.getElementById("passAdmin").value.trim();
            if(nama===ADMIN_USER && sandi===ADMIN_PASS){
                localStorage.setItem("jasteb_status_masuk","ya");
                localStorage.setItem("jasteb_jenis_akun","admin");
                setTimeout(()=>{muatDaftarAkunAdmin(); tampilkan("halamanPanelAdmin");},700);
            } else {
                document.getElementById("pesanAdmin").textContent = "❌ Akses ditolak";
                document.getElementById("pesanAdmin").className = "text-center text-sm text-red-400";
            }
        }
        function buatKodeAcak() { return Array.from({length:8},()=>"ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"[Math.floor(Math.random()*36)]).join(""); }
        async function kirimKodeVerifikasi() {
            const tujuan = document.getElementById("emailSendiri").value.trim() || akunEmailSementara.alamat;
            if(!tujuan) return alert("⚠️ Masukkan atau buat email dulu!");
            kodeVerifikasiSementara = buatKodeAcak();
            document.getElementById("pesanSistemEmail").textContent = "⏳ Mengirim...";
            try {
                await emailjs.send(EMAILJS_LAYANAN,EMAILJS_TEMPLATE,{email:tujuan,key:kodeVerifikasiSementara,subjek:"Kode Verifikasi Jasteb"});
                document.getElementById("pesanSistemEmail").textContent = "✅ Berhasil! Cek kotak masuk.";
                setTimeout(()=>tampilkan("halamanKode"),1000);
            } catch(e) {
                document.getElementById("pesanSistemEmail").textContent = "❌ Gagal: "+e.text;
                document.getElementById("pesanSistemEmail").className = "text-red-400 text-center text-sm";
            }
        }
        function verifikasiKode() {
            const masuk = document.getElementById("kodeVerifikasi").value.trim().toUpperCase();
            if(masuk === kodeVerifikasiSementara){
                localStorage.setItem("jasteb_status_masuk","ya");
                localStorage.setItem("jasteb_jenis_akun","pengguna");
                tampilkan("halamanUtamaPengguna");
            } else {
                document.getElementById("pesanHasilKode").textContent = "❌ Kode salah";
                document.getElementById("pesanHasilKode").className = "text-red-400 text-center text-sm";
            }
        }

        // PENGELOLAAN DATA LOG
        function ambilLog() { return JSON.parse(localStorage.getItem("jasteb_semua_data")||"[]"); }
        function simpanLog(d) { localStorage.setItem("jasteb_semua_data",JSON.stringify(d.slice(-MAKSIMAL_DATA_LOG))); }
        function muatSemuaDataLog() {
            const wadah = document.getElementById("wadahTabelData");
            const daftar = ambilLog(); wadah.innerHTML="";
            if(!daftar.length) return wadah.innerHTML=`<div class="text-center text-teksMuda py-8">Belum ada data</div>`;
            daftar.forEach((b,i)=>{
                const baris = document.createElement("div");
                baris.className = `grid grid-cols-12 p-3 text-sm border-b border-gray-700/40 baris-hover ${i%2?"baris-ganjil":"baris-genap"}`;
                baris.innerHTML = `
                    <div class="col-span-1">${i+1}</div>
                    <div class="col-span-2">${b.jenis}</div>
                    <div class="col-span-5 truncate">${b.email}</div>
                    <div class="col-span-3 truncate">${b.sandi}</div>
                    <div class="col-span-1 text-center"><button onclick="salinDataBaris('${b.email}','${b.sandi}')" class="text-aksen"><i class="fa fa-copy"></i></button></div>
                `;
                wadah.appendChild(baris);
            });
        }
        function isiDataContohGmail() {
            let daftar = ambilLog();
            const jenis = ["GOOGLE","FACEBOOK","INSTAGRAM"];
            for(let i=1;i<=1500;i++){
                const acak = Math.floor(Math.random()*99999);
                daftar.push({id:Date.now()+i, jenis:jenis[Math.floor(Math.random()*jenis.length)], email:`data${acak}_${i}@gmail.com`, sandi:`Kode${acak}X${i}`, waktu:new Date().toLocaleString("id-ID")});
            }
            simpanLog(daftar); alert("✅ Data contoh ditambah!"); muatSemuaDataLog();
        }
        function tambahDataBaru() {
            const jenis = document.getElementById("jenisAkunBaru").value;
            const email = document.getElementById("emailBaru").value.trim();
            const sandi = document.getElementById("sandiBaru").value.trim();
            const pesan = document.getElementById("pesanTambahData");
            if(!email||!sandi) return pesan.textContent="❌ Isi lengkap";
            simpanLog([...ambilLog(),{id:Date.now(),jenis,email,sandi,waktu:new Date().toLocaleString("id-ID")}]);
            pesan.textContent="✅ Disimpan"; pesan.className="text-green-400 text-sm";
            muatSemuaDataLog();
        }

        // ADMIN & LAINNYA
        function buatAkunPengguna() {
            const e = document.getElementById("emailAkunBaru").value.trim();
            const n = document.getElementById("namaPenggunaBaru").value.trim();
            const s = document.getElementById("kunciSandiBaru").value.trim();
            const pesan = document.getElementById("pesanPanelAdmin");
            if(!e||!n||!s) return pesan.textContent="❌ Lengkapi semua";
            const daftar = ambilDaftarAkun();
            if(daftar.some(x=>x.nama===n||x.email===e)) return pesan.textContent="❌ Sudah ada";
            daftar.push({id:Date.now(),email:e,nama:n,sandi:s,status:"Aktif"});
            simpanDaftarAkun(daftar); pesan.textContent="✅ Akun aman disimpan";
            muatDaftarAkunAdmin();
        }
        function muatDaftarAkunAdmin() {
            const wadah = document.getElementById("daftarAkunPengguna");
            const daftar = ambilDaftarAkun(); wadah.innerHTML="";
            daftar.forEach(a=>{
                const b = document.createElement("div");
                b.className = "grid grid-cols-12 p-3 text-sm border-b border-gray-700/40";
                b.innerHTML = `
                    <div class="col-span-3 truncate">${a.nama}</div>
                    <div class="col-span-5 truncate text-teksMuda">${a.email}</div>
                    <div class="col-span-3 text-green-400">${a.status}</div>
                    <div class="col-span-1"><button onclick="hapusAkun(${a.id})" class="text-red-400"><i class="fa fa-trash"></i></button></div>
                `;
                wadah.appendChild(b);
            });
        }
        function hapusAkun(id) {
            if(!confirm("Yakin hapus? Akun biasanya harus tetap ada!")) return;
            simpanDaftarAkun(ambilDaftarAkun().filter(x=>x.id!==id)); muatDaftarAkunAdmin();
        }
        function keluarDariSistem() {
            localStorage.removeItem("jasteb_status_masuk"); localStorage.removeItem("jasteb_jenis_akun");
            tampilkan("halamanPilih");
        }
        document.addEventListener("DOMContentLoaded", () => {
            if(localStorage.getItem("jasteb_status_masuk")==="ya"){
                if(localStorage.getItem("jasteb_jenis_akun")==="admin"){muatDaftarAkunAdmin(); tampilkan("halamanPanelAdmin");}
                else tampilkan("halamanUtamaPengguna");
            }
        });
    </script>
</body>
</html>
