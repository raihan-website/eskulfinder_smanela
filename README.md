<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Eskul Finder</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome for icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        navy: '#1E3A8A',
                        primaryBlue: '#3B82F6',
                        lightBlue: '#60A5FA',
                        successGreen: '#10B981',
                        warningOrange: '#F59E0B',
                        darkBg: '#0F172A',
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        /* Custom scrollbar and mobile frame styling */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 9999px;
        }
        .app-container {
            max-width: 480px;
            margin: 0 auto;
            min-height: 100vh;
            background-color: #f8fafc;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1), 0 8px 10px -6px rgba(0, 0, 0, 0.1);
            position: relative;
            padding-bottom: 5rem;
        }
        @media (min-width: 640px) {
            body {
                background-color: #e2e8f0;
                display: flex;
                justify-content: center;
                align-items: center;
                padding: 20px 0;
            }
            .app-container {
                border-radius: 2.5rem;
                overflow: hidden;
                border: 8px solid #334155;
            }
        }
        .tab-content {
            display: none;
        }
        .tab-content.active {
            display: block;
            animation: fadeIn 0.3s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(4px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body class="font-sans antialiased text-slate-800">

    <div class="app-container flex flex-col relative">

        <!-- Top Header Bar -->
        <header class="bg-navy text-white px-5 pt-6 pb-4 rounded-b-3xl shadow-md sticky top-0 z-30">
            <div class="flex justify-between items-center mb-3">
                <div>
                    <p class="text-xs text-blue-200 font-medium">Selamat Datang Kembali,</p>
                    <h1 class="text-xl font-bold tracking-tight">Halo, Sebastian! 👋</h1>
                </div>
                <div class="flex items-center space-x-2">
                    <button onclick="switchTab('profile')" class="w-10 h-10 rounded-full bg-blue-600 flex items-center justify-center font-bold text-white shadow hover:bg-blue-500 transition">
                        S
                    </button>
                </div>
            </div>
            <!-- Quick Search Bar -->
            <div class="relative mt-2">
                <span class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none text-slate-400">
                    <i class="fa-solid fa-magnifying-glass"></i>
                </span>
                <input type="text" id="globalSearchInput" oninput="handleGlobalSearch(this.value)" placeholder="Cari ekstrakurikuler, pembina, atau jadwal..." class="w-full pl-10 pr-4 py-2.5 bg-slate-800/60 backdrop-blur border border-slate-700 rounded-2xl text-sm text-white placeholder-slate-400 focus:outline-none focus:ring-2 focus:ring-primaryBlue transition">
            </div>
        </header>

        <!-- Main Scrollable Body Area -->
        <main class="flex-1 overflow-y-auto px-4 py-5" id="mainScrollArea">

            <div id="tab-home" class="tab-content active space-y-6">
                <!-- Banner / Announcement Card -->
                <div class="bg-gradient-to-r from-navy to-blue-700 text-white p-5 rounded-2xl shadow-lg relative overflow-hidden">
                    <div class="absolute -right-6 -bottom-6 w-32 h-32 bg-white/10 rounded-full blur-xl pointer-events-none"></div>
                    <div class="flex items-start justify-between">
                        <div>
                            <span class="bg-warningOrange text-slate-900 text-[10px] font-bold px-2.5 py-0.5 rounded-full uppercase tracking-wider">Pengumuman</span>
                            <h2 class="text-lg font-bold mt-2">Pendaftaran Eskul Dibuka!</h2>
                            <p class="text-xs text-slate-100 mt-1 leading-relaxed">Segera ikuti tes minat atau daftar langsung sebelum kuota penuh pada 30 September 2026.</p>
                        </div>
                        <div class="bg-white/20 p-3 rounded-2xl text-warningOrange text-xl">
                            <i class="fa-solid fa-bullhorn"></i>
                        </div>
                    </div>
                    <button onclick="switchTab('cari')" class="mt-4 bg-white text-navy font-semibold text-xs px-4 py-2 rounded-xl shadow hover:bg-blue-50 transition flex items-center space-x-2">
                        <span>Cari Eskul Sekarang</span>
                        <i class="fa-solid fa-arrow-right text-[10px]"></i>
                    </button>
                </div>

                <!-- Quick Action Buttons -->
                <div class="grid grid-cols-4 gap-3">
                    <button onclick="switchTab('cari')" class="flex flex-col items-center p-3 bg-white rounded-2xl shadow-sm hover:shadow-md transition border border-slate-100">
                        <div class="w-12 h-12 rounded-2xl bg-blue-50 text-primaryBlue flex items-center justify-center text-lg mb-1.5">
                            <i class="fa-solid fa-compass"></i>
                        </div>
                        <span class="text-xs font-medium text-slate-700">Quiz Minat</span>
                    </button>
                    <button onclick="switchTab('daftar-list')" class="flex flex-col items-center p-3 bg-white rounded-2xl shadow-sm hover:shadow-md transition border border-slate-100">
                        <div class="w-12 h-12 rounded-2xl bg-emerald-50 text-successGreen flex items-center justify-center text-lg mb-1.5">
                            <i class="fa-solid fa-list-check"></i>
                        </div>
                        <span class="text-xs font-medium text-slate-700">Semua Eskul</span>
                    </button>
                    <button onclick="switchTab('jadwal')" class="flex flex-col items-center p-3 bg-white rounded-2xl shadow-sm hover:shadow-md transition border border-slate-100">
                        <div class="w-12 h-12 rounded-2xl bg-amber-50 text-warningOrange flex items-center justify-center text-lg mb-1.5">
                            <i class="fa-solid fa-calendar-days"></i>
                        </div>
                        <span class="text-xs font-medium text-slate-700">Jadwal</span>
                    </button>
                    <button onclick="switchTab('admin')" class="flex flex-col items-center p-3 bg-white rounded-2xl shadow-sm hover:shadow-md transition border border-slate-100">
                        <div class="w-12 h-12 rounded-2xl bg-indigo-50 text-indigo-600 flex items-center justify-center text-lg mb-1.5">
                            <i class="fa-solid fa-user-shield"></i>
                        </div>
                        <span class="text-xs font-medium text-slate-700">Dashboard</span>
                    </button>
                </div>

                <!-- Today's Activities -->
                <div>
                    <div class="flex justify-between items-center mb-3">
                        <h3 class="font-bold text-slate-800 text-sm">Jadwal Hari Ini</h3>
                        <span class="text-xs text-primaryBlue font-semibold cursor-pointer" onclick="switchTab('jadwal')">Lihat Semua</span>
                    </div>
                    <div class="space-y-3" id="todayScheduleContainer">
                        <!-- Populated by JS -->
                    </div>
                </div>

                <!-- Popular Extracurriculars -->
                <div>
                    <div class="flex justify-between items-center mb-3">
                        <h3 class="font-bold text-slate-800 text-sm">Eskul Populer</h3>
                        <span class="text-xs text-primaryBlue font-semibold cursor-pointer" onclick="switchTab('daftar-list')">Eksplor</span>
                    </div>
                    <div class="grid grid-cols-2 gap-3" id="popularEskulContainer">
                        <!-- Populated by JS -->
                    </div>
                </div>
            </div>

            <div id="tab-cari" class="tab-content space-y-5">
                <div class="bg-gradient-to-r from-blue-600 to-indigo-700 p-5 rounded-2xl text-white shadow">
                    <h2 class="text-lg font-bold">Cari Eskul yang Cocok 🎯</h2>
                    <p class="text-xs text-blue-100 mt-1">Ikuti Tes Minat & Bakat interaktif singkat untuk menemukan rekomendasi eskul dengan persentase kecocokan akurat!</p>
                    <button onclick="openQuizModal()" class="mt-4 bg-white text-navy font-bold text-xs px-5 py-2.5 rounded-xl shadow hover:bg-slate-100 transition flex items-center space-x-2">
                        <i class="fa-solid fa-wand-magic-sparkles text-warningOrange"></i>
                        <span>Mulai Tes Minat Sekarang</span>
                    </button>
                </div>

                <!-- Category Filters -->
                <div class="flex space-x-2 overflow-x-auto pb-1 text-xs no-scrollbar">
                    <button onclick="filterCategory('Semua')" class="cat-btn bg-navy text-white px-4 py-2 rounded-xl font-medium whitespace-nowrap shadow-sm transition">Semua</button>
                    <button onclick="filterCategory('Olahraga')" class="cat-btn bg-white text-slate-600 border border-slate-200 px-4 py-2 rounded-xl font-medium whitespace-nowrap shadow-sm hover:bg-slate-50 transition">Olahraga</button>
                    <button onclick="filterCategory('Seni & Budaya')" class="cat-btn bg-white text-slate-600 border border-slate-200 px-4 py-2 rounded-xl font-medium whitespace-nowrap shadow-sm hover:bg-slate-50 transition">Seni & Budaya</button>
                    <button onclick="filterCategory('Teknologi')" class="cat-btn bg-white text-slate-600 border border-slate-200 px-4 py-2 rounded-xl font-medium whitespace-nowrap shadow-sm hover:bg-slate-50 transition">Teknologi</button>
                    <button onclick="filterCategory('Akademik')" class="cat-btn bg-white text-slate-600 border border-slate-200 px-4 py-2 rounded-xl font-medium whitespace-nowrap shadow-sm hover:bg-slate-50 transition">Akademik</button>
                </div>

                <!-- Eskul List Grid -->
                <div class="space-y-3" id="fullEskulListContainer">
                    <!-- Populated by JS -->
                </div>
            </div>

            <!-- Alternative Alias Tab for List -->
            <div id="tab-daftar-list" class="tab-content space-y-4">
                <div class="flex justify-between items-center">
                    <h2 class="font-bold text-slate-800 text-base">Daftar Seluruh Ekstrakurikuler</h2>
                    <span class="text-xs bg-blue-100 text-primaryBlue px-2.5 py-1 rounded-full font-semibold" id="totalEskulBadge">0 Aktif</span>
                </div>
                <div class="space-y-3" id="allEskulListContainer2">
                    <!-- Populated by JS -->
                </div>
            </div>

            <div id="tab-jadwal" class="tab-content space-y-4">
                <div class="flex justify-between items-center">
                    <div>
                        <h2 class="font-bold text-slate-800 text-base">Jadwal Kegiatan Mingguan</h2>
                        <p class="text-xs text-slate-500">Pilih hari untuk melihat detail kegiatan eskul</p>
                    </div>
                </div>

                <!-- Day Tabs -->
                <div class="grid grid-cols-5 gap-1 bg-white p-1.5 rounded-2xl border border-slate-200 text-center text-xs font-semibold">
                    <button onclick="filterDay('Senin')" class="day-tab py-2 rounded-xl bg-navy text-white transition shadow-sm">Senin</button>
                    <button onclick="filterDay('Selasa')" class="day-tab py-2 rounded-xl text-slate-600 hover:bg-slate-100 transition">Selasa</button>
                    <button onclick="filterDay('Rabu')" class="day-tab py-2 rounded-xl text-slate-600 hover:bg-slate-100 transition">Rabu</button>
                    <button onclick="filterDay('Kamis')" class="day-tab py-2 rounded-xl text-slate-600 hover:bg-slate-100 transition">Kamis</button>
                    <button onclick="filterDay('Jumat')" class="day-tab py-2 rounded-xl text-slate-600 hover:bg-slate-100 transition">Jumat</button>
                </div>

                <!-- Schedule List -->
                <div class="space-y-3" id="scheduleListContainer">
                    <!-- Populated by JS -->
                </div>
            </div>

            <div id="tab-profile" class="tab-content space-y-5">
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-100 text-center relative overflow-hidden">
                    <div class="w-20 h-20 bg-blue-600 text-white rounded-full flex items-center justify-center text-2xl font-bold mx-auto shadow-md mb-3">
                        S
                    </div>
                    <h2 class="font-bold text-slate-800 text-lg">Sebastian</h2>
                    <p class="text-xs text-slate-500">Kelas XI MIPA 2 • NIS: 998214</p>
                    <div class="mt-4 pt-4 border-t border-slate-100 grid grid-cols-2 gap-4 text-center">
                        <div>
                            <span class="text-xs text-slate-400 block">Eskul Diikuti</span>
                            <span id="userRegisteredCount" class="font-bold text-navy text-base">1 Eskul</span>
                        </div>
                        <div>
                            <span class="text-xs text-slate-400 block">Status Akun</span>
                            <span class="font-bold text-successGreen text-sm flex items-center justify-center gap-1">
                                <i class="fa-solid fa-circle-check text-[10px]"></i> Aktif
                            </span>
                        </div>
                    </div>
                </div>

                <!-- My Registered Activities -->
                <div>
                    <h3 class="font-bold text-slate-800 text-sm mb-3">Eskul Saya</h3>
                    <div class="space-y-3" id="myEskulContainer">
                        <!-- Populated by JS -->
                    </div>
                </div>

                <!-- Quick Registration Status Form trigger -->
                <div class="bg-blue-50 border border-blue-100 p-4 rounded-2xl flex items-center justify-between">
                    <div>
                        <h4 class="font-bold text-navy text-sm">Ingin daftar eskul tambahan?</h4>
                        <p class="text-xs text-slate-600">Pilih dari daftar eskul yang tersedia sekarang.</p>
                    </div>
                    <button onclick="switchTab('cari')" class="bg-primaryBlue text-white text-xs px-4 py-2 rounded-xl font-semibold shadow hover:bg-blue-600 transition">
                        Daftar
                    </button>
                </div>
            </div>

            <div id="tab-admin" class="tab-content space-y-5">
                <div class="bg-slate-900 text-white p-5 rounded-2xl shadow-lg relative overflow-hidden">
                    <div class="flex justify-between items-center">
                        <div>
                            <span class="bg-indigo-500 text-white text-[10px] font-bold px-2.5 py-0.5 rounded-full uppercase">Panel Pembina</span>
                            <h2 class="text-lg font-bold mt-1">Dashboard Admin</h2>
                            <p class="text-xs text-slate-300">Kelola kuota eskul, jadwal, pembina, dan pengumuman sekolah.</p>
                        </div>
                        <div class="w-12 h-12 bg-white/10 rounded-2xl flex items-center justify-center text-warningOrange text-xl">
                            <i class="fa-solid fa-sliders"></i>
                        </div>
                    </div>
                </div>

                <!-- Admin Action Bar -->
                <div class="grid grid-cols-2 gap-3">
                    <button onclick="openAddEskulModal()" class="bg-white border border-slate-200 p-3.5 rounded-2xl shadow-sm hover:border-primaryBlue transition flex items-center space-x-3 text-left">
                        <div class="w-10 h-10 rounded-xl bg-emerald-50 text-successGreen flex items-center justify-center text-base">
                            <i class="fa-solid fa-plus"></i>
                        </div>
                        <div>
                            <span class="block text-xs font-bold text-slate-800">Tambah Eskul</span>
                            <span class="block text-[10px] text-slate-400">Buat eskul baru</span>
                        </div>
                    </button>
                    <button onclick="openBroadcastModal()" class="bg-white border border-slate-200 p-3.5 rounded-2xl shadow-sm hover:border-primaryBlue transition flex items-center space-x-3 text-left">
                        <div class="w-10 h-10 rounded-xl bg-blue-50 text-primaryBlue flex items-center justify-center text-base">
                            <i class="fa-solid fa-bullhorn"></i>
                        </div>
                        <div>
                            <span class="block text-xs font-bold text-slate-800">Pengumuman</span>
                            <span class="block text-[10px] text-slate-400">Kirim info baru</span>
                        </div>
                    </button>
                </div>

                <!-- Manage Eskul Table/Cards -->
                <div>
                    <h3 class="font-bold text-slate-800 text-sm mb-3">Kelola Kuota & Anggota</h3>
                    <div class="space-y-3" id="adminEskulListContainer">
                        <!-- Populated by JS -->
                    </div>
                </div>
            </div>

        </main>

        <nav class="absolute bottom-0 left-0 right-0 bg-white border-t border-slate-100 px-4 py-2.5 flex justify-around items-center z-30 shadow-lg">
            <button onclick="switchTab('home')" class="nav-btn flex flex-col items-center text-primaryBlue transition" data-target="home">
                <i class="fa-solid fa-house text-lg mb-1"></i>
                <span class="text-[10px] font-semibold">Beranda</span>
            </button>
            <button onclick="switchTab('cari')" class="nav-btn flex flex-col items-center text-slate-400 hover:text-primaryBlue transition" data-target="cari">
                <i class="fa-solid fa-compass text-lg mb-1"></i>
                <span class="text-[10px] font-medium">Cari</span>
            </button>
            <button onclick="switchTab('jadwal')" class="nav-btn flex flex-col items-center text-slate-400 hover:text-primaryBlue transition" data-target="jadwal">
                <i class="fa-solid fa-calendar-days text-lg mb-1"></i>
                <span class="text-[10px] font-medium">Jadwal</span>
            </button>
            <button onclick="switchTab('profile')" class="nav-btn flex flex-col items-center text-slate-400 hover:text-primaryBlue transition" data-target="profile">
                <i class="fa-solid fa-user text-lg mb-1"></i>
                <span class="text-[10px] font-medium">Profil</span>
            </button>
            <button onclick="switchTab('admin')" class="nav-btn flex flex-col items-center text-slate-400 hover:text-primaryBlue transition" data-target="admin">
                <i class="fa-solid fa-user-shield text-lg mb-1"></i>
                <span class="text-[10px] font-medium">Admin</span>
            </button>
        </nav>


        <!-- Detail Eskul Modal -->
        <div id="detailModal" class="fixed inset-0 bg-black/60 backdrop-blur-sm z-50 hidden flex items-end sm:items-center justify-center p-0 sm:p-4">
            <div class="bg-white w-full max-w-lg rounded-t-3xl sm:rounded-3xl max-h-[90vh] overflow-y-auto shadow-2xl animate-in fade-in slide-in-from-bottom duration-200">
                <div class="relative h-48 bg-gradient-to-r from-navy to-blue-700 p-6 text-white flex flex-col justify-end">
                    <button onclick="closeDetailModal()" class="absolute top-4 right-4 w-9 h-9 bg-black/30 hover:bg-black/50 rounded-full flex items-center justify-center text-white transition">
                        <i class="fa-solid fa-xmark"></i>
                    </button>
                    <span id="modalCategoryBadge" class="bg-white/20 backdrop-blur text-white text-[10px] font-bold px-3 py-1 rounded-full uppercase tracking-wider w-max mb-2">Olahraga</span>
                    <h2 id="modalTitle" class="text-xl font-bold">Basket Putra/Putri</h2>
                    <p id="modalSchedule" class="text-xs text-blue-100 mt-1"><i class="fa-regular fa-clock mr-1"></i> Senin, 15:30 - 17:30 WIB</p>
                </div>
                <div class="p-6 space-y-5">
                    <div class="grid grid-cols-3 gap-3 text-center">
                        <div class="bg-slate-50 p-3 rounded-2xl border border-slate-100">
                            <span class="text-[10px] text-slate-400 block font-medium">Pembina</span>
                            <span id="modalCoach" class="font-bold text-xs text-slate-800 mt-0.5 block truncate">Bpk. Ahmad R.</span>
                        </div>
                        <div class="bg-slate-50 p-3 rounded-2xl border border-slate-100">
                            <span class="text-[10px] text-slate-400 block font-medium">Kuota Tersisa</span>
                            <span id="modalQuota" class="font-bold text-xs text-successGreen mt-0.5 block">5 / 30 Kursi</span>
                        </div>
                        <div class="bg-slate-50 p-3 rounded-2xl border border-slate-100">
                            <span class="text-[10px] text-slate-400 block font-medium">Ruangan</span>
                            <span id="modalLocation" class="font-bold text-xs text-slate-800 mt-0.5 block">Lapangan Indoor</span>
                        </div>
                    </div>

                    <div>
                        <h4 class="font-bold text-slate-800 text-sm mb-1.5">Deskripsi Kegiatan</h4>
                        <p id="modalDesc" class="text-xs text-slate-600 leading-relaxed">Ekstrakurikuler bola basket melatih teknik dribble, passing, shooting, serta membangun kerjasama tim yang solid dalam kompetisi antar pelajar.</p>
                    </div>

                    <div>
                        <h4 class="font-bold text-slate-800 text-sm mb-2">Dokumentasi / Galeri</h4>
                        <div class="grid grid-cols-3 gap-2">
                            <img src="https://placehold.co/200x130/1e3a8a/ffffff?text=Aksi+1" alt="Galeri" class="rounded-xl object-cover h-20 w-full">
                            <img src="https://placehold.co/200x130/3b82f6/ffffff?text=Aksi+2" alt="Galeri" class="rounded-xl object-cover h-20 w-full">
                            <img src="https://placehold.co/200x130/10b981/ffffff?text=Aksi+3" alt="Galeri" class="rounded-xl object-cover h-20 w-full">
                        </div>
                    </div>

                    <div class="pt-3">
                        <button id="modalRegisterBtn" onclick="openRegisterForm()" class="w-full bg-primaryBlue hover:bg-blue-600 text-white font-bold py-3 px-4 rounded-2xl shadow-lg shadow-blue-500/20 transition flex items-center justify-center space-x-2">
                            <i class="fa-solid fa-user-plus"></i>
                            <span>Daftar Eskul Ini</span>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Registration Form Modal (Pre-filled for Sebastian) -->
        <div id="registerModal" class="fixed inset-0 bg-black/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
            <div class="bg-white w-full max-w-md rounded-3xl p-6 shadow-2xl animate-in fade-in zoom-in duration-200">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="font-bold text-slate-800 text-base">Formulir Pendaftaran Eskul</h3>
                    <button onclick="closeRegisterModal()" class="w-8 h-8 rounded-full bg-slate-100 flex items-center justify-center text-slate-500 hover:bg-slate-200">
                        <i class="fa-solid fa-xmark"></i>
                    </button>
                </div>
                <form id="registrationForm" onsubmit="submitRegistration(event)" class="space-y-4 text-xs">
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Nama Lengkap</label>
                        <input type="text" id="regName" value="Sebastian" readonly class="w-full bg-slate-100 border border-slate-200 rounded-xl px-3 py-2.5 text-slate-600 font-medium cursor-not-allowed">
                    </div>
                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block font-semibold text-slate-700 mb-1">Kelas</label>
                            <input type="text" id="regClass" value="XI MIPA 2" readonly class="w-full bg-slate-100 border border-slate-200 rounded-xl px-3 py-2.5 text-slate-600 font-medium cursor-not-allowed">
                        </div>
                        <div>
                            <label class="block font-semibold text-slate-700 mb-1">Nomor Induk Siswa (NIS)</label>
                            <input type="text" id="regNis" value="998214" readonly class="w-full bg-slate-100 border border-slate-200 rounded-xl px-3 py-2.5 text-slate-600 font-medium cursor-not-allowed">
                        </div>
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Ekstrakurikuler Dipilih</label>
                        <input type="text" id="regEskulName" readonly class="w-full bg-blue-50 border border-blue-200 rounded-xl px-3 py-2.5 text-navy font-bold">
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Alasan / Motivasi Bergabung</label>
                        <textarea id="regMotivation" rows="3" placeholder="Tuliskan alasan singkat bergabung..." required class="w-full bg-white border border-slate-200 rounded-xl px-3 py-2.5 text-slate-800 focus:outline-none focus:ring-2 focus:ring-primaryBlue"></textarea>
                    </div>
                    <div class="pt-2">
                        <button type="submit" class="w-full bg-successGreen hover:bg-emerald-600 text-white font-bold py-3 rounded-xl shadow-lg shadow-emerald-500/20 transition flex items-center justify-center space-x-2 text-sm">
                            <i class="fa-solid fa-paper-plane"></i>
                            <span>Kirim Pendaftaran</span>
                        </button>
                    </div>
                </form>
            </div>
        </div>

        <!-- Success Notification Popup -->
        <div id="successToast" class="fixed top-5 left-1/2 -translate-x-1/2 bg-successGreen text-white px-5 py-3 rounded-2xl shadow-xl z-50 hidden flex items-center space-x-3 animate-in fade-in slide-in-from-top duration-300">
            <i class="fa-solid fa-circle-check text-xl"></i>
            <div>
                <h4 class="font-bold text-xs">Pendaftaran Berhasil!</h4>
                <p class="text-[11px] text-emerald-100" id="successToastMsg">Sebastian resmi terdaftar di ekstrakurikuler.</p>
            </div>
        </div>

        <!-- Interactive Quiz Modal -->
        <div id="quizModal" class="fixed inset-0 bg-black/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
            <div class="bg-white w-full max-w-md rounded-3xl p-6 shadow-2xl animate-in zoom-in duration-200">
                <div class="flex justify-between items-center mb-4">
                    <span class="bg-warningOrange text-slate-900 text-[10px] font-bold px-2.5 py-0.5 rounded-full">Tes Minat & Bakat</span>
                    <button onclick="closeQuizModal()" class="w-8 h-8 rounded-full bg-slate-100 flex items-center justify-center text-slate-500">
                        <i class="fa-solid fa-xmark"></i>
                    </button>
                </div>

                <div id="quizQuestionContainer" class="space-y-4">
                    <!-- Dynamic Quiz Content -->
                </div>
            </div>
        </div>

        <!-- Add Eskul Modal (Admin) -->
        <div id="addEskulModal" class="fixed inset-0 bg-black/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
            <div class="bg-white w-full max-w-md rounded-3xl p-6 shadow-2xl">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="font-bold text-slate-800 text-base">Tambah Ekstrakurikuler Baru</h3>
                    <button onclick="closeAddEskulModal()" class="w-8 h-8 rounded-full bg-slate-100 flex items-center justify-center text-slate-500">
                        <i class="fa-solid fa-xmark"></i>
                    </button>
                </div>
                <form onsubmit="handleAddNewEskul(event)" class="space-y-3 text-xs">
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Nama Eskul</label>
                        <input type="text" id="newEskulName" required placeholder="Contoh: Robotik & AI" class="w-full bg-white border border-slate-200 rounded-xl px-3 py-2.5">
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Kategori</label>
                        <select id="newEskulCat" class="w-full bg-white border border-slate-200 rounded-xl px-3 py-2.5">
                            <option value="Teknologi">Teknologi</option>
                            <option value="Olahraga">Olahraga</option>
                            <option value="Seni & Budaya">Seni & Budaya</option>
                            <option value="Akademik">Akademik</option>
                        </select>
                    </div>
                    <div class="grid grid-cols-2 gap-2">
                        <div>
                            <label class="block font-semibold text-slate-700 mb-1">Hari</label>
                            <select id="newEskulDay" class="w-full bg-white border border-slate-200 rounded-xl px-3 py-2.5">
                                <option value="Senin">Senin</option>
                                <option value="Selasa">Selasa</option>
                                <option value="Rabu">Rabu</option>
                                <option value="Kamis">Kamis</option>
                                <option value="Jumat">Jumat</option>
                            </select>
                        </div>
                        <div>
                            <label class="block font-semibold text-slate-700 mb-1">Jam</label>
                            <input type="text" id="newEskulTime" required placeholder="15:30 - 17:00" class="w-full bg-white border border-slate-200 rounded-xl px-3 py-2.5">
                        </div>
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Nama Pembina</label>
                        <input type="text" id="newEskulCoach" required placeholder="Bpk. Budi, M.Kom" class="w-full bg-white border border-slate-200 rounded-xl px-3 py-2.5">
                    </div>
                    <div class="grid grid-cols-2 gap-2">
                        <div>
                            <label class="block font-semibold text-slate-700 mb-1">Kuota Maksimal</label>
                            <input type="number" id="newEskulQuota" required value="25" class="w-full bg-white border border-slate-200 rounded-xl px-3 py-2.5">
                        </div>
                        <div>
                            <label class="block font-semibold text-slate-700 mb-1">Ruangan</label>
                            <input type="text" id="newEskulLoc" required value="Lab Komputer 1" class="w-full bg-white border border-slate-200 rounded-xl px-3 py-2.5">
                        </div>
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Deskripsi Singkat</label>
                        <textarea id="newEskulDesc" rows="2" required placeholder="Deskripsi eskul..." class="w-full bg-white border border-slate-200 rounded-xl px-3 py-2.5"></textarea>
                    </div>
                    <button type="submit" class="w-full bg-navy text-white font-bold py-3 rounded-xl shadow mt-2">Simpan Ekstrakurikuler</button>
                </form>
            </div>
        </div>

    </div>

    <script>
        // Initial Mock Database for Extracurriculars
        let eskulData = [
            {
                id: 1,
                name: 'Basket Putra/Putri',
                category: 'Olahraga',
                day: 'Senin',
                time: '15:30 - 17:30',
                coach: 'Bpk. Ahmad R.',
                quotaTotal: 30,
                quotaFilled: 25,
                location: 'Lapangan Indoor',
                desc: 'Ekstrakurikuler bola basket melatih teknik dribble, passing, shooting, serta membangun kerjasama tim yang solid dalam kompetisi antar pelajar.',
                image: 'https://placehold.co/400x250/1e3a8a/ffffff?text=Basket'
            },
            {
                id: 2,
                name: 'Futsal Club',
                category: 'Olahraga',
                day: 'Selasa',
                time: '16:00 - 18:00',
                coach: 'Bpk. Deni Setiawan',
                quotaTotal: 25,
                quotaFilled: 25, // Full quota test
                location: 'Lapangan Sekolah',
                desc: 'Futsal sekolah memfokuskan taktik permainan cepat, ketahanan fisik, dan partisipasi turnamen tingkat kota.',
                image: 'https://placehold.co/400x250/3b82f6/ffffff?text=Futsal'
            },
            {
                id: 3,
                name: 'Paduan Suara & Musik',
                category: 'Seni & Budaya',
                day: 'Rabu',
                time: '15:00 - 17:00',
                coach: 'Ibu Siska Melati',
                quotaTotal: 35,
                quotaFilled: 18,
                location: 'Ruang Musik',
                desc: 'Mengembangkan olah vokal, harmoni suara, serta memainkan alat musik ansambel untuk acara resmi sekolah.',
                image: 'https://placehold.co/400x250/8b5cf6/ffffff?text=Paduan+Suara'
            },
            {
                id: 4,
                name: 'Coding & Web Dev',
                category: 'Teknologi',
                day: 'Kamis',
                time: '15:30 - 17:30',
                coach: 'Bpk. Hendra Pratama',
                quotaTotal: 20,
                quotaFilled: 12,
                location: 'Lab Komputer 2',
                desc: 'Belajar HTML, CSS, JavaScript, dan dasar kecerdasan buatan (AI) untuk mencetak programmer muda berbakat.',
                image: 'https://placehold.co/400x250/10b981/ffffff?text=Coding'
            },
            {
                id: 5,
                name: 'English Debate Club',
                category: 'Akademik',
                day: 'Jumat',
                time: '14:00 - 16:00',
                coach: 'Ms. Sarah Jenkins',
                quotaTotal: 20,
                quotaFilled: 8,
                location: 'Ruang Bahasa',
                desc: 'Melatih kemampuan public speaking, argumentasi kritis, dan teknik debat bahasa Inggris standar internasional.',
                image: 'https://placehold.co/400x250/f59e0b/ffffff?text=Debate'
            }
        ];

        // User registered eskul list for Sebastian
        let userRegisteredEskuls = [1]; // Basket by default

        // Current filter states
        let currentCategory = 'Semua';
        let currentDay = 'Senin';
        let activeModalEskulId = null;

        // Quiz State
        let quizStep = 0;
        let quizAnswers = { interest: '', style: '' };

        window.addEventListener('DOMContentLoaded', () => {
            renderAll();
        });

        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
            document.getElementById('tab-' + tabId).classList.add('active');

            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('text-primaryBlue');
                btn.classList.add('text-slate-400');
                if(btn.getAttribute('data-target') === tabId) {
                    btn.classList.remove('text-slate-400');
                    btn.classList.add('text-primaryBlue');
                }
            });

            document.getElementById('mainScrollArea').scrollTo({ top: 0, behavior: 'smooth' });
            renderAll();
        }

        function renderAll() {
            renderTodaySchedule();
            renderPopularEskul();
            renderFullEskulList();
            renderScheduleList();
            renderMyProfileEskuls();
            renderAdminDashboard();
        }

        function renderTodaySchedule() {
            const container = document.getElementById('todayScheduleContainer');
            // Assuming today is Monday or matching day
            const todayEskuls = eskulData.filter(e => e.day === 'Senin');
            
            if(todayEskuls.length === 0) {
                container.innerHTML = `<p class="text-xs text-slate-400 italic">Tidak ada jadwal eskul hari ini.</p>`;
                return;
            }

            container.innerHTML = todayEskuls.map(e => `
                <div class="bg-white p-3.5 rounded-2xl shadow-sm border border-slate-100 flex items-center justify-between">
                    <div class="flex items-center space-x-3">
                        <div class="w-10 h-10 rounded-xl bg-blue-50 text-primaryBlue flex items-center justify-center font-bold text-sm">
                            <i class="fa-solid fa-clock"></i>
                        </div>
                        <div>
                            <h4 class="font-bold text-slate-800 text-xs">${e.name}</h4>
                            <p class="text-[11px] text-slate-500">${e.time} • ${e.location}</p>
                        </div>
                    </div>
                    <span class="text-[10px] bg-emerald-50 text-successGreen font-bold px-2.5 py-1 rounded-full">Hari Ini</span>
                </div>
            `).join('');
        }

        function renderPopularEskul() {
            const container = document.getElementById('popularEskulContainer');
            const popular = eskulData.slice(0, 4);

            container.innerHTML = popular.map(e => `
                <div onclick="openDetailModal(${e.id})" class="bg-white p-3 rounded-2xl shadow-sm border border-slate-100 cursor-pointer hover:border-primaryBlue transition group">
                    <div class="h-24 rounded-xl overflow-hidden mb-2 relative">
                        <img src="${e.image}" alt="${e.name}" class="w-full h-full object-cover group-hover:scale-105 transition duration-300">
                        <span class="absolute top-2 right-2 bg-black/40 backdrop-blur text-white text-[9px] px-2 py-0.5 rounded-full font-medium">${e.category}</span>
                    </div>
                    <h4 class="font-bold text-slate-800 text-xs truncate">${e.name}</h4>
                    <p class="text-[10px] text-slate-400 mt-0.5 truncate"><i class="fa-solid fa-user-tie mr-1"></i>${e.coach}</p>
                </div>
            `).join('');
        }

        function filterCategory(cat) {
            currentCategory = cat;
            document.querySelectorAll('.cat-btn').forEach(btn => {
                if(btn.textContent.trim() === cat) {
                    btn.classList.remove('bg-white', 'text-slate-600', 'border');
                    btn.classList.add('bg-navy', 'text-white', 'shadow-sm');
                } else {
                    btn.classList.remove('bg-navy', 'text-white', 'shadow-sm');
                    btn.classList.add('bg-white', 'text-slate-600', 'border', 'border-slate-200');
                }
            });
            renderFullEskulList();
        }

        function renderFullEskulList() {
            const container1 = document.getElementById('fullEskulListContainer');
            const container2 = document.getElementById('allEskulListContainer2');
            document.getElementById('totalEskulBadge').textContent = eskulData.length + ' Aktif';

            let filtered = eskulData;
            if(currentCategory !== 'Semua') {
                filtered = eskulData.filter(e => e.category === currentCategory);
            }

            const htmlContent = filtered.map(e => {
                const isFull = e.quotaFilled >= e.quotaTotal;
                const isRegistered = userRegisteredEskuls.includes(e.id);
                return `
                    <div onclick="openDetailModal(${e.id})" class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100 hover:border-primaryBlue transition cursor-pointer flex items-center justify-between">
                        <div class="flex items-center space-x-3.5">
                            <img src="${e.image}" class="w-14 h-14 rounded-xl object-cover shadow-sm">
                            <div>
                                <span class="text-[10px] font-semibold text-primaryBlue bg-blue-50 px-2 py-0.5 rounded-full">${e.category}</span>
                                <h4 class="font-bold text-slate-800 text-sm mt-1">${e.name}</h4>
                                <p class="text-[11px] text-slate-500 mt-0.5"><i class="fa-regular fa-clock mr-1"></i>${e.day}, ${e.time}</p>
                            </div>
                        </div>
                        <div class="text-right">
                            ${isRegistered ? 
                                `<span class="bg-emerald-100 text-successGreen text-[10px] font-bold px-2.5 py-1 rounded-full">Terdaftar</span>` :
                                isFull ? 
                                `<span class="bg-amber-100 text-warningOrange text-[10px] font-bold px-2.5 py-1 rounded-full">Penuh</span>` :
                                `<span class="bg-blue-50 text-primaryBlue text-[10px] font-bold px-2.5 py-1 rounded-full">Tersedia</span>`
                            }
                            <span class="block text-[10px] text-slate-400 mt-1">Kuota: ${e.quotaFilled}/${e.quotaTotal}</span>
                        </div>
                    </div>
                `;
            }).join('');

            if(container1) container1.innerHTML = htmlContent;
            if(container2) container2.innerHTML = htmlContent;
        }

        function filterDay(day) {
            currentDay = day;
            document.querySelectorAll('.day-tab').forEach(btn => {
                if(btn.textContent.trim() === day) {
                    btn.classList.add('bg-navy', 'text-white', 'shadow-sm');
                    btn.classList.remove('text-slate-600', 'hover:bg-slate-100');
                } else {
                    btn.classList.remove('bg-navy', 'text-white', 'shadow-sm');
                    btn.classList.add('text-slate-600', 'hover:bg-slate-100');
                }
            });
            renderScheduleList();
        }

        function renderScheduleList() {
            const container = document.getElementById('scheduleListContainer');
            const dayEskuls = eskulData.filter(e => e.day === currentDay);

            if(dayEskuls.length === 0) {
                container.innerHTML = `<div class="bg-white p-6 rounded-2xl text-center text-slate-400 text-xs border border-slate-100">Tidak ada kegiatan ekstrakurikuler pada hari ${currentDay}.</div>`;
                return;
            }

            container.innerHTML = dayEskuls.map(e => `
                <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100 flex items-center justify-between">
                    <div class="flex items-center space-x-3">
                        <div class="w-12 h-12 rounded-2xl bg-amber-50 text-warningOrange flex items-center justify-center font-bold text-base">
                            <i class="fa-solid fa-calendar-day"></i>
                        </div>
                        <div>
                            <h4 class="font-bold text-slate-800 text-xs">${e.name}</h4>
                            <p class="text-[11px] text-slate-500 mt-0.5"><i class="fa-regular fa-clock mr-1"></i>${e.time} WIB</p>
                            <p class="text-[10px] text-slate-400 mt-0.5"><i class="fa-solid fa-location-dot mr-1"></i>${e.location} • <i class="fa-solid fa-user-tie ml-1"></i>${e.coach}</p>
                        </div>
                    </div>
                    <button onclick="openDetailModal(${e.id})" class="bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs px-3 py-2 rounded-xl font-medium transition">Detail</button>
                </div>
            `).join('');
        }

        function renderMyProfileEskuls() {
            const container = document.getElementById('myEskulContainer');
            document.getElementById('userRegisteredCount').textContent = userRegisteredEskuls.length + ' Eskul';

            const myEskuls = eskulData.filter(e => userRegisteredEskuls.includes(e.id));

            container.innerHTML = myEskuls.map(e => `
                <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100 flex items-center justify-between">
                    <div class="flex items-center space-x-3">
                        <img src="${e.image}" class="w-12 h-12 rounded-xl object-cover">
                        <div>
                            <h4 class="font-bold text-slate-800 text-xs">${e.name}</h4>
                            <p class="text-[11px] text-slate-500">${e.day}, ${e.time}</p>
                        </div>
                    </div>
                    <span class="bg-emerald-50 text-successGreen text-[10px] font-bold px-3 py-1 rounded-full">Aktif</span>
                </div>
            `).join('');
        }

        function renderAdminDashboard() {
            const container = document.getElementById('adminEskulListContainer');

            container.innerHTML = eskulData.map(e => `
                <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100 flex items-center justify-between">
                    <div>
                        <div class="flex items-center space-x-2">
                            <h4 class="font-bold text-slate-800 text-xs">${e.name}</h4>
                            <span class="text-[9px] bg-slate-100 text-slate-600 px-2 py-0.5 rounded-full">${e.category}</span>
                        </div>
                        <p class="text-[11px] text-slate-500 mt-1">Pembina: <span class="font-semibold text-slate-700">${e.coach}</span></p>
                        <p class="text-[10px] text-slate-400 mt-0.5">Kuota: <strong class="${e.quotaFilled >= e.quotaTotal ? 'text-warningOrange' : 'text-successGreen'}">${e.quotaFilled}</strong> / ${e.quotaTotal} Peserta</p>
                    </div>
                    <div class="flex items-center space-x-1.5">
                        <button onclick="increaseQuota(${e.id})" title="Tambah Kuota" class="w-8 h-8 rounded-xl bg-blue-50 text-primaryBlue flex items-center justify-center hover:bg-blue-100 transition"><i class="fa-solid fa-plus text-xs"></i></button>
                        <button onclick="deleteEskul(${e.id})" title="Hapus Eskul" class="w-8 h-8 rounded-xl bg-rose-50 text-rose-500 flex items-center justify-center hover:bg-rose-100 transition"><i class="fa-solid fa-trash text-xs"></i></button>
                    </div>
                </div>
            `).join('');
        }

        // Modal Handlers
        function openDetailModal(id) {
            activeModalEskulId = id;
            const e = eskulData.find(item => item.id === id);
            if(!e) return;

            document.getElementById('modalCategoryBadge').textContent = e.category;
            document.getElementById('modalTitle').textContent = e.name;
            document.getElementById('modalSchedule').innerHTML = `<i class="fa-regular fa-clock mr-1"></i> ${e.day}, ${e.time} WIB`;
            document.getElementById('modalCoach').textContent = e.coach;
            document.getElementById('modalQuota').textContent = `${e.quotaFilled} / ${e.quotaTotal} Kursi`;
            document.getElementById('modalLocation').textContent = e.location;
            document.getElementById('modalDesc').textContent = e.desc;

            const regBtn = document.getElementById('modalRegisterBtn');
            if(userRegisteredEskuls.includes(e.id)) {
                regBtn.innerHTML = `<i class="fa-solid fa-check"></i><span>Anda Sudah Terdaftar</span>`;
                regBtn.className = "w-full bg-slate-200 text-slate-500 font-bold py-3 px-4 rounded-2xl cursor-not-allowed flex items-center justify-center space-x-2";
                regBtn.disabled = true;
            } else if(e.quotaFilled >= e.quotaTotal) {
                regBtn.innerHTML = `<i class="fa-solid fa-ban"></i><span>Kuota Penuh</span>`;
                regBtn.className = "w-full bg-amber-100 text-warningOrange font-bold py-3 px-4 rounded-2xl cursor-not-allowed flex items-center justify-center space-x-2";
                regBtn.disabled = true;
            } else {
                regBtn.innerHTML = `<i class="fa-solid fa-user-plus"></i><span>Daftar Eskul Ini</span>`;
                regBtn.className = "w-full bg-primaryBlue hover:bg-blue-600 text-white font-bold py-3 px-4 rounded-2xl shadow-lg shadow-blue-500/20 transition flex items-center justify-center space-x-2";
                regBtn.disabled = false;
            }

            document.getElementById('detailModal').classList.remove('hidden');
        }

        function closeDetailModal() {
            document.getElementById('detailModal').classList.add('hidden');
        }

        function openRegisterForm() {
            const e = eskulData.find(item => item.id === activeModalEskulId);
            if(!e) return;
            document.getElementById('regEskulName').value = e.name;
            closeDetailModal();
            document.getElementById('registerModal').classList.remove('hidden');
        }

        function closeRegisterModal() {
            document.getElementById('registerModal').classList.add('hidden');
        }

        function submitRegistration(event) {
            event.preventDefault();
            const e = eskulData.find(item => item.id === activeModalEskulId);
            if(e) {
                userRegisteredEskuls.push(e.id);
                e.quotaFilled += 1;
            }
            closeRegisterModal();
            renderAll();

            // Show success toast
            const toast = document.getElementById('successToast');
            document.getElementById('successToastMsg').textContent = `Sebastian berhasil terdaftar di ${e ? e.name : 'ekstrakurikuler'}.`;
            toast.classList.remove('hidden');
            setTimeout(() => {
                toast.classList.add('hidden');
            }, 3500);
        }

        // Quiz Minat & Bakat Logic
        function openQuizModal() {
            quizStep = 1;
            renderQuizStep();
            document.getElementById('quizModal').classList.remove('hidden');
        }

        function closeQuizModal() {
            document.getElementById('quizModal').classList.add('hidden');
        }

        function renderQuizStep() {
            const container = document.getElementById('quizQuestionContainer');
            if(quizStep === 1) {
                container.innerHTML = `
                    <h4 class="font-bold text-slate-800 text-sm mb-2">Pertanyaan 1/2: Apa aktivitas kesukaanmu di waktu luang?</h4>
                    <div class="space-y-2">
                        <button onclick="answerQuiz('Olahraga')" class="w-full text-left p-3 bg-slate-50 hover:bg-blue-50 hover:text-primaryBlue border border-slate-200 rounded-xl font-medium transition text-xs">⚽ Berolahraga & Aktivitas Fisik di Lapangan</button>
                        <button onclick="answerQuiz('Seni & Budaya')" class="w-full text-left p-3 bg-slate-50 hover:bg-blue-50 hover:text-primaryBlue border border-slate-200 rounded-xl font-medium transition text-xs">🎨 Menggambar, Musik, atau Seni Pertunjukan</button>
                        <button onclick="answerQuiz('Teknologi')" class="w-full text-left p-3 bg-slate-50 hover:bg-blue-50 hover:text-primaryBlue border border-slate-200 rounded-xl font-medium transition text-xs">💻 Bermain Komputer & Belajar Teknologi</button>
                        <button onclick="answerQuiz('Akademik')" class="w-full text-left p-3 bg-slate-50 hover:bg-blue-50 hover:text-primaryBlue border border-slate-200 rounded-xl font-medium transition text-xs">📚 Membaca, Berdebat, & Berpikir Kritis</button>
                    </div>
                `;
            } else if(quizStep === 2) {
                container.innerHTML = `
                    <h4 class="font-bold text-slate-800 text-sm mb-2">Pertanyaan 2/2: Bagaimana gaya kerja tim favoritmu?</h4>
                    <div class="space-y-2">
                        <button onclick="finishQuiz('Dinamis')" class="w-full text-left p-3 bg-slate-50 hover:bg-emerald-50 hover:text-successGreen border border-slate-200 rounded-xl font-medium transition text-xs">🔥 Energik, kompetitif, dan bergerak aktif</button>
                        <button onclick="finishQuiz('Kreatif')" class="w-full text-left p-3 bg-slate-50 hover:bg-emerald-50 hover:text-successGreen border border-slate-200 rounded-xl font-medium transition text-xs">✨ Kreatif, ekspresif, dan santai</button>
                        <button onclick="finishQuiz('Analitis')" class="w-full text-left p-3 bg-slate-50 hover:bg-emerald-50 hover:text-successGreen border border-slate-200 rounded-xl font-medium transition text-xs">🧠 Fokus memecahkan masalah & logika</button>
                    </div>
                `;
            } else if(quizStep === 3) {
                // Results matching calculation
                container.innerHTML = `
                    <div class="text-center py-4 space-y-3">
                        <div class="w-16 h-16 bg-emerald-100 text-successGreen rounded-full flex items-center justify-center text-2xl mx-auto">
                            <i class="fa-solid fa-award"></i>
                        </div>
                        <h4 class="font-bold text-slate-800 text-base">Hasil Tes Minat Sebastian!</h4>
                        <p class="text-xs text-slate-500">Berdasarkan jawaban Anda, berikut rekomendasi eskul paling cocok:</p>
                        <div class="bg-blue-50 p-4 rounded-2xl border border-blue-100 text-left space-y-2">
                            <div class="flex justify-between items-center font-bold text-xs text-navy">
                                <span>🏀 Basket Putra/Putri</span>
                                <span class="bg-primaryBlue text-white px-2 py-0.5 rounded-full text-[10px]">92% Cocok</span>
                            </div>
                            <div class="flex justify-between items-center font-bold text-xs text-navy">
                                <span>💻 Coding & Web Dev</span>
                                <span class="bg-successGreen text-white px-2 py-0.5 rounded-full text-[10px]">88% Cocok</span>
                            </div>
                        </div>
                        <button onclick="closeQuizModal(); switchTab('cari');" class="w-full bg-navy text-white font-bold py-2.5 rounded-xl shadow text-xs">Lihat Detail Eskul</button>
                    </div>
                `;
            }
        }

        function answerQuiz(val) {
            quizAnswers.interest = val;
            quizStep = 2;
            renderQuizStep();
        }

        function finishQuiz(val) {
            quizAnswers.style = val;
            quizStep = 3;
            renderQuizStep();
        }

        // Admin Actions
        function openAddEskulModal() {
            document.getElementById('addEskulModal').classList.remove('hidden');
        }

        function closeAddEskulModal() {
            document.getElementById('addEskulModal').classList.add('hidden');
        }

        function handleAddNewEskul(event) {
            event.preventDefault();
            const newObj = {
                id: eskulData.length + 1,
                name: document.getElementById('newEskulName').value,
                category: document.getElementById('newEskulCat').value,
                day: document.getElementById('newEskulDay').value,
                time: document.getElementById('newEskulTime').value,
                coach: document.getElementById('newEskulCoach').value,
                quotaTotal: parseInt(document.getElementById('newEskulQuota').value),
                quotaFilled: 0,
                location: document.getElementById('newEskulLoc').value,
                desc: document.getElementById('newEskulDesc').value,
                image: 'https://placehold.co/400x250/334155/ffffff?text=' + encodeURIComponent(document.getElementById('newEskulName').value)
            };
            eskulData.push(newObj);
            closeAddEskulModal();
            renderAll();

            const toast = document.getElementById('successToast');
            document.getElementById('successToastMsg').textContent = `Ekstrakurikuler ${newObj.name} berhasil ditambahkan!`;
            toast.classList.remove('hidden');
            setTimeout(() => toast.classList.add('hidden'), 3000);
        }

        function increaseQuota(id) {
            const e = eskulData.find(item => item.id === id);
            if(e) {
                e.quotaTotal += 5;
                renderAll();
            }
        }

        function deleteEskul(id) {
            if(confirm("Yakin ingin menghapus ekstrakurikuler ini?")) {
                eskulData = eskulData.filter(item => item.id !== id);
                renderAll();
            }
        }

        function openBroadcastModal() {
            alert("Fitur broadcast pengumuman berhasil dibuka. Pesan akan dikirimkan ke seluruh perangkat siswa.");
        }

        // Global search handler
        function handleGlobalSearch(query) {
            if(!query) return;
            const q = query.toLowerCase();
            const found = eskulData.find(e => e.name.toLowerCase().includes(q) || e.coach.toLowerCase().includes(q));
            if(found) {
                openDetailModal(found.id);
            }
        }
    </script>
</body>
</html>
