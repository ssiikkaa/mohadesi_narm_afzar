```html
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
    table {
      width: 100%;
      border-collapse: separate;
      border-spacing: 0 1rem;
    }
    th, td {
      padding: 1rem;
      text-align: right;
    }
    th {
      background: var(--primary);
      color: white;
    }
    tr {
      background: white;
      box-shadow: 0 2px 10px rgba(0,0,0,0.05);
      border-radius: 8px;
    }
    .dark tr {
      background: #1f2937;
    }
    .dark th {
      background: #111827;
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
        <a href="#home" class="hover:text-yellow-300 transition-colors font-medium">خانه</a>
        <a href="#unit" class="hover:text-yellow-300 transition-colors font-medium">انتخاب واحد</a>
        <a href="#dorm" class="hover:text-yellow-300 transition-colors font-medium">خوابگاه</a>
        <a href="#food" class="hover:text-yellow-300 transition-colors font-medium">رزرو غذا</a>
        <a href="#" class="text-yellow-300 font-bold" onclick="logout()">خروج</a>
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
      <a href="#home" class="block text-white hover:text-yellow-400 transition">خانه</a>
      <a href="#unit" class="block text-white hover:text-yellow-400 transition">انتخاب واحد</a>
      <a href="#dorm" class="block text-white hover:text-yellow-400 transition">خوابگاه</a>
      <a href="#food" class="block text-white hover:text-yellow-400 transition">رزرو غذا</a>
      <a href="#" class="block text-yellow-400 font-bold" onclick="logout()">خروج</a>
    </nav>
  </div>

  <!-- Hero Section (Home) -->
  <section id="home" class="relative py-24 overflow-hidden">
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
          <a href="#unit" class="btn-glow w-full py-3 rounded-xl bg-gradient-to-r from-blue-600 to-indigo-700 text-white font-bold shadow-lg hover:shadow-blue-500/25 transition-all block text-center">
            ورود به سیستم
          </a>
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
          <a href="#dorm" class="btn-glow w-full py-3 rounded-xl bg-gradient-to-r from-amber-500 to-orange-600 text-white font-bold shadow-lg hover:shadow-amber-500/25 transition-all block text-center">
            رزرو اتاق
          </a>
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
          <a href="#food" class="btn-glow w-full py-3 rounded-xl bg-gradient-to-r from-green-500 to-emerald-600 text-white font-bold shadow-lg hover:shadow-green-500/25 transition-all block text-center">
            انتخاب غذا
          </a>
        </div>
      </div>
    </div>
  </section>

  <!-- Unit Selection Section -->
  <section id="unit" class="py-16 bg-slate-100 dark:bg-slate-900">
    <div class="container mx-auto px-6">
      <h2 class="text-3xl font-bold text-center mb-12 text-blue-900 dark:text-blue-300">انتخاب واحد</h2>
      <div class="bg-white dark:bg-slate-800 rounded-3xl p-8 shadow-xl">
        <div class="mb-6 flex justify-between items-center">
          <input type="text" id="unit-search" placeholder="جستجو دروس..." class="p-3 rounded-xl border border-slate-300 dark:border-slate-600 bg-transparent w-1/2">
          <select id="unit-filter" class="p-3 rounded-xl border border-slate-300 dark:border-slate-600 bg-transparent">
            <option>همه گروه‌ها</option>
            <option>کامپیوتر</option>
            <option>مهندسی</option>
            <option>علوم پایه</option>
          </select>
        </div>
        <table>
          <thead>
            <tr>
              <th>نام درس</th>
              <th>واحد</th>
              <th>استاد</th>
              <th>زمان</th>
              <th>انتخاب</th>
            </tr>
          </thead>
          <tbody id="unit-table">
            <!-- Sample Rows -->
            <tr>
              <td>برنامه‌نویسی پیشرفته</td>
              <td>3</td>
              <td>دکتر احمدی</td>
              <td>شنبه 10-12</td>
              <td><input type="checkbox" class="unit-checkbox"></td>
            </tr>
            <tr>
              <td>ریاضیات گسسته</td>
              <td>3</td>
              <td>دکتر رضایی</td>
              <td>یکشنبه 14-16</td>
              <td><input type="checkbox" class="unit-checkbox"></td>
            </tr>
            <tr>
              <td>فیزیک 1</td>
              <td>4</td>
              <td>دکتر محمدی</td>
              <td>دوشنبه 8-10</td>
              <td><input type="checkbox" class="unit-checkbox"></td>
            </tr>
            <!-- Add more rows as needed -->
          </tbody>
        </table>
        <div class="mt-8 flex justify-end">
          <button onclick="saveUnits()" class="btn-glow px-8 py-3 rounded-xl bg-blue-600 text-white font-bold shadow-lg">ثبت انتخاب واحد</button>
        </div>
      </div>
    </div>
  </section>

  <!-- Dorm Reservation Section -->
  <section id="dorm" class="py-16">
    <div class="container mx-auto px-6">
      <h2 class="text-3xl font-bold text-center mb-12 text-amber-700 dark:text-amber-300">رزرو خوابگاه</h2>
      <div class="bg-white dark:bg-slate-800 rounded-3xl p-8 shadow-xl">
        <form id="dorm-form">
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
            <div>
              <label class="block mb-2 font-medium">نوع اتاق</label>
              <select class="w-full p-3 rounded-xl border border-slate-300 dark:border-slate-600 bg-transparent">
                <option>تک نفره</option>
                <option>دو نفره</option>
                <option>سه نفره</option>
              </select>
            </div>
            <div>
              <label class="block mb-2 font-medium">ساختمان</label>
              <select class="w-full p-3 rounded-xl border border-slate-300 dark:border-slate-600 bg-transparent">
                <option>ساختمان A</option>
                <option>ساختمان B</option>
                <option>ساختمان C</option>
              </select>
            </div>
            <div>
              <label class="block mb-2 font-medium">طبقه</label>
              <input type="number" min="1" max="10" class="w-full p-3 rounded-xl border border-slate-300 dark:border-slate-600 bg-transparent">
            </div>
            <div>
              <label class="block mb-2 font-medium">شماره اتاق</label>
              <input type="text" placeholder="مثال: 101" class="w-full p-3 rounded-xl border border-slate-300 dark:border-slate-600 bg-transparent">
            </div>
          </div>
          <div class="flex justify-end">
            <button type="button" onclick="saveDorm()" class="btn-glow px-8 py-3 rounded-xl bg-amber-600 text-white font-bold shadow-lg">رزرو اتاق</button>
          </div>
        </form>
      </div>
    </div>
  </section>

  <!-- Food Reservation Section -->
  <section id="food" class="py-16 bg-slate-100 dark:bg-slate-900">
    <div class="container mx-auto px-6">
      <h2 class="text-3xl font-bold text-center mb-12 text-green-700 dark:text-green-300">رزرو غذا</h2>
      <div class="bg-white dark:bg-slate-800 rounded-3xl p-8 shadow-xl">
        <div class="mb-6">
          <label class="block mb-2 font-medium">انتخاب روز</label>
          <select id="food-day" class="w-full p-3 rounded-xl border border-slate-300 dark:border-slate-600 bg-transparent">
            <option>شنبه</option>
            <option>یکشنبه</option>
            <option>دوشنبه</option>
            <option>سه‌شنبه</option>
            <option>چهارشنبه</option>
            <option>پنجشنبه</option>
            <option>جمعه</option>
          </select>
        </div>
        <table>
          <thead>
            <tr>
              <th>نام غذا</th>
              <th>قیمت (تومان)</th>
              <th>انتخاب</th>
            </tr>
          </thead>
          <tbody id="food-table">
            <!-- Sample Rows -->
            <tr>
              <td>چلو کباب</td>
              <td>۵۰,۰۰۰</td>
              <td><input type="checkbox" class="food-checkbox"></td>
            </tr>
            <tr>
              <td>زرشک پلو با مرغ</td>
              <td>۴۰,۰۰۰</td>
              <td><input type="checkbox" class="food-checkbox"></td>
            </tr>
            <tr>
              <td>قورمه سبزی</td>
              <td>۳۵,۰۰۰</td>
              <td><input type="checkbox" class="food-checkbox"></td>
            </tr>
            <!-- Add more rows as needed -->
          </tbody>
        </table>
        <div class="mt-8 flex justify-end">
          <button onclick="saveFood()" class="btn-glow px-8 py-3 rounded-xl bg-green-600 text-white font-bold shadow-lg">ثبت رزرو غذا</button>
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
      localStorage.setItem('theme', html.classList.contains('dark') ? 'dark' : 'light');
    });

    // Load saved theme
    if (localStorage.getItem('theme') === 'dark') {
      html.classList.add('dark');
      themeToggle.innerHTML = sunIcon;
    }

    // Mobile Menu
    const mobileBtn = document.getElementById('mobile-menu-btn');
    const mobileMenu = document.getElementById('mobile-menu');
    const closeMenu = document.getElementById('close-menu');

    mobileBtn.addEventListener('click', () => mobileMenu.classList.remove('hidden'));
    closeMenu.addEventListener('click', () => mobileMenu.classList.add('hidden'));
    mobileMenu.addEventListener('click', (e) => {
      if (e.target === mobileMenu) mobileMenu.classList.add('hidden');
    });

    // Smooth Scroll for Links
    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
      anchor.addEventListener('click', function (e) {
        e.preventDefault();
        document.querySelector(this.getAttribute('href')).scrollIntoView({
          behavior: 'smooth'
        });
        mobileMenu.classList.add('hidden');
      });
    });

    // Unit Selection Functions
    function saveUnits() {
      const selected = Array.from(document.querySelectorAll('.unit-checkbox:checked')).map(cb => cb.parentElement.parentElement.children[0].textContent);
      localStorage.setItem('selectedUnits', JSON.stringify(selected));
      alert('انتخاب واحد ثبت شد: ' + selected.join(', '));
    }

    // Dorm Reservation Functions
    function saveDorm() {
      const formData = new FormData(document.getElementById('dorm-form'));
      const data = Object.fromEntries(formData);
      localStorage.setItem('dormReservation', JSON.stringify(data));
      alert('رزرو خوابگاه ثبت شد!');
    }

    // Food Reservation Functions
    function saveFood() {
      const day = document.getElementById('food-day').value;
      const selected = Array.from(document.querySelectorAll('.food-checkbox:checked')).map(cb => cb.parentElement.parentElement.children[0].textContent);
      localStorage.setItem('foodReservation_' + day, JSON.stringify(selected));
      alert('رزرو غذا برای ' + day + ' ثبت شد: ' + selected.join(', '));
    }

    // Logout Function
    function logout() {
      localStorage.clear();
      alert('شما از سیستم خارج شدید.');
      window.location.href = '#home';
    }

    // Search and Filter for Units
    const unitSearch = document.getElementById('unit-search');
    const unitFilter = document.getElementById('unit-filter');
    const unitTable = document.getElementById('unit-table');

    function filterUnits() {
      const searchText = unitSearch.value.toLowerCase();
      const filterGroup = unitFilter.value;
      Array.from(unitTable.rows).forEach(row => {
        const name = row.cells[0].textContent.toLowerCase();
        const group = row.getAttribute('data-group') || ''; // Add data-group to rows if needed
        row.style.display = (name.includes(searchText) && (filterGroup === 'همه گروه‌ها' || group === filterGroup)) ? '' : 'none';
      });
    }

    unitSearch.addEventListener('input', filterUnits);
    unitFilter.addEventListener('change', filterUnits);
  </script>
</body>
</html>
```
