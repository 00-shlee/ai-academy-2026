26년 6월 16일 학습 기록

# python 인공지능사관학교 진도 백로그
## 00) 사전 학습 ~ 06) 예외 처리

헷갈리는 부분, 까먹은 부분만 다시 정리

### 00. 사전 학습
**산술 연산자**

| 연산자 | 의미 | 예시 |
|---|---|---|
| + | 더하기 | 10 + 3 |
| - | 빼기 | 10 - 3 |
| * | 곱하기 | 10 * 3 |
| / | 나누기 | 10 / 3 |
| // | 몫 | 10 // 3 |
| % | 나머지 | 10 % 3 |
| ** | 거듭제곱 | 10 ** 3 |
---

**비교 연산자**
| 연산자 | 의미 |
|---|---|
| == | 같다 |
| != | 같지 않다 |
| > | 크다 |
| < | 작다 |
| >= | 크거나 같다 |
| <= | 작거나 같다 |

### 02. list, tuple

**list와 tuple의 차이점**
| 동작 | List | Tuple |
|------|:---:|:---:|
| 읽기 | ✅ | ✅ |
| 수정 | ✅ | ❌ |
| `append`, `remove` 등 | ✅ | ❌ |
| Index로 한 개 수정 (`a[0]=10`) | ✅ | ❌ |
| 사용예시| 변경되는 데이터 (장바구니, 게임 인벤토리) | 고정된 데이터 (좌표값, RGB 색상, 데이터베이스 조회 결과) |

- **따로 정리해 두었던 것**
``` python
from getpass import getpass
```
비밀번호, API 키, 토큰처럼 **숨겨야 하는 값을 안전하게 입력**받기 위해 getpass() 함수를 불러오는 코드(input과 달리 **입력 시 화면에 표시되지 않음**)

### 03. 반복문
#### 기본 구조

for문은 **정해진 횟수만큼 반복**할 때 자주 사용
```python
for 변수 in 반복할대상:
    실행할 코드

# 값을 사용하지 않는 반복 변수는 i 대신 _를 쓰는 것이 관례
# range: 범위 지정 함수 range(n)
for _ in range(5):
    print("안녕하세요")
```

| 코드                | 의미        |
| ----------------- | --------- |
| `range(5)`        | 0 ~ 4     |
| `range(1, 5)`    | 1 ~ 4     |
| `range(1, 10, 2)` | 1부터 2씩 증가 |

``` python
# range(시작,끝,간격) 시작부터 끝-1까지, 간격만큼 점프 / 즉, 거꾸로 출력하고 싶으면 간격을 -1로 설정
```

- **헷갈려서 정리해 두었던 코드**
``` python
# 실습 5 (실전)
# 리스트 안의 숫자 중 60미만인 숫자를 60으로 수정하시오.

scores = [50, 80, 40, 90]  # [60, 80, 60, 90]

for i in range(len(scores)):
    if scores[i] < 60:
        scores[i] = 60

print(scores) 

'''
해당 코드 이해하려면 
scores = [50, 80, 40, 90]라는 리스트가 있는데,
이걸 len으로 해당 리스트의 개수 (4)를 구한 뒤,
range로 0부터 시작해서 4 직전까지의 숫자를 만들고,
 ==> len(scores) = 4이기 때문 / scores의 요소 개수가 4개니까 range(len(scores)) = range(4)가 됨
for문으로 그 숫자를 i라는 변수에 하나씩 넣어 반복하면서,
i를 인덱스로 사용해 scores[i] 값이 60미만이면 60으로 바꾼 뒤,
 ==> scores[i] = 60은 원본 리스트의 i번째 자리(if 조건에 해당하는 것)를 직접 60으로 덮어 씀
반복이 끝나면 수정된 리스트를 한 번 출력하는 것
'''



for score in scores:
    if score < 60:
        print(scores.index(score))
        scores[scores.index(score)] = 60

print(scores)

'''
해당 코드는 위의 것보다 조금 복잡한데
for문으로 scores에서 score의 값을 하나씩 꺼내 반복하는데,
if문에서 해당 score의 값이 60미만이면
.index(score)에서 해당 score에 해당하는 index 번호를 찾고 print로 출력한 뒤,
그 인덱스 번호에 해당하는 score 값을 60으로 변경해서
반복이 끝난 뒤, 수정된 리스트를 한 번에 출력하는 것

단점이 있는데, 
.index()는 중복 값이 있으면 가장 먼저 나온 인덱스 위치만 반환하기 때문에
중복값이 있어도 첫 번째 위치만 알려 주므로, 나머지 중복 위치는 찾지 못함
'''
```

### 04. 딕셔너리
``` python
student = {
    "name": "홍길동",
    "age": 20
}

student["age"] = 21 #수정(기존에 존재하는 key)
student["major"] = "컴퓨터공학" #추가(기존에 존재하지 않는 key)

print(student)
```
해당 코드와 같이 딕셔너리는 **수정과 추가가 가능**하며, 위 내용에는 작성하지 않았지만 **del로 삭제 또한 가능**함

