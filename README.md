<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>모닝 영감 대시보드</title>
    <!-- 폰트: 모던하고 깔끔한 Pretendard 사용 -->
    <link rel="stylesheet" as="style" crossorigin href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.8/dist/web/static/pretendard.css" />
    <!-- 아이콘: FontAwesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        /* 정부/공공기관 스타일의 신뢰감 있는 컬러 팔레트 */
        :root {
            --bg-color: #F3F4F6;         /* 차분하고 밝은 배경 */
            --card-bg: #FFFFFF;          /* 순백색 카드 */
            --border-color: #E5E7EB;     /* 아주 연한 그레이 테두리 */
            --text-main: #1F2937;        /* 가독성 높은 짙은 차콜 */
            --text-sub: #6B7280;         /* 정돈된 서브 텍스트 */
            --primary-color: #1E3A8A;    /* 신뢰감을 주는 딥 네이비 (정부 상징색 느낌) */
            --primary-light: #EFF6FF;    /* 네이비 연한 배경 */
            --accent-red: #DC2626;       /* 강조용 레드 */
            --accent-blue: #2563EB;      /* 포인트 블루 */
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Pretendard', sans-serif;
        }

        body {
            background-color: var(--bg-color);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 30px 20px 50px 20px;
            color: var(--text-main);
        }

        .dashboard {
            width: 100%;
            max-width: 1100px;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        /* 공통 카드 스타일: 라운딩을 줄여 공식적이고 단정한 느낌 부여 */
        .card {
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px; /* 정부 사이트 특유의 각진 듯한 단정함 */
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.03);
            overflow: hidden;
        }

        /* --- Header Section (공공기관 메인 비주얼 스타일) --- */
        .header-visual {
            position: relative;
            width: 100%;
            height: 240px;
            /* 신뢰감을 주는 깔끔한 건축물/하늘 사진으로 교체 */
            background-image: url('https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?q=80&w=2000&auto=format&fit=crop'); 
            background-size: cover;
            background-position: center;
        }

        /* 사진 위에 다크 네이비 그라데이션을 덮어 글씨 가독성 극대화 */
        .header-overlay {
            position: absolute;
            top: 0; left: 0; right: 0; bottom: 0;
            background: linear-gradient(to right, rgba(30, 58, 138, 0.9), rgba(30, 58, 138, 0.4));
            display: flex;
            flex-direction: column;
            justify-content: center;
            padding: 0 40px;
        }

        .header-overlay .greeting {
            color: rgba(255, 255, 255, 0.8);
            font-size: 1.1rem;
            margin-bottom: 10px;
        }

        .header-overlay .datetime-container {
            display: flex;
            align-items: baseline;
            gap: 15px;
            color: #ffffff;
        }

        .header-overlay #time-display {
            font-size: 3rem;
            font-weight: 700;
            letter-spacing: -1px;
        }

        .header-overlay #date-display {
            font-size: 1.2rem;
            font-weight: 400;
            opacity: 0.9;
        }

        /* 공지사항 느낌의 질문 박스 */
        .notice-box {
            display: flex;
            align-items: center;
            padding: 18px 40px;
            background-color: #ffffff;
            border-bottom: 1px solid var(--border-color);
            gap: 15px;
        }

        .notice-badge {
            background-color: var(--primary-color);
            color: #ffffff;
            font-size: 0.85rem;
            font-weight: 600;
            padding: 4px 10px;
            border-radius: 4px;
            letter-spacing: 1px;
        }

        .notice-text {
            font-size: 1.1rem;
            font-weight: 500;
            color: var(--text-main);
        }

        /* --- Main Content Section --- */
        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }

        .section-header {
            padding: 25px 30px 20px 30px;
            border-bottom: 1px solid var(--border-color);
        }

        .section-title {
            font-size: 1.2rem;
            font-weight: 700;
            color: var(--text-main);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .section-title i {
            color: var(--primary-color);
        }

        .section-body {
            padding: 25px 30px;
        }

        /* --- Keywords (정부/포털 해시태그 스타일) --- */
        .keywords-container {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }

        .keyword-tag {
            display: inline-flex;
            align-items: center;
            padding: 10px 18px;
            background: #F9FAFB;
            border: 1px solid var(--border-color);
            color: var(--text-main);
            border-radius: 6px;
            font-size: 1.05rem;
            font-weight: 500;
            transition: all 0.2s ease;
            cursor: pointer;
        }

        .keyword-tag span.badge {
            font-size: 0.75rem;
            font-weight: 700;
            margin-left: 8px;
            padding: 2px 6px;
            border-radius: 4px;
        }

        .keyword-tag.hot {
            border-color: #FECACA;
            background-color: #FEF2F2;
        }
        .keyword-tag.hot span.badge {
            background-color: var(--accent-red);
            color: #fff;
        }

        .keyword-tag.new {
            border-color: #BFDBFE;
            background-color: #EFF6FF;
        }
        .keyword-tag.new span.badge {
            background-color: var(--accent-blue);
            color: #fff;
        }

        .keyword-tag:hover {
            border-color: var(--primary-color);
            background-color: var(--primary-light);
            transform: translateY(-2px);
        }

        /* --- Link Cards (공공기관 바로가기 배너 스타일) --- */
        .links-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 12px;
        }

        .link-card {
            display: flex;
            align-items: center;
            padding: 18px 20px;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            text-decoration: none;
            background: #ffffff;
            transition: all 0.2s ease;
            group: hover;
        }

        .link-icon-box {
            width: 46px;
            height: 46px;
            background-color: var(--primary-light);
            color: var(--primary-color);
            border-radius: 8px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.4rem;
            margin-right: 18px;
            transition: all 0.2s ease;
        }

        .link-info {
            flex: 1;
        }

        .link-title {
            font-size: 1.1rem;
            font-weight: 700;
            color: var(--text-main);
            margin-bottom: 4px;
        }

        .link-desc {
            font-size: 0.9rem;
            color: var(--text-sub);
        }

        .link-arrow {
            color: #D1D5DB;
            font-size: 1.2rem;
            transition: all 0.2s ease;
        }

        /* 호버 시 고급스러운 변화 */
        .link-card:hover {
            border-color: var(--primary-color);
            box-shadow: 0 4px 12px rgba(30, 58, 138, 0.08);
        }

        .link-card:hover .link-icon-box {
            background-color: var(--primary-color);
            color: #ffffff;
        }

        .link-card:hover .link-arrow {
            color: var(--primary-color);
            transform: translateX(4px); /* 화살표가 살짝 오른쪽으로 이동 */
        }

        /* --- Responsive --- */
        @media (max-width: 900px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            .header-visual {
                height: 200px;
            }
            .header-overlay #time-display {
                font-size: 2.2rem;
            }
            .header-overlay #date-display {
                font-size: 1rem;
            }
            .notice-box {
                flex-direction: column;
                align-items: flex-start;
                padding: 20px;
                gap: 10px;
            }
            .notice-text {
                font-size: 1rem;
            }
        }
    </style>
