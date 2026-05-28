# 26년 5월 28일 학습 기록

## Python_예외 처리
### 1. 예외(Exception)이란
프로그램 실행 중 발생하는 오류를 예외라고 칭함
- 숫자가 아닌 값을 숫자로 변환할 때
- 0으로 나눌 때
- 존재하지 않는 리스트 인덱스를 사용할 때

오류가 발생할 수 있는데, 예시로는
``` python
num = int("hello")
```
문자열 "hello"를 숫자(정수형)으로 변환하려고 해서 오류가 발생했음

### 2. 예외 처리가 필요한 이유는?
예외 처리를 하지 않으면 프로그램이 강제 종료가 됨
``` python
num = int(input("숫자를 입력하세요.: "))
print(num)
```
사용자가 숫자가 아닌 값을 입력하면 프로그램이 종료됨


| 예외 이름 | 설명 |
|---|---|
| ValueError | 잘못된 값 입력 |
| ZeroDivisionError | 0으로 나누기 |
| IndexError | 리스트 범위 초과 |
| KeyError | 딕셔너리 key 없음 |
| TypeError | 잘못된 자료형 연산 |

### 3. try ~ except
예외가 발생할 가능성이 있는 코드는 try문 안에 작성하며, 오류가 발생하면 except가 실행됨

``` python
# try : 내가 실행해야 하는 코드(에러 처리가 발생할 수 있는 코드)
# 실행 흐름: 1) try 코드 실행 2) 오류가 없다면 정상적으로 실행 3) 오류 발생 시 except 실행
try:
    num = int(input("숫자를 입력해 주세요.: "))
    print(num)

except:
    print("숫자만 입력해 주세요.")
```

예시
``` python
# 사용자로부터 숫자 2개를 입력 받고 두 숫자를 더한 합을 출력하시오.
# 이때, 숫자가 아닌 값을 입력한 경우 "잘못된 입력입니다" 를 출력하시오.

# 사용자가 숫자를 두 개 입력 받음
# split으로 공백을 기준으로 두 개의 숫자를 구분한 뒤,
# int로 해당 문자열을 정수형으로 치환
try:
    num_1, num_2 = map(int, input("숫자를 입력해 주세요.: ").split())
    result = num_1 + num_2
    print(result)

# 이때, 숫자가 두 개가 아닌 개수로 입력되거나 소수, 숫자가 아닌 것 등이 입력되면 모두 except로 이동
except ValueError:
    print("잘못된 입력입니다. ")


try:
    input_num = input("숫자를 입력해 주세요.: ").split()

    if len(input_num) != 2:
        print("숫자를 두 개 입력해 주세요.")
    else:
        num = map(int, input_num)
        result = sum(num)
        print(result)

except ValueError:
    print("잘못된 입력입니다.")
```

### 4. ZeroDivisionError
0으로 나누면 오류가 발생함

예시
```python
# num 10 / 0
# 입력 받은 숫자를 0으로 나누려고 할 때, "0으로는 나눌 수 없습니다." 출력 

try:
    input_num = int(input("숫자를 입력해 주세요.: "))
    print(10 / input_num)

except ZeroDivisionError:
    print("0으로는 나눌 수 없습니다.")

except ValueError:
    print("잘못된 입력입니다.")
```

### 5. IndexError
``` python
numbers = [1, 2, 3]

try:
    num = int(input("해당 인덱스 번호를 입력해 주세요."))
    print(numbers[num])

except ValueError:
    print("잘못된 입력입니다.")

except IndexError:
    print("해당 인덱스 번호가 존재하지 않습니다. 다시 입력해 주세요.")
```

### 6. 딕셔너리에서의 오류 처리

``` python
student = {
    "name": "홍길동"
}

try:
    input_key = input("찾고자 하는 항목을 입력해 주세요.")
    print(student[input_key])

except KeyError:
    print("존재하지 않는 항목입니다. 다시 입력해 주세요.")
```