- **틀려서 정리해 두었던 코드**
``` python
## 실습2. 반복문으로 학생 정보 출력하기/ + 60점을 기준으로 합격/ 불합격

students = [
    {"name": "홍길동", "score": 80},
    {"name": "김철수", "score": 55},
    {"name": "이영희", "score": 90}
]

'''

#실수했던 것들


1. 처음 코드
for item in students.items:
    if ["score"] >= 60:
        print(f'{"name"}: "합격"')
else:
    print(f'{"name"}: "불합격"')
이라고 작성했음
틀린 이유 1) students는 list, .items() = dic의 method
 ==> 수정은 for item in students: // item에 dic 요소 하나씩 들어옴
 ==> 심지어 method인데 .items 뒤에 ()도 빼먹음

틀린 이유 2) if ["score"] >= 60:
 ==> 이건 "score"이라는 문자열이 들어 있는 리스트
 ==> 내가 원하는 건 'item 안의 score 값을 꺼내서 60이랑 비교하는 것'
 ==> 수정은 if item["score"] >= 60:

틀린 이유 3) print(f'{"name"}: "합격"')
 ==> {"name"}은 그냥 "name"이라는 글자를 출력함 ex) #결과: "name: 합격"
 ==> 수정: print(f'{item["name"]}: 합격')

틀린 이유 4) "합격"에 따옴표
 ==> print(f'{"name"}: "합격"') < 이러면 출력에 따옴표도 같이 나옴

틀린 이유 5) else의 들여쓰기
 ==> else가 if가 아니라 for문과 연결된 위치에 있음
  내가 원하는 게 점수 조건에 따른 if-else이므로,
  else를 if와 같은 들여쓰기 위치에 둬야 함(for문 안에)


2. 두 번째 코드
for item in students:
    if item["score"] >= 60:
        print(f'{item["name""score"]}: 합격')
    else:
        print(f'{item["name""score"]}: 불합격')

 틀린 이유
==> item["name""score"] < 파이썬은 문자열 두 개가 붙어 있으면 합쳐서 하나의 문자열로 해석

3. 세 번째 코드
for item in students:
    if item["score"] >= 60:
        print(f'{name}:{score}점, 합격')
    else:
        print(f'{name}:{score}점, 불합격')

틀린 이유
==> 현재 내 코드 안에 name, score이라는 변수를 만든 적이 없음 / 변수는 내가 만들지 않으면 존재하지 않음
==> 수정
1) 매번 직접 꺼내기 print(f'{item["name"]}: {item["score"]}점, 합격')
2) 변수에 담아두기 < 깔끔함
name = item["name"]
score = item["score"]
print(f'{name}: {score}점, 합격')


'''


# 정답 코드
# 1) 변수에 미리 담아두기
for item in students:
    name = item['name']
    score = item['score']

    if score >= 60:
        print(f'{name} {score} 합격')
    else:
        print(f'{name} {score} 불합격')

# 2) 매번 직접 꺼내서 쓰기
for student in students:
    if student['score'] >= 60:
        print(student['name'], student['score'], "합격")
    else:
        print(student['name'], student['score'], "불합격")

# 3) 수정본
for student in students:
    name = student['name']
    score = student['score']

    if score >= 60:
        print(f'{name}: {score}점, 합격')
    else:
        print(f'{name}: {score}점, 불합격')

# 4) 삼항연산자 사용
# 삼항연산자: a if b else c // b: 조건식(T,F), a: T일 때 사용할 값, c: F일 때 사용할 값

for student in students:
    result = "합격" if student["score"] >= 60 else "불합격"
    print(student["name"], student["score"], result)
```

### 6. 예외 처리
``` python
# 실습 1 (실전)
# 사용자로부터 숫자 2개를 입력 받고 두 숫자를 더한 합을 출력하시오.
# 이 때, 숫자가 아닌 값을 입력한 경우 "잘못된 입력입니다" 를 출력하시오.

try:
    num_1 = int(input("더할 숫자를 입력해 주세요.: "))
    num_2 = int(input("더할 숫자를 입력해 주세요.: "))
    result = num_1 + num_2
    print(result)


# 숫자 두 개를 한 번에 입력하고 싶을 때는?
# try:
#    num_1, num_2 = map(int, input("숫자를 입력해 주세요.").split())
#   result = num_1 + num_2
#   print(result)


# 숫자 두 개를 한 번에 입력 받고 싶은데 하나만 입력했을 때는?

try:
    nums = input("숫자를 입력해 주세요.: ")split.()

    if len(nums) != 2:
        print("숫자를 두 개 입력해 주세요.")
    else:
        num_1, num_2 = map(int, nums)
        result = num_1 + num_2
        print(result)

except ValueError:
    print("숫자를 입력해 주세요.")
```
| 예외 이름               | 설명          |
| ------------------- | ----------- |
| `ValueError`        | 잘못된 값 입력    |
| `ZeroDivisionError` | 0으로 나누기     |
| `IndexError`        | 리스트 범위 초과   |
| `KeyError`          | 딕셔너리 key 없음 |
| `TypeError`         | 잘못된 자료형 연산  |
