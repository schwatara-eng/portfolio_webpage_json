# 과제 포트폴리오 웹페이지

AI 데이터 저널리즘 과정에서 제작한 과제물(이미지, 영상, AI 앱 등)을 카드 형태로 모아 보여주는 포트폴리오 웹사이트입니다.

과제 정보는 `data.json`에 저장하고, JavaScript의 `fetch()`를 이용해 불러옵니다.
카드를 누르면 상세 창이 열리고 이미지·영상·설명·링크 등을 확인할 수 있습니다.

---

## 1. 폴더 구성

```text
portfolio/
├─ index.html      페이지의 뼈대
├─ style.css       디자인과 화면 배치
├─ script.js       데이터 처리와 화면 동작
├─ data.json       과제 데이터
├─ README.md       프로젝트 설명
└─ images/         이미지 파일 폴더
```

---

## 2. 실행하는 방법

1. VS Code에서 프로젝트 폴더를 엽니다.
2. 확장 프로그램 **Live Server**를 설치합니다.
3. `index.html`을 마우스 오른쪽 버튼으로 누릅니다.
4. **Open with Live Server**를 선택합니다.

> `index.html`을 직접 더블클릭해서 열면 `fetch()`가 정상적으로 작동하지 않을 수 있습니다.  
> 반드시 Live Server로 실행합니다.

---

## 3. 화면 구성

| 영역 | 내용 |
|---|---|
| 상단 메뉴 | 이름, Portfolio, 작품·소개·연락처 이동 |
| 자기소개 | 프로필 사진, 한 줄 소개, 태그 |
| 분류 필터 | 전체, AI영상, Opal, 기타 |
| 과제 카드 | 썸네일, 제목, 분류, 과목, 날짜 |
| 상세 창 | 이미지·영상, 과목, 제출일, 사용 툴, 기획 의도, 작업 과정, 링크 |
| 소개 | 수강 과정 정보 |
| 연락처 | 이메일, Instagram |

---

## 4. JSON 데이터 구조

과제 정보는 `data.json`에 배열 형태로 저장합니다.

```json
[
  {
    "title": "숫자로 보는 2026 아이치·나고야 아시안 게임",
    "category": "AI영상",
    "course": "AI 데이터 저널리즘",
    "date": "2026.09",
    "tools": "ChatGPT, Midjourney, CapCut",
    "intent": "아시안 게임 개최 현황을 숫자를 통해 전해드립니다.",
    "process": "기획 구성 → 스토리보드 및 대본 작성 → 이미지 및 영상 생성 → TTS 생성 → 최종편집",
    "youtube": "유튜브 영상 ID",
    "embed": "",
    "app": "",
    "images": ["images/썸네일.png"],
    "file": ""
  }
]
```

---

## 5. JSON 데이터 불러오기

`script.js`에서 `fetch()`를 사용해 `data.json`을 불러옵니다.

```javascript
let WORKS = [];

fetch("data.json")
  .then(function(response) {
    return response.json();
  })
  .then(function(data) {
    WORKS = data;

    showFilters();
    showCards();
  });
```

### 데이터 처리 흐름

```text
data.json
   ↓
fetch()
   ↓
response.json()
   ↓
JavaScript 객체/배열
   ↓
WORKS
   ↓
showFilters()
showCards()
   ↓
웹페이지 출력
```

---

## 6. 주요 JavaScript 기능

- `fetch()` : 외부 JSON 파일 불러오기
- `response.json()` : JSON 데이터를 JavaScript에서 사용할 수 있게 변환
- `querySelector()` / `getElementById()` : HTML 요소 찾기
- `forEach()` : 여러 과제 데이터를 하나씩 처리
- `filter()` : 선택한 분류의 과제만 추출
- `innerHTML` : 카드와 상세 내용을 화면에 출력
- `addEventListener()` : 클릭 등의 사용자 동작 처리

---

## 7. 과제 추가 방법

새 과제를 추가할 때는 `script.js`를 수정하지 않고 `data.json`에 새로운 객체를 추가합니다.

```json
{
  "title": "새 과제 제목",
  "category": "AI영상",
  "course": "AI 데이터 저널리즘",
  "date": "2026.09",
  "tools": "사용한 도구",
  "intent": "기획 의도",
  "process": "작업 과정",
  "youtube": "",
  "embed": "",
  "app": "",
  "images": ["images/이미지파일.png"],
  "file": ""
}
```

여러 과제 객체 사이에는 쉼표(`,`)가 필요합니다.

---

## 8. 이번 실습에서 익힌 내용

이 프로젝트를 통해 다음 구조를 실습했습니다.

**HTML/CSS → JavaScript → JSON → fetch → DOM → 웹페이지 출력**

특히 과제 데이터를 JavaScript 코드 안에 직접 작성하는 대신 별도의 `data.json` 파일로 분리하고, `fetch()`로 데이터를 불러와 기존 화면에 출력하는 방식을 적용했습니다.