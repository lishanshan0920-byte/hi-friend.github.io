
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>北京海友共创技术有限公司 - IT外包服务专家</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Three.js -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <!-- GSAP 动画库 -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.4/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.4/ScrollTrigger.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@300;400;500;700&display=swap');
        
        :root {
            --primary-color: #0056b3;
            --secondary-color: #003366;
            --accent-color: #00a0e9;
            --dark-color: #333333;
            --light-color: #f5f5f5;
        }
        
        body {
            font-family: 'Noto Sans SC', sans-serif;
            color: var(--dark-color);
            overflow-x: hidden;
        }
        
        .text-gradient {
            background: linear-gradient(90deg, var(--primary-color), var(--accent-color));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        
        .bg-gradient {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
        }
        
        .card-hover {
            transition: all 0.3s ease;
        }
        
        .card-hover:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }
        
        .service-card {
            transition: all 0.4s ease;
            border-bottom: 3px solid transparent;
        }
        
        .service-card:hover {
            border-bottom: 3px solid var(--accent-color);
        }
        
        .animate-float {
            animation: float 6s ease-in-out infinite;
        }
        
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
            100% { transform: translateY(0px); }
        }
        
        #hero-canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }
        
        .chatbot-container {
            position: fixed;
            bottom: 30px;
            right: 30px;
            z-index: 1000;
        }
        
        .chatbot-button {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: var(--primary-color);
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(0, 86, 179, 0.3);
            transition: all 0.3s ease;
        }
        
        .chatbot-button:hover {
            transform: scale(1.1);
            background: var(--secondary-color);
        }
        
        .chatbot-panel {
            position: absolute;
            bottom: 80px;
            right: 0;
            width: 350px;
            height: 450px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
            display: none;
            flex-direction: column;
            overflow: hidden;
        }
        
        .chatbot-header {
            padding: 15px;
            background: var(--primary-color);
            color: white;
            font-weight: bold;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .chatbot-messages {
            flex: 1;
            padding: 15px;
            overflow-y: auto;
        }
        
        .message {
            margin-bottom: 15px;
            max-width: 80%;
            padding: 10px 15px;
            border-radius: 20px;
        }
        
        .bot-message {
            background: #f1f1f1;
            border-top-left-radius: 5px;
            align-self: flex-start;
        }
        
        .user-message {
            background: var(--primary-color);
            color: white;
            border-top-right-radius: 5px;
            align-self: flex-end;
            margin-left: auto;
        }
        
        .chatbot-input {
            padding: 15px;
            border-top: 1px solid #eee;
            display: flex;
        }
        
        .chatbot-input input {
            flex: 1;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 20px;
            margin-right: 10px;
        }
        
        .chatbot-input button {
            background: var(--primary-color);
            color: white;
            border: none;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: all 0.3s ease;
        }
        
        .chatbot-input button:hover {
            background: var(--secondary-color);
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            .chatbot-panel {
                width: 300px;
                height: 400px;
                right: -10px;
            }
        }
        
        @media (max-width: 640px) {
            .chatbot-panel {
                width: 280px;
                height: 350px;
            }
        }
        
        /* 滚动动画 */
        .fade-in {
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.6s ease, transform 0.6s ease;
        }
        
        .fade-in.active {
            opacity: 1;
            transform: translateY(0);
        }
        
        /* 数字增长动画 */
        .counter {
            font-weight: bold;
            font-size: 2.5rem;
            color: var(--primary-color);
        }
        
        /* 案例轮播 */
        .case-carousel {
            overflow: hidden;
            position: relative;
        }
        
        .case-slide {
            min-width: 100%;
            transition: transform 0.5s ease;
        }
        
        /* 导航菜单动画 */
        .nav-link {
            position: relative;
        }
        
        .nav-link::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--accent-color);
            transition: width 0.3s ease;
        }
        
        .nav-link:hover::after {
            width: 100%;
        }
        
        /* 移动端菜单 */
        .mobile-menu {
            position: fixed;
            top: 0;
            right: -100%;
            width: 80%;
            height: 100vh;
            background: white;
            z-index: 1000;
            transition: right 0.3s ease;
            box-shadow: -5px 0 15px rgba(0, 0, 0, 0.1);
            padding: 20px;
        }
        
        .mobile-menu.active {
            right: 0;
        }
        
        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 999;
            display: none;
        }
        
        .overlay.active {
            display: block;
        }
    </style>
