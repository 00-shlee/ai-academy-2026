# 26-05-14 HTML, CSS, JS 학습 정리

## 1. input-field에서 field를 사용하는 이유
- field = 입력 공간
- input = html 태그 이름, input-field = 입력 공간 스타일

## 2. let vs const
- let = 나중에 값이 바뀔 수 있는 변수
- const = 한 번 정하면 절대 안 바뀌는 변수
- ex) let은 나이, const는 이름 / let은 inputValue, const는 loginBtn (로그인 버튼은 안 바뀌니까)
- 엄밀히는 let = 변수, const = 상수
- 일상 대화(실무)에서는 const도 "변수"라고 부름
- Python 2강에서 변수를 "데이터를 담아두는 상자"라고 칭함
- JS에서도 동일: `const loginBtn = document.querySelector('#loginBtn')` → loginBtn = 버튼을 담아두는 상자

## 3. querySelector(getElementBy... 대신 사용)
- 뒤에 오는 기호로 구별 = CSS와 동일
  - `#`: id 선택자 (페이지에 하나만 존재)
  - `.`: class 선택자 (여러 개 동시 존재 가능)
  - 기호 없음: 태그 선택자 (그 태그 전부 선택)

## 4. if(loginBtn)
- loginBtn이 진짜 존재하면 (loginBtn이 null이 아니면)
- 사용 이유: html에 로그인 버튼이 없는 페이지 (ex. 회원가입)에서 이 js가 실행되면 에러 발생

## 5. addEventListener
- 특정 요소에게 특정 이벤트가 발생하면 특정 함수를 실행하라고 등록하는 것
- ex) 요소: 경비원(특정 문), 이벤트: 경비원이 감지할 것(누가 문 두드리는지), 함수: 문 두드리면 할 행동(문 열기, 신원 확인 등)
- `loginBtn.addEventListener('click', function(){ alert('환영합니다!') })`
- 로그인 버튼(경비원)아, 클릭 소리 들리면(문 두드리면), 환영합니다 알림 띄워 줘(문 열어 줘)

## 6. return이 사용되는 이유
- return이 해당 함수 전체의 강제 종료 역할 (마침표 느낌)
- if절 안에 있어도 함수 전체를 강제 종료
- return이 없으면 '아이디와 비밀번호를 입력하세요.' 창이 뜬 후, 바로 '환영합니다!' 팝업창 뜸

## 7. section vs div
- section = 해당 구역 전체를 나타내며 타 section과 구별이 가능함
- div = 그저 해당 내용(결과)을 채울 빈 공간에 불과
- section은 구역, div는 그릇 같은 느낌

## 8. querySelector에서 # 기호를 사용한 이유
- loadPostBtn, result는 각 페이지에 하나밖에 없는 고유한 값이라 id이기 때문에 (#)

## 9. result가 let이 아닌 const를 사용한 이유
- result는 값의 결과값이 아닌 result가 나오는 상자, 공간
- 상자 자체(const)는 안 바뀜, 상자 안 내용(result.innerHTML)은 바뀜

## 10. API 흐름
- 사용자 → 버튼 클릭
- JS → fetch()로 api 서버에 요청 ('이 url로 다녀와 줘.' / 결과가 '언젠가 도착할' 작업을 비동기(async)로 처리)
  - 동기: 순서대로, 하나 끝나야 다음 진행 (ex. 카운터에서 기다리는 느낌)
  - 비동기: 기다리는 동안 다른 거 먼저 진행 (ex. 진동벨)
- api server → 데이터 응답 / json 형식 (데이터 포장 형식)
  - json: 키-값 쌍, 라벨(키)로 데이터(값)를 찾는 방식, python 딕셔너리와 매우 유사
- JS → 화면 출력

## 11. async/await
```javascript
async function(){ 
    const response = await fetch(url) 
}
```
- await 줄에서 잠깐 대기
- 함수 바깥에 있는 다른 것들은 계속 돌아감
- url에서 응답이 오면 다음 줄 실행

## 12. response와 response.json()
```javascript
const response = await fetch('url link')
const data = await response.json()
```
- response = 서버에서 받아온 택배 상자 (변수)
- response.json() = response 안의 내용을 JSON 형태로 변환해줘
- JSON = 데이터 형식 (포장 방식)
- .json() = JSON 형식으로 변환 실행
- () = 실행 기호 (버튼 누르기)
- data['키'] = 변환된 데이터에서 값 꺼내기

## 13. 백틱(``)
- 문자열 안에 변수를 끼워넣을 때 사용
- 기존 방식: `"<h2>" + 제목 + "</h2>"`
- 백틱 방식: `` `<h2>${제목}</h2>` ``
- \+ 기호 없이 변수 바로 끼워넣기 가능, 줄바꿈이 자유로움

## 14. forEach
- 배열의 모든 요소를 처음부터 끝까지 반복하여 실행

## 15. document.createElement
```javascript
const card = document.createElement("article")
```
- html의 article(기호 없으니 태그 선택자)를 js에서 새로 만드는 것
- 영화의 수를 모르니까 html에 미리 못 씀 → js가 그때그때 article 태그를 새로 만듦
- const card = 만든 article 태그를 card라는 변수에 담기
- Elements가 아닌 Element인 이유: 태그를 딱 하나만 만드니까 / 여러 개를 만들고 싶으면 forEach 사용
- 어쨌든 태그를 만드는 건 단수 행위이고, forEach가 반복하는 거니까 s는 오지 않음

## 16. appendChild
```javascript
movieList.appendChild(card)
```
- movieList라는 상위 개념에 ()의 해당 내용을 appendChild로 넣는 것

## 17. data.results
- 변환된 data에서 results 값을 꺼내는 것
- ex) movie.title → movie에서 title 값을 꺼내는 것

## 18. fetch 두 번째 인자
```javascript
fetch(TMDB_URL, {
    method: "GET",
    headers: {
        accept: "application/json",
        Authorization: `Bearer ${TMDB_TOKEN}`
    }
})
```
- method: "GET" → 영화 데이터를 가져오는 거니까 GET
- headers: 요청할 때 함께 보내는 부가 정보(봉투 겉면) / '이제부터 부가 정보를 말할 거야~'라고 암시하는 단어
- accept: "application/json" → json 형식으로 데이터를 받고 싶음
- Authorization: Bearer ${TMDB_TOKEN} → 회원증(TOKEN)을 보여주고 증명하는 것
  - Authorization = "나 회원이에요." 증명
  - Bearer ${TMDB_TOKEN} = "여기 회원증이에요."
