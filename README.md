<html lang="id"><head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Notifikasi Pemeliharaan Server | NEXUS-GAMER & NEXUS.ID</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/emailjs-com@3/dist/email.min.js"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        utama: '#165DFF',
                        peringatan: '#F59E0B',
                        bahaya: '#DC2626',
                        gelap: '#1E293B',
                        nexus: '#4F46E5'
                    },
                    fontFamily: {
                        inter: ['Inter', 'system-ui', 'sans-serif'],
                    },
                }
            }
        }
    </script>
    <style type="text/tailwindcss">
        @layer utilities {
            .bayangan {
                box-shadow: 0 8px 32px rgba(0, 0, 0, 0.12);
            }
            .bayangan-tebal {
                box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
            }
        }
    </style>
</head>
<body class="font-inter bg-gradient-to-br from-gray-100 to-gray-200 min-h-screen flex items-center justify-center p-4">
    <div class="w-full max-w-lg">
        <!-- Kotak Utama -->
        <div class="bg-white rounded-2xl bayangan overflow-hidden">
            <!-- Bagian Kepala -->
            <div class="bg-nexus text-white p-6 text-center">
                <div class="w-16 h-16 bg-white/20 rounded-full flex items-center justify-center mx-auto mb-3 text-2xl">
                    <i class="fa fa-gamepad"></i>
                </div>
                <h1 class="text-xl font-bold">NEXUS-GAMER & NEXUS.ID</h1>
                <p class="text-white/80 text-sm mt-1">Sistem Pemberitahuan Resmi</p>
            </div>

            <!-- Bagian Isi -->
            <div class="p-6">
                <!-- Kotak Peringatan -->
                <div class="bg-peringatan/10 border-l-4 border-peringatan p-4 rounded-r-lg mb-5">
                    <div class="flex items-start gap-2">
                        <i class="fa fa-exclamation-triangle text-peringatan text-lg mt-0.5"></i>
                        <div class="text-sm text-gelap">
                            <p class="font-medium mb-1">PEMBERITAHUAN PEMELIHARAAN SERVER</p>
                            <p class="text-gray-700">Silakan masukkan alamat email terdaftar kamu agar mendapatkan notifikasi resmi ini langsung ke kotak masuk.</p>
                        </div>
                    </div>
                </div>

                <!-- Kotak Pesan Notifikasi -->
                <div id="pesanNotifikasi" class="hidden mb-4 p-3 rounded-lg text-sm"></div>

                <!-- Formulir Email -->
                <form id="formEmail" class="space-y-4">
                    <div>
                        <label for="alamatEmail" class="block text-sm font-medium text-gray-700 mb-1">Alamat Email Terdaftar</label>
                        <div class="relative">
                            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                                <i class="fa fa-envelope-o text-gray-400"></i>
                            </div>
                            <input 
                                type="email" 
                                id="alamatEmail" 
                                required
                                placeholder="contoh@gmail.com"
                                class="w-full pl-10 pr-3 py-2.5 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-nexus/50 focus:border-nexus transition-all"
                            >
                        </div>
                        <p class="text-xs text-gray-500 mt-1">* Masukkan email yang benar dan aktif</p>
                    </div>

                    <button 
                        type="submit"
                        class="w-full bg-nexus hover:bg-nexus/90 text-white font-medium py-2.5 px-4 rounded-lg transition-all transform hover:scale-[1.01] active:scale-98 flex items-center justify-center gap-2 bayangan-tebal"
                    >
                        <i class="fa fa-paper-plane"></i>
                        Kirim Pemberitahuan ke Email
                    </button>
                </form>
            </div>

            <!-- Bagian Bawah -->
            <div class="bg-gray-50 px-6 py-4 border-t border-gray-200 text-center text-xs text-gray-600">
                <p>Dikelola oleh Tim NEXUS-GAMER & NEXUS.ID</p>
            </div>
        </div>
    </div>

    <script>
        // DATA LENGKAP DARI AKUN ANDA
        const EMAILJS_USER_ID = "kivoJM0EuLz9XxVpu";
        const EMAILJS_SERVICE_ID = "service_r4a15ej";
        const EMAILJS_TEMPLATE_ID = "template_6cneczm";

        // Inisialisasi EmailJS
        (function(){
            emailjs.init(EMAILJS_USER_ID);
        })();

        const form = document.getElementById('formEmail');
        const notifikasi = document.getElementById('pesanNotifikasi');

        form.addEventListener('submit', async (e) => {
            e.preventDefault();
            const emailTujuan = document.getElementById('alamatEmail').value.trim();

            tampilkanPesan('⏳ Sedang mengirim pesan ke email kamu...', 'proses');

            try {
                const hasil = await emailjs.send(
                    EMAILJS_SERVICE_ID,
                    EMAILJS_TEMPLATE_ID,
                    {
                        email: emailTujuan // Sesuai variabel {{email}} di templat kamu
                    }
                );

                if (hasil.status === 200) {
                    tampilkanPesan(`✅ Berhasil! Pesan sudah dikirim ke ${emailTujuan}. Silakan cek kotak masuk atau folder Spam/Junk.`, 'sukses');
                    form.reset();
                } else {
                    throw new Error('Gagal kirim');
                }
            } catch (err) {
                console.error('Kesalahan:', err);
                tampilkanPesan('❌ Gagal mengirim pesan. Periksa koneksi internet atau pengaturan templat EmailJS.', 'gagal');
            }
        });

        function tampilkanPesan(teks, jenis) {
            notifikasi.classList.remove('hidden', 'bg-green-100','text-green-800','bg-red-100','text-red-800','bg-yellow-100','text-yellow-800');
            notifikasi.textContent = teks;
            if(jenis === 'sukses'){
                notifikasi.className = 'mb-4 p-3 rounded-lg text-sm bg-green-100 text-green-800';
            }else if(jenis === 'gagal'){
                notifikasi.className = 'mb-4 p-3 rounded-lg text-sm bg-red-100 text-red-800';
            }else if(jenis === 'proses'){
                notifikasi.className = 'mb-4 p-3 rounded-lg text-sm bg-yellow-100 text-yellow-800';
            }
        }
    </script>
</body>
</html>
