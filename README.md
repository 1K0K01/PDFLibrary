# 📚 ARCANE SHELF — 로컬 라이브러리

> **서버 없이 브라우저만으로 작동하는 관리 웹앱**  
> IndexedDB에 저장 · pdf.js로 표지 생성 · AI 자동 요약 · GitHub Pages 무료 배포

---

## ✨ 주요 기능

| 기능 | 설명 |
|------|------|
| 📂 PDF 드래그&드롭 | 로컬 PDF를 드래그하거나 버튼으로 가져오기 |
| 🖼️ 자동 표지 썸네일 | pdf.js가 첫 페이지를 캡처하여 카드에 표시 |
| 💾 로컬 영구 저장 | IndexedDB에 썸네일·메타데이터·PDF 데이터 저장 (서버 없음) |
| ✏️ 메타데이터 편집 | 룰 시스템, 라이터, 플레이 인원 직접 입력 |
| ✨ AI 자동 요약 | Gemini / OpenAI / Claude로 줄거리 3줄 요약 + 태그 자동 생성 |
| 🔍 필터링 & 검색 | 룰별, 저자별, 태그별 사이드바 필터 + 키워드 검색 |
| 📄 PDF 뷰어 | 브라우저 내장 뷰어로 즉시 읽기 |

---

## 📦 사용된 라이브러리 (CDN — 별도 설치 불필요)

| 라이브러리 | 버전 | 역할 |
|------------|------|------|
| Tailwind CSS | CDN | 스타일링 |
| pdf.js | 3.11.174 | PDF 렌더링 & 텍스트 추출 |
| Google Fonts | - | Cinzel, Noto Sans KR 폰트 |

> ⚠️ **모든 의존성이 CDN으로 로드됩니다.** `npm install` 불필요. `index.html` 하나만 있으면 됩니다.

---

## ⚙️ AI API 설정

앱 우측 상단 ⚙️ 설정 버튼에서 입력:

### Google Gemini (무료 플랜 있음, 추천)
1. [Google AI Studio](https://aistudio.google.com/app/apikey) → `Get API Key`
2. 설정 창에서 제공자: `Google Gemini` 선택
3. API 키 입력 → 저장
- 기본 모델: `gemini-1.5-flash` (무료, 빠름)

### OpenAI GPT
1. [platform.openai.com](https://platform.openai.com/api-keys) → API Key 발급
2. 제공자: `OpenAI GPT` 선택
- 기본 모델: `gpt-4o-mini` (저렴)

### Anthropic Claude
1. [console.anthropic.com](https://console.anthropic.com/) → API Key 발급
2. 제공자: `Anthropic Claude` 선택
- 기본 모델: `claude-haiku-4-5-20251001`

> 🔒 **API 키는 브라우저 localStorage에만 저장되며, 어떤 서버로도 전송되지 않습니다.**

---

## 💾 데이터 저장 구조 (IndexedDB)

```
Database: arcane-shelf-v2
└── ObjectStore: scenarios
    ├── id          (고유 ID)
    ├── title       (제목)
    ├── filename    (원본 파일명)
    ├── rule        (룰 시스템)
    ├── author      (라이터)
    ├── players     (플레이 인원)
    ├── tags        (태그 배열)
    ├── summary     (AI 요약)
    ├── thumbnail   (표지 Base64 JPEG)
    ├── extractedText (텍스트 앞부분 4000자)
    ├── pdfData     (전체 PDF Base64)
    ├── pageCount   (페이지 수)
    └── addedAt     (추가 시각)
```

> ⚠️ **브라우저 데이터를 삭제하면 라이브러리도 초기화됩니다.**  
> 크롬 기준 IndexedDB 용량은 수 GB이므로 일반 사용에서는 문제없습니다.

---

## 🔧 로컬에서 테스트하기

GitHub Pages 없이 로컬에서 바로 열면 CORS 오류가 발생합니다.  
간단한 로컬 서버를 사용하세요:

```bash
# Python 3
python -m http.server 8080
# 브라우저에서: http://localhost:8080

# Node.js (npx)
npx serve .
```

또는 VS Code의 **Live Server** 확장을 사용하세요.

---

## ❓ 자주 묻는 질문

**Q: PDF가 너무 커서 저장이 안 돼요**  
A: 브라우저 IndexedDB는 수 GB를 지원하지만, 크기가 큰 PDF는 Base64로 변환 시 1.3배 커집니다. 500MB 이상 PDF는 분할 권장.

**Q: 스캔 PDF는 텍스트 추출이 안 돼요**  
A: pdf.js는 텍스트 레이어가 있는 PDF만 지원합니다. 스캔본은 OCR 처리 후 사용하세요.

**Q: 다른 기기에서도 라이브러리를 쓰고 싶어요**  
A: IndexedDB는 브라우저 로컬 전용입니다. 동기화를 원한다면 Google Drive 연동 등을 추가해야 합니다.

**Q: AI 요약 버튼을 눌렀는데 오류가 나요**  
A: API 키와 제공자 선택이 올바른지 확인하고, 인터넷 연결 상태를 확인하세요.
