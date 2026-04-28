# 📚 [ARCANE SHELF — 로컬 라이브러리](https://1K0K01.github.io/PDFLibrary)

> **서버 없이 브라우저만으로 작동하는 관리 웹앱**  
> IndexedDB에 저장 · pdf.js로 표지 생성 · 자동 요약

---

## ✨ 주요 기능

| 기능 | 설명 |
|------|------|
| 📂 PDF 드래그&드롭 | 로컬 PDF를 드래그하거나 버튼으로 가져오기 |
| 🖼️ 자동 표지 썸네일 | pdf.js가 첫 페이지를 캡처하여 카드에 표시 |
| 💾 로컬 영구 저장 | IndexedDB에 썸네일·메타데이터·PDF 데이터 저장 (서버 없음) |
| ✏️ 메타데이터 편집 | 룰 시스템, 라이터, 플레이 인원 직접 입력 |
| ✨ AI 자동 요약 | AI로 줄거리 3줄 요약 + 태그 자동 생성 |
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
