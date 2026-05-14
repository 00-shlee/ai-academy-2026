# 26-05-13 HTML, CSS 학습 정리

## 1. <!DOCTYPE html>
- doctype = document type
- html5 이전 버전은 DOCTYPE이 길고 복잡했음
- html5부터 `<!DOCTYPE html>`으로 간결하게 고정됨
- 즉, "html"이라고만 쓰여있으면 = html5 규격

## 2. `<head>`와 `<body>`의 차이
- `<head>` : 설정 정보 (화면에 안 보임) → 페이지 제목, 인코딩, CSS 연결, 메타데이터 등
- `<body>` : 실제 내용 (화면에 보임) → 제목, 글, 이미지, 버튼 등

## 3. `<meta charset="UTF-8">`
- meta = 메타데이터 (부가 정보)
- charset = character set (문자 집합)
- "이 페이지의 글자는 UTF-8 방식으로 인코딩되어 있다"고 브라우저에게 알려줌

### 3-1. UTF-8이란?
- 유니코드 : 전 세계 모든 글자에 고유 번호를 매긴 것
- UTF-8 : 유니코드를 저장하는 방법 (구현 방식)
- 즉, 유니코드 번호를 효율적으로 압축해서 저장하는 방식

## 4. `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
- viewport : 화면 영역 (보이는 창)
- width=device-width : 페이지의 너비를 기기 화면 너비에 맞춰라
- width : 너비, 가로 길이
- meta는 페이지에 대한 부가 정보를 적는 태그이기 때문에 `<head>`에만 사용

### 4-1. viewport를 정할 때 거의 width만 사용하는 이유
- 웹페이지는 기본적으로 '세로로 긴' 구조
- 위에서 아래로 읽도록 만들어지기 때문에 height는 굳이 설정하지 않음

## 5. `<link rel="stylesheet" href="css/style.css">`
- href = hypertext reference (하이퍼텍스트 참조) → "연결할 곳의 주소"
- `<link href="...">` : 외부 리소스 가져오기 (주로 CSS) → 브라우저를 위한 것
- `<a href="...">` : 클릭 시 이동할 링크 주소 지정 (외부 사이트, 이메일, 전화번호 등) → 사용자를 위한 것

### 2 + 5 정리
- `<head>`와 `<body>`는 각각 `<link href>`와 `<a href>`의 상위 개념 (공간)
- `<link>`와 `<a>`는 그 공간 안의 개별 태그 (하위)

## 6. `<main class="page">`
- `<main>` : 그 페이지의 핵심 콘텐츠를 감싸는 상자
- `class="page"` : 태그에 "별명/이름표"를 붙이는 속성
- CSS에서 해당 별명으로 디자인을 적용할 때 사용

## 7. `<section>`
- "내용을 의미 단위로 묶는 구역"을 만드는 태그
- 로그인, 회원가입처럼 목적이 하나인 페이지 → section 하나
- 회사 홈페이지, 쇼핑몰 메인 등 → section 여러 개
- 각 section 구분 방법 → class 사용

```html
<section class="intro">회사소개</section>
<section class="reviews">고객 후기</section>
<section class="contact">문의하기</section>
```

- CSS에서 class 참조할 때 "."을 붙임
  - `.intro` → intro라는 class를 가진 곳에 디자인 적용
  - `.reviews` → reviews라는 class를 가진 곳에 디자인 적용

## 8. `<h1>` ~ `<h6>` (제목 태그)
- h = heading (제목)
- 숫자가 클수록 작은 제목
- `<h1>` : 가장 큰 제목 (페이지당 하나만 사용 권장)

## 9. `<p>` (문단)
- p = paragraph (문단)
- 일반적인 글, 문장을 적을 때 사용
- 자동으로 줄바꿈 + 위아래 여백 생김
- ex) `<p>아이디와 비밀번호를 입력하세요.</p>`

## 10. `<form>` (입력 양식)
- "사용자가 입력하는 양식들을 묶는 상자"
- 로그인, 회원가입, 검색창, 댓글 작성 등 사용자가 입력하고 제출하는 모든 곳에 사용

```html
<form>
  <input ...>            ← 입력칸
  <input ...>            ← 또 다른 입력칸
  <button>전송</button>  ← 제출 버튼
</form>
```

## 11. `<div>` (구역 나누기)
- div = division (구분, 나누기)
- 아무 의미 없이 그냥 묶기 위한 상자
- `<section>`과의 차이 : 의미의 유무
  - `<section>` : 의미 있는 구역
  - `<div>` : 의미 없는 그냥 묶음용 상자

## 12. `<label>` (이름표)
- 입력칸 옆에 붙는 설명 글자
- for 속성으로 어떤 input과 연결되는지 지정

```html
<label for="loginId">아이디</label>
<input id="loginId" type="text">
```

- 화면 표시 → 아이디 : [__________]
- 라벨 클릭 시 자동으로 해당 입력칸에 커서 이동

## 13. 시맨틱(Semantic) 태그
- "의미 있는 태그" → 태그 이름만 봐도 역할을 알 수 있음
- 검색엔진, 스크린 리더, 개발자 협업에 유리

| 태그 | 역할 |
|------|------|
| `<header>` | 페이지/섹션의 맨 위쪽 영역 (로고, 메뉴, 검색창 등) |
| `<nav>` | 메뉴/네비게이션 |
| `<main>` | 페이지의 핵심 콘텐츠 |
| `<section>` | 의미 있는 구역 |
| `<article>` | 독립적인 글 (블로그 글 등) |
| `<aside>` | 부가 정보 / 사이드바 |
| `<footer>` | 페이지의 맨 아래쪽 영역 (회사 정보, 저작권, 연락처 등) |

## 14. align
- `text-align` : 텍스트 정렬
- `align-items` : 요소들 세로 정렬
- `align-self` : 나 자신만 세로 정렬
- `vertical-align` : 인라인 요소 세로 정렬

## 15. border
- border는 테두리, 있고 없고는 테두리의 차이

## 16. input-field로 동시에 디자인
- 같은 class가 붙어 있으면 같이 적용

```html
<input class="input-field" type="text"     placeholder="아이디">
<input class="input-field" type="password" placeholder="비밀번호">
```

## 17. height vs min-height
- `height: 100vh` = "딱 화면 높이 만큼만" (스크롤 없이 보이는 영역의 전체)
- `min-height: 100vh` = "최소 그 높이는 되어야 함", 콘텐츠가 더 많으면 자연스럽게 늘어남(스크롤)
  - height를 사용하는 상황: "이 크기에서 절대 벗어나면 안 돼"
  - ex) 크기가 절대 변하면 안 되는 요소 (이미지, 네비게이션 바, 카드 등)