### 7. finally
finally는 오류의 여부와 관계 없이 항상 실행됨
``` python
student = {
    "name": "홍길동"
}
try:
    input_key = input("찾고 싶은 항목을 말씀해 주세요.")
    print(student[input_key])

except KeyError:
    print("존재하지 않는 항목입니다.")

# 예외 발생 여부에 상관없이 무조건 실행
finally:
    print("프로그램을 종료합니다.")
```

### 8. else
else는 오류가 발생하지 않았을 때만 실행됨
``` python
student = {
    "name": "홍길동"
}
try:
    input_key = input("찾고 싶은 항목을 말씀해 주세요.")
    print(student[input_key])

except KeyError:
    print("존재하지 않는 항목입니다.")

# 예외가 발생하지 않았을 때만 실행
else:
    print("프로그램을 종료합니다.")
```

### 9. 예외 객체 사용하기
해당 객체를 사용하면 오류의 내용 직접 확인할 수 있다는 장점이 있음
``` python
try:
    num = 10/0
except Exception as Error_Name:
    print(Error_Name) #division by zero
```

### 10. 반복문
예외 처리는 반복문과 함께 자주 사용되는데, 올바른 입력이 들어올 때까지 반복할 수 있다.
``` python
while True:
    try:
        input_num = int(input("올바른 숫자를 입력해 주세요."))
        break
    except:
        print("잘못된 입력입니다.")
```

## NumPy
### 1. NumPy란?
NumPy는 파이썬에서 수치 계산을 쉽게 하기 위한 라이브러리인데
특히
- 배열(Array) 처리
- 행렬 계산
- 수학 연산
- 데이터 분석
- AI / 머신러닝
분야에서 매우 자주 사용됨

### 2. NumPy 불러오기
NumPy는 보통 np라는 별칭으로 자주 사용되는데,
``` python
import numpy as np
```
를 꼭 실행 시켜 둔 뒤, 작업을 진행해야 함

### 3. 배열(Array)
NumPy에서는 리스트 대신 배열 사용
``` python
arr = np.array([1,2,3,4,5])
arr 
# array([1,2,3,4,5])
```

### 4. Array의 자료형 확인하기
``` python
arr1 = np.array([1,2,3,4])
arr2 = np.array([1.2, 0.5, 7.2])
arr3 = np.array(['딸기', '바나나', '포도'])

print(arr1.dtype)
print(arr2.dtype)
print(arr3.dtype)
# data type; data가 어떤 type인지 확인
# dtype은 함수나 method가 아닌 기능의 역할
```

### 5. Array의 차원
NumPy의 Array는 여러 차원을 가질 수 있음

예시
### 1차원 배열
``` python
arr1 = np.array([1,2,3,4])

print(arr1) #[1 2 3 4]
# (n,) -> 출력되는 값이 n 하나이니 1차원
print(arr1.shape) #(4,) 
# ndim;number of dimensions; 해당 데이터가 몇 차원인지 나타냄
print(arr1.ndim) #1
# size -> 총 요소의 개수를 알려줌
print(arr1.size) #4
```

### 2차원 배열
``` python 
# 각각 list의 요소의 개수가 같아야 함
arr2 = np.array([[1,2,3], [4,5,6], [7,8,9]])

print(arr2.shape) # (3, 3) -> 행과 열이 각 3개임을 의미
print(arr2.ndim) # 2 
print(arr2.size) # 9 -> 요소의 "총 개수"를 알려 주니 9
```

### 6. 임의의 Array 생성
예시
### 0으로만 이루어진 Array
``` python
# 여기에서 2와 3은 각각 행과 열의 개수를 의미함
# 1차원은 열이라고 표현하기는 애매하고 일직선의 값들(요소의 개수)
np.zeros((2, 3), dtype = "int") #int64
```

