<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>سامانه دانشگاهی | ۲۰۲۵</title>

  <!-- Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Vazirmatn:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">

  <!-- Icons -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/dist/tabler-icons.min.css">

  <!-- AOS Animation -->
  <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">

  <!-- Tailwind (via CDN for demo) -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: {
            sans: ['Vazirmatn', 'sans-serif'],
          },
          animation: {
            'float': 'float 6s ease-in-out infinite',
            'pulse-slow': 'pulse 3s cubic-bezier(0.4, 0, 0.6, 1) infinite',
          },
          keyframes: {
            float: {
              '0%, 100%': { transform: 'translateY(0)' },
              '50%': { transform: 'translateY(-20px)' },
            }
          }
        }
      }
    }
  </script>

  <style>
    :root {
      --primary: #004aad;
      --primary-light: #0065d9;
      --accent: #ffde59;
      --gradient: linear-gradient(135deg, #004aad, #007bff);
    }
    .dark {
      --primary: #1e40af;
      --primary-light: #3b82f6;
      --accent: #fbbf24;
    }
    .glass {
      background: rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.2);
    }
    .card-hover {
      transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.1);
    }
    .card-hover:hover {
      transform: translateY(-16px) scale(1.02);
      box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
    }
    .btn-glow {
      position: relative;
      overflow: hidden;
      z-index: 1;
    }
    .btn-glow::before {
      content: '';
      position: absolute;
      top: 0; left: -100%;
      width: 100%; height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
      transition: 0.6s;
      z-index: -1;
    }
    .btn-glow:hover::before {
      left: 100%;
    }
  </style>
