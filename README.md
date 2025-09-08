# 여행&날씨 기사 생성기

AI 기반 여행지 추천 기사와 날씨 기사를 자동으로 생성하는 PyQt5 데스크톱 애플리케이션입니다.

## 📋 프로젝트 개요

이 프로그램은 네이버 크롤링 데이터를 기반으로 여행지를 검색하고, 실시간 날씨 정보를 수집하여 전문적인 뉴스 기사 스타일의 콘텐츠를 자동 생성합니다.

### 🎯 주요 기능

### 🛏️ 여행지 검색 탭

- **다단계 지역 필터**: 도/특별시 → 시/군/구 → 읍/면/동 단계별 필터링
- **카테고리 필터**: 음식점, 카페, 관광지 등 16개 세분화된 카테고리
- **리뷰 기반 필터**: 가격, 맛, 분위기 등 12개 리뷰 특성별 필터
- **실시간 크롤링**: 선택한 장소의 최신 정보 자동 업데이트
- **AI 기사 생성**: Google Gemini API를 활용한 전문 여행 기사 작성
- **랜덤 선택**: 리뷰 상위 10-30% 장소에서 3-5개 자동 선택

### 🌤️ 날씨 조회 탭

- **전국 날씨 조회**: 카카오 지도 + 기상청 API 연동
- **기상특보 모니터링**: 전국 기상특보 실시간 조회
- **AI 날씨 기사**: 실제 기상 데이터 기반 뉴스 기사 생성
- **특보 기사 생성**: 발효 중인 기상특보 전문 보도 자료 작성

## 🛠️ 설치 및 실행

### 1. 사전 요구사항

- Python 3.8 이상
- Chrome 브라우저 (Selenium 크롤링용)
- 각종 API 키 (아래 참조)

### 2. 프로젝트 설정

프로젝트 파일들을 원하는 위치에 압축 해제한 후, 해당 폴더로 이동하세요.

```bash
cd 프로젝트폴더명

```

### 3. 가상환경 생성 (권장)

```bash
python -m venv venv

# Windows
venv\\Scripts\\activate

# macOS/Linux
source venv/bin/activate

```

### 4. 의존성 설치

```bash
pip install -r requirements.txt

```

### 5. 환경변수 설정

프로젝트 루트에 `.env` 파일을 생성하고 다음 API 키들을 설정하세요:

```
# Google Gemini AI API (필수)
GOOGLE_API_KEY=your_google_api_key_here

# 카카오 지도 API (날씨 기능용)
KAKAO_API_KEY=your_kakao_api_key_here

# 기상청 API (날씨 기능용)
KMA_API_KEY=your_kma_api_key_here

```

### API 키 발급 방법

- **Google Gemini API**: [Google AI Studio](https://aistudio.google.com/) → API 키 생성
- **카카오 지도 API**: [Kakao Developers](https://developers.kakao.com/) → 애플리케이션 등록 → 지도 API 활성화
- **기상청 API**: [공공데이터포털](https://www.data.go.kr/) → 기상청 단기예보 서비스 신청

### 6. 데이터베이스 준비

네이버 크롤링 데이터가 포함된 SQLite DB 파일을 준비하여 `crw_data/` 폴더에 배치하세요:

```
프로젝트_폴더/
├── crw_data/
│   └── 250904_naver_travel_places.db
└── ...

```

### 7. 프로그램 실행

```bash
python article_generator_app.py

```

## 📁 프로젝트 구조

```
├── article_generator_app.py      # 메인 애플리케이션 진입점
├── travel_tab.py                 # 여행지 검색 탭 컨트롤러
├── travel_ui.py                  # 여행지 탭 UI 컴포넌트
├── travel_logic.py               # 여행지 검색 비즈니스 로직
├── weather_tab.py                # 날씨 탭 통합 UI
├── weather_api.py                # 기상청 API 연동
├── weather_warning.py            # 기상특보 API 연동
├── weather_ai_generator.py       # AI 날씨 기사 생성
├── weather_article_prompts.py    # 날씨 기사 프롬프트 템플릿
├── chatbot_app.py               # AI 여행 기사 생성
├── prompts.py                   # 여행 기사 프롬프트 템플릿
├── db_manager.py                # SQLite DB 관리
├── realtime_crawler.py          # 실시간 네이버 크롤링
├── category_utils.py            # 장소 카테고리 분류
├── visitor_reviews_utils.py     # 리뷰 태그 분류
├── ui_components.py             # 커스텀 UI 컴포넌트
├── config.py                    # API 설정 관리
├── data.py                      # 지역 데이터 및 상수
├── debug_test.py               # 크롤링 테스트 스크립트
├── requirements.txt             # 의존성 목록
└── README.md                   # 프로젝트 문서

```

## 🎮 사용법

### 여행지 기사 생성

1. **지역 선택**: 도/시/동 필터 또는 통합 검색 사용
2. **카테고리 필터**: 관심 있는 장소 유형 선택
3. **리뷰 필터**: 원하는 특성 (맛, 분위기 등) 선택
4. **검색 실행**: "필터 적용" 버튼 클릭
5. **장소 선택**: 테이블에서 원하는 장소들 체크
6. **기사 생성**: "선택한 장소로 기사 생성" 또는 "랜덤 선택으로 기사 생성"

### 날씨 기사 생성

1. **날씨 조회**: 지역명 입력 후 검색
2. **특보 확인**: "전국 기상특보 조회" 버튼 클릭
3. **AI 기사 생성**: "날씨 기사 생성" 또는 "특보 기사 생성" 선택
4. **결과 복사**: "기사 복사" 버튼으로 클립보드에 복사

## ⚙️ 주요 기술

- **GUI**: PyQt5
- **AI**: Google Gemini 2.5 Flash
- **웹 크롤링**: Selenium + Chrome WebDriver
- **데이터베이스**: SQLite
- **API 연동**: 카카오 지도, 기상청 공공데이터
- **아키텍처**: MVC 패턴, 비동기 처리

## 🔧 설정 옵션

### config.py에서 수정 가능한 설정

- API 타임아웃 시간
- 재시도 횟수
- 크롤링 딜레이 설정

### 프롬프트 커스터마이징

- `prompts.py`: 여행 기사 생성 프롬프트
- `weather_article_prompts.py`: 날씨 기사 생성 프롬프트

## 🚨 문제 해결

### 일반적인 오류

1. **DB 파일 없음**: `crw_data/` 폴더에 SQLite DB 파일 확인
2. **API 키 오류**: `.env` 파일의 API 키 설정 확인
3. **크롤링 실패**: Chrome 브라우저 설치 및 업데이트 확인
4. **날씨 조회 실패**: 카카오/기상청 API 키 유효성 확인

### 디버깅

- `debug_test.py`: 크롤링 기능 테스트
- `config.py`: API 키 연결 테스트 (`python config.py`)
- `weather_api_log.txt`: 날씨 API 호출 로그 확인

## 👥 개발자

- **하승주**, **홍석원**

## 📞 문의사항

프로그램 사용 중 문제가 발생하거나 개선 아이디어가 있으시면 이슈를 등록해주세요.
