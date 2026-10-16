
<html lang="id" class="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Portir Lapas Kembangkuning - Keluar Masuk WBP Asimilasi</title>
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
                    <h1 class="text-lg font-bold tracking-tight text-slate-900 dark:text-white leading-tight">PORTIR LAPAS KEMBANGKUNING</h1>
                    <p class="text-xs text-slate-500 dark:text-slate-400">Pengawasan Keluar-Masuk WBP Pekerja Asimilasi Luar Lapas</p>
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
                    <span>Petugas Regu Portir</span>
                    <span class="inline-block w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
                </div>
                <div class="text-slate-600 dark:text-slate-400 space-y-1">
                    <p><span class="font-semibold text-slate-700 dark:text-slate-300">Komandan Portir:</span> Petugas Regu Jaga</p>
                    <p><span class="font-semibold text-slate-700 dark:text-slate-300">Pintu Utama (P2U):</span> Petugas Portir Lapas</p>
                </div>
            </div>
        </aside>

        <!-- Dynamic Content Area -->
        <main class="flex-1">

            <!-- TAB 1: DASHBOARD -->
            <section id="tab-dashboard" class="tab-content space-y-6">
                <div class="bg-gradient-to-r from-slate-900 via-slate-800 to-slate-900 text-white rounded-2xl p-6 shadow-md relative overflow-hidden">
                    <div class="absolute right-0 bottom-0 opacity-10 translate-x-4 translate-y-4">
                        <i class="fa-solid fa-building-shield text-9xl"></i>
                    </div>
                    <div class="relative z-10">
                        <span class="bg-lapas-600 text-white text-xs px-3 py-1 rounded-full font-semibold uppercase tracking-wider">Portir Lapas Kelas IIA Kembangkuning</span>
                        <h2 class="text-2xl font-bold mt-2">Pencatatan Rombongan Pekerja Asimilasi</h2>
                        <p class="text-slate-300 text-sm mt-1">Kontrol presensi pengeluaran dan pemasukan WBP Pekerja (Peternakan Kambing, Perikanan, Greenhouse, TPA, Kebersihan).</p>
                        
                        <div class="mt-6 flex flex-wrap gap-3">
                            <button onclick="switchTab('keluar')" class="bg-white text-slate-900 hover:bg-slate-100 px-4 py-2 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                                <i class="fa-solid fa-user-plus text-lapas-600"></i>
                                <span>Izin Keluar Rombongan</span>
                            </button>
                            <button onclick="switchTab('masuk')" class="bg-lapas-600 hover:bg-lapas-700 text-white px-4 py-2 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                                <i class="fa-solid fa-list-check"></i>
                                <span>Presensi Kembali (Pintu P2U)</span>
                            </button>
                        </div>
                    </div>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium text-slate-500 dark:text-slate-400 uppercase tracking-wider">Total WBP Pekerja</p>
                            <h3 id="stat-total-wbp" class="text-3xl font-bold text-slate-900 dark:text-white mt-1">0</h3>
                            <span class="text-xs text-slate-500 mt-1 inline-block">Terdata di Master</span>
                        </div>
                        <div class="bg-blue-50 dark:bg-blue-900/30 text-blue-600 dark:text-blue-400 p-3.5 rounded-xl text-xl">
                            <i class="fa-solid fa-id-card"></i>
                        </div>
                    </div>

                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium text-slate-500 dark:text-slate-400 uppercase tracking-wider">Sedang di Luar Area</p>
                            <h3 id="stat-sedang-luar" class="text-3xl font-bold text-amber-600 dark:text-amber-400 mt-1">0</h3>
                            <span class="text-xs text-amber-600 dark:text-amber-400 font-medium mt-1 inline-block"><i class="fa-solid fa-person-walking-arrow-right"></i> Bekerja Asimilasi</span>
                        </div>
                        <div class="bg-amber-50 dark:bg-amber-900/30 text-amber-600 dark:text-amber-400 p-3.5 rounded-xl text-xl">
                            <i class="fa-solid fa-users"></i>
                        </div>
                    </div>

                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium text-slate-500 dark:text-slate-400 uppercase tracking-wider">Di Dalam Lapas</p>
                            <h3 id="stat-dalam-lapas" class="text-3xl font-bold text-emerald-600 dark:text-emerald-400 mt-1">0</h3>
                            <span class="text-xs text-emerald-600 dark:text-emerald-400 font-medium mt-1 inline-block"><i class="fa-solid fa-house-lock"></i> Ada di Dalam</span>
                        </div>
                        <div class="bg-emerald-50 dark:bg-emerald-900/30 text-emerald-600 dark:text-emerald-400 p-3.5 rounded-xl text-xl">
                            <i class="fa-solid fa-building-user"></i>
                        </div>
                    </div>

                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium text-slate-500 dark:text-slate-400 uppercase tracking-wider">Sesi Tugas Aktif</p>
                            <h3 id="stat-sesi-aktif" class="text-3xl font-bold text-lapas-600 dark:text-lapas-500 mt-1">0</h3>
                            <span class="text-xs text-slate-500 mt-1 inline-block">Kelompok Rombongan</span>
                        </div>
                        <div class="bg-red-50 dark:bg-red-900/30 text-lapas-600 dark:text-lapas-500 p-3.5 rounded-xl text-xl">
                            <i class="fa-solid fa-layer-group"></i>
                        </div>
                    </div>
                </div>

                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="flex items-center justify-between mb-4">
                        <h3 class="font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                            <i class="fa-solid fa-list-check text-lapas-600"></i>
                            <span>Daftar Sesi Rombongan Yang Sedang Bertugas Di Luar</span>
                        </h3>
                        <button onclick="switchTab('riwayat')" class="text-xs text-lapas-600 hover:underline font-semibold">Lihat Semua Log</button>
                    </div>
                    
                    <div id="dashboard-active-sessions" class="space-y-4"></div>
                </div>
            </section>

            <!-- TAB 2: FORM KELUAR ROMBONGAN -->
            <section id="tab-keluar" class="tab-content space-y-6 hidden">
                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="border-b border-slate-200 dark:border-slate-700 pb-4 mb-6">
                        <h2 class="text-lg font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                            <i class="fa-solid fa-users-viewfinder text-lapas-600"></i>
                            <span>Form Izin Keluar Rombongan WBP Asimilasi</span>
                        </h2>
                        <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Pilih beberapa WBP pekerja sekaligus sesuai bidang penugasan kerja luar.</p>
                    </div>

                    <form id="form-bulk-out" onsubmit="handleBulkCheckout(event)" class="space-y-6">
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 bg-slate-50 dark:bg-slate-700/40 p-4 rounded-xl border border-slate-200 dark:border-slate-700">
                            <div>
                                <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Bidang Penugasan / Kerja *</label>
                                <select id="out-category" onchange="toggleCustomCategoryInput()" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                                    <option value="Lahan Peternakan Kambing">Lahan Peternakan Kambing</option>
                                    <option value="Pengolah Pakan Kambing">Pengolah Pakan Kambing</option>
                                    <option value="Laundry & Greenhouse">Laundry & Greenhouse</option>
                                    <option value="Pembangunan / Operasional TPA">Pembangunan / Operasional TPA</option>
                                    <option value="Asimilasi Perikanan / Tambak">Asimilasi Perikanan / Tambak</option>
                                    <option value="Pertanian / Perkebunan">Pertanian / Perkebunan</option>
                                    <option value="Dan / Lain-lain">Dan / Lain-lain (Ketik Manual)</option>
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
                                <input type="text" id="out-officer-escort" placeholder="Contoh: Staf Seksi Kegiatan Kerja / Pengawal Asimilasi" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                            </div>

                            <div>
                                <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Lokasi Kegiatan</label>
                                <input type="text" id="out-location" placeholder="Area Peternakan Kambing & TPA Lapas Kembangkuning" class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                            </div>
                        </div>

                        <div class="space-y-3">
                            <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-2">
                                <div>
                                    <h3 class="font-bold text-sm text-slate-900 dark:text-white flex items-center space-x-2">
                                        <i class="fa-solid fa-square-check text-lapas-600"></i>
                                        <span>Pilih Warga Binaan (Tersedia: <span id="out-available-count">0</span> WBP)</span>
                                    </h3>
                                    <p class="text-xs text-slate-500">Centang nama WBP yang akan dikeluarkan pada sesi ini.</p>
                                </div>
                                <div class="flex items-center space-x-2">
                                    <button type="button" onclick="selectAllAvailableOutWbp(true)" class="px-2.5 py-1 text-xs rounded bg-blue-100 text-blue-700 dark:bg-blue-900/50 dark:text-blue-300 font-medium">Centang Semua</button>
                                    <button type="button" onclick="selectAllAvailableOutWbp(false)" class="px-2.5 py-1 text-xs rounded bg-slate-200 text-slate-700 dark:bg-slate-700 dark:text-slate-300">Kosongkan</button>
                                </div>
                            </div>

                            <input type="text" id="out-wbp-filter" onkeyup="renderOutWbpSelectionList()" placeholder="Ketik nama atau No. Registrasi WBP..." class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">

                            <div id="out-wbp-checkbox-grid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-3 max-h-80 overflow-y-auto p-3 bg-slate-50 dark:bg-slate-900/40 rounded-xl border border-slate-200 dark:border-slate-700"></div>
                            
                            <div class="text-xs text-slate-600 dark:text-slate-400 font-semibold flex items-center justify-between">
                                <span>Terpilih: <strong id="out-selected-count" class="text-lapas-600 dark:text-lapas-400 text-sm">0</strong> WBP</span>
                            </div>
                        </div>

                        <div class="flex justify-end space-x-3 pt-4 border-t border-slate-200 dark:border-slate-700">
                            <button type="submit" class="bg-lapas-600 hover:bg-lapas-700 text-white px-6 py-2.5 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                                <i class="fa-solid fa-receipt"></i>
                                <span>Proses Keluar & Cetak Surat Jalan</span>
                            </button>
                        </div>
                    </form>
                </div>
            </section>

            <!-- TAB 3: FORM PRESENSI MASUK -->
            <section id="tab-masuk" class="tab-content space-y-6 hidden">
                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="border-b border-slate-200 dark:border-slate-700 pb-4 mb-6">
                        <h2 class="text-lg font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                            <i class="fa-solid fa-list-check text-lapas-600"></i>
                            <span>Presensi Masuk & Penggeledahan Portir (P2U)</span>
                        </h2>
                        <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Lakukan pemanggilan & centang WBP yang telah kembali ke pos portir.</p>
                    </div>

                    <div class="space-y-5">
                        <div>
                            <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Pilih Sesi Rombongan Aktif *</label>
                            <select id="in-session-select" onchange="loadSessionForCheckin()" class="w-full px-3.5 py-2.5 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                                <option value="">-- Pilih Sesi Rombongan Yang Sedang Bekerja --</option>
                            </select>
                        </div>

                        <div id="in-session-detail-container" class="hidden space-y-5">
                            <div class="bg-slate-50 dark:bg-slate-700/50 p-4 rounded-xl border border-slate-200 dark:border-slate-700 grid grid-cols-2 md:grid-cols-4 gap-4 text-xs">
                                <div>
                                    <span class="block text-slate-500">Penugasan Kerja</span>
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
                                    <span class="block text-slate-500">Status Waktu</span>
                                    <span id="in-session-status-badge" class="inline-block mt-0.5">-</span>
                                </div>
                            </div>

                            <form id="form-bulk-in" onsubmit="handleBulkCheckin(event)" class="space-y-4">
                                <div class="flex items-center justify-between">
                                    <h3 class="font-bold text-sm text-slate-900 dark:text-white">Daftar Anggota Rombongan (Centang Yang Kembali)</h3>
                                    <div class="space-x-2">
                                        <button type="button" onclick="toggleAllCheckinWbp(true)" class="text-xs bg-emerald-100 text-emerald-800 dark:bg-emerald-900/50 dark:text-emerald-300 px-2.5 py-1 rounded font-semibold">Tandai Semua</button>
                                        <button type="button" onclick="toggleAllCheckinWbp(false)" class="text-xs bg-slate-200 text-slate-700 dark:bg-slate-700 dark:text-slate-300 px-2.5 py-1 rounded">Batal Semua</button>
                                    </div>
                                </div>

                                <div id="in-wbp-checklist-grid" class="grid grid-cols-1 md:grid-cols-2 gap-3 max-h-80 overflow-y-auto p-3 bg-slate-50 dark:bg-slate-900/40 rounded-xl border border-slate-200 dark:border-slate-700"></div>

                                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 pt-2">
                                    <div>
                                        <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Jam Kembali Riil *</label>
                                        <input type="time" id="in-actual-time" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                                    </div>
                                    <div>
                                        <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Hasil Penggeledahan P2U *</label>
                                        <select id="in-search-result" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                                            <option value="Aman / Nihil Temuan">Aman / Nihil Temuan Barang Terlarang</option>
                                            <option value="Temuan Barang Dilarang">Ada Temuan Dilarang (Lapor KPLP)</option>
                                            <option value="Catatan Kesehatan">Catatan Kesehatan / Pengobatan</option>
                                        </select>
                                    </div>
                                    <div>
                                        <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Petugas Verifikator Portir *</label>
                                        <input type="text" id="in-officer-name" value="Petugas Portir / P2U Lapas" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-slate-100 dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">
                                    </div>
                                </div>

                                <div>
                                    <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Catatan Penggeledahan</label>
                                    <input type="text" id="in-notes" placeholder="Contoh: Badan & peralatan kerja diserahterimakan dalam keadaan aman dan lengkap." class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">
                                </div>

                                <div class="flex justify-end space-x-3 pt-4 border-t border-slate-200 dark:border-slate-700">
                                    <button type="submit" class="bg-emerald-600 hover:bg-emerald-700 text-white px-6 py-2.5 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                                        <i class="fa-solid fa-clipboard-check"></i>
                                        <span>Simpan Presensi Masuk & Tutup Sesi</span>
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
                                <span>Master Data WBP Pekerja Asimilasi Lapas Kembangkuning</span>
                            </h2>
                            <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Daftar WBP yang ditetapkan berdasarkan Surat Perintah Kalapas Kembangkuning.</p>
                        </div>
                        <button onclick="openAddWbpModal()" class="bg-lapas-600 hover:bg-lapas-700 text-white px-4 py-2 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                            <i class="fa-solid fa-user-plus"></i>
                            <span>Tambah WBP Pekerja</span>
                        </button>
                    </div>

                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-3 mb-4">
                        <input type="text" id="wbp-search" onkeyup="renderWbpTable()" placeholder="Cari nama atau No. Reg..." class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">
                        <select id="wbp-filter-cat" onchange="renderWbpTable()" class="px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">
                            <option value="">Semua Penugasan</option>
                            <option value="Lahan Peternakan Kambing">Lahan Peternakan Kambing</option>
                            <option value="Pengolah Pakan Kambing">Pengolah Pakan Kambing</option>
                            <option value="Laundry & Greenhouse">Laundry & Greenhouse</option>
                            <option value="Pembangunan / Operasional TPA">Pembangunan / Operasional TPA</option>
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
                                    <th class="p-3">Kamar / Blok</th>
                                    <th class="p-3">Penugasan Kerja Utama</th>
                                    <th class="p-3">Status Lokasi</th>
                                    <th class="p-3 text-right rounded-r-lg">Aksi</th>
                                </tr>
                            </thead>
                            <tbody id="wbp-table-tbody" class="divide-y divide-slate-100 dark:divide-slate-700"></tbody>
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
                            <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Daftar arsip seluruh kelompok pekerjaan asimilasi yang pernah keluar-masuk portir.</p>
                        </div>
                        <button onclick="exportLogCSV()" class="bg-slate-800 hover:bg-slate-700 text-white px-4 py-2 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                            <i class="fa-solid fa-file-csv"></i>
                            <span>Export Laporan CSV</span>
                        </button>
                    </div>

                    <div id="session-log-list-container" class="space-y-4"></div>
                </div>
            </section>

            <!-- TAB 6: ALARM / KETERLAMBATAN -->
            <section id="tab-alarm" class="tab-content space-y-6 hidden">
                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="border-b border-slate-200 dark:border-slate-700 pb-4 mb-6">
                        <h2 class="text-lg font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                            <i class="fa-solid fa-triangle-exclamation text-lapas-600"></i>
                            <span>Peringatan Waktu & Keterlambatan Rombongan</span>
                        </h2>
                        <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Sesi rombongan WBP yang telah melebihi batas jam kembali.</p>
                    </div>

                    <div id="alarm-container" class="space-y-4"></div>
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
                <p class="text-xs text-slate-500">Pos Pengamanan Pintu Utama (Portir) Lapas Kelas IIA Kembangkuning</p>
            </div>

            <div id="receipt-content" class="text-xs space-y-3 text-slate-700 dark:text-slate-300"></div>

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
                    <input type="text" id="new-wbp-id" placeholder="BI. 200/2025" required class="w-full px-3 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white">
                </div>
                <div>
                    <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">Nama Lengkap WBP *</label>
                    <input type="text" id="new-wbp-name" placeholder="Nama WBP" required class="w-full px-3 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white">
                </div>
                <div>
                    <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">Bin / Alias</label>
                    <input type="text" id="new-wbp-alias" placeholder="Bin ..." class="w-full px-3 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white">
                </div>
                <div>
                    <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">Blok / Kamar Hunian</label>
                    <input type="text" id="new-wbp-block" placeholder="Blok C / Asimilasi" required class="w-full px-3 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white">
                </div>
                <div>
                    <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">Penugasan Kerja Utama *</label>
                    <select id="new-wbp-category" required class="w-full px-3 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white">
                        <option value="Lahan Peternakan Kambing">Lahan Peternakan Kambing</option>
                        <option value="Pengolah Pakan Kambing">Pengolah Pakan Kambing</option>
                        <option value="Laundry & Greenhouse">Laundry & Greenhouse</option>
                        <option value="Pembangunan / Operasional TPA">Pembangunan / Operasional TPA</option>
                        <option value="Asimilasi Perikanan / Tambak">Asimilasi Perikanan / Tambak</option>
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
        // Data WBP Asimilasi Pekerja Lapas Kembangkuning
        let wbpList = [
            // Penugasan Lahan Peternakan Kambing
            { id: 'BI.101/2025', name: 'Mochamad Mashudin', alias: 'Bin Su\'ud Kayat', block: 'Blok Asimilasi', defaultCategory: 'Lahan Peternakan Kambing', status: 'Di Lapas' },
            { id: 'BI.102/2025', name: 'Fransiskus Jimi', alias: 'Als Jimi Anak Sabi', block: 'Blok Asimilasi', defaultCategory: 'Lahan Peternakan Kambing', status: 'Di Lapas' },
            { id: 'BI.103/2025', name: 'Jatmiko', alias: 'Bin Sutikno', block: 'Blok Asimilasi', defaultCategory: 'Lahan Peternakan Kambing', status: 'Di Lapas' },
            { id: 'BI.104/2025', name: 'Fadlun', alias: 'Bin Somadiharjo', block: 'Blok Asimilasi', defaultCategory: 'Lahan Peternakan Kambing', status: 'Di Lapas' },
            { id: 'BI.105/2025', name: 'Suhardi', alias: 'Bin Kasan', block: 'Blok Asimilasi', defaultCategory: 'Lahan Peternakan Kambing', status: 'Di Lapas' },
            { id: 'BI.106/2025', name: 'Khoirul Anam', alias: 'Bin Taufik', block: 'Blok Asimilasi', defaultCategory: 'Lahan Peternakan Kambing', status: 'Di Lapas' },
            { id: 'BI.107/2025', name: 'Darnoto', alias: 'Als Anto Bin Carum', block: 'Blok Asimilasi', defaultCategory: 'Lahan Peternakan Kambing', status: 'Di Lapas' },
            { id: 'BI.108/2025', name: 'Pandi Amalga', alias: 'Bin Gumilar Budiyanto', block: 'Blok Asimilasi', defaultCategory: 'Lahan Peternakan Kambing', status: 'Di Lapas' },
            { id: 'BI.109/2025', name: 'Marzuli YS', alias: 'Bin M. Yunus', block: 'Blok Asimilasi', defaultCategory: 'Lahan Peternakan Kambing', status: 'Di Lapas' },
            { id: 'BI.110/2025', name: 'Bruri Sulistiyono', alias: 'Bin Sutardi', block: 'Blok Asimilasi', defaultCategory: 'Lahan Peternakan Kambing', status: 'Di Lapas' },
            { id: 'BI.111/2025', name: 'Hendri Asnanto', alias: 'Bin Asnan', block: 'Blok Asimilasi', defaultCategory: 'Lahan Peternakan Kambing', status: 'Di Lapas' },
            { id: 'BI.112/2025', name: 'Romli', alias: 'Bin Honali', block: 'Blok Asimilasi', defaultCategory: 'Lahan Peternakan Kambing', status: 'Di Lapas' },

            // Penugasan Pengolah Pakan Kambing
            { id: 'BI.113/2025', name: 'Heri Pramono', alias: 'Bin Nawi Krama', block: 'Blok Asimilasi', defaultCategory: 'Pengolah Pakan Kambing', status: 'Di Lapas' },
            { id: 'BI.114/2025', name: 'Junaedi', alias: 'Als Boboy Bin Sanusi', block: 'Blok Asimilasi', defaultCategory: 'Pengolah Pakan Kambing', status: 'Di Lapas' },

            // Penugasan Laundry & Greenhouse
            { id: 'BI.115/2025', name: 'Soiri', alias: 'Bin Hasan', block: 'Blok Asimilasi', defaultCategory: 'Laundry & Greenhouse', status: 'Di Lapas' },
            { id: 'BI.116/2025', name: 'Sandi Arrijaya', alias: 'Bin Ahmad Jaya', block: 'Blok Asimilasi', defaultCategory: 'Laundry & Greenhouse', status: 'Di Lapas' },

            // Pembangunan / Operasional TPA
            { id: 'BI.117/2025', name: 'Resa Muhammad Zam', alias: 'Bin Jumadi', block: 'Blok Asimilasi', defaultCategory: 'Pembangunan / Operasional TPA', status: 'Di Lapas' },
            { id: 'BI.118/2025', name: 'Rudi Ramdani', alias: 'Bin Ramdani', block: 'Blok Asimilasi', defaultCategory: 'Pembangunan / Operasional TPA', status: 'Di Lapas' },
            { id: 'BI.119/2025', name: 'Andri Kurniawan', alias: 'Bin Kurniawan', block: 'Blok Asimilasi', defaultCategory: 'Pembangunan / Operasional TPA', status: 'Di Lapas' }
        ];

        // Sesi Logs awal
        let sessionLogs = [
            {
                sessionId: 'SESI-KMB-001',
                category: 'Lahan Peternakan Kambing',
                outTime: '07:30',
                limitTime: '16:00',
                actualInTime: '-',
                officerEscort: 'Staf Seksi Kegiatan Kerja / Pengawal',
                location: 'Area Peternakan Kambing & Greenhouse Lapas Kembangkuning',
                date: new Date().toISOString().split('T')[0],
                status: 'Aktif / Di Luar',
                members: [
                    { wbpId: 'BI.101/2025', name: 'Mochamad Mashudin', returned: false, returnTime: '-', searchResult: '-' },
                    { wbpId: 'BI.102/2025', name: 'Fransiskus Jimi', returned: false, returnTime: '-', searchResult: '-' },
                    { wbpId: 'BI.103/2025', name: 'Jatmiko', returned: false, returnTime: '-', searchResult: '-' },
                    { wbpId: 'BI.104/2025', name: 'Fadlun', returned: false, returnTime: '-', searchResult: '-' }
                ]
            }
        ];

        // Sinkronisasi status awal WBP yang ada di sesi aktif
        sessionLogs.forEach(s => {
            if(s.status === 'Aktif / Di Luar') {
                s.members.forEach(m => {
                    const found = wbpList.find(w => w.id === m.wbpId);
                    if(found && !m.returned) found.status = 'Di Luar';
                });
            }
        });

        // Jam Digital
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
            const grid = document.getElementById('out-wbp-checkbox-grid');

            const availableWbp = wbpList.filter(w => w.status === 'Di Lapas');
            document.getElementById('out-available-count').innerText = availableWbp.length;

            const filtered = availableWbp.filter(w => {
                return w.name.toLowerCase().includes(filterText) || w.id.toLowerCase().includes(filterText);
            });

            if(filtered.length === 0) {
                grid.innerHTML = `<div class="col-span-full p-6 text-center text-slate-400">Tidak ada WBP yang tersedia di dalam Lapas.</div>`;
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
            const location = document.getElementById('out-location').value || 'Area Luar Lapas Kembangkuning';

            const selectedIds = Array.from(selectedCheckboxes).map(cb => cb.value);

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
                    wbp.status = 'Di Luar';
                    return { wbpId: wbp.id, name: wbp.name, returned: false, returnTime: '-', searchResult: '-' };
                })
            };

            sessionLogs.unshift(newSession);

            showToast(`Sesi Rombongan (${selectedIds.length} WBP) berhasil diproses!`, 'success');
            showGroupReceiptModal(newSession);
            renderOutWbpSelectionList();
            renderDashboard();
        }

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
                : `<span class="bg-emerald-100 text-emerald-800 px-2 py-0.5 rounded font-bold">SESUAI JADWAL</span>`;

            const grid = document.getElementById('in-wbp-checklist-grid');
            grid.innerHTML = session.members.map(m => {
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

            const returnedIds = Array.from(selectedCbs).map(cb => cb.value);

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

            const allReturned = session.members.every(m => m.returned);
            if(allReturned) {
                session.status = 'Selesai / Lengkap';
                session.actualInTime = actualTime;
            }

            showToast(`Presensi masuk untuk ${returnedIds.length} WBP berhasil dicatat!`, 'success');
            populateCheckinSessions();
            renderDashboard();
        }

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
                            <span class="text-xs font-bold text-slate-700 dark:text-slate-300 block mb-1">Anggota Rombongan (${returnedCount}/${s.members.length} Kembali):</span>
                            <div class="flex flex-wrap gap-1.5">
                                ${s.members.map(m => `
                                    <span class="text-[11px] px-2 py-0.5 rounded border ${m.returned ? 'bg-emerald-50 text-emerald-800 border-emerald-200' : 'bg-amber-50 text-amber-800 border-amber-200'}">
                                        ${m.name} (${m.wbpId})${m.returned ? '✓' : '⌛'}
                                    </span>
                                `).join('')}
                            </div>
                        </div>
                    </div>
                `;
            }).join('');
        }

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

        function showGroupReceiptModal(session) {
            const content = document.getElementById('receipt-content');
            content.innerHTML = `
                <p><strong>ID Sesi Rombongan:</strong> ${session.sessionId}</p>
                <p><strong>Penugasan Kerja:</strong> ${session.category}</p>
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
            let csvContent = "data:text/csv;charset=utf-8,ID Sesi,Kategori Penugasan,Pengawal,Jam Keluar,Batas Kembali,Status,Jumlah WBP\n";
            sessionLogs.forEach(s => {
                csvContent += `"${s.sessionId}","${s.category}","${s.officerEscort}","${s.outTime}","${s.limitTime}","${s.status}","${s.members.length}"\n`;
            });
            const encodedUri = encodeURI(csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", `log_rombongan_portir_lapaskk_${new Date().toISOString().split('T')[0]}.csv`);
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            showToast('Log Rombongan berhasil di-export ke CSV', 'success');
        }
    </script>
</body>
</html>
