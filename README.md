<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>สถานการณ์งานวิจัยภาคประชาสังคมไทย | Thai CSO Research Report</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;500;700&display=swap" rel="stylesheet">

    <!-- Chosen Palette: Warm Neutrals & Earth Tones -->
    <!-- Background: Cream (#FAF9F6) -->
    <!-- Text: Dark Slate (#334155) -->
    <!-- Accents: Terracotta (#E76F51), Sage Green (#2A9D8F), Muted Blue (#457B9D) -->

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Sarabun', 'sans-serif'],
                    },
                    colors: {
                        cream: '#FAF9F6',
                        slate: '#334155',
                        terracotta: '#E76F51',
                        sage: '#2A9D8F',
                        mutedBlue: '#457B9D',
                        sand: '#E9C46A'
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #FAF9F6;
            color: #334155;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin: 0 auto;
            height: 300px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
        .card {
            transition: all 0.3s ease;
        }
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
        }
        .nav-item.active {
            border-bottom: 3px solid #E76F51;
            font-weight: 700;
        }
        /* Custom scrollbar for better aesthetics */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1; 
        }
        ::-webkit-scrollbar-thumb {
            background: #ccc; 
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #aaa; 
        }
    </style>

    <!-- Application Structure Plan:
         1. Header/Hero: Establishes the theme "From Activism to Evidence".
         2. Context Section: Explains 'Why Research?' with clickable cards.
         3. Dashboard Section: Quantitative data (Topics, Funding) using Chart.js.
         4. Analysis Section: Radar chart for Skill Gaps (Capacity Building).
         5. Process Section: Step-by-step interactive guide on how CSOs conduct research.
         6. Conclusion: Summary and Recommendations.
         Rationale: This structure moves from the 'Why' to the 'What' (Data) and 'How' (Process), typical for a strategic report.
    -->

    <!-- Visualization & Content Choices:
         1. Donut Chart: To show the distribution of research topics (Environment vs Rights etc). Goal: Inform.
         2. Bar Chart: To compare funding sources (Domestic vs International). Goal: Compare.
         3. Radar Chart: To visualize the gap between current skills and required skills. Goal: Compare/Relationships.
         4. Interactive List: To explain the research methodology/process without clutter. Goal: Change/Process.
         All visualizations use Chart.js (Canvas) or HTML/CSS. NO SVG.
    -->
    
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

</head>
<body class="font-sans antialiased selection:bg-terracotta selection:text-white">

    <!-- Navigation -->
    <nav class="sticky top-0 z-50 bg-white/90 backdrop-blur-md shadow-sm border-b border-gray-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16">
                <div class="flex items-center">
                    <span class="text-2xl font-bold text-terracotta tracking-tight">CSO Research Focus</span>
                </div>
                <div class="hidden md:flex space-x-8 items-center">
                    <button onclick="scrollToSection('hero')" class="nav-item text-slate hover:text-terracotta px-3 py-2 text-sm font-medium transition-colors">หน้าแรก</button>
                    <button onclick="scrollToSection('context')" class="nav-item text-slate hover:text-terracotta px-3 py-2 text-sm font-medium transition-colors">บริบท</button>
                    <button onclick="scrollToSection('data')" class="nav-item text-slate hover:text-terracotta px-3 py-2 text-sm font-medium transition-colors">ข้อมูลสถิติ</button>
                    <button onclick="scrollToSection('capacity')" class="nav-item text-slate hover:text-terracotta px-3 py-2 text-sm font-medium transition-colors">ศักยภาพ</button>
                    <button onclick="scrollToSection('process')" class="nav-item text-slate hover:text-terracotta px-3 py-2 text-sm font-medium transition-colors">กระบวนการ</button>
                </div>
                <!-- Mobile menu button placeholder (functional logic omitted for brevity in SPA focus) -->
                <div class="flex items-center md:hidden">
                    <button class="text-slate hover:text-terracotta p-2">☰</button>
                </div>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <header id="hero" class="relative bg-cream pt-16 pb-20 lg:pt-24 lg:pb-28 overflow-hidden">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative">
            <div class="text-center">
                <h1 class="text-4xl tracking-tight font-extrabold text-slate sm:text-5xl md:text-6xl">
                    <span class="block">ทิศทางใหม่ภาคประชาสังคม</span>
                    <span class="block text-terracotta mt-2">สู่การขับเคลื่อนด้วยงานวิจัย</span>
                </h1>
                <p class="mt-4 max-w-2xl mx-auto text-xl text-gray-500">
                    รายงานสถานการณ์การปรับตัวขององค์กรพัฒนาเอกชน (NGOs) และภาคประชาสังคมในประเทศไทย ที่เริ่มนำกระบวนการวิจัยมาใช้เพื่อสร้างข้อเสนอเชิงนโยบายที่แข็งแกร่ง
                </p>
                <div class="mt-8 flex justify-center gap-4">
                    <div class="bg-white p-4 rounded-xl shadow-sm border border-gray-100 text-center w-32">
                        <span class="block text-3xl font-bold text-sage">65%</span>
                        <span class="text-xs text-gray-500">องค์กรเริ่มทำวิจัย</span>
                    </div>
                    <div class="bg-white p-4 rounded-xl shadow-sm border border-gray-100 text-center w-32">
                        <span class="block text-3xl font-bold text-mutedBlue">120+</span>
                        <span class="text-xs text-gray-500">โครงการในปีนี้</span>
                    </div>
                </div>
                <div class="mt-8">
                    <button onclick="scrollToSection('context')" class="inline-flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-full text-white bg-terracotta hover:bg-orange-600 md:py-4 md:text-lg md:px-10 transition-all shadow-lg shadow-terracotta/30">
                        เริ่มสำรวจข้อมูล
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- Section 1: Context (Why Research?) -->
    <section id="context" class="py-16 bg-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-slate">ทำไมต้องวิจัย?</h2>
                <p class="mt-4 text-lg text-gray-600 max-w-3xl mx-auto">
                    ส่วนนี้อธิบายถึงแรงกดดันและการเปลี่ยนแปลงที่ทำให้องค์กรภาคประชาสังคมต้องหันมาให้ความสำคัญกับการรวบรวมข้อมูลอย่างเป็นระบบ (Evidence-Based Advocacy) แทนการรณรงค์แบบดั้งเดิมเพียงอย่างเดียว
                </p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <!-- Card 1 -->
                <div class="card bg-cream p-8 rounded-2xl border border-gray-100 cursor-pointer" onclick="highlightContext(1)">
                    <div class="h-12 w-12 bg-sage/20 rounded-full flex items-center justify-center mb-4 text-2xl">📊</div>
                    <h3 class="text-xl font-bold text-slate mb-2">ความน่าเชื่อถือของข้อมูล</h3>
                    <p class="text-gray-600 text-sm">การเจรจากับภาครัฐจำเป็นต้องมีตัวเลขและสถิติที่อ้างอิงได้ชัดเจน เพื่อสนับสนุนข้อเรียกร้อง</p>
                </div>
                <!-- Card 2 -->
                <div class="card bg-cream p-8 rounded-2xl border border-gray-100 cursor-pointer" onclick="highlightContext(2)">
                    <div class="h-12 w-12 bg-mutedBlue/20 rounded-full flex items-center justify-center mb-4 text-2xl">💰</div>
                    <h3 class="text-xl font-bold text-slate mb-2">เงื่อนไขแหล่งทุน</h3>
                    <p class="text-gray-600 text-sm">แหล่งทุนสากลเริ่มกำหนดให้มีการวิจัยประเมินผลและข้อมูลพื้นฐาน (Baseline Data) ในโครงการ</p>
                </div>
                <!-- Card 3 -->
                <div class="card bg-cream p-8 rounded-2xl border border-gray-100 cursor-pointer" onclick="highlightContext(3)">
                    <div class="h-12 w-12 bg-terracotta/20 rounded-full flex items-center justify-center mb-4 text-2xl">📣</div>
                    <h3 class="text-xl font-bold text-slate mb-2">การสื่อสารสาธารณะ</h3>
                    <p class="text-gray-600 text-sm">สังคมปัจจุบันต้องการข้อเท็จจริง (Fact) มากกว่าความเห็น การวิจัยช่วยให้การสื่อสารมีพลังมากขึ้น</p>
                </div>
            </div>
            
            <!-- Context Detail View (Dynamic) -->
            <div id="context-detail" class="mt-8 p-6 bg-slate text-white rounded-xl hidden transition-all duration-500">
                <h4 id="context-title" class="text-lg font-bold mb-2"></h4>
                <p id="context-desc" class="text-gray-200"></p>
            </div>
        </div>
    </section>

    <!-- Section 2: Data Dashboard -->
    <section id="data" class="py-16 bg-cream">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="mb-10">
                <h2 class="text-3xl font-bold text-slate">สถิติและข้อมูลสำคัญ</h2>
                <p class="mt-4 text-lg text-gray-600 max-w-4xl">
                    การสำรวจโครงการวิจัยของภาคประชาสังคมไทยในปีที่ผ่านมา พบความหลากหลายในประเด็นที่ศึกษาและที่มาของงบประมาณ ข้อมูลนี้สะท้อนถึงทิศทางความสนใจของสังคม
                </p>
            </div>

            <!-- Filters -->
            <div class="flex flex-wrap gap-4 mb-8 justify-center md:justify-start">
                <button onclick="updateCharts('all')" class="filter-btn active px-4 py-2 rounded-full bg-white border border-gray-200 text-sm hover:border-terracotta hover:text-terracotta transition-colors shadow-sm">ข้อมูลทั้งหมด</button>
                <button onclick="updateCharts('north')" class="filter-btn px-4 py-2 rounded-full bg-white border border-gray-200 text-sm hover:border-terracotta hover:text-terracotta transition-colors shadow-sm">ภาคเหนือ</button>
                <button onclick="updateCharts('northeast')" class="filter-btn px-4 py-2 rounded-full bg-white border border-gray-200 text-sm hover:border-terracotta hover:text-terracotta transition-colors shadow-sm">ภาคอีสาน</button>
                <button onclick="updateCharts('south')" class="filter-btn px-4 py-2 rounded-full bg-white border border-gray-200 text-sm hover:border-terracotta hover:text-terracotta transition-colors shadow-sm">ภาคใต้</button>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
                <!-- Chart 1: Topics -->
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-gray-100">
                    <h3 class="text-xl font-semibold text-slate mb-4 text-center">สัดส่วนประเด็นที่ทำการวิจัย</h3>
                    <div class="chart-container">
                        <canvas id="topicChart"></canvas>
                    </div>
                    <p class="mt-4 text-xs text-gray-400 text-center">ที่มา: การสำรวจข้อมูลองค์กรภาคประชาสังคม 2567</p>
                </div>

                <!-- Chart 2: Funding -->
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-gray-100">
                    <h3 class="text-xl font-semibold text-slate mb-4 text-center">แหล่งทุนสนับสนุนการวิจัย</h3>
                    <div class="chart-container">
                        <canvas id="fundingChart"></canvas>
                    </div>
                    <p class="mt-4 text-xs text-gray-400 text-center">หน่วย: ล้านบาท (THB Million)</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Section 3: Capacity Gap (Analysis) -->
    <section id="capacity" class="py-16 bg-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-12 items-center">
                <div class="lg:col-span-1">
                    <h2 class="text-3xl font-bold text-slate mb-6">ช่องว่างศักยภาพ (Skill Gaps)</h2>
                    <p class="text-gray-600 mb-6">
                        แม้จะมีความตื่นตัวในการทำวิจัย แต่บุคลากรในภาคประชาสังคมยังเผชิญความท้าทายด้านทักษะ โดยเฉพาะด้านการวิเคราะห์ข้อมูลเชิงลึก (Data Analytics) และการเขียนรายงานวิชาการ
                    </p>
                    <div class="bg-cream p-4 rounded-xl border-l-4 border-terracotta">
                        <h4 class="font-bold text-terracotta">ข้อค้นพบสำคัญ</h4>
                        <p class="text-sm text-gray-600 mt-2">
                            ทักษะด้าน "การลงพื้นที่เก็บข้อมูล" อยู่ในระดับดีเยี่ยม แต่ทักษะด้าน "สถิติ" และ "การนำเสนอข้อมูล" จำเป็นต้องได้รับการพัฒนาอย่างเร่งด่วน
                        </p>
                    </div>
                </div>
                <div class="lg:col-span-2">
                    <div class="bg-white p-4 rounded-2xl shadow-none md:shadow-lg border border-gray-100 md:border-none">
                        <div class="chart-container" style="max-height: 450px;">
                            <canvas id="radarChart"></canvas>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Section 4: Process (Interactive Timeline) -->
    <section id="process" class="py-16 bg-slate text-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-white">กระบวนการวิจัยฉบับภาคประชาสังคม</h2>
                <p class="mt-4 text-gray-300">
                    รูปแบบการวิจัยที่เน้นการมีส่วนร่วม (Participatory Action Research) มีขั้นตอนที่แตกต่างจากการวิจัยวิชาการทั่วไป คลิกเพื่อดูรายละเอียดแต่ละขั้นตอน
                </p>
            </div>

            <!-- Horizontal Stepper (Desktop) / Vertical (Mobile) -->
            <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4 relative">
                <!-- Line connector for desktop -->
                <div class="hidden md:block absolute top-1/2 left-0 w-full h-1 bg-gray-600 -z-0 transform -translate-y-1/2"></div>

                <!-- Steps -->
                <div class="step-item relative z-10 flex md:flex-col items-center gap-4 md:gap-2 cursor-pointer group w-full md:w-auto" onclick="showStep(1)">
                    <div class="w-12 h-12 rounded-full bg-terracotta flex items-center justify-center font-bold text-xl shadow-lg ring-4 ring-slate transition-transform group-hover:scale-110">1</div>
                    <span class="md:text-center font-semibold text-lg">ตั้งโจทย์</span>
                </div>
                <div class="step-item relative z-10 flex md:flex-col items-center gap-4 md:gap-2 cursor-pointer group w-full md:w-auto" onclick="showStep(2)">
                    <div class="w-12 h-12 rounded-full bg-gray-600 flex items-center justify-center font-bold text-xl shadow-lg ring-4 ring-slate transition-transform group-hover:scale-110 group-hover:bg-terracotta">2</div>
                    <span class="md:text-center font-semibold text-lg">เก็บข้อมูล</span>
                </div>
                <div class="step-item relative z-10 flex md:flex-col items-center gap-4 md:gap-2 cursor-pointer group w-full md:w-auto" onclick="showStep(3)">
                    <div class="w-12 h-12 rounded-full bg-gray-600 flex items-center justify-center font-bold text-xl shadow-lg ring-4 ring-slate transition-transform group-hover:scale-110 group-hover:bg-terracotta">3</div>
                    <span class="md:text-center font-semibold text-lg">วิเคราะห์</span>
                </div>
                <div class="step-item relative z-10 flex md:flex-col items-center gap-4 md:gap-2 cursor-pointer group w-full md:w-auto" onclick="showStep(4)">
                    <div class="w-12 h-12 rounded-full bg-gray-600 flex items-center justify-center font-bold text-xl shadow-lg ring-4 ring-slate transition-transform group-hover:scale-110 group-hover:bg-terracotta">4</div>
                    <span class="md:text-center font-semibold text-lg">คืนข้อมูล</span>
                </div>
            </div>

            <!-- Dynamic Content Area for Steps -->
            <div id="step-content" class="mt-12 bg-white/10 backdrop-blur-sm p-8 rounded-2xl border border-white/20 min-h-[200px] flex flex-col justify-center animate-fade-in">
                <h3 class="text-2xl font-bold text-terracotta mb-4">ขั้นตอนที่ 1: การตั้งโจทย์ร่วมกับชุมชน</h3>
                <p class="text-lg text-gray-200">
                    จุดเด่นของการวิจัยภาคประชาสังคมคือ "โจทย์ต้องมาจากปัญหาจริง" ไม่ใช่จากผู้วิจัยภายนอก มีการจัดเวทีชาวบ้านเพื่อระดมความคิดเห็น ค้นหาปัญหาเร่งด่วน เช่น ปัญหาที่ดินทำกิน หรือผลกระทบจากมลพิษ เพื่อนำมาออกแบบคำถามวิจัย
                </p>
                <div class="mt-6 flex gap-2">
                    <span class="px-3 py-1 bg-white/20 rounded-full text-xs">Brainstorming</span>
                    <span class="px-3 py-1 bg-white/20 rounded-full text-xs">Stakeholder Analysis</span>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-900 text-gray-400 py-12">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
            <h2 class="text-white text-2xl font-bold mb-4">บทสรุป</h2>
            <p class="max-w-2xl mx-auto mb-8">
                การเปลี่ยนผ่านสู่การใช้ "ข้อมูลนำทาง" (Data-Driven) ของภาคประชาสังคมไทย เป็นก้าวสำคัญที่จะช่วยให้การแก้ปัญหาสังคมมีประสิทธิภาพ ยั่งยืน และได้รับการยอมรับในระดับนโยบายมากขึ้น
            </p>
            <div class="border-t border-gray-800 pt-8 flex flex-col md:flex-row justify-between items-center text-sm">
                <p>&copy; 2024 Thai CSO Research Monitor. All rights reserved.</p>
                <div class="mt-4 md:mt-0 space-x-4">
                    <a href="#" class="hover:text-white">ดาวน์โหลดรายงานฉบับเต็ม</a>
                    <a href="#" class="hover:text-white">เกี่ยวกับเรา</a>
                </div>
            </div>
        </div>
    </footer>

    <!-- JavaScript Logic -->
    <script>
        // --- State Management ---
        const state = {
            currentStep: 1,
            currentFilter: 'all'
        };

        // --- Data Store ---
        const reportData = {
            context: [
                { id: 1, title: "ความน่าเชื่อถือ (Credibility)", desc: "งานวิจัยช่วยเปลี่ยนสถานะจาก 'ผู้เรียกร้อง' เป็น 'ผู้เชี่ยวชาญเฉพาะด้าน' ทำให้ภาครัฐรับฟังข้อเสนอมากขึ้น" },
                { id: 2, title: "ข้อกำหนดแหล่งทุน (Funding Requirements)", desc: "แหล่งทุนอย่าง EU หรือ USAID ต้องการเห็น Logic Model และตัวชี้วัดความสำเร็จที่วัดผลได้จริงจากการวิจัย" },
                { id: 3, title: "พลังการสื่อสาร (Communication Power)", desc: "Infographic ที่สร้างจากข้อมูลวิจัย ถูกแชร์ใน Social Media มากกว่าคำขวัญรณรงค์ถึง 3 เท่า" }
            ],
            steps: [
                { id: 1, title: "ขั้นตอนที่ 1: การตั้งโจทย์ร่วมกับชุมชน", desc: "จุดเด่นของการวิจัยภาคประชาสังคมคือ 'โจทย์ต้องมาจากปัญหาจริง' ไม่ใช่จากผู้วิจัยภายนอก มีการจัดเวทีชาวบ้านเพื่อระดมความคิดเห็น ค้นหาปัญหาเร่งด่วน เช่น ปัญหาที่ดินทำกิน หรือผลกระทบจากมลพิษ", tags: ["Brainstorming", "Stakeholder Analysis"] },
                { id: 2, title: "ขั้นตอนที่ 2: นักวิจัยไทบ้านเก็บข้อมูล", desc: "ฝึกอบรมชาวบ้านให้เป็น 'นักวิจัยไทบ้าน' ใช้เครื่องมือทั้งแบบสอบถาม การสัมภาษณ์ และการใช้ GPS จับพิกัดพื้นที่ เพื่อรวบรวมข้อมูลดิบที่มีความละเอียดสูง", tags: ["Field Survey", "Interview", "Mapping"] },
                { id: 3, title: "ขั้นตอนที่ 3: วิเคราะห์และสังเคราะห์", desc: "นำข้อมูลดิบมาประมวลผล ร่วมกับนักวิชาการพี่เลี้ยง (Mentors) เพื่อหาความสัมพันธ์ของปัญหาและแนวทางแก้ไขที่เป็นไปได้จริงตามหลักวิชาการ", tags: ["Data Analysis", "Validation"] },
                { id: 4, title: "ขั้นตอนที่ 4: คืนข้อมูลและผลักดันนโยบาย", desc: "นำผลวิจัยกลับไปคืนให้ชุมชนตรวจสอบ (Public Hearing) ก่อนนำไปยื่นต่อหน่วยงานรัฐหรือจัดเวทีสาธารณะเพื่อผลักดันข้อเสนอเชิงนโยบาย", tags: ["Public Hearing", "Policy Brief"] }
            ],
            charts: {
                topics: {
                    all: [35, 25, 20, 15, 5],
                    north: [45, 15, 20, 10, 10], // Focus on Environment/Resources
                    northeast: [20, 40, 20, 10, 10], // Focus on Rights/Inequality
                    south: [50, 10, 15, 15, 10] // Focus on Resources/Conflict
                },
                funding: {
                    all: [12, 19, 8, 5], // Domestic Gov, Int NGO, Public Donation, CSR
                    north: [3, 5, 2, 1],
                    northeast: [4, 7, 3, 2],
                    south: [2, 4, 1, 1]
                }
            }
        };

        // --- Chart Initialization ---
        let topicChartInstance = null;
        let fundingChartInstance = null;
        let radarChartInstance = null;

        document.addEventListener('DOMContentLoaded', () => {
            initCharts();
            highlightContext(1); // Default selection
        });

        function initCharts() {
            // Chart 1: Topics (Doughnut)
            const ctxTopic = document.getElementById('topicChart').getContext('2d');
            topicChartInstance = new Chart(ctxTopic, {
                type: 'doughnut',
                data: {
                    labels: ['ทรัพยากร/สิ่งแวดล้อม', 'สิทธิมนุษยชน', 'ความเหลื่อมล้ำ/ปากท้อง', 'การศึกษา/เยาวชน', 'อื่นๆ'],
                    datasets: [{
                        data: reportData.charts.topics.all,
                        backgroundColor: ['#2A9D8F', '#E76F51', '#F4A261', '#457B9D', '#E9C46A'],
                        borderWidth: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { position: 'right', labels: { font: { family: 'Sarabun' } } }
                    }
                }
            });

            // Chart 2: Funding (Bar)
            const ctxFunding = document.getElementById('fundingChart').getContext('2d');
            fundingChartInstance = new Chart(ctxFunding, {
                type: 'bar',
                data: {
                    labels: ['กองทุนภาครัฐ', 'องค์กรระหว่างประเทศ', 'บริจาคสาธารณะ', 'CSR ภาคธุรกิจ'],
                    datasets: [{
                        label: 'งบประมาณ (ล้านบาท)',
                        data: reportData.charts.funding.all,
                        backgroundColor: '#E76F51',
                        borderRadius: 5
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: { beginAtZero: true }
                    },
                    plugins: {
                        legend: { display: false }
                    }
                }
            });

            // Chart 3: Skills Radar
            const ctxRadar = document.getElementById('radarChart').getContext('2d');
            radarChartInstance = new Chart(ctxRadar, {
                type: 'radar',
                data: {
                    labels: ['การลงพื้นที่', 'การสร้างเครือข่าย', 'การเขียนโครงการ', 'การวิเคราะห์ข้อมูล', 'สถิติวิจัย', 'การใช้เทคโนโลยีดิจิทัล'],
                    datasets: [{
                        label: 'ทักษะปัจจุบัน',
                        data: [90, 85, 60, 40, 30, 45],
                        fill: true,
                        backgroundColor: 'rgba(231, 111, 81, 0.2)',
                        borderColor: '#E76F51',
                        pointBackgroundColor: '#E76F51',
                        pointBorderColor: '#fff',
                        pointHoverBackgroundColor: '#fff',
                        pointHoverBorderColor: '#E76F51'
                    }, {
                        label: 'ทักษะที่คาดหวัง',
                        data: [90, 90, 80, 80, 70, 80],
                        fill: true,
                        backgroundColor: 'rgba(42, 157, 143, 0.2)',
                        borderColor: '#2A9D8F',
                        pointBackgroundColor: '#2A9D8F',
                        pointBorderColor: '#fff',
                        pointHoverBackgroundColor: '#fff',
                        pointHoverBorderColor: '#2A9D8F'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    elements: { line: { tension: 0.3 } },
                    scales: {
                        r: {
                            angleLines: { display: true },
                            suggestedMin: 0,
                            suggestedMax: 100
                        }
                    }
                }
            });
        }

        // --- Interaction Logic ---

        // 1. Filter Logic
        function updateCharts(region) {
            // Update State
            state.currentFilter = region;

            // Update Buttons UI
            document.querySelectorAll('.filter-btn').forEach(btn => {
                btn.classList.remove('active', 'bg-terracotta', 'text-white');
                btn.classList.add('bg-white', 'text-slate');
            });
            event.target.classList.remove('bg-white', 'text-slate');
            event.target.classList.add('active', 'bg-terracotta', 'text-white');

            // Update Chart Data
            topicChartInstance.data.datasets[0].data = reportData.charts.topics[region];
            fundingChartInstance.data.datasets[0].data = reportData.charts.funding[region];

            topicChartInstance.update();
            fundingChartInstance.update();
        }

        // 2. Context Card Logic
        function highlightContext(id) {
            const detailBox = document.getElementById('context-detail');
            const title = document.getElementById('context-title');
            const desc = document.getElementById('context-desc');
            const data = reportData.context.find(item => item.id === id);

            if(data) {
                // Fade out effect
                detailBox.classList.add('opacity-0');
                
                setTimeout(() => {
                    detailBox.classList.remove('hidden');
                    title.innerText = data.title;
                    desc.innerText = data.desc;
                    detailBox.classList.remove('opacity-0');
                }, 200);
            }
        }

        // 3. Stepper Logic
        function showStep(stepId) {
            const contentDiv = document.getElementById('step-content');
            const data = reportData.steps.find(s => s.id === stepId);

            // Update UI dots
            const steps = document.querySelectorAll('.step-item div');
            steps.forEach((el, index) => {
                if (index + 1 === stepId) {
                    el.classList.remove('bg-gray-600');
                    el.classList.add('bg-terracotta');
                } else {
                    el.classList.remove('bg-terracotta');
                    el.classList.add('bg-gray-600');
                }
            });

            // Update Content with simple animation
            contentDiv.classList.add('opacity-50', 'scale-95');
            setTimeout(() => {
                let tagsHtml = data.tags.map(t => `<span class="px-3 py-1 bg-white/20 rounded-full text-xs">${t}</span>`).join('');
                contentDiv.innerHTML = `
                    <h3 class="text-2xl font-bold text-terracotta mb-4">${data.title}</h3>
                    <p class="text-lg text-gray-200">${data.desc}</p>
                    <div class="mt-6 flex gap-2 flex-wrap">${tagsHtml}</div>
                `;
                contentDiv.classList.remove('opacity-50', 'scale-95');
            }, 200);
        }

        // 4. Smooth Scroll
        function scrollToSection(id) {
            document.getElementById(id).scrollIntoView({ behavior: 'smooth' });
        }

    </script>
</body>
</html>
