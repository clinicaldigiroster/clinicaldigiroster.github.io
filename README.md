<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>Clinical Tracker Mobile</title>
    
    <!-- Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>

    <!-- Config -->
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: { sans: ['Inter', 'sans-serif'] },
                    colors: {
                        brand: {
                            50: '#eef2ff',
                            100: '#e0e7ff',
                            500: '#6366f1',
                            600: '#4f46e5',
                            700: '#4338ca',
                        }
                    },
                    boxShadow: {
                        'soft': '0 4px 20px -2px rgba(0, 0, 0, 0.05)',
                        'nav': '0 -4px 20px rgba(0,0,0,0.03)',
                        'float': '0 10px 30px -5px rgba(79, 70, 229, 0.3)'
                    }
                }
            }
        }
    </script>

    <style>
        html { -webkit-tap-highlight-color: transparent; scroll-behavior: smooth; }
        
        /* Native scrolling for reliability */
        body { 
            background-color: #f8fafc;
            min-height: 100vh;
            /* Ensure bottom nav doesn't cover content */
            padding-bottom: 100px; 
            padding-top: 60px;
        }
        
        /* Utilities */
        .calendar-grid { 
            display: grid; 
            grid-template-columns: repeat(7, 1fr); 
            gap: 6px; 
        }
        
        .fade-in { 
            animation: fadeIn 0.4s ease-out forwards; 
            opacity: 0;
            transform: translateY(10px);
        }
        @keyframes fadeIn { 
            to { opacity: 1; transform: translateY(0); } 
        }

        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }

        /* Safe Area Support */
        .pb-safe { padding-bottom: env(safe-area-inset-bottom); }
        .pt-safe { padding-top: env(safe-area-inset-top); }
    </style>