### 1으로만 이루어진 Array
``` python
np.ones([3, 2], dtype = "int")
```

### 원하는 숫자로 채워진 Array
``` python
#full(shape, 원하는 숫자)
np.full((3, 2), 832)
# 832가 3행 2열로 채워진 배열
```

### 0~49까지의 숫자가 들어간 Array 생성

방법 1. 반복문 사용
예시
``` python
# 1. 0~49의 숫자가 들어간 list생성
num_list = []

# for문으로 인해 반복되는 i값이 num_list에 누적되어 저장
for i in range(50):
    num_list.append(i)

print(np.array(num_list))
```
방법 2. 함수 활용
``` python
# 함수는 순차적으로 작성이 가능함
# reshape(n, m): 열의 개수가 m개, 행의 개수가 n개인 2차원의 배열로 재구성

np.arange(50).reshape(5, 10)
```

### 7. Array의 data 접근
``` python
# 1차원 배열

arr = np.array([1, 2, 3])

arr[0] 
# np.int64[1]
```

``` python
# 2차원 배열

arr = np.array([[1, 2, 3], [4, 5, 6]])

# 배열 내 리스트의 각 행과 열이 1번째인 자료니까 1번행의 1번열인 5가 나옴
# 늘 접근은 index 기준
arr[1][1] 
```

``` python
# 슬라이싱 
# 1차원 슬라이싱
arr = np.array([10, 20, 30, 40, 50])

arr[1:3] #array([20, 30])

# 2차원 슬라이싱
arr = np.arange(50).reshape(5, 10)

arr[1:3] # 1번부터 2번행이 출력
arr[1:3, 3] # 1번부터 2번 행의 3번열에 속한 데이터값 출력
arr[:, 5] # 모든 행의 5번 열에 속한 데이터값 출력
arr[2, 1:4] # 2번 행의 1번부터 3번 열에 속한 데이터값 출력
arr[2:5, 1:4] # 2번 행부터 4번 행의 1번부터 3번 열에 속한 데이터값 출력
arr[[2, 3], [3, 4]] # 2번 행의 3번열, 3번 행의 4번 열에 응하는 데이터값 출력
```

### 8. NumPy Array 연산
예시
``` python
arr = np.array([1, 2, 3])

print(arr + 10) # [11 12 13]
print(arr * 10) # [10 20 30]
```

``` python
# array끼리 계산(이때 array는 같은 요소의 개수를 가진 배열들의 같은 열끼리 계산함)

a = np.array([10, 20, 30])
b = np.array([5, 10, 15])

print(a + b) # 15 30 45
print(a - b) # 5 10 15
print(a * b) # 50 200 450
print(a / b) # 2 2 2 
```

``` python
# 평균, 합계, 최댓값, 최솟값 구하기

arr = np.array([1, 2, 3, 4])

# average는 가중치가 있는 평균을 구할 때 사용하기 좋음
print(np.mean(arr))
print(np.sum(arr))
print(np.max(arr))
print(np.min(arr))
```

### 9. 조건문과 NumPy
조건을 사용해 원하는 데이터만을 가져올 수 있음

예시
``` python
arr = np.array([10, 20, 30, 40, 50])

#30 이상만 추출
print(arr[arr >= 30]) #Boolean Indexing(불리언 색인)
```
### 10. 반복문과 NumPy
예시
``` python 
arr = np.array([3, 8, 15, 20, 11, 6])

for num in arr:
    if num % 2 == 0:
        print(num)
```

### 11. 랜덤 데이터
예시
``` python
# 랜덤 정수
np.random.randint(1, 10) # 1~10
np.random.randint(1, 10, size = 3) # 3 = 랜덤으로 뽑힐 요소의 개수

# 랜덤 실수
print(np.random.rand(5) * 10)
# 소수점 2번째 자리만 오게 하고 싶으면
print(np.round(np.random.rand(5) * 10, 2))
```

