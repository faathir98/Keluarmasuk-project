```html
<!DOCTYPE html>
<html lang="id" class="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Portir Lapas - Keluar Masuk WBP Asimilasi Rombongan</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        lapas: {
                            50: '#fdf8f6',
                            100: '#f2e8e5',
                            500: '#b91c1c',
                            600: '#991b1b',
                            700: '#7f1d1d',
                            800: '#691b1b',
                            900: '#450a0a',
                        }
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        ::-webkit-scrollbar { width: 6px; height: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 9999px; }
        .dark ::-webkit-scrollbar-thumb { background: #475569; }
    </style>
</head>
<body class="bg-slate-100 dark:bg-slate-900 text-slate-800 dark:text-slate-100 min-h-screen flex flex-col transition-colors duration-200">

    <!-- Top Navigation Bar -->
    <header class="bg-white dark:bg-slate-800 border-b border-slate-200 dark:border-slate-700 sticky top-0 z-30 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="bg-lapas-600 text-white p-2.5 rounded-xl shadow-md flex items-center justify-center">
                    <i class="fa-solid fa-shield-halved text-xl"></i>
                </div>
                <div>
                    <h1 class="text-lg font-bold tracking-tight text-slate-900 dark:text-white leading-tight">PORTIR LAPAS - ASIMILASI ROMBONGAN</h1>
                    <p class="text-xs text-slate-500 dark:text-slate-400">Kontrol Keluar-Masuk WBP Pekerja (Perikanan, Tambak, Peternakan, Sampah)</p>
                </div>
            </div>
            
            <div class="flex items-center space-x-3">
                <div class="hidden md:flex items-center space-x-2 bg-slate-100 dark:bg-slate-700 px-3 py-1.5 rounded-lg text-sm font-medium">
                    <i class="fa-regular fa-clock text-lapas-600 dark:text-lapas-400"></i>
                    <span id="live-clock">--:--:--</span>
                </div>

                <button onclick="toggleDarkMode()" class="p-2 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 transition" title="Ubah Tema">
                    <i id="theme-icon" class="fa-solid fa-moon"></i>
                </button>

                <button onclick="switchTab('alarm')" class="relative p-2 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 transition" title="Peringatan Waktu">
                    <i class="fa-solid fa-bell"></i>
                    <span id="notif-badge" class="absolute top-1 right-1 bg-lapas-600 text-white text-[10px] w-4 h-4 rounded-full flex items-center justify-center font-bold hidden">0</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <div class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 flex flex-col md:flex-row gap-6">

        <!-- Sidebar Navigation -->
        <aside class="w-full md:w-64 shrink-0">
            <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-3 space-y-1">
                <button onclick="switchTab('dashboard')" id="nav-dashboard" class="w-full flex items-center space-x-3 px-4 py-3 rounded-lg text-sm font-medium transition tab-btn active bg-lapas-600 text-white shadow-sm">
                    <i class="fa-solid fa-chart-pie w-5 text-center"></i>
                    <span>Dashboard Utama</span>
                </button>
                <button onclick="switchTab('keluar')" id="nav-keluar" class="w-full flex items-center space-x-3 px-4 py-3 rounded-lg text-sm font-medium text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 transition tab-btn">
                    <i class="fa-solid fa-users-viewfinder w-5 text-center"></i>
                    <span>Keluar Rombongan</span>
                </button>
                <button onclick="switchTab('masuk')" id="nav-masuk" class="w-full flex items-center space-x-3 px-4 py-3 rounded-lg text-sm font-medium text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 transition tab-btn">
                    <i class="fa-solid fa-list-check w-5 text-center"></i>
                    <span>Presensi Masuk (Kembali)</span>
                </button>
                <button onclick="switchTab('warga')" id="nav-warga" class="w-full flex items-center space-x-3 px-4 py-3 rounded-lg text-sm font-medium text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 transition tab-btn">
                    <i class="fa-solid fa-users-between-lines w-5 text-center"></i>
                    <span>Data Master WBP</span>
                </button>
                <button onclick="switchTab('riwayat')" id="nav-riwayat" class="w-full flex items-center space-x-3 px-4 py-3 rounded-lg text-sm font-medium text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 transition tab-btn">
                    <i class="fa-solid fa-clock-rotate-left w-5 text-center"></i>
                    <span>Sesi & Log Rombongan</span>
                </button>
                <button onclick="switchTab('alarm')" id="nav-alarm" class="w-full flex items-center space-x-3 px-4 py-3 rounded-lg text-sm font-medium text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 transition tab-btn justify-between">
                    <div class="flex items-center space-x-3">
                        <i class="fa-solid fa-triangle-exclamation w-5 text-center"></i>
                        <span>Alarm / Keterlambatan</span>
                    </div>
                    <span id="alarm-count-pill" class="bg-amber-100 text-amber-800 dark:bg-amber-900/50 dark:text-amber-300 text-xs px-2 py-0.5 rounded-full font-bold">0</span>
                </button>
            </div>

            <div class="mt-4 bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-4 text-xs space-y-2">
                <div class="font-bold text-slate-900 dark:text-white uppercase tracking-wider flex items-center justify-between">
                    <span>Petugas Regu Jaga</span>
                    <span class="inline-block w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
                </div>
                <div class="text-slate-600 dark:text-slate-400">
                    <p><span class="font-semibold text-slate-700 dark:text-slate-300">Komandan Portir:</span> Bripka H. Kurniawan</p>
                    <p><span class="font-semibold text-slate-700 dark:text-slate-300">Pemeriksa Pintu:</span> Bripda M. Rizky</p>
                </div>
            </div>
        </aside>

        <!-- Dynamic Content Area -->
        <main class="flex-1">

            <!-- TAB 1: DASHBOARD -->
            <section id="tab-dashboard" class="tab-content space-y-6">
                <!-- Welcome Banner -->
                <div class="bg-gradient-to-r from-slate-900 via-slate-800 to-slate-900 text-white rounded-2xl p-6 shadow-md relative overflow-hidden">
                    <div class="absolute right-0 bottom-0 opacity-10 translate-x-4 translate-y-4">
                        <i class="fa-solid fa-fish-fins text-9xl"></i>
                    </div>
                    <div class="relative z-10">
                        <span class="bg-lapas-600 text-white text-xs px-3 py-1 rounded-full font-semibold uppercase tracking-wider">Sistem Portir Asimilasi Massal</span>
                        <h2 class="text-2xl font-bold mt-2">Pencatatan Rombongan Pekerja WBP</h2>
                        <p class="text-slate-300 text-sm mt-1">Dukungan pemilihan massal hingga 20+ warga binaan per kelompok kerja (Perikanan, Tambak, Peternakan, Sampah, dll).</p>
                        
                        <div class="mt-6 flex flex-wrap gap-3">
                            <button onclick="switchTab('keluar')" class="bg-white text-slate-900 hover:bg-slate-100 px-4 py-2 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                                <i class="fa-solid fa-user-plus text-lapas-600"></i>
                                <span>Izin Keluar Rombongan Baru</span>
                            </button>
                            <button onclick="switchTab('masuk')" class="bg-lapas-600 hover:bg-lapas-700 text-white px-4 py-2 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                                <i class="fa-solid fa-list-check"></i>
                                <span>Presensi Kembali (Kelompok)</span>
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Statistics Grid -->
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium text-slate-500 dark:text-slate-400 uppercase tracking-wider">Total WBP Terdata</p>
                            <h3 id="stat-total-wbp" class="text-3xl font-bold text-slate-900 dark:text-white mt-1">0</h3>
                            <span class="text-xs text-slate-500 mt-1 inline-block">WBP Pekerja / Asimilasi</span>
                        </div>
                        <div class="bg-blue-50 dark:bg-blue-900/30 text-blue-600 dark:text-blue-400 p-3.5 rounded-xl text-xl">
                            <i class="fa-solid fa-id-card"></i>
                        </div>
                    </div>

                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium text-slate-500 dark:text-slate-400 uppercase tracking-wider">Sedang di Luar Area</p>
                            <h3 id="stat-sedang-luar" class="text-3xl font-bold text-amber-600 dark:text-amber-400 mt-1">0</h3>
                            <span class="text-xs text-amber-600 dark:text-amber-400 font-medium mt-1 inline-block"><i class="fa-solid fa-person-walking-arrow-right"></i> Bekerja di Luar</span>
                        </div>
                        <div class="bg-amber-50 dark:bg-amber-900/30 text-amber-600 dark:text-amber-400 p-3.5 rounded-xl text-xl">
                            <i class="fa-solid fa-users"></i>
                        </div>
                    </div>

                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium text-slate-500 dark:text-slate-400 uppercase tracking-wider">Di Dalam Lapas</p>
                            <h3 id="stat-dalam-lapas" class="text-3xl font-bold text-emerald-600 dark:text-emerald-400 mt-1">0</h3>
                            <span class="text-xs text-emerald-600 dark:text-emerald-400 font-medium mt-1 inline-block"><i class="fa-solid fa-house-lock"></i> Ada di Kamar/Blok</span>
                        </div>
                        <div class="bg-emerald-50 dark:bg-emerald-900/30 text-emerald-600 dark:text-emerald-400 p-3.5 rounded-xl text-xl">
                            <i class="fa-solid fa-building-user"></i>
                        </div>
                    </div>

                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium text-slate-500 dark:text-slate-400 uppercase tracking-wider">Kegiatan Sesi Aktif</p>
                            <h3 id="stat-sesi-aktif" class="text-3xl font-bold text-lapas-600 dark:text-lapas-500 mt-1">0</h3>
                            <span class="text-xs text-slate-500 mt-1 inline-block">Kelompok Rombongan</span>
                        </div>
                        <div class="bg-red-50 dark:bg-red-900/30 text-lapas-600 dark:text-lapas-500 p-3.5 rounded-xl text-xl">
                            <i class="fa-solid fa-layer-group"></i>
                        </div>
                    </div>
                </div>

                <!-- Session Group Active List -->
                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="flex items-center justify-between mb-4">
                        <h3 class="font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                            <i class="fa-solid fa-list-check text-lapas-600"></i>
                            <span>Daftar Sesi Rombongan Yang Sedang Bertugas / Bekerja</span>
                        </h3>
                        <button onclick="switchTab('riwayat')" class="text-xs text-lapas-600 hover:underline font-semibold">Lihat Semua Sesi Log</button>
                    </div>
                    
                    <div id="dashboard-active-sessions" class="space-y-4">
                        <!-- Populated dynamically -->
                    </div>
                </div>
            </section>

            <!-- TAB 2: FORM KELUAR ROMBONGAN -->
            <section id="tab-keluar" class="tab-content space-y-6 hidden">
                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="border-b border-slate-200 dark:border-slate-700 pb-4 mb-6">
                        <h2 class="text-lg font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                            <i class="fa-solid fa-users-viewfinder text-lapas-600"></i>
                            <span>Form Pengeluaran Rombongan WBP (Multi-Select)</span>
                        </h2>
                        <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Pilih beberapa WBP sekaligus (misal: Rombongan Perikanan 20 Orang) dalam satu sesi pekerjaan.</p>
                    </div>

                    <form id="form-bulk-out" onsubmit="handleBulkCheckout(event)" class="space-y-6">
                        <!-- Group Category & Details -->
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 bg-slate-50 dark:bg-slate-700/40 p-4 rounded-xl border border-slate-200 dark:border-slate-700">
                            <div>
                                <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Jenis Asimilasi / Pekerjaan *</label>
                                <select id="out-category" onchange="toggleCustomCategoryInput()" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                                    <option value="Asimilasi Perikanan">Asimilasi Perikanan</option>
                                    <option value="Asimilasi Peternakan">Asimilasi Peternakan</option>
                                    <option value="Buang Sampah / Kebersihan">Buang Sampah / Kebersihan Lingkungan</option>
                                    <option value="Tambak / Pengolahan Tambak">Tambak / Pengolahan Tambak</option>
                                    <option value="Pertanian / Perkebunan">Pertanian / Perkebunan</option>
                                    <option value="Pertukangan / Konstruksi">Pertukangan / Konstruksi</option>
                                    <option value="Dan / Lain-lain">Dan / Lain-lain (Ketik Sendiri)</option>
                                </select>
                                <input type="text" id="out-custom-category" placeholder="Tuliskan nama kegiatan..." class="w-full mt-2 px-3 py-1.5 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-sm hidden">
                            </div>

                            <div>
                                <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Jam Keluar *</label>
                                <input type="time" id="out-time" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                            </div>

                            <div>
                                <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Batas Jam Kembali *</label>
                                <input type="time" id="out-limit-time" value="16:00" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                            </div>

                            <div class="md:col-span-2">
                                <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Petugas Pengawal / Penanggung Jawab *</label>
                                <input type="text" id="out-officer-escort" placeholder="Contoh: Kasi Kegiatan Kerja / Kasubsi Portir" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                            </div>

                            <div>
                                <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Lokasi Kegiatan</label>
                                <input type="text" id="out-location" placeholder="Kolam Perikanan Lapas / Samping Pintu Utama" class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                            </div>
                        </div>

                        <!-- Multi-Select Inmates Area -->
                        <div class="space-y-3">
                            <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-2">
                                <div>
                                    <h3 class="font-bold text-sm text-slate-900 dark:text-white flex items-center space-x-2">
                                        <i class="fa-solid fa-square-check text-lapas-600"></i>
                                        <span>Pilih Warga Binaan (Tersedia: <span id="out-available-count">0</span> WBP di Lapas)</span>
                                    </h3>
                                    <p class="text-xs text-slate-500">Centang WBP yang akan dikeluarkan hari ini.</p>
                                </div>
                                <div class="flex items-center space-x-2">
                                    <button type="button" onclick="filterOutWbpCategory('ALL')" class="px-2.5 py-1 text-xs rounded bg-slate-200 dark:bg-slate-700 hover:bg-slate-300">Semua</button>
                                    <button type="button" onclick="selectAllAvailableOutWbp(true)" class="px-2.5 py-1 text-xs rounded bg-blue-100 text-blue-700 dark:bg-blue-900/50 dark:text-blue-300 font-medium">Centang Semua</button>
                                    <button type="button" onclick="selectAllAvailableOutWbp(false)" class="px-2.5 py-1 text-xs rounded bg-slate-200 text-slate-700 dark:bg-slate-700 dark:text-slate-300">Kosongkan</button>
                                </div>
                            </div>

                            <!-- Search bar for inmate list -->
                            <input type="text" id="out-wbp-filter" onkeyup="renderOutWbpSelectionList()" placeholder="Ketik nama atau No. Registrasi untuk menyaring..." class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">

                            <!-- Checkbox Grid Container -->
                            <div id="out-wbp-checkbox-grid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-3 max-h-80 overflow-y-auto p-3 bg-slate-50 dark:bg-slate-900/40 rounded-xl border border-slate-200 dark:border-slate-700">
                                <!-- Populated dynamically -->
                            </div>
                            
                            <div class="text-xs text-slate-600 dark:text-slate-400 font-semibold flex items-center justify-between">
                                <span>Terpilih: <strong id="out-selected-count" class="text-lapas-600 dark:text-lapas-400 text-sm">0</strong> WBP</span>
                                <span>Total Kapasitas Rombongan: Tidak terbatas</span>
                            </div>
                        </div>

                        <!-- Submit Button -->
                        <div class="flex justify-end space-x-3 pt-4 border-t border-slate-200 dark:border-slate-700">
                            <button type="submit" class="bg-lapas-600 hover:bg-lapas-700 text-white px-6 py-2.5 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                                <i class="fa-solid fa-receipt"></i>
                                <span>Proses Sesi Keluar & Cetak Surat Jalan Rombongan</span>
                            </button>
                        </div>
                    </form>
                </div>
            </section>

            <!-- TAB 3: FORM PRESENSI MASUK (KEMBALI) -->
            <section id="tab-masuk" class="tab-content space-y-6 hidden">
                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="border-b border-slate-200 dark:border-slate-700 pb-4 mb-6">
                        <h2 class="text-lg font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                            <i class="fa-solid fa-list-check text-lapas-600"></i>
                            <span>Presensi Masuk & Penggeledahan Rombongan</span>
                        </h2>
                        <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Lakukan pemanggilan & centang WBP yang sudah kembali ke area portir.</p>
                    </div>

                    <!-- Select Active Session -->
                    <div class="space-y-5">
                        <div>
                            <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Pilih Sesi Rombongan Aktif *</label>
                            <select id="in-session-select" onchange="loadSessionForCheckin()" class="w-full px-3.5 py-2.5 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                                <option value="">-- Pilih Sesi Rombongan Yang Sedang Bekerja --</option>
                            </select>
                        </div>

                        <!-- Active Session Details & Checklist Area -->
                        <div id="in-session-detail-container" class="hidden space-y-5">
                            <div class="bg-slate-50 dark:bg-slate-700/50 p-4 rounded-xl border border-slate-200 dark:border-slate-700 grid grid-cols-2 md:grid-cols-4 gap-4 text-xs">
                                <div>
                                    <span class="block text-slate-500">Kategori Pekerjaan</span>
                                    <span id="in-session-category" class="font-bold text-slate-900 dark:text-white text-sm">-</span>
                                </div>
                                <div>
                                    <span class="block text-slate-500">Jam Keluar / Batas</span>
                                    <span id="in-session-times" class="font-bold text-slate-900 dark:text-white text-sm">-</span>
                                </div>
                                <div>
                                    <span class="block text-slate-500">Pengawal / PIC</span>
                                    <span id="in-session-officer" class="font-bold text-slate-900 dark:text-white text-sm">-</span>
                                </div>
                                <div>
                                    <span class="block text-slate-500">Status Waktu Saat Ini</span>
                                    <span id="in-session-status-badge" class="inline-block mt-0.5">-</span>
                                </div>
                            </div>

                            <form id="form-bulk-in" onsubmit="handleBulkCheckin(event)" class="space-y-4">
                                <div class="flex items-center justify-between">
                                    <h3 class="font-bold text-sm text-slate-900 dark:text-white">Daftar Anggota Rombongan (Centang Yang Sudah Kembali)</h3>
                                    <div class="space-x-2">
                                        <button type="button" onclick="toggleAllCheckinWbp(true)" class="text-xs bg-emerald-100 text-emerald-800 dark:bg-emerald-900/50 dark:text-emerald-300 px-2.5 py-1 rounded font-semibold">Tandai Semua Kembali</button>
                                        <button type="button" onclick="toggleAllCheckinWbp(false)" class="text-xs bg-slate-200 text-slate-700 dark:bg-slate-700 dark:text-slate-300 px-2.5 py-1 rounded">Batal Semua</button>
                                    </div>
                                </div>

                                <div id="in-wbp-checklist-grid" class="grid grid-cols-1 md:grid-cols-2 gap-3 max-h-80 overflow-y-auto p-3 bg-slate-50 dark:bg-slate-900/40 rounded-xl border border-slate-200 dark:border-slate-700">
                                    <!-- Dynamic inmates checklist -->
                                </div>

                                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 pt-2">
                                    <div>
                                        <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Jam Kembali Riil *</label>
                                        <input type="time" id="in-actual-time" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                                    </div>
                                    <div>
                                        <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Hasil Penggeledahan Pintu *</label>
                                        <select id="in-search-result" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                                            <option value="Aman / Nihil Temuan">Aman / Nihil Temuan Barang Terlarang</option>
                                            <option value="Temuan Barang Dilarang">Ada Temuan Dilarang (Lapor KPLP)</option>
                                            <option value="Catatan Kesehatan/Fisik">Catatan Kesehatan / Pengobatan (Lapor Klinik)</option>
                                        </select>
                                    </div>
                                    <div>
                                        <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Petugas Verifikator Portir *</label>
                                        <input type="text" id="in-officer-name" value="Bripka H. Kurniawan (Portir Utama)" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-slate-100 dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">
                                    </div>
                                </div>

                                <div>
                                    <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Catatan Tambahan Penggeledahan</label>
                                    <input type="text" id="in-notes" placeholder="Contoh: Seluruh WBP diperiksa badan dan peralatan kerja tambak/perikanan diserah-terimakan lengkap." class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">
                                </div>

                                <div class="flex justify-end space-x-3 pt-4 border-t border-slate-200 dark:border-slate-700">
                                    <button type="submit" class="bg-emerald-600 hover:bg-emerald-700 text-white px-6 py-2.5 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                                        <i class="fa-solid fa-clipboard-check"></i>
                                        <span>Simpan Presensi Masuk & Tutup Sesi Jika Lengkap</span>
                                    </button>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </section>

            <!-- TAB 4: DATA MASTER WBP -->
            <section id="tab-warga" class="tab-content space-y-6 hidden">
                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 border-b border-slate-200 dark:border-slate-700 pb-4 mb-6">
                        <div>
                            <h2 class="text-lg font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                                <i class="fa-solid fa-users-between-lines text-lapas-600"></i>
                                <span>Master Data WBP Asimilasi / Pekerja Lapas</span>
                            </h2>
                            <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Daftar warga binaan yang terdaftar pada program kerja & asimilasi.</p>
                        </div>
                        <button onclick="openAddWbpModal()" class="bg-lapas-600 hover:bg-lapas-700 text-white px-4 py-2 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                            <i class="fa-solid fa-user-plus"></i>
                            <span>Tambah WBP Pekerja</span>
                        </button>
                    </div>

                    <!-- Filters -->
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-3 mb-4">
                        <input type="text" id="wbp-search" onkeyup="renderWbpTable()" placeholder="Cari nama atau No. Reg..." class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">
                        <select id="wbp-filter-cat" onchange="renderWbpTable()" class="px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">
                            <option value="">Semua Kategori Asimilasi</option>
                            <option value="Asimilasi Perikanan">Asimilasi Perikanan</option>
                            <option value="Asimilasi Peternakan">Asimilasi Peternakan</option>
                            <option value="Buang Sampah / Kebersihan">Buang Sampah / Kebersihan</option>
                            <option value="Tambak / Pengolahan Tambak">Tambak / Pengolahan Tambak</option>
                            <option value="Pertanian / Perkebunan">Pertanian / Perkebunan</option>
                        </select>
                        <select id="wbp-filter-status" onchange="renderWbpTable()" class="px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">
                            <option value="">Semua Lokasi Status</option>
                            <option value="Di Lapas">Di Lapas</option>
                            <option value="Di Luar">Di Luar Lapas</option>
                        </select>
                    </div>

                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-sm">
                            <thead class="bg-slate-50 dark:bg-slate-700 text-slate-600 dark:text-slate-300 text-xs uppercase tracking-wider">
                                <tr>
                                    <th class="p-3 rounded-l-lg">No. Reg / ID</th>
                                    <th class="p-3">Nama Lengkap / Alias</th>
                                    <th class="p-3">Blok Kamar</th>
                                    <th class="p-3">Kategori Pekerjaan Utama</th>
                                    <th class="p-3">Status Lokasi</th>
                                    <th class="p-3 text-right rounded-r-lg">Aksi</th>
                                </tr>
                            </thead>
                            <tbody id="wbp-table-tbody" class="divide-y divide-slate-100 dark:divide-slate-700">
                                <!-- Populated dynamically -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- TAB 5: SESI & LOG ROMBONGAN -->
            <section id="tab-riwayat" class="tab-content space-y-6 hidden">
                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 border-b border-slate-200 dark:border-slate-700 pb-4 mb-6">
                        <div>
                            <h2 class="text-lg font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                                <i class="fa-solid fa-clock-rotate-left text-lapas-600"></i>
                                <span>Riwayat Sesi Keluar Masuk Rombongan</span>
                            </h2>
                            <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Daftar arsip seluruh kelompok pekerjaan yang pernah keluar-masuk portir.</p>
                        </div>
                        <button onclick="exportLogCSV()" class="bg-slate-800 hover:bg-slate-700 text-white px-4 py-2 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                            <i class="fa-solid fa-file-csv"></i>
                            <span>Export Laporan CSV</span>
                        </button>
                    </div>

                    <div id="session-log-list-container" class="space-y-4">
                        <!-- Populated dynamically -->
                    </div>
                </div>
            </section>

            <!-- TAB 6: ALARM / KETERLAMBATAN -->
            <section id="tab-alarm" class="tab-content space-y-6 hidden">
                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="border-b border-slate-200 dark:border-slate-700 pb-4 mb-6">
                        <h2 class="text-lg font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                            <i class="fa-solid fa-triangle-exclamation text-lapas-600"></i>
                            <span>Peringatan Waktu & Keterlambatan WBP</span>
                        </h2>
                        <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Sesi rombongan atau anggota WBP yang telah melewati batas jam kembali.</p>
                    </div>

                    <div id="alarm-container" class="space-y-4">
                        <!-- Populated dynamically -->
                    </div>
                </div>
            </section>

        </main>
    </div>

    <!-- MODAL: SURAT JALAN ROMBONGAN -->
    <div id="modal-receipt" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4 hidden">
        <div class="bg-white dark:bg-slate-800 rounded-2xl max-w-lg w-full p-6 shadow-2xl border border-slate-200 dark:border-slate-700 space-y-4">
            <div class="text-center pb-3 border-b border-dashed border-slate-300 dark:border-slate-700">
                <div class="inline-block bg-lapas-600 text-white p-3 rounded-full mb-2">
                    <i class="fa-solid fa-stamp text-2xl"></i>
                </div>
                <h3 class="font-bold text-base text-slate-900 dark:text-white">SURAT JALAN ROMBONGAN ASIMILASI</h3>
                <p class="text-xs text-slate-500">Pos Pengamanan Utama Portir Lapas</p>
            </div>

            <div id="receipt-content" class="text-xs space-y-3 text-slate-700 dark:text-slate-300">
                <!-- Dynamically filled -->
            </div>

            <div class="flex space-x-3 pt-3 border-t border-slate-200 dark:border-slate-700">
                <button onclick="closeReceiptModal()" class="flex-1 bg-slate-200 dark:bg-slate-700 text-slate-800 dark:text-white py-2 rounded-lg font-semibold text-sm">Tutup</button>
                <button onclick="window.print()" class="flex-1 bg-lapas-600 text-white py-2 rounded-lg font-semibold text-sm flex items-center justify-center space-x-2">
                    <i class="fa-solid fa-print"></i>
                    <span>Cetak Surat Jalan</span>
                </button>
            </div>
        </div>
    </div>

    <!-- MODAL: ADD WBP -->
    <div id="modal-wbp" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4 hidden">
        <div class="bg-white dark:bg-slate-800 rounded-2xl max-w-md w-full p-6 shadow-2xl border border-slate-200 dark:border-slate-700">
            <div class="flex items-center justify-between pb-3 border-b border-slate-200 dark:border-slate-700 mb-4">
                <h3 class="font-bold text-slate-900 dark:text-white">Tambah WBP Pekerja Baru</h3>
                <button onclick="closeModalWbp()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>

            <form onsubmit="saveWbpData(event)" class="space-y-4 text-xs">
                <div>
                    <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">No. Registrasi / ID *</label>
                    <input type="text" id="new-wbp-id" placeholder="REG-PERI-021" required class="w-full px-3 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white">
                </div>
                <div>
                    <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">Nama Lengkap WBP *</label>
                    <input type="text" id="new-wbp-name" placeholder="Rahmat Hidayat" required class="w-full px-3 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white">
                </div>
                <div>
                    <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">Bin / Alias</label>
                    <input type="text" id="new-wbp-alias" placeholder="Bin Amir" class="w-full px-3 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white">
                </div>
                <div>
                    <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">Blok Kamar</label>
                    <input type="text" id="new-wbp-block" placeholder="Blok C (Asimilasi)" required class="w-full px-3 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white">
                </div>
                <div>
                    <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">Kategori Pekerjaan Utama *</label>
                    <select id="new-wbp-category" required class="w-full px-3 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white">
                        <option value="Asimilasi Perikanan">Asimilasi Perikanan</option>
                        <option value="Asimilasi Peternakan">Asimilasi Peternakan</option>
                        <option value="Buang Sampah / Kebersihan">Buang Sampah / Kebersihan</option>
                        <option value="Tambak / Pengolahan Tambak">Tambak / Pengolahan Tambak</option>
                        <option value="Pertanian / Perkebunan">Pertanian / Perkebunan</option>
                        <option value="Pertukangan / Konstruksi">Pertukangan / Konstruksi</option>
                    </select>
                </div>

                <div class="flex justify-end space-x-2 pt-3">
                    <button type="button" onclick="closeModalWbp()" class="px-4 py-2 rounded-lg bg-slate-200 text-slate-800">Batal</button>
                    <button type="submit" class="px-4 py-2 rounded-lg bg-lapas-600 text-white font-semibold">Simpan Data WBP</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col space-y-2 pointer-events-none"></div>

    <script>
        // --- INITIAL DATA SEED (20+ Inmates across categories) ---
        let wbpList = [
            // Perikanan Batch
            { id: 'REG-FISH-01', name: 'Budi Santoso', alias: 'Bin Slamet', block: 'Blok C (Asimilasi)', defaultCategory: 'Asimilasi Perikanan', status: 'Di Lapas' },
            { id: 'REG-FISH-02', name: 'Agus Prayitno', alias: 'Bin Dahlan', block: 'Blok C (Asimilasi)', defaultCategory: 'Asimilasi Perikanan', status: 'Di Lapas' },
            { id: 'REG-FISH-03', name: 'Suharto', alias: 'Bin Mulyono', block: 'Blok C (Asimilasi)', defaultCategory: 'Asimilasi Perikanan', status: 'Di Lapas' },
            { id: 'REG-FISH-04', name: 'Heri Gunawan', alias: 'Bin Kasan', block: 'Blok C (Asimilasi)', defaultCategory: 'Asimilasi Perikanan', status: 'Di Lapas' },
            { id: 'REG-FISH-05', name: 'Bambang Irawan', alias: 'Bin Karto', block: 'Blok C (Asimilasi)', defaultCategory: 'Asimilasi Perikanan', status: 'Di Lapas' },
            { id: 'REG-FISH-06', name: 'Rudi Hartono', alias: 'Bin Taufik', block: 'Blok C (Asimilasi)', defaultCategory: 'Asimilasi Perikanan', status: 'Di Lapas' },
            { id: 'REG-FISH-07', name: 'Ahmad Supardi', alias: 'Bin Yasin', block: 'Blok C (Asimilasi)', defaultCategory: 'Asimilasi Perikanan', status: 'Di Lapas' },
            { id: 'REG-FISH-08', name: 'Dedi Kurniawan', alias: 'Bin Aris', block: 'Blok C (Asimilasi)', defaultCategory: 'Asimilasi Perikanan', status: 'Di Lapas' },
            
            // Tambak Batch
            { id: 'REG-TMBK-01', name: 'Samsul Bahri', alias: 'Bin Usman', block: 'Blok D (Wisma Tambak)', defaultCategory: 'Tambak / Pengolahan Tambak', status: 'Di Lapas' },
            { id: 'REG-TMBK-02', name: 'Eko Prasetyo', alias: 'Bin Darmo', block: 'Blok D (Wisma Tambak)', defaultCategory: 'Tambak / Pengolahan Tambak', status: 'Di Lapas' },
            { id: 'REG-TMBK-03', name: 'Hendra Sucipto', alias: 'Bin Nurdin', block: 'Blok D (Wisma Tambak)', defaultCategory: 'Tambak / Pengolahan Tambak', status: 'Di Lapas' },
            { id: 'REG-TMBK-04', name: 'M. Ridwan', alias: 'Bin Fadhil', block: 'Blok D (Wisma Tambak)', defaultCategory: 'Tambak / Pengolahan Tambak', status: 'Di Lapas' },
            { id: 'REG-TMBK-05', name: 'Zulkifli', alias: 'Bin Ibrahim', block: 'Blok D (Wisma Tambak)', defaultCategory: 'Tambak / Pengolahan Tambak', status: 'Di Lapas' },

            // Peternakan Batch
            { id: 'REG-TRNK-01', name: 'Toni Wijaya', alias: 'Bin Syamsudin', block: 'Blok C (Asimilasi)', defaultCategory: 'Asimilasi Peternakan', status: 'Di Lapas' },
            { id: 'REG-TRNK-02', name: 'Nur Hidayat', alias: 'Bin Badri', block: 'Blok C (Asimilasi)', defaultCategory: 'Asimilasi Peternakan', status: 'Di Lapas' },
            { id: 'REG-TRNK-03', name: 'Aris Munandar', alias: 'Bin Sukri', block: 'Blok C (Asimilasi)', defaultCategory: 'Asimilasi Peternakan', status: 'Di Lapas' },

            // Sampah / Kebersihan Batch
            { id: 'REG-SMPH-01', name: 'Joko Susilo', alias: 'Bin Sutrisno', block: 'Blok A (Kebersihan)', defaultCategory: 'Buang Sampah / Kebersihan', status: 'Di Lapas' },
            { id: 'REG-SMPH-02', name: 'Andi Saputra', alias: 'Bin Basri', block: 'Blok A (Kebersihan)', defaultCategory: 'Buang Sampah / Kebersihan', status: 'Di Lapas' },
            { id: 'REG-SMPH-03', name: 'Fajar Hamzah', alias: 'Bin Latif', block: 'Blok A (Kebersihan)', defaultCategory: 'Buang Sampah / Kebersihan', status: 'Di Lapas' },
            { id: 'REG-SMPH-04', name: 'Suhardi', alias: 'Bin Kasiran', block: 'Blok A (Kebersihan)', defaultCategory: 'Buang Sampah / Kebersihan', status: 'Di Lapas' }
        ];

        // Group Session Logs
        let sessionLogs = [
            {
                sessionId: 'SESI-FISH-001',
                category: 'Asimilasi Perikanan',
                outTime: '07:30',
                limitTime: '16:00',
                actualInTime: '-',
                officerEscort: 'Kasi Kegiatan Kerja & Staf',
                location: 'Tambak & Kolam Perikanan Sektor Luar Lapas',
                date: new Date().toISOString().split('T')[0],
                status: 'Aktif / Di Luar',
                members: [
                    { wbpId: 'REG-FISH-01', name: 'Budi Santoso', returned: false, returnTime: '-', searchResult: '-' },
                    { wbpId: 'REG-FISH-02', name: 'Agus Prayitno', returned: false, returnTime: '-', searchResult: '-' },
                    { wbpId: 'REG-FISH-03', name: 'Suharto', returned: false, returnTime: '-', searchResult: '-' },
                    { wbpId: 'REG-FISH-04', name: 'Heri Gunawan', returned: false, returnTime: '-', searchResult: '-' }
                ]
            }
        ];

        // Sync initial statuses
        sessionLogs.forEach(s => {
            if(s.status === 'Aktif / Di Luar') {
                s.members.forEach(m => {
                    const found = wbpList.find(w => w.id === m.wbpId);
                    if(found && !m.returned) found.status = 'Di Luar';
                });
            }
        });

        // --- CLOCK & TIMERS ---
        function updateClock() {
            const now = new Date();
            document.getElementById('live-clock').innerText = now.toTimeString().split(' ')[0];
            checkAlarms();
        }
        setInterval(updateClock, 1000);

        function toggleDarkMode() {
            const html = document.documentElement;
            const icon = document.getElementById('theme-icon');
            if (html.classList.contains('dark')) {
                html.classList.remove('dark');
                icon.className = 'fa-solid fa-moon';
            } else {
                html.classList.add('dark');
                icon.className = 'fa-solid fa-sun';
            }
        }

        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.tab-btn').forEach(el => {
                el.classList.remove('bg-lapas-600', 'text-white', 'shadow-sm');
                el.classList.add('text-slate-600', 'dark:text-slate-300', 'hover:bg-slate-100', 'dark:hover:bg-slate-700');
            });

            document.getElementById(`tab-${tabId}`).classList.remove('hidden');
            const activeBtn = document.getElementById(`nav-${tabId}`);
            if (activeBtn) {
                activeBtn.classList.remove('text-slate-600', 'dark:text-slate-300', 'hover:bg-slate-100', 'dark:hover:bg-slate-700');
                activeBtn.classList.add('bg-lapas-600', 'text-white', 'shadow-sm');
            }

            if (tabId === 'dashboard') renderDashboard();
            if (tabId === 'keluar') renderOutWbpSelectionList();
            if (tabId === 'masuk') populateCheckinSessions();
            if (tabId === 'warga') renderWbpTable();
            if (tabId === 'riwayat') renderSessionLogs();
            if (tabId === 'alarm') renderAlarmList();
        }

        window.onload = function() {
            const nowTime = new Date().toTimeString().substring(0, 5);
            if(document.getElementById('out-time')) document.getElementById('out-time').value = nowTime;
            if(document.getElementById('in-actual-time')) document.getElementById('in-actual-time').value = nowTime;
            
            renderDashboard();
            renderOutWbpSelectionList();
        };

        // --- DASHBOARD LOGIC ---
        function renderDashboard() {
            const totalWbp = wbpList.length;
            const sedangLuar = wbpList.filter(w => w.status === 'Di Luar').length;
            const dalamLapas = wbpList.filter(w => w.status === 'Di Lapas').length;
            const sesiAktif = sessionLogs.filter(s => s.status === 'Aktif / Di Luar').length;

            document.getElementById('stat-total-wbp').innerText = totalWbp;
            document.getElementById('stat-sedang-luar').innerText = sedangLuar;
            document.getElementById('stat-dalam-lapas').innerText = dalamLapas;
            document.getElementById('stat-sesi-aktif').innerText = sesiAktif;

            const activeContainer = document.getElementById('dashboard-active-sessions');
            const activeSessions = sessionLogs.filter(s => s.status === 'Aktif / Di Luar');

            if(activeSessions.length === 0) {
                activeContainer.innerHTML = `<div class="p-8 text-center text-slate-400 bg-slate-50 dark:bg-slate-700/30 rounded-xl">Tidak ada rombongan WBP yang sedang bertugas di luar saat ini.</div>`;
                return;
            }

            activeContainer.innerHTML = activeSessions.map(s => {
                const returnedCount = s.members.filter(m => m.returned).length;
                const totalMembers = s.members.length;

                return `
                    <div class="p-4 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-700/30 flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                        <div>
                            <div class="flex items-center space-x-2">
                                <span class="bg-lapas-600 text-white font-bold text-xs px-2.5 py-0.5 rounded-full">${s.category}</span>
                                <span class="text-xs text-slate-500 font-mono">${s.sessionId}</span>
                            </div>
                            <h4 class="font-bold text-slate-900 dark:text-white mt-1">Pengawal: ${s.officerEscort}</h4>
                            <p class="text-xs text-slate-500">Lokasi: ${s.location} | Jam Keluar: ${s.outTime} | Batas Kembali: <strong class="text-lapas-600 dark:text-lapas-400">${s.limitTime}</strong></p>
                        </div>

                        <div class="flex items-center space-x-4 w-full md:w-auto justify-between md:justify-end">
                            <div class="text-right">
                                <span class="block text-xs text-slate-500">Anggota Rombongan</span>
                                <span class="font-bold text-sm text-slate-900 dark:text-white">${returnedCount} / ${totalMembers} Kembali</span>
                            </div>
                            <button onclick="quickPresensiSession('${s.sessionId}')" class="bg-emerald-600 hover:bg-emerald-700 text-white px-3.5 py-2 rounded-lg text-xs font-semibold">Presensi Masuk</button>
                        </div>
                    </div>
                `;
            }).join('');
        }

        // --- BULK CHECKOUT SELECTION ---
        function toggleCustomCategoryInput() {
            const cat = document.getElementById('out-category').value;
            const customInput = document.getElementById('out-custom-category');
            if(cat === 'Dan / Lain-lain') {
                customInput.classList.remove('hidden');
                customInput.required = true;
            } else {
                customInput.classList.add('hidden');
                customInput.required = false;
            }
            renderOutWbpSelectionList();
        }

        function renderOutWbpSelectionList() {
            const filterText = document.getElementById('out-wbp-filter').value.toLowerCase();
            const categorySelect = document.getElementById('out-category').value;
            const grid = document.getElementById('out-wbp-checkbox-grid');

            const availableWbp = wbpList.filter(w => w.status === 'Di Lapas');
            document.getElementById('out-available-count').innerText = availableWbp.length;

            const filtered = availableWbp.filter(w => {
                const matchSearch = w.name.toLowerCase().includes(filterText) || w.id.toLowerCase().includes(filterText);
                return matchSearch;
            });

            if(filtered.length === 0) {
                grid.innerHTML = `<div class="col-span-full p-6 text-center text-slate-400">Tidak ada WBP yang tersedia untuk dipilih di dalam lapas.</div>`;
                return;
            }

            grid.innerHTML = filtered.map(w => {
                return `
                    <label class="flex items-start space-x-3 p-2.5 rounded-lg border border-slate-200 dark:border-slate-700 bg-white dark:bg-slate-800 hover:bg-slate-100 dark:hover:bg-slate-700 cursor-pointer transition">
                        <input type="checkbox" name="selected-out-wbp" value="${w.id}" onchange="updateOutSelectedCount()" class="w-4 h-4 mt-0.5 rounded text-lapas-600 focus:ring-lapas-600">
                        <div class="text-xs">
                            <span class="font-bold block text-slate-900 dark:text-white">${w.name}</span>
                            <span class="text-slate-500 font-mono block">${w.id} • ${w.block}</span>
                            <span class="inline-block mt-1 text-[10px] bg-slate-100 dark:bg-slate-700 text-slate-600 dark:text-slate-300 px-1.5 py-0.5 rounded">${w.defaultCategory}</span>
                        </div>
                    </label>
                `;
            }).join('');

            updateOutSelectedCount();
        }

        function updateOutSelectedCount() {
            const selected = document.querySelectorAll('input[name="selected-out-wbp"]:checked');
            document.getElementById('out-selected-count').innerText = selected.length;
        }

        function selectAllAvailableOutWbp(status) {
            const checkboxes = document.querySelectorAll('input[name="selected-out-wbp"]');
            checkboxes.forEach(cb => cb.checked = status);
            updateOutSelectedCount();
        }

        function handleBulkCheckout(event) {
            event.preventDefault();
            const selectedCheckboxes = document.querySelectorAll('input[name="selected-out-wbp"]:checked');
            
            if(selectedCheckboxes.length === 0) {
                showToast('Pilih setidaknya 1 WBP untuk rombongan!', 'error');
                return;
            }

            let category = document.getElementById('out-category').value;
            if(category === 'Dan / Lain-lain') {
                category = document.getElementById('out-custom-category').value || 'Lain-lain';
            }

            const outTime = document.getElementById('out-time').value;
            const limitTime = document.getElementById('out-limit-time').value;
            const officer = document.getElementById('out-officer-escort').value;
            const location = document.getElementById('out-location').value || 'Lingkungan Luar Lapas';

            const selectedIds = Array.from(selectedCheckboxes).map(cb => cb.value);

            // Create new group session
            const newSession = {
                sessionId: 'SESI-' + Math.floor(1000 + Math.random() * 9000),
                category: category,
                outTime: outTime,
                limitTime: limitTime,
                actualInTime: '-',
                officerEscort: officer,
                location: location,
                date: new Date().toISOString().split('T')[0],
                status: 'Aktif / Di Luar',
                members: selectedIds.map(id => {
                    const wbp = wbpList.find(w => w.id === id);
                    wbp.status = 'Di Luar'; // update WBP master state
                    return { wbpId: wbp.id, name: wbp.name, returned: false, returnTime: '-', searchResult: '-' };
                })
            };

            sessionLogs.unshift(newSession);

            showToast(`Sesi Rombongan (${selectedIds.length} WBP) berhasil dibuat & dikeluarkan!`, 'success');
            showGroupReceiptModal(newSession);
            renderOutWbpSelectionList();
            renderDashboard();
        }

        // --- BULK CHECKIN LOGIC ---
        function populateCheckinSessions() {
            const select = document.getElementById('in-session-select');
            const activeSessions = sessionLogs.filter(s => s.status === 'Aktif / Di Luar');

            select.innerHTML = `<option value="">-- Pilih Sesi Rombongan Yang Sedang Bekerja --</option>` +
                activeSessions.map(s => `<option value="${s.sessionId}">${s.sessionId} - ${s.category} (${s.members.length} WBP) - Keluar: ${s.outTime}</option>`).join('');

            document.getElementById('in-session-detail-container').classList.add('hidden');
        }

        function quickPresensiSession(sessionId) {
            switchTab('masuk');
            const select = document.getElementById('in-session-select');
            select.value = sessionId;
            loadSessionForCheckin();
        }

        function loadSessionForCheckin() {
            const sessionId = document.getElementById('in-session-select').value;
            const container = document.getElementById('in-session-detail-container');

            if(!sessionId) {
                container.classList.add('hidden');
                return;
            }

            const session = sessionLogs.find(s => s.sessionId === sessionId);
            if(!session) return;

            document.getElementById('in-session-category').innerText = session.category;
            document.getElementById('in-session-times').innerText = `${session.outTime} WIB (Batas: ${session.limitTime} WIB)`;
            document.getElementById('in-session-officer').innerText = session.officerEscort;

            const nowStr = new Date().toTimeString().substring(0, 5);
            const isLate = nowStr > session.limitTime;
            document.getElementById('in-session-status-badge').innerHTML = isLate 
                ? `<span class="bg-red-100 text-lapas-600 px-2 py-0.5 rounded font-bold">TERLAMBAT</span>`
                : `<span class="bg-emerald-100 text-emerald-800 px-2 py-0.5 rounded font-bold">DALAM JADWAL</span>`;

            // Render WBP Checklist
            const grid = document.getElementById('in-wbp-checklist-grid');
            grid.innerHTML = session.members.map(m => {
                const wbp = wbpList.find(w => w.id === m.wbpId);
                const isChecked = m.returned ? 'checked disabled' : '';
                const bgStyle = m.returned ? 'bg-slate-100 dark:bg-slate-800 opacity-60' : 'bg-white dark:bg-slate-800';

                return `
                    <label class="flex items-center justify-between p-3 rounded-lg border border-slate-200 dark:border-slate-700 ${bgStyle}">
                        <div class="flex items-center space-x-3">
                            <input type="checkbox" name="in-wbp-check" value="${m.wbpId}" ${isChecked} class="w-4 h-4 rounded text-emerald-600 focus:ring-emerald-500">
                            <div>
                                <span class="font-bold text-xs block text-slate-900 dark:text-white">${m.name}</span>
                                <span class="text-[11px] text-slate-500 font-mono">${m.wbpId}</span>
                            </div>
                        </div>
                        <div>
                            ${m.returned ? `<span class="text-[10px] bg-emerald-100 text-emerald-800 px-2 py-0.5 rounded font-semibold">Sudah Kembali (${m.returnTime})</span>` : `<span class="text-[10px] bg-amber-100 text-amber-800 px-2 py-0.5 rounded font-semibold">Belum Kembali</span>`}
                        </div>
                    </label>
                `;
            }).join('');

            container.classList.remove('hidden');
        }

        function toggleAllCheckinWbp(status) {
            const checkboxes = document.querySelectorAll('input[name="in-wbp-check"]:not([disabled])');
            checkboxes.forEach(cb => cb.checked = status);
        }

        function handleBulkCheckin(event) {
            event.preventDefault();
            const sessionId = document.getElementById('in-session-select').value;
            const session = sessionLogs.find(s => s.sessionId === sessionId);
            if(!session) return;

            const selectedCbs = document.querySelectorAll('input[name="in-wbp-check"]:checked:not([disabled])');
            if(selectedCbs.length === 0) {
                showToast('Pilih setidaknya 1 WBP yang kembali!', 'error');
                return;
            }

            const actualTime = document.getElementById('in-actual-time').value;
            const searchResult = document.getElementById('in-search-result').value;
            const notes = document.getElementById('in-notes').value;

            const returnedIds = Array.from(selectedCbs).map(cb => cb.value);

            // Update member statuses in session
            returnedIds.forEach(id => {
                const member = session.members.find(m => m.wbpId === id);
                if(member) {
                    member.returned = true;
                    member.returnTime = actualTime;
                    member.searchResult = searchResult;
                }
                const wbp = wbpList.find(w => w.id === id);
                if(wbp) wbp.status = 'Di Lapas';
            });

            // Check if all members returned to close session
            const allReturned = session.members.every(m => m.returned);
            if(allReturned) {
                session.status = 'Selesai / Lengkap';
                session.actualInTime = actualTime;
            }

            showToast(`Presensi masuk untuk ${returnedIds.length} WBP telah dicatat!`, 'success');
            populateCheckinSessions();
            renderDashboard();
        }

        // --- MASTER WBP TABLE ---
        function renderWbpTable() {
            const search = document.getElementById('wbp-search').value.toLowerCase();
            const catFilter = document.getElementById('wbp-filter-cat').value;
            const statusFilter = document.getElementById('wbp-filter-status').value;
            const tbody = document.getElementById('wbp-table-tbody');

            const filtered = wbpList.filter(w => {
                const matchSearch = w.name.toLowerCase().includes(search) || w.id.toLowerCase().includes(search);
                const matchCat = catFilter === '' || w.defaultCategory === catFilter;
                const matchStatus = statusFilter === '' || w.status === statusFilter;
                return matchSearch && matchCat && matchStatus;
            });

            if(filtered.length === 0) {
                tbody.innerHTML = `<tr><td colspan="6" class="p-6 text-center text-slate-400">Tidak ada WBP yang cocok dengan filter.</td></tr>`;
                return;
            }

            tbody.innerHTML = filtered.map(w => {
                const badge = w.status === 'Di Lapas'
                    ? `<span class="px-2 py-0.5 rounded text-xs font-semibold bg-emerald-100 text-emerald-800">Di Lapas</span>`
                    : `<span class="px-2 py-0.5 rounded text-xs font-semibold bg-amber-100 text-amber-800">Di Luar Lapas</span>`;

                return `
                    <tr class="hover:bg-slate-50 dark:hover:bg-slate-700/50">
                        <td class="p-3 font-mono font-bold text-slate-900 dark:text-white">${w.id}</td>
                        <td class="p-3">
                            <span class="font-bold block text-slate-900 dark:text-white">${w.name}</span>
                            <span class="text-xs text-slate-500">${w.alias}</span>
                        </td>
                        <td class="p-3 text-slate-600 dark:text-slate-300">${w.block}</td>
                        <td class="p-3 text-slate-700 dark:text-slate-300">${w.defaultCategory}</td>
                        <td class="p-3">${badge}</td>
                        <td class="p-3 text-right">
                            <button onclick="deleteWbp('${w.id}')" class="text-xs text-red-600 hover:underline">Hapus</button>
                        </td>
                    </tr>
                `;
            }).join('');
        }

        function openAddWbpModal() { document.getElementById('modal-wbp').classList.remove('hidden'); }
        function closeModalWbp() { document.getElementById('modal-wbp').classList.add('hidden'); }

        function saveWbpData(event) {
            event.preventDefault();
            const id = document.getElementById('new-wbp-id').value;
            const name = document.getElementById('new-wbp-name').value;
            const alias = document.getElementById('new-wbp-alias').value;
            const block = document.getElementById('new-wbp-block').value;
            const cat = document.getElementById('new-wbp-category').value;

            wbpList.push({ id, name, alias, block, defaultCategory: cat, status: 'Di Lapas' });
            closeModalWbp();
            showToast('WBP Pekerja Baru Berhasil Ditambahkan!', 'success');
            renderWbpTable();
        }

        function deleteWbp(id) {
            wbpList = wbpList.filter(w => w.id !== id);
            renderWbpTable();
            showToast('Data WBP dihapus', 'success');
        }

        // --- SESSION LOGS TABLE ---
        function renderSessionLogs() {
            const container = document.getElementById('session-log-list-container');

            if(sessionLogs.length === 0) {
                container.innerHTML = `<div class="p-8 text-center text-slate-400 bg-slate-50 dark:bg-slate-700/30 rounded-xl">Belum ada riwayat sesi rombongan.</div>`;
                return;
            }

            container.innerHTML = sessionLogs.map(s => {
                const returnedCount = s.members.filter(m => m.returned).length;
                const isComplete = s.status === 'Selesai / Lengkap';

                return `
                    <div class="bg-slate-50 dark:bg-slate-700/30 rounded-xl border border-slate-200 dark:border-slate-700 p-4 space-y-3">
                        <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-2 border-b border-slate-200 dark:border-slate-700 pb-2">
                            <div>
                                <span class="bg-lapas-600 text-white font-bold text-xs px-2.5 py-0.5 rounded">${s.category}</span>
                                <span class="text-xs text-slate-500 font-mono ml-2">${s.sessionId} • ${s.date}</span>
                            </div>
                            <div>
                                ${isComplete 
                                    ? `<span class="bg-emerald-100 text-emerald-800 text-xs px-2.5 py-1 rounded-full font-bold">Selesai / Lengkap (${s.actualInTime} WIB)</span>`
                                    : `<span class="bg-amber-100 text-amber-800 text-xs px-2.5 py-1 rounded-full font-bold">Sesi Aktif di Luar</span>`
                                }
                            </div>
                        </div>

                        <div class="grid grid-cols-2 sm:grid-cols-4 gap-2 text-xs">
                            <div><span class="text-slate-500">Pengawal:</span> <strong class="block text-slate-800 dark:text-slate-200">${s.officerEscort}</strong></div>
                            <div><span class="text-slate-500">Lokasi:</span> <strong class="block text-slate-800 dark:text-slate-200">${s.location}</strong></div>
                            <div><span class="text-slate-500">Jam Keluar:</span> <strong class="block text-slate-800 dark:text-slate-200">${s.outTime} WIB</strong></div>
                            <div><span class="text-slate-500">Batas Kembali:</span> <strong class="block text-lapas-600 dark:text-lapas-400">${s.limitTime} WIB</strong></div>
                        </div>

                        <div class="pt-2 border-t border-slate-200 dark:border-slate-700/50">
                            <span class="text-xs font-bold text-slate-700 dark:text-slate-300 block mb-1">Anggota Rombongan (${returnedCount}/${s.members.length} Sudah Kembali):</span>
                            <div class="flex flex-wrap gap-1.5">
                                ${s.members.map(m => `
                                    <span class="text-[11px] px-2 py-0.5 rounded border ${m.returned ? 'bg-emerald-50 text-emerald-800 border-emerald-200' : 'bg-amber-50 text-amber-800 border-amber-200'}">
                                        ${m.name} (${m.wbpId}) ${m.returned ? '✓' : '⌛'}
                                    </span>
                                `).join('')}
                            </div>
                        </div>
                    </div>
                `;
            }).join('');
        }

        // --- ALARM CHECKING ---
        function checkAlarms() {
            const nowStr = new Date().toTimeString().substring(0, 5);
            const overdueSessions = sessionLogs.filter(s => s.status === 'Aktif / Di Luar' && nowStr > s.limitTime);

            const badge = document.getElementById('notif-badge');
            const pill = document.getElementById('alarm-count-pill');

            if(overdueSessions.length > 0) {
                badge.innerText = overdueSessions.length;
                badge.classList.remove('hidden');
                pill.innerText = overdueSessions.length;
            } else {
                badge.classList.add('hidden');
                pill.innerText = '0';
            }
        }

        function renderAlarmList() {
            const container = document.getElementById('alarm-container');
            const nowStr = new Date().toTimeString().substring(0, 5);
            const overdueSessions = sessionLogs.filter(s => s.status === 'Aktif / Di Luar' && nowStr > s.limitTime);

            if(overdueSessions.length === 0) {
                container.innerHTML = `<div class="p-8 text-center text-slate-400 bg-slate-50 dark:bg-slate-700/30 rounded-xl">Tidak ada keterlambatan rombongan saat ini.</div>`;
                return;
            }

            container.innerHTML = overdueSessions.map(s => {
                return `
                    <div class="p-4 rounded-xl border border-red-200 bg-red-50 dark:bg-red-900/20 text-lapas-700 dark:text-red-300 flex justify-between items-center">
                        <div>
                            <span class="font-bold text-sm block"><i class="fa-solid fa-triangle-exclamation"></i> TERLAMBAT: ${s.category} (${s.sessionId})</span>
                            <p class="text-xs mt-1">Pengawal: ${s.officerEscort} | Batas Kembali: ${s.limitTime} WIB</p>
                        </div>
                        <button onclick="quickPresensiSession('${s.sessionId}')" class="bg-lapas-600 text-white text-xs px-3.5 py-2 rounded-lg font-bold">Proses Presensi</button>
                    </div>
                `;
            }).join('');
        }

        // --- SURAT JALAN ROMBONGAN MODAL ---
        function showGroupReceiptModal(session) {
            const content = document.getElementById('receipt-content');
            content.innerHTML = `
                <p><strong>ID Sesi Rombongan:</strong> ${session.sessionId}</p>
                <p><strong>Jenis Pekerjaan:</strong> ${session.category}</p>
                <p><strong>Pengawal / PIC:</strong> ${session.officerEscort}</p>
                <p><strong>Lokasi Kegiatan:</strong> ${session.location}</p>
                <p><strong>Waktu Keluar / Batas:</strong> ${session.outTime} WIB s/d ${session.limitTime} WIB</p>
                <hr class="border-dashed border-slate-300 my-2">
                <p class="font-bold mb-1">Daftar WBP Rombongan (${session.members.length} Orang):</p>
                <ol class="list-decimal list-inside text-[11px] space-y-0.5">
                    ${session.members.map(m => `<li>${m.name} (${m.wbpId})</li>`).join('')}
                </ol>
            `;
            document.getElementById('modal-receipt').classList.remove('hidden');
        }

        function closeReceiptModal() {
            document.getElementById('modal-receipt').classList.add('hidden');
        }

        function showToast(message, type = 'success') {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            const bgClass = type === 'success' ? 'bg-emerald-600 text-white' : 'bg-lapas-600 text-white';
            toast.className = `${bgClass} px-4 py-3 rounded-xl shadow-lg text-xs font-semibold flex items-center space-x-2 transition transform translate-y-2 opacity-0 pointer-events-auto`;
            toast.innerHTML = `<i class="fa-solid fa-circle-info"></i><span>${message}</span>`;
            container.appendChild(toast);
            setTimeout(() => toast.classList.remove('translate-y-2', 'opacity-0'), 50);
            setTimeout(() => {
                toast.classList.add('translate-y-2', 'opacity-0');
                setTimeout(() => toast.remove(), 300);
            }, 3500);
        }

        function exportLogCSV() {
            let csvContent = "data:text/csv;charset=utf-8,ID Sesi,Kategori,Pengawal,Jam Keluar,Batas Kembali,Status,Jumlah WBP\n";
            sessionLogs.forEach(s => {
                csvContent += `"${s.sessionId}","${s.category}","${s.officerEscort}","${s.outTime}","${s.limitTime}","${s.status}","${s.members.length}"\n`;
            });
            const encodedUri = encodeURI(csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", `log_rombongan_portir_${new Date().toISOString().split('T')[0]}.csv`);
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            showToast('Log Rombongan berhasil di-export ke CSV', 'success');
        }
    </script>
</body>
</html>
```# Keluarmasuk-project