</head>
<body class="text-slate-900 selection:bg-brand-100 relative">

    <!-- TOP BAR (Fixed) -->
    <header class="fixed top-0 inset-x-0 h-16 bg-white/90 backdrop-blur-md border-b border-slate-200 flex items-center justify-between px-5 z-40 pt-safe transition-all shadow-sm">
        <h1 id="header-title" class="font-bold text-lg text-slate-800">Dashboard</h1>
        <button onclick="toggleProfileModal()" class="w-9 h-9 rounded-full bg-brand-50 text-brand-600 flex items-center justify-center text-xs font-bold border border-brand-100 shadow-sm active:scale-95 transition-transform">
            ME
        </button>
    </header>

    <!-- MAIN CONTENT -->
    <main id="main-container" class="px-4 pt-2">
        <!-- Injected via JS -->
    </main>

    <!-- SCROLL TO TOP BUTTON -->
    <button id="scrollTopBtn" onclick="window.scrollTo(0,0)" class="fixed bottom-24 right-5 z-30 bg-white text-brand-600 p-3 rounded-full shadow-lg border border-slate-100 opacity-0 translate-y-10 transition-all duration-300 pointer-events-none active:scale-90">
        <i data-lucide="arrow-up" class="w-5 h-5"></i>
    </button>

    <!-- BOTTOM NAV (Fixed - Reverted Style) -->
    <nav class="fixed bottom-0 inset-x-0 h-[80px] bg-white border-t border-slate-100 shadow-nav flex justify-around items-center px-2 pb-2 z-50 pb-safe">
        <button onclick="switchTab('home')" class="nav-btn group flex flex-col items-center justify-center w-16 h-full text-brand-600" data-tab="home">
            <div class="p-1.5 rounded-xl group-hover:bg-slate-50 transition-colors">
                <i data-lucide="layout-dashboard" class="w-6 h-6 mb-1 transition-transform group-active:scale-95"></i>
            </div>
            <span class="text-[10px] font-medium">Dash</span>
        </button>
        
        <button onclick="switchTab('calendar')" class="nav-btn group flex flex-col items-center justify-center w-16 h-full text-slate-400" data-tab="calendar">
            <div class="p-1.5 rounded-xl group-hover:bg-slate-50 transition-colors">
                <i data-lucide="calendar" class="w-6 h-6 mb-1 transition-transform group-active:scale-95"></i>
            </div>
            <span class="text-[10px] font-medium">Schedule</span>
        </button>

        <!-- Floating Center Button -->
        <button onclick="switchTab('requirements')" class="nav-btn group flex flex-col items-center justify-center w-16 h-full text-slate-400 relative" data-tab="requirements">
            <div class="bg-brand-600 text-white p-3.5 rounded-2xl -mt-8 shadow-lg shadow-brand-500/40 border-[4px] border-[#f8fafc] transition-transform group-active:scale-95 active:shadow-none">
                <i data-lucide="clipboard-list" class="w-6 h-6"></i>
            </div>
            <span class="text-[10px] font-medium mt-1">Checklists</span>
        </button>

        <button onclick="switchTab('friends')" class="nav-btn group flex flex-col items-center justify-center w-16 h-full text-slate-400" data-tab="friends">
            <div class="p-1.5 rounded-xl group-hover:bg-slate-50 transition-colors">
                <i data-lucide="users" class="w-6 h-6 mb-1 transition-transform group-active:scale-95"></i>
            </div>
            <span class="text-[10px] font-medium">Directory</span>
        </button>
        
        <button onclick="switchTab('profile')" class="nav-btn group flex flex-col items-center justify-center w-16 h-full text-slate-400" data-tab="profile">
            <div class="p-1.5 rounded-xl group-hover:bg-slate-50 transition-colors">
                <i data-lucide="user" class="w-6 h-6 mb-1 transition-transform group-active:scale-95"></i>
            </div>
            <span class="text-[10px] font-medium">Profile</span>
        </button>
    </nav>

    <!-- PROFILE MODAL -->
    <div id="profile-modal" class="fixed inset-0 z-[100] hidden">
        <div class="absolute inset-0 bg-black/40 backdrop-blur-sm transition-opacity opacity-0" id="modal-backdrop" onclick="toggleProfileModal()"></div>
        <div class="absolute bottom-0 inset-x-0 bg-white rounded-t-[32px] p-6 transition-transform transform translate-y-full duration-300 shadow-2xl max-h-[85vh] flex flex-col pb-safe" id="profile-sheet-content">
            <div class="w-12 h-1.5 bg-slate-200 rounded-full mx-auto mb-6 flex-none"></div>
            <h2 class="text-xl font-bold text-slate-800 mb-2 flex-none">Select Student</h2>
            
            <div class="flex-none mb-4 relative">
                <i data-lucide="search" class="absolute left-4 top-3.5 w-5 h-5 text-slate-400"></i>
                <input type="text" id="modal-search" placeholder="Search name or reg..." 
                    class="w-full bg-slate-100 border-none pl-12 pr-4 py-3 rounded-xl text-sm focus:ring-2 focus:ring-brand-500">
            </div>

            <div class="flex-1 overflow-y-auto no-scrollbar space-y-1" id="user-selector-list">
                <!-- Users injected here -->
            </div>
        </div>
    </div>

    <!-- SCRIPT -->
    <script>
        // ==================== DATABASE ====================

        const DATE_RANGES = [
            { id: 0, label: '23 Dec - 02 Jan', start: '2025-12-23', end: '2026-01-02' },
            { id: 1, label: '03 Jan - 05 Jan', start: '2026-01-03', end: '2026-01-05' },
            { id: 2, label: '06 Jan - 07 Jan', start: '2026-01-06', end: '2026-01-07' },
            { id: 3, label: '08 Jan - 09 Jan', start: '2026-01-08', end: '2026-01-09' },
            { id: 4, label: '10 Jan - 12 Jan', start: '2026-01-10', end: '2026-01-12' },
            { id: 5, label: '19 Jan - 20 Jan', start: '2026-01-19', end: '2026-01-20' },
            { id: 6, label: '21 Jan - 22 Jan', start: '2026-01-21', end: '2026-01-22' },
            { id: 7, label: '23 Jan - 24 Jan', start: '2026-01-23', end: '2026-01-24' },
            { id: 8, label: '27 Jan - 28 Jan', start: '2026-01-27', end: '2026-01-28' },
            { id: 9, label: '29 Jan - 30 Jan', start: '2026-01-29', end: '2026-01-30' },
        ];

        const LOCATIONS = [
            "OPD GROUND FLOOR", "EMERGENCY ROOM", "PICU", "NICU", "DEIC/ FEVER WARD",
            "MEDICAL WARD 3rd FLOOR", "SURGICAL WARD 7th FLOOR", "OT/8th FLOOR",
            "MEDICAL WARD 5th FLOOR", "MEDICAL WARD 4th FLOOR"
        ];

        const GROUP_PATTERNS = {
            1: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
            2: [4, 0, 1, 2, 3, 9, 5, 6, 7, 8],
            3: [3, 4, 0, 1, 2, 8, 9, 5, 6, 7],
            4: [2, 3, 4, 0, 1, 7, 8, 9, 5, 6],
        };

        const STUDENTS = [
            { id: 1, reg: "232131104063", name: "PAVITHRA E", group: 1 },
            { id: 2, reg: "232131104064", name: "PRIYA NANDHANA S", group: 1 },
            { id: 3, reg: "232131104065", name: "PRIYADHARSHINI E", group: 1 },
            { id: 4, reg: "232131104066", name: "PRIYANTH P", group: 1 },
            { id: 5, reg: "232131104067", name: "RAGAVAN V", group: 1 },
            { id: 6, reg: "232131104068", name: "RAGUL RAVI R U", group: 2 },
            { id: 7, reg: "232131104069", name: "RAKSHAN S", group: 2 },
            { id: 8, reg: "232131104070", name: "RENUGAMBAL M", group: 2 },
            { id: 9, reg: "232131104071", name: "RIYAS AHAMED R", group: 2 },
            { id: 10, reg: "232131104072", name: "RIYAS MOHAMAD A", group: 2 },
            { id: 11, reg: "232131104073", name: "RODRIC DELSIN", group: 3 },
            { id: 12, reg: "232131104074", name: "ROMAL ROY", group: 3 },
            { id: 13, reg: "232131104075", name: "SAHANA V", group: 3 },
            { id: 14, reg: "232131104076", name: "SALONI B", group: 3 },
            { id: 15, reg: "232131104077", name: "SAMSON SMITH M", group: 3 },
            { id: 16, reg: "232131104078", name: "SANDHIYA I", group: 4 },
            { id: 17, reg: "232131104079", name: "SANDHIYA JAYAKUMAR", group: 4 },
            { id: 18, reg: "232131104080", name: "SANDHIYA JOSEPH", group: 4 },
            { id: 19, reg: "232131104081", name: "SANDHIYA L", group: 4 },
            { id: 20, reg: "232131104082", name: "SANDHIYA T", group: 4 },
        ];

        const CLINICAL_DATA = [
            {
                id: 'med-3',
                name: 'Medical Ward (3rd Floor)',
                locationMatch: "MEDICAL WARD 3rd FLOOR",
                logbook: [
                    { id: 1, text: 'Growth & Development - Newborn' },
                    { id: 2, text: 'Growth & Development - Infant' },
                    { id: 3, text: 'Growth & Development - Toddler' },
                    { id: 4, text: 'Growth & Development - Preschooler' },
                    { id: 5, text: 'Growth & Development - Schooler' },
                    { id: 6, text: 'Growth & Development - Adolescent' },
                    { id: 7, text: 'Play therapy' }
                ],
                files: [
                    { id: 'f_title', text: 'Growth & Development File' },
                    { id: 'f2', text: 'Section: Infant' },
                    { id: 'f3', text: 'Section: Toddler' },
                    { id: 'f4', text: 'Section: Preschooler' },
                    { id: 'f5', text: 'Section: Schooler' },
                    { id: 'f6', text: 'Section: Adolescent' }
                ]
            },
            {
                id: 'med-4',
                name: 'Medical Ward (4th Floor)',
                locationMatch: "MEDICAL WARD 4th FLOOR",
                logbook: [
                    { id: 8, text: 'Weaning' },
                    { id: 9, text: 'Diet Planning - PEM, PSGN, NS, JDM' },
                    { id: 10, text: 'Collection of Specimen' },
                    { id: 11, text: 'Baby bath' },
                    { id: 12, text: 'Tepid Sponge' },
                    { id: 13, text: 'Dehydration Assessment' },
                    { id: 14, text: 'Urinary Catheterization' }
                ],
                files: [ { id: 'f_case_med', text: 'Medical Case Study' } ]
            },
            {
                id: 'med-5',
                name: 'Medical Ward (5th Floor)',
                locationMatch: "MEDICAL WARD 5th FLOOR",
                logbook: [
                    { id: 15, text: 'Administration of Medication' },
                    { id: 16, text: 'IV Fluids - Calculations' },
                    { id: 17, text: 'Chest Physiotherapy' },
                    { id: 18, text: 'Breast feeding' },
                    { id: 19, text: 'Preservation of milk' },
                    { id: 20, text: 'Care of child on ventilator' },
                    { id: 21, text: 'Endotracheal Suctioning' },
                    { id: 22, text: 'Bowel Wash' }
                ],
                files: [ { id: 'f_pres_med', text: 'Case Presentation' } ]
            },
            {
                id: 'med-6',
                name: 'Medical Ward (6th Floor)',
                locationMatch: null, 
                logbook: [
                    { id: 23, text: 'Colostomy Irrigation' },
                    { id: 24, text: 'Uterostomy Care' },
                    { id: 25, text: 'Gastrostomy Care' },
                    { id: 26, text: 'Enterostomy Care' },
                    { id: 27, text: 'Cleaning & Sterilization' },
                    { id: 28, text: 'Formula Preparation' },
                    { id: 29, text: 'Surgical Dressing' }
                ],
                files: [ { id: 'f_careplan_med', text: 'Care Plan - Medical' } ]
            },
            {
                id: 'surg-7',
                name: 'Surgical Ward (7th Floor)',
                locationMatch: "SURGICAL WARD 7th FLOOR",
                logbook: [
                    { id: 30, text: 'Suture Removal' },
                    { id: 31, text: 'Burns Assessment' },
                    { id: 32, text: 'Child With Cast/Splint' },
                    { id: 33, text: 'Lumbar Puncture' },
                    { id: 34, text: 'Bonemarrow Aspiration' }
                ],
                files: [
                    { id: 'f_careplan_surg', text: 'Care Plan - Surgical' },
                    { id: 'f_casestudy_surg', text: 'Case Study - Surgical' }
                ]
            },
            {
                id: 'opd-g',
                name: 'OPD (Ground Floor)',
                locationMatch: "OPD GROUND FLOOR",
                logbook: [
                    { id: 35, text: 'Length/Height' },
                    { id: 36, text: 'Weight' },
                    { id: 37, text: 'Head circumference' },
                    { id: 38, text: 'Chest Circumference' },
                    { id: 39, text: 'Midarm Circumference' },
                    { id: 40, text: 'Abdominal Circumference' },
                    { id: 41, text: 'Skin Fold Thickness' },
                    { id: 42, text: 'Body Mass Index' }
                ],
                files: [ { id: 'f_health_ed', text: 'Health Education' } ]
            },
            {
                id: 'opd-2',
                name: 'OPD (2nd Floor)',
                locationMatch: null,
                logbook: [
                    { id: 43, text: 'Vital signs - TPR, BP, O2' },
                    { id: 44, text: 'Pain Assessment' },
                    { id: 45, text: 'Immunization' },
                    { id: 46, text: 'Nebulization' },
                    { id: 47, text: 'CPAP' },
                    { id: 48, text: 'O2 Admin' }
                ],
                files: [ { id: 'f_health_ed2', text: 'Health Education II' } ]
            },
            {
                id: 'er',
                name: 'Emergency Room',
                locationMatch: "EMERGENCY ROOM",
                logbook: [
                    { id: 49, text: 'Case Mx Young Infants' },
                    { id: 50, text: 'Case Mx Children 2m-5y' },
                    { id: 51, text: 'Restraints' },
                    { id: 52, text: 'Gastrostomy Feeding' },
                    { id: 53, text: 'Jejunostomy Feeding' }
                ],
                files: [
                    { id: 'f_gd_newborn', text: 'G&D - Newborn' },
                    { id: 'f_neuro', text: 'Neuro Assessment' }
                ]
            },
            {
                id: 'picu',
                name: 'PICU',
                locationMatch: "PICU",
                logbook: [
                    { id: 54, text: 'Maintenance Of I/O Chart' },
                    { id: 55, text: 'Infusion Pump' },
                    { id: 56, text: 'Syringe Pump' },
                    { id: 57, text: 'TPN' },
                    { id: 58, text: 'NG-Insertion & Feeding' }
                ],
                files: []
            },
            {
                id: 'nicu',
                name: 'NICU',
                locationMatch: "NICU",
                logbook: [
                    { id: 59, text: 'Preterm & LBW' },
                    { id: 60, text: 'KMC' },
                    { id: 61, text: 'Warmer/Incubator' },
                    { id: 62, text: 'Phototherapy' },
                    { id: 63, text: 'Exchange Transfusion' }
                ],
                files: [ { id: 'f_careplan_nb', text: 'Care Plan - Newborn' } ]
            }
        ];

        // ==================== STATE ====================

        const todayStr = new Date().toISOString().split('T')[0];
        
        let state = {
            view: 'home',
            currentUser: JSON.parse(localStorage.getItem('user')) || STUDENTS[0],
            selectedDate: todayStr,
            pinnedFriends: JSON.parse(localStorage.getItem('pinned')) || [],
            checklist: JSON.parse(localStorage.getItem('checklist')) || {},
            viewingWard: null,
            viewingStudent: null, // New: for student detail timeline
            studentSearch: ''
        };

        // ==================== HELPERS ====================

        function saveState() {
            localStorage.setItem('user', JSON.stringify(state.currentUser));
            localStorage.setItem('pinned', JSON.stringify(state.pinnedFriends));
            localStorage.setItem('checklist', JSON.stringify(state.checklist));
        }

        function getLocation(group, dateStr) {
            const rangeIndex = DATE_RANGES.findIndex(r => dateStr >= r.start && dateStr <= r.end);
            if (rangeIndex === -1) return "Off Duty";
            const pattern = GROUP_PATTERNS[group];
            if (!pattern) return "Unknown";
            return LOCATIONS[pattern[rangeIndex]];
        }

        function getWardFromLocation(locString) {
            return CLINICAL_DATA.find(w => w.locationMatch === locString);
        }

        function getWardProgress(ward) {
            const items = [...ward.logbook, ...ward.files].filter(i => i.id !== 'f_title');
            if (items.length === 0) return 0;
            const completed = items.filter(i => state.checklist[i.id]).length;
            return Math.round((completed / items.length) * 100);
        }

        function switchTab(tab, param) {
            state.view = tab;
            state.viewingWard = (tab === 'requirements' && param) ? param : null;
            state.viewingStudent = null; // Reset sub-views
            
            // UI Update
            document.querySelectorAll('.nav-btn').forEach(btn => {
                const isAuth = btn.dataset.tab === tab;
                if(isAuth) {
                    btn.classList.remove('text-slate-400');
                    btn.classList.add('text-brand-600');
                } else {
                    btn.classList.add('text-slate-400');
                    btn.classList.remove('text-brand-600');
                }
            });

            const titles = { 'home': 'Dashboard', 'calendar': 'Schedule', 'requirements': 'Requirements', 'friends': 'Directory', 'profile': 'My Profile' };
            document.getElementById('header-title').innerText = titles[tab] || 'Clinical Tracker';

            window.scrollTo(0,0);
            render();
        }

        function render() {
            const c = document.getElementById('main-container');
            c.innerHTML = '';
            
            if(state.view === 'home') renderHome(c);
            else if(state.view === 'calendar') renderCalendar(c);
            else if(state.view === 'requirements') renderRequirements(c);
            else if(state.view === 'friends') {
                if(state.viewingStudent) renderStudentDetail(c, state.viewingStudent);
                else renderFriends(c);
            }
            else if(state.view === 'profile') renderProfile(c);
            
            lucide.createIcons();
        }

        // ==================== VIEWS ====================

        function renderHome(c) {
            const myLoc = getLocation(state.currentUser.group, todayStr);
            const ward = getWardFromLocation(myLoc);
            const wardProgress = ward ? getWardProgress(ward) : 0;
            const activeRange = DATE_RANGES.find(r => todayStr >= r.start && todayStr <= r.end);
            
            // Calculate Days Left
            let daysLeftText = "No active rotation";
            if (activeRange) {
                const today = new Date(todayStr);
                const end = new Date(activeRange.end);
                const diffTime = Math.abs(end - today);
                const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24)); 
                daysLeftText = diffDays === 0 ? "Last Day" : `${diffDays} Day${diffDays > 1 ? 's' : ''} Left`;
            }
            
            // Stats
            const totalItems = CLINICAL_DATA.reduce((acc, w) => acc + w.logbook.length + w.files.length - (w.files.some(f=>f.id==='f_title')?1:0), 0);
            const completedItems = Object.keys(state.checklist).length;
            const totalProgress = Math.round((completedItems / totalItems) * 100) || 0;

            c.innerHTML = `
                <div class="mb-5 fade-in">
                    <div class="flex items-center justify-between">
                        <div>
                            <p class="text-slate-500 text-sm font-medium">Good Morning,</p>
                            <h2 class="text-2xl font-bold text-slate-800 tracking-tight">${state.currentUser.name.split(' ')[0]}</h2>
                        </div>
                        <div class="bg-indigo-50 px-3 py-1 rounded-full text-indigo-600 font-bold text-xs border border-indigo-100/50 shadow-sm">
                            Sem V/VI
                        </div>
                    </div>
                </div>

                <!-- MAIN STATUS CARD -->
                <div class="bg-gradient-to-br from-brand-600 to-indigo-700 rounded-[28px] p-6 text-white shadow-float mb-6 relative overflow-hidden fade-in transform transition-transform">
                    <div class="absolute top-0 right-0 w-40 h-40 bg-white/10 rounded-full -mr-16 -mt-16 blur-3xl"></div>
                    <div class="absolute bottom-0 left-0 w-32 h-32 bg-brand-500/30 rounded-full -ml-10 -mb-10 blur-2xl"></div>
                    
                    <div class="relative z-10">
                        <div class="flex items-start justify-between mb-6">
                            <div>
                                <div class="flex items-center gap-2 mb-2">
                                    <span class="bg-white/20 px-2.5 py-1 rounded-md text-[10px] font-bold backdrop-blur-md border border-white/10 uppercase tracking-wider text-brand-50 shadow-sm">Current Posting</span>
                                </div>
                                <h3 class="text-2xl font-bold leading-tight max-w-[200px] text-white">${myLoc}</h3>
                            </div>
                            <div class="bg-white/10 p-3 rounded-2xl backdrop-blur-md border border-white/20 shadow-inner">
                                <i data-lucide="map-pin" class="w-6 h-6 text-white"></i>
                            </div>
                        </div>
                        
                        <div class="flex items-end justify-between">
                            <div class="bg-black/20 backdrop-blur-md border border-white/5 px-4 py-2.5 rounded-2xl">
                                <span class="text-[10px] text-brand-100 font-bold uppercase tracking-wider block mb-0.5">Time Remaining</span>
                                <span class="text-lg font-bold text-white flex items-center gap-2">
                                    <i data-lucide="clock" class="w-4 h-4 text-brand-200"></i> ${daysLeftText}
                                </span>
                            </div>
                            ${ward ? `<button onclick="switchTab('requirements', '${ward.id}')" class="bg-white text-brand-700 text-xs font-bold px-4 py-3 rounded-xl shadow-lg hover:bg-brand-50 transition-all flex items-center gap-1 active:scale-95">Open <i data-lucide="arrow-right" class="w-3.5 h-3.5"></i></button>` : ''}
                        </div>
                    </div>
                </div>

                <!-- QUICK STATS GRID -->
                <div class="grid grid-cols-3 gap-3 mb-6 fade-in" style="animation-delay: 0.1s">
                    <div class="bg-white p-3 rounded-2xl border border-slate-100 shadow-soft flex flex-col items-center justify-center text-center py-4">
                        <div class="w-8 h-8 rounded-full bg-emerald-50 text-emerald-500 flex items-center justify-center mb-2"><i data-lucide="check-circle-2" class="w-4 h-4"></i></div>
                        <span class="text-xl font-bold text-slate-800 leading-none mb-1">${completedItems}</span>
                        <span class="text-[9px] text-slate-400 font-bold uppercase tracking-wide">Done</span>
                    </div>
                    <div class="bg-white p-3 rounded-2xl border border-slate-100 shadow-soft flex flex-col items-center justify-center text-center py-4">
                        <div class="w-8 h-8 rounded-full bg-blue-50 text-blue-500 flex items-center justify-center mb-2"><i data-lucide="list-todo" class="w-4 h-4"></i></div>
                        <span class="text-xl font-bold text-slate-800 leading-none mb-1">${totalItems}</span>
                        <span class="text-[9px] text-slate-400 font-bold uppercase tracking-wide">Total</span>
                    </div>
                    <div class="bg-white p-3 rounded-2xl border border-slate-100 shadow-soft flex flex-col items-center justify-center text-center py-4">
                         <div class="w-8 h-8 rounded-full bg-orange-50 text-orange-500 flex items-center justify-center mb-2"><i data-lucide="pie-chart" class="w-4 h-4"></i></div>
                        <span class="text-xl font-bold text-slate-800 leading-none mb-1">${totalProgress}%</span>
                        <span class="text-[9px] text-slate-400 font-bold uppercase tracking-wide">Progress</span>
                    </div>
                </div>

                <!-- RESOURCES LINK -->
                <a href="https://drive.google.com/drive/folders/16K54NpWLnqiZCD7wcha10Uew9UnkCuDi?usp=drive_link" target="_blank" class="block bg-gradient-to-r from-orange-50 to-amber-50 border border-orange-100/50 p-4 rounded-2xl mb-8 flex items-center justify-between active:scale-[0.98] transition-all fade-in shadow-sm hover:shadow-md" style="animation-delay: 0.15s">
                    <div class="flex items-center gap-4">
                        <div class="w-12 h-12 rounded-2xl bg-white text-orange-500 flex items-center justify-center shadow-sm">
                            <i data-lucide="folder-heart" class="w-6 h-6"></i>
                        </div>
                        <div>
                            <h3 class="font-bold text-slate-800 text-sm">Study Resources</h3>
                            <p class="text-xs text-slate-500 mt-0.5">Evaluation Forms, Vivas & More</p>
                        </div>
                    </div>
                    <div class="bg-white p-2 rounded-full shadow-sm text-slate-300">
                        <i data-lucide="chevron-right" class="w-4 h-4"></i>
                    </div>
                </a>

                <!-- FRIENDS WIDGET -->
                <div class="mb-6 fade-in" style="animation-delay: 0.2s">
                    <div class="flex items-center justify-between mb-4 px-1">
                        <h3 class="font-bold text-slate-800 flex items-center gap-2">
                            <i data-lucide="users" class="w-4 h-4 text-slate-400"></i> Pinned Friends
                        </h3>
                        <button onclick="switchTab('friends')" class="text-xs text-brand-600 font-bold bg-brand-50 px-2.5 py-1.5 rounded-lg active:bg-brand-100">Manage</button>
                    </div>
                    
                    <div class="flex gap-3 overflow-x-auto no-scrollbar pb-4 -mx-4 px-4 snap-x">
                        ${state.pinnedFriends.length === 0 ? 
                            `<div onclick="switchTab('friends')" class="w-full bg-slate-50 border border-slate-200 border-dashed rounded-2xl p-6 text-center text-slate-400 text-sm flex flex-col items-center gap-2">
                                <i data-lucide="user-plus" class="w-6 h-6 opacity-50"></i>
                                <span>Tap Directory to pin friends</span>
                            </div>` : 
                            state.pinnedFriends.map(fid => {
                                const f = STUDENTS.find(s => s.id === fid);
                                if(!f) return '';
                                const loc = getLocation(f.group, todayStr);
                                return `
                                <div onclick="viewStudent(${f.id})" class="snap-start flex-shrink-0 w-36 bg-white border border-slate-100 rounded-2xl p-4 shadow-soft flex flex-col items-center text-center active:scale-95 transition-transform relative overflow-hidden">
                                    <div class="absolute inset-x-0 top-0 h-1 bg-gradient-to-r from-brand-400 to-indigo-400"></div>
                                    <div class="w-12 h-12 rounded-full bg-slate-50 text-slate-600 flex items-center justify-center font-bold text-lg mb-3 shadow-inner">
                                        ${f.name.charAt(0)}
                                    </div>
                                    <p class="text-xs font-bold text-slate-800 truncate w-full mb-1">${f.name.split(' ')[0]}</p>
                                    <div class="w-full bg-slate-50 rounded-lg py-1 px-2">
                                        <p class="text-[10px] text-slate-500 truncate font-medium">${loc}</p>
                                    </div>
                                </div>`;
                            }).join('')
                        }
                    </div>
                </div>
            `;
        }

        // --- Student Detail / Timeline View ---
        function viewStudent(id) {
            state.viewingStudent = id;
            state.view = 'friends'; // Ensure we are in the friends tab context
            // Update Tab UI manually to reflect we are in friends section
             document.querySelectorAll('.nav-btn').forEach(btn => {
                const isAuth = btn.dataset.tab === 'friends';
                if(isAuth) {
                     btn.classList.remove('text-slate-400');
                    btn.classList.add('text-brand-600');
                } else {
                     btn.classList.add('text-slate-400');
                    btn.classList.remove('text-brand-600');
                }
            });
            render();
            window.scrollTo(0,0);
        }

        function renderStudentDetail(c, studentId) {
            const student = STUDENTS.find(s => s.id === studentId);
            if(!student) { state.viewingStudent = null; render(); return; }

            // Calculate schedule
            const schedule = DATE_RANGES.map((range, idx) => {
                const isCurrent = todayStr >= range.start && todayStr <= range.end;
                const isPast = todayStr > range.end;
                return {
                    range,
                    location: getLocation(student.group, range.start),
                    status: isCurrent ? 'current' : (isPast ? 'past' : 'future')
                };
            });

            c.innerHTML = `
                <div class="fade-in">
                    <button onclick="state.viewingStudent=null; render()" class="flex items-center gap-2 text-sm text-slate-500 font-bold hover:text-brand-600 mb-6 bg-white px-3 py-2 rounded-xl shadow-sm w-fit border border-slate-100">
                        <i data-lucide="arrow-left" class="w-4 h-4"></i> Back
                    </button>

                    <div class="bg-white rounded-[24px] p-6 shadow-soft border border-slate-100 text-center mb-8 relative overflow-hidden">
                        <div class="absolute top-0 left-0 w-full h-20 bg-gradient-to-r from-brand-50 to-indigo-50"></div>
                        <div class="relative z-10 mt-4">
                             <div class="w-24 h-24 rounded-full bg-white text-brand-600 flex items-center justify-center text-3xl font-bold shadow-lg mx-auto mb-4 ring-4 ring-white">
                                ${student.name.charAt(0)}
                            </div>
                            <h2 class="text-xl font-bold text-slate-900">${student.name}</h2>
                            <div class="flex justify-center gap-2 mt-3">
                                <span class="text-xs font-mono bg-slate-100 px-3 py-1.5 rounded-lg text-slate-600 border border-slate-200">${student.reg}</span>
                                <span class="text-xs font-bold bg-brand-50 text-brand-700 px-3 py-1.5 rounded-lg border border-brand-100">Group ${student.group}</span>
                            </div>
                        </div>
                    </div>

                    <h3 class="font-bold text-slate-800 mb-5 px-1 flex items-center gap-2 text-sm uppercase tracking-wider">
                        <i data-lucide="calendar-clock" class="w-4 h-4 text-brand-500"></i> Rotation Timeline
                    </h3>
                    
                    <div class="relative border-l-2 border-slate-200 ml-5 space-y-8 pb-8">
                        ${schedule.map((item) => `
                            <div class="relative pl-8 ${item.status === 'past' ? 'opacity-60 grayscale-[0.5]' : ''}">
                                <div class="absolute -left-[9px] top-4 w-4 h-4 rounded-full border-[3px] bg-white ${item.status === 'current' ? 'border-brand-500 ring-4 ring-brand-100' : 'border-slate-300'} z-10"></div>
                                
                                <div class="bg-white p-4 rounded-2xl border ${item.status === 'current' ? 'border-brand-200 shadow-float ring-1 ring-brand-100' : 'border-slate-100 shadow-sm'} transition-all">
                                    <div class="flex justify-between items-center mb-2">
                                        <span class="text-[10px] font-bold uppercase tracking-wider ${item.status === 'current' ? 'text-brand-600' : 'text-slate-400'}">
                                            ${item.range.label}
                                        </span>
                                        ${item.status === 'current' ? '<span class="px-2.5 py-1 bg-brand-600 text-white text-[9px] font-bold rounded-full shadow-sm animate-pulse">NOW</span>' : ''}
                                    </div>
                                    <div class="text-sm font-bold text-slate-800 leading-snug">${item.location}</div>
                                </div>
                            </div>
                        `).join('')}
                    </div>
                </div>
            `;
        }

        // --- Other Views ---

        function renderFriends(c) {
            const filtered = STUDENTS.filter(s => 
                s.name.toLowerCase().includes(state.studentSearch.toLowerCase()) || 
                s.reg.includes(state.studentSearch)
            );

            c.innerHTML = `
                <div class="sticky top-16 bg-slate-50/95 backdrop-blur-sm z-20 pb-4 pt-1">
                     <div class="relative shadow-sm group">
                        <i data-lucide="search" class="absolute left-4 top-3.5 w-5 h-5 text-slate-400 group-focus-within:text-brand-500 transition-colors"></i>
                        <input type="text" placeholder="Search 20 students..." 
                            value="${state.studentSearch}"
                            oninput="updateSearch(this.value)"
                            class="w-full bg-white border border-slate-200 pl-12 pr-4 py-3 rounded-2xl text-sm focus:outline-none focus:ring-2 focus:ring-brand-500 focus:border-transparent shadow-sm">
                    </div>
                </div>

                <div class="space-y-3 pb-8 fade-in">
                    ${filtered.map(s => {
                        const isPinned = state.pinnedFriends.includes(s.id);
                        const isMe = s.id === state.currentUser.id;
                        return `
                        <div onclick="viewStudent(${s.id})" class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100 flex items-center justify-between active:scale-[0.98] transition-transform">
                            <div class="flex items-center gap-4">
                                <div class="w-12 h-12 rounded-full ${isMe ? 'bg-brand-50 text-brand-600' : 'bg-slate-100 text-slate-500'} flex items-center justify-center font-bold text-base">
                                    ${s.name.charAt(0)}
                                </div>
                                <div>
                                    <div class="flex items-center gap-2 mb-0.5">
                                        <p class="font-bold text-slate-800 text-sm">${s.name}</p>
                                        ${isMe ? '<span class="bg-brand-100 text-brand-700 text-[9px] font-bold px-1.5 py-0.5 rounded uppercase">You</span>' : ''}
                                    </div>
                                    <p class="text-xs text-slate-500 font-mono">${s.reg} • Group ${s.group}</p>
                                </div>
                            </div>
                            ${!isMe ? `
                            <button onclick="event.stopPropagation(); togglePin(${s.id})" class="p-2.5 rounded-full transition-colors ${isPinned ? 'bg-pink-50 text-pink-500' : 'bg-slate-50 text-slate-300'}">
                                <i data-lucide="heart" class="w-5 h-5 ${isPinned ? 'fill-current' : ''}"></i>
                            </button>` : ''}
                        </div>
                        `;
                    }).join('')}
                    ${filtered.length === 0 ? '<div class="flex flex-col items-center justify-center py-12 text-slate-400 gap-2"><i data-lucide="search-x" class="w-8 h-8 opacity-50"></i><p class="text-sm">No students found</p></div>' : ''}
                </div>
            `;
        }

        function renderRequirements(c) {
            if (state.viewingWard) {
                const ward = CLINICAL_DATA.find(w => w.id === state.viewingWard);
                const progress = getWardProgress(ward);
                
                c.innerHTML = `
                    <div class="mb-6 fade-in sticky top-16 bg-slate-50/95 backdrop-blur-sm z-20 py-2">
                        <div class="flex items-center gap-3 mb-4">
                            <button onclick="switchTab('requirements')" class="bg-white border border-slate-200 p-2 rounded-xl shadow-sm text-slate-500 hover:text-brand-600">
                                <i data-lucide="arrow-left" class="w-5 h-5"></i>
                            </button>
                            <h2 class="text-lg font-bold text-slate-800 leading-tight truncate flex-1">${ward.name}</h2>
                        </div>
                        
                        <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
                             <div class="flex items-center justify-between mb-2">
                                <span class="text-xs font-bold text-slate-500 uppercase">Completion</span>
                                <span class="text-xs font-bold text-brand-600">${progress}%</span>
                            </div>
                            <div class="h-2.5 bg-slate-100 rounded-full overflow-hidden">
                                <div class="h-full bg-brand-500 transition-all duration-500 ease-out" style="width: ${progress}%"></div>
                            </div>
                        </div>
                    </div>

                    <div class="space-y-6 fade-in pb-8">
                        ${ward.logbook.length > 0 ? `
                        <div>
                            <h3 class="text-xs font-bold text-slate-400 uppercase tracking-wider mb-3 px-1 flex items-center gap-2"><i data-lucide="book-open" class="w-3 h-3"></i> Logbook Items</h3>
                            <div class="space-y-2">
                                ${ward.logbook.map(item => renderCheckItem(item)).join('')}
                            </div>
                        </div>` : ''}

                        ${ward.files.length > 0 ? `
                        <div>
                            <h3 class="text-xs font-bold text-slate-400 uppercase tracking-wider mb-3 px-1 flex items-center gap-2"><i data-lucide="file-text" class="w-3 h-3"></i> Files & Reports</h3>
                            <div class="space-y-2">
                                ${ward.files.map(item => renderCheckItem(item)).join('')}
                            </div>
                        </div>` : ''}
                    </div>
                `;
                return;
            }

            c.innerHTML = `
                <div class="mb-6 fade-in">
                    <h2 class="text-2xl font-bold text-slate-800 mb-1">Requirements</h2>
                    <p class="text-sm text-slate-500">Track your clinical progress by ward</p>
                </div>

                <div class="grid gap-3 fade-in pb-8">
                    ${CLINICAL_DATA.map(ward => {
                        const prog = getWardProgress(ward);
                        const isComplete = prog === 100;
                        return `
                        <div onclick="switchTab('requirements', '${ward.id}')" class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100 flex items-center justify-between active:scale-[0.98] transition-all group relative overflow-hidden">
                            ${isComplete ? '<div class="absolute right-0 top-0 w-16 h-16 bg-emerald-500/10 rounded-bl-full -mr-8 -mt-8"></div>' : ''}
                            <div class="flex items-center gap-4 overflow-hidden relative z-10">
                                <div class="w-12 h-12 rounded-xl ${isComplete ? 'bg-emerald-100 text-emerald-600' : 'bg-indigo-50 text-indigo-600'} flex-shrink-0 flex items-center justify-center transition-colors">
                                    <i data-lucide="${isComplete ? 'check-circle-2' : 'folder'}" class="w-6 h-6"></i>
                                </div>
                                <div class="min-w-0">
                                    <h3 class="font-bold text-slate-800 text-sm truncate pr-2 group-hover:text-brand-600 transition-colors">${ward.name}</h3>
                                    <div class="flex items-center gap-2 mt-1">
                                        <span class="text-[10px] bg-slate-100 px-1.5 py-0.5 rounded text-slate-500 font-medium">${ward.logbook.length + ward.files.length} Tasks</span>
                                    </div>
                                </div>
                            </div>
                            <div class="flex flex-col items-end pl-2 relative z-10">
                                <span class="text-sm font-bold ${isComplete?'text-emerald-600':'text-slate-300'}">${prog}%</span>
                                <i data-lucide="chevron-right" class="w-4 h-4 text-slate-300 mt-1"></i>
                            </div>
                        </div>
                        `;
                    }).join('')}
                </div>
            `;
        }

        function renderCheckItem(item) {
            if(item.id === 'f_title') return `<div class="text-xs font-bold text-brand-600 mt-4 mb-2 pl-1 uppercase tracking-wide border-b border-slate-100 pb-1">${item.text}</div>`;
            const isDone = state.checklist[item.id];
            return `
                <div onclick="toggleCheck('${item.id}')" class="group bg-white p-3.5 rounded-xl border ${isDone ? 'border-emerald-200 bg-emerald-50/30' : 'border-slate-100'} shadow-sm flex items-start gap-3 active:scale-[0.98] transition-all cursor-pointer select-none">
                    <div class="mt-0.5 w-6 h-6 rounded-lg border-2 ${isDone ? 'bg-emerald-500 border-emerald-500' : 'border-slate-200 group-hover:border-brand-400'} flex items-center justify-center transition-all flex-shrink-0">
                        <i data-lucide="check" class="w-3.5 h-3.5 text-white ${isDone ? 'opacity-100 scale-100' : 'opacity-0 scale-50'} transition-all duration-300"></i>
                    </div>
                    <span class="text-sm font-medium leading-tight ${isDone ? 'text-slate-400 line-through' : 'text-slate-700'} pt-0.5">${item.text}</span>
                </div>
            `;
        }

        function toggleCheck(id) {
            if(state.checklist[id]) delete state.checklist[id];
            else state.checklist[id] = true;
            saveState();
            render();
        }

        function updateSearch(val) {
            state.studentSearch = val;
            render();
        }

        function togglePin(id) {
            if(state.pinnedFriends.includes(id)) state.pinnedFriends = state.pinnedFriends.filter(x => x !== id);
            else state.pinnedFriends.push(id);
            saveState();
            render();
        }

        function renderCalendar(c) {
            const date = new Date(state.selectedDate);
            const year = 2026, month = 0; 
            const firstDay = new Date(year, month, 1).getDay();
            const daysInMonth = 32 - new Date(year, month, 32).getDate();
            
            let daysHTML = '';
            // Add empty cells for start of month
            for(let i=0; i<firstDay; i++) daysHTML += `<div class="aspect-square"></div>`;
            
            for(let d=1; d<=daysInMonth; d++) {
                const currentStr = `${year}-${String(month+1).padStart(2,'0')}-${String(d).padStart(2,'0')}`;
                const isSelected = currentStr === state.selectedDate;
                const isToday = currentStr === todayStr;
                
                // Determine styling based on state
                let bgClass = isSelected ? 'bg-brand-600 text-white shadow-md scale-105' : 'bg-slate-50 text-slate-600 hover:bg-slate-100';
                if (isToday && !isSelected) bgClass = 'bg-brand-50 text-brand-600 font-bold border border-brand-200';
                
                daysHTML += `
                    <button onclick="selectDate('${currentStr}')" class="w-full aspect-square flex flex-col items-center justify-center rounded-xl text-sm font-medium transition-all duration-200 relative ${bgClass}">
                        <span>${d}</span>
                        ${isToday ? '<span class="w-1 h-1 rounded-full bg-current mt-0.5"></span>' : ''}
                    </button>
                `;
            }

            const selectedLoc = getLocation(state.currentUser.group, state.selectedDate);
            const pinnedLocs = state.pinnedFriends.map(fid => {
                const f = STUDENTS.find(s => s.id === fid);
                return { name: f.name, loc: getLocation(f.group, state.selectedDate) };
            });

            c.innerHTML = `
                <div class="mb-6 fade-in">
                    <h2 class="text-2xl font-bold text-slate-800 mb-1">Schedule</h2>
                    <p class="text-sm text-slate-500">View rotations and locations</p>
                </div>

                <div class="bg-white rounded-[24px] p-5 shadow-soft border border-slate-100 mb-6 fade-in">
                    <div class="flex items-center justify-between mb-4 px-1">
                        <h2 class="text-lg font-bold text-slate-800">January 2026</h2>
                        <span class="text-xs bg-slate-100 px-2 py-1 rounded-lg text-slate-500 font-medium">Final Year</span>
                    </div>
                    <div class="grid grid-cols-7 gap-2 text-center text-[10px] font-bold text-slate-400 uppercase tracking-widest mb-3">
                        <span>Su</span><span>Mo</span><span>Tu</span><span>We</span><span>Th</span><span>Fr</span><span>Sa</span>
                    </div>
                    <div class="grid grid-cols-7 gap-2">${daysHTML}</div>
                </div>

                <div class="fade-in pb-8" style="animation-delay: 0.1s">
                    <h3 class="font-bold text-slate-800 mb-3 px-1 text-sm uppercase tracking-wide">Details for ${new Date(state.selectedDate).toLocaleDateString('en-GB', {day: 'numeric', month: 'short'})}</h3>
                    
                    <div class="bg-gradient-to-r from-brand-600 to-indigo-600 rounded-2xl p-5 shadow-float mb-4 flex items-center justify-between text-white relative overflow-hidden">
                        <div class="absolute right-0 top-0 w-24 h-24 bg-white/10 rounded-full -mr-8 -mt-8 blur-xl"></div>
                        <div class="relative z-10">
                            <p class="text-[10px] text-brand-100 font-bold uppercase tracking-widest mb-1">My Posting</p>
                            <p class="text-lg font-bold leading-tight max-w-[220px]">${selectedLoc}</p>
                        </div>
                        <div class="w-10 h-10 bg-white/20 backdrop-blur-md rounded-xl flex items-center justify-center text-white relative z-10">
                            <i data-lucide="map-pin" class="w-5 h-5"></i>
                        </div>
                    </div>

                    ${pinnedLocs.length > 0 ? `
                    <div class="space-y-3">
                         <p class="text-[10px] text-slate-400 font-bold uppercase tracking-widest px-1">Friend Locations</p>
                         ${pinnedLocs.map(p => `
                            <div class="bg-white rounded-xl p-3.5 flex items-center justify-between shadow-sm border border-slate-100">
                                <div class="flex items-center gap-3">
                                    <div class="w-8 h-8 rounded-full bg-slate-100 text-slate-500 flex items-center justify-center text-xs font-bold">
                                        ${p.name.charAt(0)}
                                    </div>
                                    <span class="font-bold text-slate-700 text-sm">${p.name.split(' ')[0]}</span>
                                </div>
                                <span class="text-[10px] bg-slate-50 border border-slate-100 px-2 py-1 rounded text-slate-500 font-medium truncate max-w-[140px]">${p.loc}</span>
                            </div>
                         `).join('')}
                    </div>` : ''}
                </div>
            `;
        }

        function selectDate(d) {
            state.selectedDate = d;
            // Only re-render calendar section to prevent scroll jump if possible, 
            // but for simplicity we render entire view
            render(); 
        }

        function renderProfile(c) {
            c.innerHTML = `
                <div class="flex flex-col items-center py-8 fade-in relative">
                    <div class="w-32 h-32 bg-gradient-to-tr from-brand-100 to-indigo-100 rounded-full flex items-center justify-center text-brand-600 text-4xl font-bold mb-5 shadow-float ring-8 ring-white">
                        ${state.currentUser.name.charAt(0)}
                    </div>
                    <h2 class="text-2xl font-bold text-slate-800 text-center px-4">${state.currentUser.name}</h2>
                    <p class="text-slate-500 text-sm font-mono mt-1">${state.currentUser.reg}</p>
                    
                    <div class="flex gap-2 mt-4">
                        <span class="text-xs font-bold bg-brand-50 text-brand-700 px-3 py-1.5 rounded-full border border-brand-100">Group ${state.currentUser.group}</span>
                        <span class="text-xs font-bold bg-indigo-50 text-indigo-700 px-3 py-1.5 rounded-full border border-indigo-100">Sem V</span>
                    </div>

                    <button onclick="toggleProfileModal()" class="mt-8 px-6 py-3 bg-white border border-slate-200 rounded-2xl text-sm font-bold text-slate-700 shadow-sm active:bg-slate-50 flex items-center gap-2">
                        <i data-lucide="refresh-cw" class="w-4 h-4 text-slate-400"></i> Switch Student
                    </button>
                </div>

                <div class="bg-white rounded-2xl overflow-hidden shadow-sm border border-slate-100 fade-in mx-1" style="animation-delay: 0.1s">
                    <div class="p-4 border-b border-slate-50 flex items-center justify-between">
                        <span class="text-sm font-medium text-slate-600">Total Checklists</span>
                        <span class="text-sm font-bold text-brand-600 bg-brand-50 px-2 py-1 rounded">${Object.keys(state.checklist).length} Items</span>
                    </div>
                    <div class="p-4 border-b border-slate-50 flex items-center justify-between">
                         <span class="text-sm font-medium text-slate-600">App Version</span>
                        <span class="text-sm text-slate-400 font-mono">v1.2.0 (Mobile)</span>
                    </div>
                     <div class="p-4 flex items-center justify-center">
                        <span class="text-xs text-slate-300 font-medium uppercase tracking-widest">Academic Year 2025-26</span>
                    </div>
                </div>
            `;
        }

        // ==================== MODAL ====================

        function toggleProfileModal() {
            const m = document.getElementById('profile-modal');
            const c = document.getElementById('profile-sheet-content');
            const b = document.getElementById('modal-backdrop');
            const l = document.getElementById('user-selector-list');
            const input = document.getElementById('modal-search');
            
            if (m.classList.contains('hidden')) {
                m.classList.remove('hidden');
                // Allow browser to render removing hidden before animating opacity
                requestAnimationFrame(() => {
                    b.classList.remove('opacity-0');
                    c.classList.remove('translate-y-full');
                });
                
                const renderList = (filter = '') => {
                    const matches = STUDENTS.filter(s => s.name.toLowerCase().includes(filter.toLowerCase()) || s.reg.includes(filter));
                    l.innerHTML = matches.map(s => `
                        <button onclick="switchUser(${s.id})" class="w-full text-left p-4 rounded-2xl hover:bg-slate-50 flex items-center justify-between border border-transparent hover:border-slate-100 transition-all ${state.currentUser.id === s.id ? 'bg-brand-50 border-brand-100 ring-1 ring-brand-200' : ''}">
                            <div class="flex items-center gap-3">
                                <div class="w-10 h-10 rounded-full ${state.currentUser.id === s.id ? 'bg-brand-200 text-brand-700' : 'bg-slate-100 text-slate-500'} flex items-center justify-center font-bold text-sm">
                                    ${s.name.charAt(0)}
                                </div>
                                <div>
                                    <div class="font-bold text-sm text-slate-800">${s.name}</div>
                                    <div class="text-xs text-slate-400 font-mono mt-0.5">${s.reg}</div>
                                </div>
                            </div>
                            ${state.currentUser.id === s.id ? '<div class="w-6 h-6 bg-brand-500 rounded-full flex items-center justify-center"><i data-lucide="check" class="w-3.5 h-3.5 text-white"></i></div>' : ''}
                        </button>
                    `).join('');
                    lucide.createIcons();
                };

                renderList();
                input.oninput = (e) => renderList(e.target.value);
                input.value = '';
                // Focus input after animation
                setTimeout(() => input.focus(), 300);

            } else {
                b.classList.add('opacity-0');
                c.classList.add('translate-y-full');
                setTimeout(() => m.classList.add('hidden'), 300);
            }
        }

        function switchUser(id) {
            state.currentUser = STUDENTS.find(s => s.id === id);
            saveState();
            toggleProfileModal();
            render();
        }

        // ==================== SCROLL HANDLER ====================
        
        window.onscroll = function() {
            const btn = document.getElementById('scrollTopBtn');
            if (document.body.scrollTop > 200 || document.documentElement.scrollTop > 200) {
                btn.classList.remove('opacity-0', 'translate-y-10', 'pointer-events-none');
            } else {
                btn.classList.add('opacity-0', 'translate-y-10', 'pointer-events-none');
            }
        };

        // INIT
        window.onload = () => {
            render();
            // Prevent bounce on iOS
            // document.body.addEventListener('touchmove', function(e) { e.preventDefault(); }, { passive: false });
        };

    </script>
</body>
</html>