</head>
<body>

    <div class="dashboard">
        
        <!-- Header (메인 비주얼 & 공지사항 형태) -->
        <header class="card">
            <div class="header-visual">
                <div class="header-overlay">
                    <p class="greeting">정확하고 깊이 있는 하루의 시작</p>
                    <div class="datetime-container">
                        <span id="time-display"></span>
                        <span id="date-display"></span>
                    </div>
                </div>
            </div>
            
            <div class="notice-box">
                <span class="notice-badge">오늘의 화두</span>
                <span class="notice-text" id="random-question">오늘의 질문을 불러오는 중...</span>
            </div>
        </header>

        <!-- Main Content -->
        <main class="main-content">
            
            <!-- Left: 핫이슈 키워드 -->
            <section class="card">
                <div class="section-header">
                    <h2 class="section-title">
                        <i class="fa-solid fa-chart-line"></i> 
                        주요 정책 및 트렌드 키워드
                    </h2>
                </div>
                <div class="section-body">
                    <div class="keywords-container">
                        <div class="keyword-tag hot">늘봄학교 <span class="badge">HOT</span></div>
                        <div class="keyword-tag hot">생성형AI <span class="badge">HOT</span></div>
                        <div class="keyword-tag new">디지털교과서 <span class="badge">NEW</span></div>
                        <div class="keyword-tag">촉각놀이</div>
                        <div class="keyword-tag">초저출산 대응</div>
                        <div class="keyword-tag new">자기주도학습 <span class="badge">NEW</span></div>
                    </div>
                </div>
            </section>

            <!-- Right: 바로가기 링크 -->
            <section class="card">
                <div class="section-header">
                    <h2 class="section-title">
                        <i class="fa-solid fa-building-columns"></i>
                        인사이트 정보 플랫폼
                    </h2>
                </div>
                <div class="section-body">
                    <div class="links-grid">
                        
                        <!-- 한국 교육 신문 -->
                        <a href="https://www.hangyo.com/" target="_blank" class="link-card">
                            <div class="link-icon-box"><i class="fa-regular fa-newspaper"></i></div>
                            <div class="link-info">
                                <div class="link-title">한국 교육 신문</div>
                                <div class="link-desc">교육 현장 및 정책 동향 파악</div>
                            </div>
                            <i class="fa-solid fa-chevron-right link-arrow"></i>
                        </a>

                        <!-- 뉴닉 -->
                        <a href="https://newneek.co/" target="_blank" class="link-card">
                            <div class="link-icon-box"><i class="fa-solid fa-bolt"></i></div>
                            <div class="link-info">
                                <div class="link-title">뉴닉 (NEWNEEK)</div>
                                <div class="link-desc">국내외 주요 시사 브리핑</div>
                            </div>
                            <i class="fa-solid fa-chevron-right link-arrow"></i>
                        </a>

                        <!-- 구글 트렌드 -->
                        <a href="https://trends.google.com/trending?geo=KR" target="_blank" class="link-card">
                            <div class="link-icon-box"><i class="fa-solid fa-magnifying-glass-chart"></i></div>
                            <div class="link-info">
                                <div class="link-title">구글 트렌드</div>
                                <div class="link-desc">실시간 대중 관심사 분석</div>
                            </div>
                            <i class="fa-solid fa-chevron-right link-arrow"></i>
                        </a>

                        <!-- 커뮤니티 -->
                        <a href="https://gall.dcinside.com/" target="_blank" class="link-card">
                            <div class="link-icon-box"><i class="fa-regular fa-comments"></i></div>
                            <div class="link-info">
                                <div class="link-title">디시인사이드</div>
                                <div class="link-desc">인터넷 여론 및 이슈 모니터링</div>
                            </div>
                            <i class="fa-solid fa-chevron-right link-arrow"></i>
                        </a>

                    </div>
                </div>
            </section>

        </main>

    </div>

    <!-- JavaScript 기능 구현 -->
    <script>
        // 1. 실시간 날짜 및 시간 업데이트
        function updateDateTime() {
            const now = new Date();
            const optionsDate = { year: 'numeric', month: 'long', day: 'numeric', weekday: 'long' };
            const dateString = now.toLocaleDateString('ko-KR', optionsDate);
            
            const hours = String(now.getHours()).padStart(2, '0');
            const minutes = String(now.getMinutes()).padStart(2, '0');
            const seconds = String(now.getSeconds()).padStart(2, '0');
            const timeString = `${hours}:${minutes}:${seconds}`;

            document.getElementById('time-display').textContent = timeString;
            document.getElementById('date-display').textContent = dateString;
        }

        setInterval(updateDateTime, 1000);
        updateDateTime(); 

        // 2. 오늘의 화두 (정부/기관 스타일에 맞춘 차분한 톤업)
        const questions = [
            "최근 현장에서 가장 개선이 필요하다고 느끼는 제도는 무엇입니까?",
            "오늘 마주할 가장 중요한 의사결정은 무엇입니까?",
            "데이터를 기반으로 판단하고 있습니까, 직관에 의존하고 있습니까?",
            "오늘 나의 행동이 타인에게 어떤 긍정적인 영향을 미칠 수 있습니까?",
            "새로운 변화를 받아들이기 위해 버려야 할 과거의 습관은 무엇입니까?",
            "본질을 놓치고 눈앞의 현상에만 몰두하고 있지는 않습니까?",
            "오늘 하루, 나의 우선순위는 명확하게 설정되어 있습니까?"
        ];

        function setRandomQuestion() {
            const randomIndex = Math.floor(Math.random() * questions.length);
            document.getElementById('random-question').textContent = questions[randomIndex];
        }

        setRandomQuestion(); 
    </script>
</body>
</html>