## Pandas(Series)
### 1. Pandas란
- 파이썬 데이터 분석 라이브러리를 의미
- 1차원인 Series와 2차원인 DataFrame의 자룍 구조를 제공

불러오는 방법은 NumPy와 구조가 같음
```python
import pandas as pd
```

### 2. Series
- index(라벨)과 value(값)으로 이루어져 있음
- 딕셔너리와 구조가 유사함

예시
``` python
#          값(value)
pd.Series([9668465, 3391946, 2942828, 1450062])
pd.Series([9668465, 3391946, 2942828, 1450062], index = ['서울', '부산', '인천', '광주'])

'''
서울    9668465
부산    3391946
인천    2942828
광주    1450062
dtype: int64
''' 
위 값을 출력
```

### 3. Series의 값 확인
``` python
# dictionary로 series를 생성
dict = {'서울' : 9668465, '부산' : 3391946, '인천' : 2942828, '광주' : 1450062}
population = pd.Series(dict)

# 1. Series의 value값만 따로 확인 
print(population.values) #값들만 가져와서 배열의 형태(array)로 반환
# [9668465 3391946 2942828 1450062]

# 2. Series의 index값만 따로 확인 
# Index 형태(객체_object; 데이터 + 기능 / 도구 느낌)로 반환
print(population.index) 
# Index(['서울', '부산', '인천', '광주'], dtype='object')

# 3. Series의 dtype을 확인해주는 기능
print(population.dtype)
# int64
```

### 4. Series의 이름(name) 
``` python
# Series의 이름 짓기

population.name = "2026년 각 도시 인구 데이터"
population.index.name = "도시"
population

'''
도시
서울    9668465
부산    3391946
인천    2942828
광주    1450062
Name: 2026년 각 도시 인구 데이터, dtype: int64
'''
로 값이 출력
```

### 5. Series 연산
``` python
population / 1000000

'''
도시
서울    9.668465
부산    3.391946
인천    2.942828
광주    1.450062
Name: 2026년 각 도시 인구 데이터, dtype: float64
'''
로 값이 출력
```
### 6. Series의 요약 데이터 확인(합계, 평균 등)
예시
``` python
food_name = ['치킨', '닭갈비', '삼겹살', '공기밥', '닭가슴살', '아보카도', '우유']
food_kcal = [840,585,661,310,120,322,122]
food = pd.Series(food_kcal, index = food_name)
food.name = "음식 칼로리(kcal)"
food.index.name = "음식명"

food

'''
음식명
치킨      840
닭갈비     585
삼겹살     661
공기밥     310
닭가슴살    120
아보카도    322
우유      122
Name: 음식 칼로리(kcal), dtype: int64
'''
```
를 활용해서
``` python
print(food.sum())
# 평균을 구하면 소수점 아래 숫자가 길어질 수 있으니 일단 소수점 아래 숫자를 2로 지정했음
print(round(food.mean(), 2)) 
print(food.max())
print(food.min())
print(food.count()) # food의 요소의 개수

'''
2960
422.86
840
120
7
'''
# 한 번에 확인하는 방법은
food.describe()
'''
count      7.000000
mean     422.857143
std      277.535841 <- 표준 편차; value가 평균에서 얼마나 멀리 떨어져 있는지
min      120.000000
25%      216.000000
50%      322.000000
75%      623.000000
max      840.000000
Name: 음식 칼로리(kcal), dtype: float64
'''
```

### 7. Series 인덱싱과 슬라이싱
``` python
# indexing
print(food["삼겹살"])
print(food.loc["삼겹살"])

print(food[2]) # python 2번 데이터를 인덱싱
#iloc = integer location, 컴퓨터가 인식하는 순서에 따라 데이터에 접근함
print(food.iloc[2]) # index 번호로 2번에 접근
```
food[2]처럼 접근하는 것보다는 iloc을 통해 접근하는 것을 권장