</head>
<body>
    <!-- 导航栏 -->
    <nav class="bg-white shadow-md fixed w-full z-50">
        <div class="container mx-auto px-4 py-3">
            <div class="flex justify-between items-center">
                <div class="flex items-center">
                    <a href="#" class="text-2xl font-bold text-primary-color">
                        <span class="text-gradient">海友共创</span> <span class="text-blue-600">Hi-Friend</span>
                    </a>
                </div>
                
                <!-- 桌面端菜单 -->
                <div class="hidden md:flex space-x-8">
                    <a href="#home" class="nav-link text-gray-700 hover:text-blue-600 font-medium">首页</a>
                    <a href="#about" class="nav-link text-gray-700 hover:text-blue-600 font-medium">关于我们</a>
                    <a href="#services" class="nav-link text-gray-700 hover:text-blue-600 font-medium">服务项目</a>
                    <a href="#cases" class="nav-link text-gray-700 hover:text-blue-600 font-medium">成功案例</a>
                    <a href="#contact" class="nav-link text-gray-700 hover:text-blue-600 font-medium">联系我们</a>
                </div>
                
                <!-- 移动端菜单按钮 -->
                <div class="md:hidden">
                    <button id="menu-toggle" class="text-gray-700 focus:outline-none">
                        <i class="fas fa-bars text-2xl"></i>
                    </button>
                </div>
            </div>
        </div>
    </nav>
    
    <!-- 移动端菜单 -->
    <div class="mobile-menu">
        <div class="flex justify-between items-center mb-8">
            <span class="text-2xl font-bold text-gradient">海友共创</span>
            <button id="close-menu" class="text-gray-700 focus:outline-none">
                <i class="fas fa-times text-2xl"></i>
            </button>
        </div>
        <div class="flex flex-col space-y-4">
            <a href="#home" class="mobile-nav-link text-gray-700 hover:text-blue-600 font-medium py-2 border-b border-gray-100">首页</a>
            <a href="#about" class="mobile-nav-link text-gray-700 hover:text-blue-600 font-medium py-2 border-b border-gray-100">关于我们</a>
            <a href="#services" class="mobile-nav-link text-gray-700 hover:text-blue-600 font-medium py-2 border-b border-gray-100">服务项目</a>
            <a href="#cases" class="mobile-nav-link text-gray-700 hover:text-blue-600 font-medium py-2 border-b border-gray-100">成功案例</a>
            <a href="#contact" class="mobile-nav-link text-gray-700 hover:text-blue-600 font-medium py-2 border-b border-gray-100">联系我们</a>
        </div>
    </div>
    <div class="overlay"></div>
    
    <!-- 首页横幅 -->
    <section id="home" class="relative h-screen flex items-center">
        <canvas id="hero-canvas"></canvas>
        <div class="container mx-auto px-4 z-10">
            <div class="max-w-3xl">
                <h1 class="text-4xl md:text-6xl font-bold mb-6 leading-tight">
                    专业<span class="text-gradient">IT外包服务</span><br>
                    15年经验，值得信赖
                </h1>
                <p class="text-lg md:text-xl text-gray-700 mb-8">
                    北京海友共创技术有限公司，专注于为企业提供高质量的IT人员外包服务、定制化软件开发和猎头服务，助力企业数字化转型。
                </p>
                <div class="flex flex-wrap gap-4">
                    <a href="#services" class="bg-gradient text-white px-8 py-3 rounded-full font-medium hover:opacity-90 transition duration-300 flex items-center">
                        <span>了解服务</span>
                        <i class="fas fa-arrow-right ml-2"></i>
                    </a>
                    <a href="#contact" class="bg-white text-blue-600 border border-blue-600 px-8 py-3 rounded-full font-medium hover:bg-blue-50 transition duration-300">
                        联系我们
                    </a>
                </div>
            </div>
        </div>
    </section>
    
    <!-- 关于我们 -->
    <section id="about" class="py-20 bg-gray-50">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16">
                <h2 class="text-3xl md:text-4xl font-bold mb-4">关于我们</h2>
                <div class="w-24 h-1 bg-blue-600 mx-auto mb-6"></div>
                <p class="text-gray-700 max-w-3xl mx-auto">
                    海友共创成立于2018年，核心团队拥有15年+IT行业深耕经验，是专注为企业提供全方位IT解决方案的专业外包服务公司。
                </p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-12 items-center">
                <div class="fade-in">
                    <h3 class="text-2xl font-bold mb-4">我们的优势</h3>
                    <p class="text-gray-700 mb-6">
                        凭借丰富的行业经验和专业的技术团队，我们已成功为超过100+家企业客户提供了高质量的IT服务，赢得了广泛的信任和好评。
                    </p>
                    <ul class="space-y-4">
                        <li class="flex items-start">
                            <i class="fas fa-check-circle text-blue-600 mt-1 mr-3"></i>
                            <span>15年+IT外包服务经验，深入了解各行业需求</span>
                        </li>
                        <li class="flex items-start">
                            <i class="fas fa-check-circle text-blue-600 mt-1 mr-3"></i>
                            <span>200+专业技术人员，覆盖全栈开发、测试、运维等领域</span>
                        </li>
                        <li class="flex items-start">
                            <i class="fas fa-check-circle text-blue-600 mt-1 mr-3"></i>
                            <span>100+企业客户，包括多家世界500强企业和行业领军企业</span>
                        </li>
                        <li class="flex items-start">
                            <i class="fas fa-check-circle text-blue-600 mt-1 mr-3"></i>
                            <span>严格的质量控制体系，确保交付高质量的服务和产品</span>
                        </li>
                    </ul>
                </div>
                
                <div class="fade-in">
                    <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/fca2e91a04874b2a9860532b8cce980d~tplv-a9rns2rl98-image.image?rcl=20251113174338A7967EBFFFEB4F5030A2&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1765619068&x-signature=d6OSFayd2ylCAN3%2FvZ4IwTvqJjI%3D" 
                         alt="专业团队" 
                         class="rounded-lg shadow-xl w-full h-auto">
                </div>
            </div>
            
            <!-- 数据统计 -->
            <div class="grid grid-cols-1 sm:grid-cols-3 gap-8 mt-20">
                <div class="bg-white p-8 rounded-lg shadow-lg text-center fade-in">
                    <div class="counter" data-target="15">0</div>
                    <p class="text-gray-700 mt-2">年行业经验</p>
                </div>
                
                <div class="bg-white p-8 rounded-lg shadow-lg text-center fade-in" data-delay="200">
                    <div class="counter" data-target="100">0<span class="text-2xl font-bold text-blue-600">+</span></div>
                    <p class="text-gray-700 mt-2">企业客户</p>
                </div>
                
                <div class="bg-white p-8 rounded-lg shadow-lg text-center fade-in" data-delay="400">
                    <div class="counter" data-target="200">0<span class="text-2xl font-bold text-blue-600">+</span></div>
                    <p class="text-gray-700 mt-2">专业人员</p>
                </div>
            </div>
        </div>
    </section>
    
    <!-- 服务项目 -->
    <section id="services" class="py-20">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16">
                <h2 class="text-3xl md:text-4xl font-bold mb-4">服务项目</h2>
                <div class="w-24 h-1 bg-blue-600 mx-auto mb-6"></div>
                <p class="text-gray-700 max-w-3xl mx-auto">
                    我们提供全方位的IT服务，满足企业在不同发展阶段的各种需求，助力企业数字化转型。
                </p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <!-- IT人员外包 -->
                <div class="service-card bg-white rounded-lg shadow-lg overflow-hidden fade-in">
                    <div class="p-8">
                        <div class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mb-6">
                            <i class="fas fa-users text-blue-600 text-2xl"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-4">IT人员外包</h3>
                        <p class="text-gray-700 mb-6">
                            为企业提供灵活的IT人员外包服务，包括软件开发、测试、运维等各类技术人才，帮助企业快速组建专业团队，降低人力成本。
                        </p>
                        <ul class="space-y-2 mb-6">
                            <li class="flex items-center">
                                <i class="fas fa-check text-green-500 mr-2"></i>
                                <span>专业技术人才</span>
                            </li>
                            <li class="flex items-center">
                                <i class="fas fa-check text-green-500 mr-2"></i>
                                <span>灵活的合作模式</span>
                            </li>
                            <li class="flex items-center">
                                <i class="fas fa-check text-green-500 mr-2"></i>
                                <span>快速团队组建</span>
                            </li>
                            <li class="flex items-center">
                                <i class="fas fa-check text-green-500 mr-2"></i>
                                <span>降低人力成本</span>
                            </li>
                        </ul>
                        <a href="#contact" class="text-blue-600 font-medium hover:text-blue-800 flex items-center">
                            <span>了解更多</span>
                            <i class="fas fa-arrow-right ml-2"></i>
                        </a>
                    </div>
                </div>
                
                <!-- 定制化软件开发 -->
                <div class="service-card bg-white rounded-lg shadow-lg overflow-hidden fade-in" data-delay="200">
                    <div class="p-8">
                        <div class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mb-6">
                            <i class="fas fa-code text-blue-600 text-2xl"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-4">定制化软件开发</h3>
                        <p class="text-gray-700 mb-6">
                            根据企业特定需求，提供全流程的软件开发服务，包括需求分析、系统设计、开发测试、部署维护等，打造专属的企业级应用解决方案。
                        </p>
                        <ul class="space-y-2 mb-6">
                            <li class="flex items-center">
                                <i class="fas fa-check text-green-500 mr-2"></i>
                                <span>需求深度挖掘</span>
                            </li>
                            <li class="flex items-center">
                                <i class="fas fa-check text-green-500 mr-2"></i>
                                <span>专业架构设计</span>
                            </li>
                            <li class="flex items-center">
                                <i class="fas fa-check text-green-500 mr-2"></i>
                                <span>敏捷开发流程</span>
                            </li>
                            <li class="flex items-center">
                                <i class="fas fa-check text-green-500 mr-2"></i>
                                <span>全周期维护支持</span>
                            </li>
                        </ul>
                        <a href="#contact" class="text-blue-600 font-medium hover:text-blue-800 flex items-center">
                            <span>了解更多</span>
                            <i class="fas fa-arrow-right ml-2"></i>
                        </a>
                    </div>
                </div>
                
                <!-- 猎头服务 -->
                <div class="service-card bg-white rounded-lg shadow-lg overflow-hidden fade-in" data-delay="400">
                    <div class="p-8">
                        <div class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mb-6">
                            <i class="fas fa-user-tie text-blue-600 text-2xl"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-4">猎头服务</h3>
                        <p class="text-gray-700 mb-6">
                            为企业提供高端IT人才猎头服务，凭借丰富的人才资源和专业的招聘经验，帮助企业快速找到合适的技术管理人才。
                        </p>
                        <ul class="space-y-2 mb-6">
                            <li class="flex items-center">
                                <i class="fas fa-check text-green-500 mr-2"></i>
                                <span>高端人才寻访</span>
                            </li>
                            <li class="flex items-center">
                                <i class="fas fa-check text-green-500 mr-2"></i>
                                <span>专业人才评估</span>
                            </li>
                            <li class="flex items-center">
                                <i class="fas fa-check text-green-500 mr-2"></i>
                                <span>高效招聘流程</span>
                            </li>
                            <li class="flex items-center">
                                <i class="fas fa-check text-green-500 mr-2"></i>
                                <span>行业薪资咨询</span>
                            </li>
                        </ul>
                        <a href="#contact" class="text-blue-600 font-medium hover:text-blue-800 flex items-center">
                            <span>了解更多</span>
                            <i class="fas fa-arrow-right ml-2"></i>
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <!-- 成功案例 -->
    <section id="cases" class="py-20 bg-gray-50">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16">
                <h2 class="text-3xl md:text-4xl font-bold mb-4">成功案例</h2>
                <div class="w-24 h-1 bg-blue-600 mx-auto mb-6"></div>
                <p class="text-gray-700 max-w-3xl mx-auto">
                    我们已成功为众多企业提供了专业的IT服务，以下是部分代表性客户案例。
                </p>
            </div>
            
            <div class="case-carousel relative">
                <div class="flex transition-transform duration-500" id="caseSlider">
                    <!-- 案例1 -->
                    <div class="case-slide p-4">
                        <div class="bg-white rounded-lg shadow-lg overflow-hidden">
                            <div class="grid grid-cols-1 md:grid-cols-2">
                                <div class="p-8 flex flex-col justify-center">
                                    <span class="text-sm font-semibold text-blue-600 uppercase tracking-wider">金融行业</span>
                                    <h3 class="text-xl font-bold mt-2 mb-4">某大型银行核心系统升级</h3>
                                    <p class="text-gray-700 mb-6">
                                        为国内某大型银行提供核心业务系统升级服务，包括系统架构设计、代码重构、性能优化等，成功将系统响应时间降低70%，提升了用户体验和业务处理能力。
                                    </p>
                                    <div class="flex items-center text-gray-600">
                                        <span class="mr-4"><i class="fas fa-users mr-1"></i> 15人团队</span>
                                        <span><i class="fas fa-calendar-alt mr-1"></i> 12个月</span>
                                    </div>
                                </div>
                                <div class="bg-gray-200">
                                    <img src="https://p26-doubao-search-sign.byteimg.com/tos-cn-i-be4g95zd3a/939562871019143174~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1778579033&x-signature=lmIBndL1zQerX7fr5LiIYZY6%2FGs%3D" 
                                         alt="银行系统升级" 
                                         class="w-full h-full object-cover">
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- 案例2 -->
                    <div class="case-slide p-4">
                        <div class="bg-white rounded-lg shadow-lg overflow-hidden">
                            <div class="grid grid-cols-1 md:grid-cols-2">
                                <div class="p-8 flex flex-col justify-center">
                                    <span class="text-sm font-semibold text-blue-600 uppercase tracking-wider">电商行业</span>
                                    <h3 class="text-xl font-bold mt-2 mb-4">某知名电商平台性能优化</h3>
                                    <p class="text-gray-700 mb-6">
                                        为国内某知名电商平台提供全面的性能优化服务，通过架构调整、代码优化、缓存策略改进等措施，成功支持双11期间每秒10万+的并发访问，零宕机记录。
                                    </p>
                                    <div class="flex items-center text-gray-600">
                                        <span class="mr-4"><i class="fas fa-users mr-1"></i> 12人团队</span>
                                        <span><i class="fas fa-calendar-alt mr-1"></i> 8个月</span>
                                    </div>
                                </div>
                                <div class="bg-gray-200">
                                    <img src="https://p26-doubao-search-sign.byteimg.com/tos-cn-i-be4g95zd3a/905429812438368343~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1778579033&x-signature=lEQEatIGTlH%2FGEsM57aEPvpRJkI%3D" 
                                         alt="电商平台优化" 
                                         class="w-full h-full object-cover">
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- 案例3 -->
                    <div class="case-slide p-4">
                        <div class="bg-white rounded-lg shadow-lg overflow-hidden">
                            <div class="grid grid-cols-1 md:grid-cols-2">
                                <div class="p-8 flex flex-col justify-center">
                                    <span class="text-sm font-semibold text-blue-600 uppercase tracking-wider">制造业</span>
                                    <h3 class="text-xl font-bold mt-2 mb-4">某制造企业数字化转型</h3>
                                    <p class="text-gray-700 mb-6">
                                        为某大型制造企业提供全面的数字化转型解决方案，包括ERP系统定制开发、生产流程自动化、数据分析平台构建等，提升了生产效率30%，降低了运营成本20%。
                                    </p>
                                    <div class="flex items-center text-gray-600">
                                        <span class="mr-4"><i class="fas fa-users mr-1"></i> 20人团队</span>
                                        <span><i class="fas fa-calendar-alt mr-1"></i> 18个月</span>
                                    </div>
                                </div>
                                <div class="bg-gray-200">
                                    <img src="https://p26-doubao-search-sign.byteimg.com/tos-cn-i-be4g95zd3a/1481145405085450245~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1778579033&x-signature=rMErfRwXSh6jYlA24ikjcPoDasI%3D" 
                                         alt="制造业数字化转型" 
                                         class="w-full h-full object-cover">
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                
                <!-- 轮播控制按钮 -->
                <button id="prevCase" class="absolute top-1/2 left-4 transform -translate-y-1/2 bg-white rounded-full w-10 h-10 flex items-center justify-center shadow-md focus:outline-none z-10">
                    <i class="fas fa-chevron-left text-blue-600"></i>
                </button>
                <button id="nextCase" class="absolute top-1/2 right-4 transform -translate-y-1/2 bg-white rounded-full w-10 h-10 flex items-center justify-center shadow-md focus:outline-none z-10">
                    <i class="fas fa-chevron-right text-blue-600"></i>
                </button>
                
                <!-- 轮播指示器 -->
                <div class="flex justify-center mt-8">
                    <span class="case-dot w-3 h-3 rounded-full bg-blue-600 mx-1 cursor-pointer" data-index="0"></span>
                    <span class="case-dot w-3 h-3 rounded-full bg-gray-300 mx-1 cursor-pointer" data-index="1"></span>
                    <span class="case-dot w-3 h-3 rounded-full bg-gray-300 mx-1 cursor-pointer" data-index="2"></span>
                </div>
            </div>
        </div>
    </section>
    
    <!-- 客户评价 -->
    <section class="py-20">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16">
                <h2 class="text-3xl md:text-4xl font-bold mb-4">客户评价</h2>
                <div class="w-24 h-1 bg-blue-600 mx-auto mb-6"></div>
                <p class="text-gray-700 max-w-3xl mx-auto">
                    听听我们的客户怎么说，他们的成功故事是对我们服务最好的证明。
                </p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <!-- 评价1 -->
                <div class="bg-white p-8 rounded-lg shadow-lg fade-in">
                    <div class="flex items-center mb-6">
                        <div class="text-yellow-400 flex">
                            <i class="fas fa-star"></i>
                            <i class="fas fa-star"></i>
                            <i class="fas fa-star"></i>
                            <i class="fas fa-star"></i>
                            <i class="fas fa-star"></i>
                        </div>
                        <span class="ml-2 text-gray-600">5.0</span>
                    </div>
                    <p class="text-gray-700 mb-6">
                        "海友共创的团队非常专业，他们为我们提供的IT人员外包服务帮助我们快速组建了开发团队，项目按时高质量完成，大大超出了我们的预期。"
                    </p>
                    <div class="flex items-center">
                        <div class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center mr-4">
                            <span class="text-blue-600 font-bold">张</span>
                        </div>
                        <div>
                            <h4 class="font-medium">张总监</h4>
                            <p class="text-sm text-gray-600">某金融科技公司技术负责人</p>
                        </div>
                    </div>
                </div>
                
                <!-- 评价2 -->
                <div class="bg-white p-8 rounded-lg shadow-lg fade-in" data-delay="200">
                    <div class="flex items-center mb-6">
                        <div class="text-yellow-400 flex">
                            <i class="fas fa-star"></i>
                            <i class="fas fa-star"></i>
                            <i class="fas fa-star"></i>
                            <i class="fas fa-star"></i>
                            <i class="fas fa-star"></i>
                        </div>
                        <span class="ml-2 text-gray-600">5.0</span>
                    </div>
                    <p class="text-gray-700 mb-6">
                        "我们与海友共创合作多年，他们的定制化软件开发服务非常专业，能够深入理解我们的业务需求，提供切实可行的解决方案，是值得信赖的合作伙伴。"
                    </p>
                    <div class="flex items-center">
                        <div class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center mr-4">
                            <span class="text-blue-600 font-bold">李</span>
                        </div>
                        <div>
                            <h4 class="font-medium">李经理</h4>
                            <p class="text-sm text-gray-600">某大型制造企业IT部门经理</p>
                        </div>
                    </div>
                </div>
                
                <!-- 评价3 -->
                <div class="bg-white p-8 rounded-lg shadow-lg fade-in" data-delay="400">
                    <div class="flex items-center mb-6">
                        <div class="text-yellow-400 flex">
                            <i class="fas fa-star"></i>
                            <i class="fas fa-star"></i>
                            <i class="fas fa-star"></i>
                            <i class="fas fa-star"></i>
                            <i class="fas fa-star-half-alt"></i>
                        </div>
                        <span class="ml-2 text-gray-600">4.5</span>
                    </div>
                    <p class="text-gray-700 mb-6">
                        "海友共创的猎头服务非常高效，他们为我们找到了几位核心技术人才，大大提升了我们团队的实力。整个招聘过程专业、高效，沟通顺畅。"
                    </p>
                    <div class="flex items-center">
                        <div class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center mr-4">
                            <span class="text-blue-600 font-bold">王</span>
                        </div>
                        <div>
                            <h4 class="font-medium">王总</h4>
                            <p class="text-sm text-gray-600">某互联网创业公司CEO</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <!-- 联系我们 -->
    <section id="contact" class="py-20 bg-gray-50">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16">
                <h2 class="text-3xl md:text-4xl font-bold mb-4">联系我们</h2>
                <div class="w-24 h-1 bg-blue-600 mx-auto mb-6"></div>
                <p class="text-gray-700 max-w-3xl mx-auto">
                    如果您对我们的服务感兴趣，或者有任何问题，请随时联系我们，我们将竭诚为您服务。
                </p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
                <!-- 联系表单 -->
                <div class="bg-white p-8 rounded-lg shadow-lg fade-in">
                    <h3 class="text-xl font-bold mb-6">发送消息</h3>
                    <form id="contactForm">
                        <div class="mb-4">
                            <label for="name" class="block text-gray-700 mb-2">姓名</label>
                            <input type="text" id="name" name="name" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                        </div>
                        
                        <div class="mb-4">
                            <label for="company" class="block text-gray-700 mb-2">公司</label>
                            <input type="text" id="company" name="company" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                        </div>
                        
                        <div class="mb-4">
                            <label for="email" class="block text-gray-700 mb-2">邮箱</label>
                            <input type="email" id="email" name="email" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                        </div>
                        
                        <div class="mb-4">
                            <label for="phone" class="block text-gray-700 mb-2">电话</label>
                            <input type="tel" id="phone" name="phone" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                        </div>
                        
                        <div class="mb-4">
                            <label for="service" class="block text-gray-700 mb-2">感兴趣的服务</label>
                            <select id="service" name="service" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                                <option value="">请选择</option>
                                <option value="it-outsourcing">IT人员外包</option>
                                <option value="custom-software">定制化软件开发</option>
                                <option value="headhunting">猎头服务</option>
                                <option value="other">其他</option>
                            </select>
                        </div>
                        
                        <div class="mb-6">
                            <label for="message" class="block text-gray-700 mb-2">消息</label>
                            <textarea id="message" name="message" rows="5" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required></textarea>
                        </div>
                        
                        <button type="submit" class="bg-gradient text-white px-6 py-3 rounded-lg font-medium hover:opacity-90 transition duration-300 w-full">
                            发送消息
                        </button>
                    </form>
                </div>
                
                <!-- 联系信息 -->
                <div class="fade-in">
                    <h3 class="text-xl font-bold mb-6">联系方式</h3>
                    
                    <div class="bg-white p-6 rounded-lg shadow-lg mb-6">
                        <div class="flex items-start mb-4">
                            <div class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center mr-4">
                                <i class="fas fa-map-marker-alt text-blue-600"></i>
                            </div>
                            <div>
                                <h4 class="font-medium mb-1">地址</h4>
                                <p class="text-gray-700">北京市海淀区上地中关村软件园孵化器2号楼2-1</p>
                            </div>
                        </div>
                        
                        <div class="flex items-start mb-4">
                            <div class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center mr-4">
                                <i class="fas fa-envelope text-blue-600"></i>
                            </div>
                            <div>
                                <h4 class="font-medium mb-1">邮箱</h4>
                                <p class="text-gray-700">ito@hi-friend.cn</p>
                            </div>
                        </div>
                        
                        <div class="flex items-start">
                            <div class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center mr-4">
                                <i class="fas fa-phone-alt text-blue-600"></i>
                            </div>
                            <div>
                                <h4 class="font-medium mb-1">电话</h4>
                                <p class="text-gray-700">18611110649</p>
                            </div>
                        </div>
                    </div>
                    
                    <!-- 地图 -->
                    <div class="bg-white p-6 rounded-lg shadow-lg">
                        <h4 class="font-medium mb-4">公司位置</h4>
                        <div class="h-64 bg-gray-200 rounded-lg overflow-hidden">
                            <!-- 这里可以嵌入地图，或者使用静态地图图片 -->
                            <div class="w-full h-full flex items-center justify-center bg-gray-100">
                                <span class="text-gray-500">地图加载中...</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <!-- 版权信息 -->
    <div class="bg-gray-900 text-white py-6">
        <div class="container mx-auto px-4 text-center">
            <p class="text-gray-400">© 2023 北京海友共创技术有限公司. 保留所有权利.</p>
        </div>
    </div>
    
    <!-- AI智能客服 -->
    <div class="chatbot-container">
        <div class="chatbot-button" id="chatbotToggle">
            <i class="fas fa-comments text-white text-2xl"></i>
        </div>
        
        <div class="chatbot-panel" id="chatbotPanel">
            <div class="chatbot-header">
                <span>智能客服</span>
                <button id="closeChatbot" class="text-white focus:outline-none">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <div class="chatbot-messages" id="chatbotMessages">
                <div class="message bot-message">
                    您好！我是海友共创的智能客服助手，很高兴为您服务。请问有什么可以帮助您的吗？
                </div>
            </div>
            
            <div class="chatbot-input">
                <input type="text" id="chatbotInput" placeholder="请输入您的问题..." class="focus:outline-none">
                <button id="sendMessage">
                    <i class="fas fa-paper-plane"></i>
                </button>
            </div>
        </div>
    </div>
    
    <script>
        // Three.js 背景动画
        document.addEventListener('DOMContentLoaded', function() {
            // 初始化Three.js场景
            const canvas = document.getElementById('hero-canvas');
            const scene = new THREE.Scene();
            const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            
            const renderer = new THREE.WebGLRenderer({
                canvas: canvas,
                alpha: true,
                antialias: true
            });
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.setPixelRatio(window.devicePixelRatio);
            
            // 创建粒子系统
            const particlesGeometry = new THREE.BufferGeometry();
            const particlesCount = 1500;
            
            const posArray = new Float32Array(particlesCount * 3);
            
            for(let i = 0; i < particlesCount * 3; i++) {
                posArray[i] = (Math.random() - 0.5) * 5;
            }
            
            particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
            
            const particlesMaterial = new THREE.PointsMaterial({
                size: 0.005,
                color: 0x0056b3,
                transparent: true,
                opacity: 0.8
            });
            
            const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
            scene.add(particlesMesh);
            
            camera.position.z = 2;
            
            // 添加光线
            const light = new THREE.DirectionalLight(0xffffff, 1);
            light.position.set(0, 0, 1);
            scene.add(light);
            
            // 动画循环
            const animate = () => {
                requestAnimationFrame(animate);
                
                particlesMesh.rotation.y += 0.001;
                particlesMesh.rotation.x += 0.0005;
                
                renderer.render(scene, camera);
            };
            
            animate();
            
            // 窗口大小调整
            window.addEventListener('resize', () => {
                camera.aspect = window.innerWidth / window.innerHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(window.innerWidth, window.innerHeight);
            });
            
            // 滚动动画
            const fadeElements = document.querySelectorAll('.fade-in');
            
            const fadeInOnScroll = () => {
                fadeElements.forEach(element => {
                    const elementTop = element.getBoundingClientRect().top;
                    const windowHeight = window.innerHeight;
                    const delay = element.getAttribute('data-delay') || 0;
                    
                    if (elementTop < windowHeight - 100) {
                        setTimeout(() => {
                            element.classList.add('active');
                        }, delay);
                    }
                });
            };
            
            window.addEventListener('scroll', fadeInOnScroll);
            fadeInOnScroll(); // 初始检查
            
            // 数字增长动画
            const counters = document.querySelectorAll('.counter');
            
            const startCounting = (counter) => {
                const target = parseInt(counter.getAttribute('data-target'));
                const duration = 2000; // 动画持续时间（毫秒）
                const startTime = performance.now();
                
                const updateCount = (currentTime) => {
                    const elapsedTime = currentTime - startTime;
                    const progress = Math.min(elapsedTime / duration, 1);
                    const currentValue = Math.floor(progress * target);
                    
                    counter.textContent = currentValue;
                    
                    if (progress < 1) {
                        requestAnimationFrame(updateCount);
                    }
                };
                
                requestAnimationFrame(updateCount);
            };
            
            // 检查元素是否在视口中
            const isInViewport = (element) => {
                const rect = element.getBoundingClientRect();
                return (
                    rect.top <= (window.innerHeight || document.documentElement.clientHeight) * 0.8 &&
                    rect.bottom >= 0
                );
            };
            
            // 滚动时检查计数器
            const checkCounters = () => {
                counters.forEach(counter => {
                    if (isInViewport(counter) && !counter.classList.contains('counted')) {
                        counter.classList.add('counted');
                        startCounting(counter);
                    }
                });
            };
            
            window.addEventListener('scroll', checkCounters);
            checkCounters(); // 初始检查
            
            // 案例轮播
            const caseSlider = document.getElementById('caseSlider');
            const prevCaseBtn = document.getElementById('prevCase');
            const nextCaseBtn = document.getElementById('nextCase');
            const caseDots = document.querySelectorAll('.case-dot');
            let currentSlide = 0;
            const slideCount = document.querySelectorAll('.case-slide').length;
            
            const goToSlide = (index) => {
                if (index < 0) index = slideCount - 1;
                if (index >= slideCount) index = 0;
                
                currentSlide = index;
                const slideWidth = document.querySelector('.case-slide').offsetWidth;
                caseSlider.style.transform = `translateX(-${currentSlide * slideWidth}px)`;
                
                // 更新指示器
                caseDots.forEach((dot, i) => {
                    if (i === currentSlide) {
                        dot.classList.add('bg-blue-600');
                        dot.classList.remove('bg-gray-300');
                    } else {
                        dot.classList.remove('bg-blue-600');
                        dot.classList.add('bg-gray-300');
                    }
                });
            };
            
            prevCaseBtn.addEventListener('click', () => {
                goToSlide(currentSlide - 1);
            });
            
            nextCaseBtn.addEventListener('click', () => {
                goToSlide(currentSlide + 1);
            });
            
            caseDots.forEach((dot, i) => {
                dot.addEventListener('click', () => {
                    goToSlide(i);
                });
            });
            
            // 自动轮播
            let slideInterval = setInterval(() => {
                goToSlide(currentSlide + 1);
            }, 5000);
            
            // 鼠标悬停时暂停轮播
            document.querySelector('.case-carousel').addEventListener('mouseenter', () => {
                clearInterval(slideInterval);
            });
            
            // 鼠标离开时恢复轮播
            document.querySelector('.case-carousel').addEventListener('mouseleave', () => {
                slideInterval = setInterval(() => {
                    goToSlide(currentSlide + 1);
                }, 5000);
            });
            
            // 移动端菜单
            const menuToggle = document.getElementById('menu-toggle');
            const closeMenu = document.getElementById('close-menu');
            const mobileMenu = document.querySelector('.mobile-menu');
            const overlay = document.querySelector('.overlay');
            const mobileNavLinks = document.querySelectorAll('.mobile-nav-link');
            
            menuToggle.addEventListener('click', () => {
                mobileMenu.classList.add('active');
                overlay.classList.add('active');
                document.body.style.overflow = 'hidden';
            });
            
            const closeMenuHandler = () => {
                mobileMenu.classList.remove('active');
                overlay.classList.remove('active');
                document.body.style.overflow = '';
            };
            
            closeMenu.addEventListener('click', closeMenuHandler);
            overlay.addEventListener('click', closeMenuHandler);
            
            mobileNavLinks.forEach(link => {
                link.addEventListener('click', closeMenuHandler);
            });
            
            // 平滑滚动
            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function(e) {
                    e.preventDefault();
                    
                    const targetId = this.getAttribute('href');
                    const targetElement = document.querySelector(targetId);
                    
                    if (targetElement) {
                        window.scrollTo({
                            top: targetElement.offsetTop - 80,
                            behavior: 'smooth'
                        });
                    }
                });
            });
            
            // 联系表单提交
            const contactForm = document.getElementById('contactForm');
            
            contactForm.addEventListener('submit', (e) => {
                e.preventDefault();
                
                // 模拟表单提交
                const submitButton = contactForm.querySelector('button[type="submit"]');
                const originalText = submitButton.innerHTML;
                
                submitButton.disabled = true;
                submitButton.innerHTML = '<i class="fas fa-spinner fa-spin mr-2"></i> 发送中...';
                
                setTimeout(() => {
                    // 显示成功消息
                    const formContainer = contactForm.parentElement;
                    formContainer.innerHTML = `
                        <div class="text-center py-8">
                            <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
                                <i class="fas fa-check text-green-500 text-2xl"></i>
                            </div>
                            <h3 class="text-xl font-bold mb-2">消息已发送</h3>
                            <p class="text-gray-700">
                                感谢您的留言，我们会尽快与您联系！
                            </p>
                        </div>
                    `;
                }, 1500);
            });
            
            // AI智能客服
            const chatbotToggle = document.getElementById('chatbotToggle');
            const chatbotPanel = document.getElementById('chatbotPanel');
            const closeChatbot = document.getElementById('closeChatbot');
            const chatbotMessages = document.getElementById('chatbotMessages');
            const chatbotInput = document.getElementById('chatbotInput');
            const sendMessage = document.getElementById('sendMessage');
            
            // 预设问答
            const qaDatabase = [
                {
                    keywords: ['你好', '您好', 'hi', 'hello'],
                    response: '您好！我是海友共创的智能客服助手，很高兴为您服务。请问有什么可以帮助您的吗？'
                },
                {
                    keywords: ['公司', '简介', '介绍'],
                    response: '北京海友共创技术有限公司成立于2008年，是一家拥有15年经验的专业IT外包服务公司，专注于为企业提供IT人员外包、定制化软件开发和猎头服务。'
                },
                {
                    keywords: ['服务', '业务', '项目'],
                    response: '我们提供三大核心服务：1. IT人员外包 2. 定制化软件开发 3. 猎头服务。您可以点击网站上的"服务项目"了解更多详情。'
                },
                {
                    keywords: ['价格', '费用', '报价'],
                    response: '我们的服务价格根据具体需求而定，建议您通过电话18611110649或邮箱ito@hi-friend.cn联系我们，我们会为您提供详细的报价方案。'
                },
                {
                    keywords: ['联系', '电话', '邮箱', '地址'],
                    response: '我们的联系方式：地址：北京市海淀区上地中关村软件园孵化器2号楼2-1；邮箱：ito@hi-friend.cn；电话：18611110649。'
                },
                {
                    keywords: ['合作', '咨询', '洽谈'],
                    response: '如果您有合作意向，请留下您的联系方式，我们的客户经理会尽快与您联系。您也可以直接拨打我们的电话18611110649进行咨询。'
                }
            ];
            
            // 显示/隐藏客服面板
            chatbotToggle.addEventListener('click', () => {
                chatbotPanel.style.display = chatbotPanel.style.display === 'flex' ? 'none' : 'flex';
            });
            
            closeChatbot.addEventListener('click', () => {
                chatbotPanel.style.display = 'none';
            });
            
            // 添加消息到聊天窗口
            const addMessage = (text, isUser = false) => {
                const messageDiv = document.createElement('div');
                messageDiv.classList.add('message');
                messageDiv.classList.add(isUser ? 'user-message' : 'bot-message');
                messageDiv.textContent = text;
                
                chatbotMessages.appendChild(messageDiv);
                chatbotMessages.scrollTop = chatbotMessages.scrollHeight;
            };
            
            // 处理用户输入
            const handleUserInput = () => {
                const userMessage = chatbotInput.value.trim();
                
                if (userMessage) {
                    // 添加用户消息
                    addMessage(userMessage, true);
                    chatbotInput.value = '';
                    
                    // 模拟AI思考
                    setTimeout(() => {
                        // 查找匹配的预设回答
                        let botResponse = '很抱歉，我暂时无法回答这个问题。请您直接联系我们的客服人员18611110649获取更多帮助。';
                        
                        for (const qa of qaDatabase) {
                            if (qa.keywords.some(keyword => userMessage.toLowerCase().includes(keyword))) {
                                botResponse = qa.response;
                                break;
                            }
                        }
                        
                        // 添加机器人回复
                        addMessage(botResponse);
                    }, 500);
                }
            };
            
            // 发送消息按钮点击事件
            sendMessage.addEventListener('click', handleUserInput);
            
            // 输入框回车事件
            chatbotInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    handleUserInput();
                }
            });
        });
    </script>
</body>
</html>
