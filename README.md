# nutc-home
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>探索中科大，開啟你的大學生活</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f0f2f5; /* 輕微的灰色背景 */
        }
        /* Custom styles for carousel */
        .carousel-container {
            overflow: hidden;
            position: relative;
        }
        .carousel-track {
            display: flex;
            transition: transform 0.5s ease-in-out;
        }
        .carousel-item {
            flex-shrink: 0;
            width: 100%;
        }
        .carousel-dot {
            width: 8px;
            height: 8px;
            background-color: rgba(255, 255, 255, 0.5);
            border-radius: 50%;
            margin: 0 4px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        .carousel-dot.active {
            background-color: white;
        }
        /* Custom styles for icon grid hover effect */
        .grid-item {
            transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
        }
        .grid-item:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
        }
        /* Custom styles for card hover effect */
        .content-card {
            transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
        }
        .content-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
        }
        /* Custom styles for trip style cards */
        .style-card {
            transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
        }
        .style-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
        }
    </style>
</head>
<body class="flex justify-center min-h-screen bg-gray-100">
    <div id="app-container" class="w-full max-w-md bg-white shadow-lg rounded-xl flex flex-col overflow-hidden">
        <header class="flex items-center justify-between p-4 bg-white shadow-sm">
            <div class="flex items-center">
                <div class="text-xl font-bold text-gray-800 mr-2">國立臺中科技大學</div>
                <button class="text-blue-500 hover:text-blue-700 focus:outline-none" onclick="openHelperChat()">
                    <i class="fas fa-robot text-xl"></i>
                </button>
            </div>
            <button class="text-gray-600 hover:text-blue-500 focus:outline-none" onclick="handleSearchClick()">
                <i class="fas fa-search text-xl"></i>
            </button>
        </header>

        <section class="p-4 bg-gradient-to-r from-green-400 to-blue-500 text-white rounded-b-xl shadow-md text-center">
            <h1 id="welcomeMessage" class="text-xl font-semibold mb-1">歡迎加入中科大，開啟你的大學新篇章！</h1>
            <p class="text-sm opacity-90">深入探索校園，找到你的專屬未來</p>
        </section>

        <section class="p-4 pt-6 pb-2 carousel-container">
            <h2 class="text-lg font-semibold text-gray-800 mb-4 px-2">中科大焦點 / 最新資訊</h2>
            <div class="carousel-track rounded-lg shadow-md">
                </div>
            <div class="carousel-dots flex justify-center mt-2"></div>
        </section>

        <section class="p-4 bg-white mx-4 rounded-xl shadow-md -mt-4 z-10">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-lg font-semibold text-gray-800">核心功能</h2>
                <button id="toggleCoreFeaturesBtn" class="text-gray-500 hover:text-gray-700 focus:outline-none" onclick="toggleCoreFeatures()">
                    <i class="fas fa-chevron-up text-lg"></i>
                </button>
            </div>
            <div id="coreFeaturesGrid" class="grid grid-cols-3 gap-4 text-center">
                </div>
        </section>

        <section class="flex-grow p-4 overflow-y-auto">
            <h2 class="text-lg font-semibold text-gray-800 mb-4 px-2">精選學院與特色 / 學習生活</h2>
            <div class="space-y-4" id="featuredContentCards">
                </div>
        </section>

        <nav class="flex justify-around items-center bg-white border-t border-gray-200 p-3 shadow-lg">
            <button class="flex flex-col items-center text-blue-500">
                <i class="fas fa-home text-xl mb-1"></i>
                <span class="text-xs">首頁</span>
            </button>
            <button class="flex flex-col items-center text-gray-500 hover:text-blue-500">
                <i class="fas fa-school text-xl mb-1"></i>
                <span class="text-xs">探索中科大</span>
            </button>
            <button class="flex flex-col items-center text-gray-500 hover:text-blue-500">
                <i class="fas fa-calendar-alt text-xl mb-1"></i>
                <span class="text-xs">活動</span>
            </button>
            <button class="flex flex-col items-center text-gray-500 hover:text-blue-500">
                <i class="fas fa-user-circle text-xl mb-1"></i>
                <span class="text-xs">我的</span>
            </button>
        </nav>
    </div>

    <script>
        // --- Data for dynamic content generation ---

        const carouselData = [
            {
                title: '新生入學懶人包：必備資訊全攻略',
                description: '從報到到選課，一步步帶你熟悉中科大生活。',
                imageUrl: 'https://placehold.co/400x200/A0E6FF/000000?text=新生入學懶人包',
                altText: '新生入學懶人包'
            },
            {
                title: '校園導覽報名中：親身感受中科大',
                description: '專人帶你走訪校園，體驗學術氛圍與設施。',
                imageUrl: 'https://placehold.co/400x200/FFD700/000000?text=校園導覽報名',
                altText: '校園導覽報名'
            },
            {
                title: '系所特色影音：找到你的熱情所在',
                description: '各系所專業介紹，探索你的未來學習方向。',
                imageUrl: 'https://placehold.co/400x200/FFA07A/000000?text=系所特色影音',
                altText: '系所特色影音'
            }
        ];

        const coreFeaturesData = [
            { name: '關於中科大', icon: 'fas fa-building', bgColor: 'bg-blue-50', hoverBg: 'hover:bg-blue-100', iconColor: 'text-blue-500' },
            { name: '系所介紹', icon: 'fas fa-graduation-cap', bgColor: 'bg-green-50', hoverBg: 'hover:bg-green-100', iconColor: 'text-green-500' },
            { name: '校園影片', icon: 'fas fa-video', bgColor: 'bg-red-50', hoverBg: 'hover:bg-red-100', iconColor: 'text-red-500' },
            { name: '聯絡我們', icon: 'fas fa-envelope', bgColor: 'bg-purple-50', hoverBg: 'hover:bg-purple-100', iconColor: 'text-purple-500' },
            { name: '校園地圖', icon: 'fas fa-map-marked-alt', bgColor: 'bg-yellow-50', hoverBg: 'hover:bg-yellow-100', iconColor: 'text-yellow-500' },
            { name: '資源中心', icon: 'fas fa-book', bgColor: 'bg-indigo-50', hoverBg: 'hover:bg-indigo-100', iconColor: 'text-indigo-500' },
            { name: '最新消息', icon: 'fas fa-bullhorn', bgColor: 'bg-teal-50', hoverBg: 'hover:bg-teal-100', iconColor: 'text-teal-500' },
            { name: '學生活動', icon: 'fas fa-users', bgColor: 'bg-orange-50', hoverBg: 'hover:bg-orange-100', iconColor: 'text-orange-500' },
            { name: '招生專區', icon: 'fas fa-clipboard-list', bgColor: 'bg-pink-50', hoverBg: 'hover:bg-pink-100', iconColor: 'text-pink-500' }
        ];

        const featuredCardsData = [
            {
                title: '商學院：培育國際商業人才',
                description: '跨領域學習，接軌全球市場，成為未來商業領袖。',
                imageUrl: 'https://placehold.co/400x200/9BB8CD/000000?text=商學院',
                altText: '商學院',
                infoIcon: 'fas fa-chart-line',
                infoText: '國際視野，實務應用',
                rating: '4.8'
            },
            {
                title: '設計學院：創意與實作的殿堂',
                description: '激發無限潛力，打造獨特作品，成為設計先鋒。',
                imageUrl: 'https://placehold.co/400x200/FFC0CB/000000?text=設計學院',
                altText: '設計學院',
                infoIcon: 'fas fa-palette',
                infoText: '美學素養，數位整合',
                rating: '4.7'
            },
            {
                title: '校園生活：食衣住行育樂',
                description: '豐富社團、便利設施，體驗多彩大學人生。',
                imageUrl: 'https://placehold.co/400x200/ADD8E6/000000?text=中科大校園生活',
                altText: '中科大校園生活',
                infoIcon: 'fas fa-basketball-ball',
                infoText: '社團活動，多元學習',
                rating: '4.9'
            }
        ];


        // --- Global variables for DOM elements (initialized after DOM content loaded) ---
        let currentCarouselIndex = 0;
        let carouselInterval;
        let carouselTrack;
        let carouselItems;
        let carouselDotsContainer;

        // --- Carousel Functions ---
        function generateCarouselItems() {
            const carouselTrackEl = document.querySelector('.carousel-track');
            carouselTrackEl.innerHTML = carouselData.map(item => `
                <div class="carousel-item p-2">
                    <div class="bg-white rounded-lg overflow-hidden">
                        <img src="${item.imageUrl}" alt="${item.altText}" class="w-full h-48 object-cover rounded-t-lg">
                        <div class="p-4">
                            <h3 class="text-lg font-semibold text-gray-800">${item.title}</h3>
                            <p class="text-sm text-gray-600 mt-1">${item.description}</p>
                            <button class="mt-3 w-full bg-blue-500 text-white py-2 rounded-md hover:bg-blue-600 transition duration-200" onclick="handleCarouselClick('${item.title}')">立即查看</button>
                        </div>
                    </div>
                </div>
            `).join('');
            c