</head>
<body class="bg-gradient-to-br from-slate-50 to-blue-50 dark:from-slate-900 dark:to-slate-800 text-slate-800 dark:text-slate-200 min-h-screen transition-colors duration-500">

  <!-- Loading Screen -->
  <div id="loader" class="fixed inset-0 bg-white dark:bg-slate-900 z-50 flex items-center justify-center">
    <div class="relative">
      <div class="w-20 h-20 border-4 border-slate-200 dark:border-slate-700 rounded-full animate-spin"></div>
      <div class="absolute inset-0 w-20 h-20 border-t-4 border-blue-600 rounded-full animate-spin animation-delay-200"></div>
      <div class="absolute inset-0 flex items-center justify-center">
        <svg class="w-10 h-10 text-blue-600" viewBox="0 0 24 24">
          <path fill="currentColor" d="M12 2a10 10 0 100 20 10 10 0 000-20zm0 18a8 8 0 110-16 8 8 0 010 16z"/>
          <path fill="currentColor" d="M12 6a6 6 0 100 12 6 6 0 000-12z"/>
        </svg>
      </div>
    </div>
  </div>

  <!-- Theme Toggle -->
  <button id="theme-toggle" class="fixed top-6 left-6 z-40 p-3 rounded-full bg-white dark:bg-slate-800 shadow-lg hover:shadow-xl transition-all">
    <i class="ti ti-moon text-xl"></i>
  </button>

  <!-- Header -->
  <header class="relative overflow-hidden bg-gradient-to-r from-blue-600 via-blue-700 to-indigo-700 text-white shadow-2xl">
    <div class="absolute inset-0 bg-black opacity-10"></div>
    <div class="relative container mx-auto px-6 py-5 flex justify-between items-center">
      <div class="flex items-center space-x-reverse space-x-4">
        <div class="w-12 h-12 bg-yellow-400 rounded-xl flex items-center justify-center animate-float">
          <i class="ti ti-school text-2xl text-blue-900"></i>
        </div>
        <h1 class="text-2xl md:text-3xl font-bold tracking-wide">سامانه دانشگاهی</h1>
      </div>

      <!-- Desktop Nav -->
      <nav class="hidden md:flex items-center space-x-reverse space-x-8">
        <a href="#" class="hover:text-yellow-300 transition-colors font-medium">خانه</a>
        <a href="#" class="hover:text-yellow-300 transition-colors font-medium">انتخاب واحد</a>
        <a href="#" class="hover:text-yellow-300 transition-colors font-medium">خوابگاه</a>
        <a href="#" class="hover:text-yellow-300 transition-colors font-medium">رزرو غذا</a>
        <a href="#" class="text-yellow-300 font-bold">خروج</a>
      </nav>

      <!-- Mobile Menu Button -->
      <button id="mobile-menu-btn" class="md:hidden p-2">
        <i class="ti ti-menu-2 text-2xl"></i>
      </button>
    </div>
  </header>

  <!-- Mobile Menu -->
  <div id="mobile-menu" class="fixed inset-0 bg-slate-900 bg-opacity-95 z-40 hidden flex items-center justify-center">
    <button id="close-menu" class="absolute top-6 left-6 text-white text-3xl">&times;</button>
    <nav class="text-center space-y-8 text-2xl">
      <a href="#" class="block text-white hover:text-yellow-400 transition">خانه</a>
      <a href="#" class="block text-white hover:text-yellow-400 transition">انتخاب واحد</a>
      <a href="#" class="block text-white hover:text-yellow-400 transition">خوابگاه</a>
      <a href="#" class="block text-white hover:text-yellow-400 transition">رزرو غذا</a>
      <a href="#" class="block text-yellow-400 font-bold">خروج</a>
    </nav>
  </div>

  <!-- Hero Section -->
  <section class="relative py-24 overflow-hidden">
    <div class="absolute inset-0 bg-gradient-to-br from-blue-500/10 to-indigo-600/10"></div>
    <div class="container mx-auto px-6 text-center relative z-10">
      <h2 data-aos="fade-up" class="text-4xl md:text-6xl font-extrabold text-blue-900 dark:text-blue-300 mb-6">
        به <span class="text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-indigo-700">سامانه دانشگاه</span> خوش آمدید
      </h2>
      <p data-aos="fade-up" data-aos-delay="200" class="text-lg md:text-xl text-slate-600 dark:text-slate-300 max-w-3xl mx-auto leading-relaxed">
        مدیریت هوشمند انتخاب واحد، رزرو خوابگاه و سفارش غذا — همه در یک مکان، با تجربه‌ای بی‌نظیر.
      </p>
      <div data-aos="fade-up" data-aos-delay="400" class="mt-10 flex justify-center space-x-reverse space-x-4">
        <div class="w-3 h-3 bg-blue-600 rounded-full animate-pulse"></div>
        <div class="w-3 h-3 bg-yellow-400 rounded-full animate-pulse animation-delay-200"></div>
        <div class="w-3 h-3 bg-indigo-600 rounded-full animate-pulse animation-delay-400"></div>
      </div>
    </div>
  </section>

  <!-- Cards Section -->
  <section class="container mx-auto px-6 py-16">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-10 max-w-6xl mx-auto">
      <!-- Card 1 -->
      <div data-aos="zoom-in" data-aos-delay="100" class="card-hover group relative bg-white dark:bg-slate-800 rounded-3xl p-8 shadow-lg overflow-hidden">
        <div class="absolute inset-0 bg-gradient-to-br from-blue-500/5 to-indigo-600/5 opacity-0 group-hover:opacity-100 transition-opacity"></div>
        <div class="relative z-10">
          <div class="w-20 h-20 mx-auto mb-6 bg-gradient-to-br from-blue-500 to-indigo-600 rounded-2xl flex items-center justify-center shadow-xl group-hover:scale-110 transition-transform">
            <i class="ti ti-book text-3xl text-white"></i>
          </div>
          <h3 class="text-2xl font-bold text-blue-900 dark:text-blue-300 mb-3">انتخاب واحد</h3>
          <p class="text-slate-600 dark:text-slate-400 mb-6 leading-relaxed">
            دروس ترم جدید را با فیلترهای هوشمند مشاهده و ثبت‌نام کنید.
          </p>
          <button onclick="openPage('unit')" class="btn-glow w-full py-3 rounded-xl bg-gradient-to-r from-blue-600 to-indigo-700 text-white font-bold shadow-lg hover:shadow-blue-500/25 transition-all">
            ورود به سیستم
          </button>
        </div>
      </div>

      <!-- Card 2 -->
      <div data-aos="zoom-in" data-aos-delay="300" class="card-hover group relative bg-white dark:bg-slate-800 rounded-3xl p-8 shadow-lg overflow-hidden">
        <div class="absolute inset-0 bg-gradient-to-br from-amber-500/5 to-orange-600/5 opacity-0 group-hover:opacity-100 transition-opacity"></div>
        <div class="relative z-10">
          <div class="w-20 h-20 mx-auto mb-6 bg-gradient-to-br from-amber-500 to-orange-600 rounded-2xl flex items-center justify-center shadow-xl group-hover:scale-110 transition-transform">
            <i class="ti ti-building text-3xl text-white"></i>
          </div>
          <h3 class="text-2xl font-bold text-amber-700 dark:text-amber-300 mb-3">خوابگاه</h3>
          <p class="text-slate-600 dark:text-slate-400 mb-6 leading-relaxed">
            اتاق دلخواه خود را با یک کلیک رزرو یا تمدید کنید.
          </p>
          <button onclick="openPage('dorm')" class="btn-glow w-full py-3 rounded-xl bg-gradient-to-r from-amber-500 to-orange-600 text-white font-bold shadow-lg hover:shadow-amber-500/25 transition-all">
            رزرو اتاق
          </button>
        </div>
      </div>

      <!-- Card 3 -->
      <div data-aos="zoom-in" data-aos-delay="500" class="card-hover group relative bg-white dark:bg-slate-800 rounded-3xl p-8 shadow-lg overflow-hidden">
        <div class="absolute inset-0 bg-gradient-to-br from-green-500/5 to-emerald-600/5 opacity-0 group-hover:opacity-100 transition-opacity"></div>
        <div class="relative z-10">
          <div class="w-20 h-20 mx-auto mb-6 bg-gradient-to-br from-green-500 to-emerald-600 rounded-2xl flex items-center justify-center shadow-xl group-hover:scale-110 transition-transform">
            <i class="ti ti-utensils text-3xl text-white"></i>
          </div>
          <h3 class="text-2xl font-bold text-green-700 dark:text-green-300 mb-3">رزرو غذا</h3>
          <p class="text-slate-600 dark:text-slate-400 mb-6 leading-relaxed">
            منوی هفته آینده را ببینید و غذای مورد علاقه خود را رزرو کنید.
          </p>
          <button onclick="openPage('food')" class="btn-glow w-full py-3 rounded-xl bg-gradient-to-r from-green-500 to-emerald-600 text-white font-bold shadow-lg hover:shadow-green-500/25 transition-all">
            انتخاب غذا
          </button>
        </div>
      </div>
    </div>
  </section>

  <!-- Footer -->
  <footer class="mt-24 py-12 bg-gradient-to-t from-slate-900 to-slate-800 text-white">
    <div class="container mx-auto px-6 text-center">
      <div class="flex justify-center items-center space-x-reverse space-x-6 mb-6">
        <i class="ti ti-copyright text-xl"></i>
        <p class="text-lg">۲۰۲۵ سامانه دانشگاهی | طراحی شده با <span class="text-red-500">♥</span> توسط تیم فناوری اطلاعات</p>
      </div>
      <div class="flex justify-center space-x-reverse space-x-4 text-2xl">
        <a href="#" class="hover:text-yellow-400 transition"><i class="ti ti-brand-instagram"></i></a>
        <a href="#" class="hover:text-yellow-400 transition"><i class="ti ti-brand-telegram"></i></a>
        <a href="#" class="hover:text-yellow-400 transition"><i class="ti ti-brand-linkedin"></i></a>
      </div>
    </div>
  </footer>

  <!-- Scripts -->
  <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
  <script>
    // Initialize AOS
    AOS.init({ duration: 800, once: true });

    // Loader
    window.addEventListener('load', () => {
      setTimeout(() => {
        document.getElementById('loader').style.opacity = '0';
        setTimeout(() => {
          document.getElementById('loader').style.display = 'none';
        }, 500);
      }, 800);
    });

    // Theme Toggle
    const themeToggle = document.getElementById('theme-toggle');
    const html = document.documentElement;
    const moonIcon = '<i class="ti ti-moon text-xl"></i>';
    const sunIcon = '<i class="ti ti-sun text-xl"></i>';

    themeToggle.addEventListener('click', () => {
      html.classList.toggle('dark');
      themeToggle.innerHTML = html.classList.contains('dark') ? sunIcon : moonIcon;
    });

    // Mobile Menu
    const mobileBtn = document.getElementById('mobile-menu-btn');
    const mobileMenu = document.getElementById('mobile-menu');
    const closeMenu = document.getElementById('close-menu');

    mobileBtn.addEventListener('click', () => mobileMenu.classList.remove('hidden'));
    closeMenu.addEventListener('click', () => mobileMenu.classList.add('hidden'));
    mobileMenu.addEventListener('click', (e) => {
      if (e.target === mobileMenu) mobileMenu.classList.add('hidden');
    });

    // Open Page Function
    function openPage(page) {
      const pages = {
        unit: { name: "انتخاب واحد", color: "bg-blue-600" },
        dorm: { name: "خوابگاه", color: "bg-amber-600" },
        food: { name: "رزرو غذا", color: "bg-green-600" }
      };
      
      const { name, color } = pages[page];
      const modal = document.createElement('div');
      modal.className = `fixed inset-0 ${color} bg-opacity-95 z-50 flex items-center justify-center p-6`;
      modal.innerHTML = `
        <div class="bg-white dark:bg-slate-800 rounded-3xl p-10 max-w-md w-full shadow-2xl text-center animate-pulse">
          <i class="ti ti-loader-2 text-6xl text-blue-600 mb-6 animate-spin"></i>
          <h3 class="text-2xl font-bold mb-3">در حال ورود...</h3>
          <p class="text-lg text-slate-600 dark:text-slate-300">به بخش <strong>${name}</strong></p>
          <button onclick="this.parentElement.parentElement.remove()" class="mt-8 px-6 py-2 bg-slate-200 dark:bg-slate-700 rounded-xl">بستن</button>
        </div>
      `;
      document.body.appendChild(modal);
      setTimeout(() => modal.remove(), 3000);
    }

    // Add pulse to hero dots
    setInterval(() => {
      document.querySelectorAll('.animate-pulse').forEach(el => {
        el.style.animation = 'none';
        setTimeout(() => el.style.animation = '', 10);
      });
    }, 3000);
  </script>
</body>
</html>      font-weight: bold;
      transition: background 0.3s;
    }

    .card button:hover {
      background: #0065d9;
    }

    footer {
      background: #004aad;
      color: white;
      text-align: center;
      padding: 1rem;
      margin-top: 2rem;
    }

    @media (max-width: 600px) {
      header h1 {
        font-size: 1rem;
      }
      .hero h2 {
        font-size: 1.6rem;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>سامانه دانشگاهی</h1>
    <nav>
      <ul>
        <li><a href="#">خانه</a></li>
        <li><a href="#">انتخاب واحد</a></li>
        <li><a href="#">خوابگاه</a></li>
        <li><a href="#">رزرو غذا</a></li>
        <li><a href="#">خروج</a></li>
      </ul>
    </nav>
  </header>

  <section class="hero">
    <h2>به سامانه دانشگاه خوش آمدید</h2>
    <p>اینجا می‌توانید انتخاب واحد انجام دهید، خوابگاه رزرو کنید و غذای خود را انتخاب نمایید.</p>
  </section>

  <section class="cards">
    <div class="card">
      <img src="https://cdn-icons-png.flaticon.com/512/3135/3135810.png" alt="انتخاب واحد">
      <h3>انتخاب واحد</h3>
      <p>دروس ترم جدید را مشاهده و انتخاب کنید.</p>
      <button onclick="openPage('unit')">ورود</button>
    </div>

    <div class="card">
      <img src="https://cdn-icons-png.flaticon.com/512/1046/1046857.png" alt="خوابگاه">
      <h3>خوابگاه</h3>
      <p>اتاق مورد نظر خود را رزرو یا تمدید کنید.</p>
      <button onclick="openPage('dorm')">ورود</button>
    </div>

    <div class="card">
      <img src="https://cdn-icons-png.flaticon.com/512/1046/1046784.png" alt="رزرو غذا">
      <h3>رزرو غذا</h3>
      <p>غذای هفته آینده خود را انتخاب و رزرو کنید.</p>
      <button onclick="openPage('food')">ورود</button>
    </div>
  </section>

  <footer>
    <p>© ۲۰۲۵ سامانه دانشگاهی | طراحی شده توسط تیم فناوری اطلاعات</p>
  </footer>

  <script>
    function openPage(page) {
      alert("در حال ورود به بخش " + page + "...");
      // در آینده می‌تونی به صفحه مخصوص هر بخش هدایت کنی
      // location.href = page + ".html";
    }
  </script>
</body>
</html>
