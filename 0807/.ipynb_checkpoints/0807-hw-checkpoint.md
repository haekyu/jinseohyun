### 1. 기본 연산 연습 1

- x라는 변수에 'abcdef'라는 string이 assign돼 있다고 했을 때, 'bcdefa' 라는 string을 얻어 보세요.
- 힌트: 다음 코드에서 ??? 안의 값을 채워 됩니다.

```python
x = 'abcdef'
y = ???
print(y)
```


### 2. Boolean 연습

- XOR 연산을 만들어 봅시다.
- XOR (exclusive or) 은 두 개의 명제 가운데 한개만 참일 경우를 판단하는 논리 연산이다. ([위키](https://ko.wikipedia.org/wiki/배타적_논리합))
- XOR 연산의 진리표는 다음과 같다.
  - True xor True == False
  - True xor False == True
  - False xor True == True
  - False xor True == False
- 다음 코드에서 ??? 안의 값을 채워도 됩니다.
  ```python
  x = ??? # True 아니면 False 대입
  y = ??? # True 아니면 False 대입
  z = ??? # x xor y 값이 들어가도록 만듦
  print(z)
  ```
  
## 3. Loop문 연습 1
아래 모양대로 출력을 해 보세요.
```
*
**
***
****
*****
```

## 4. Loop문 연습 2
아래 모양대로 출력을 해 보세요.
```
    *
   **
  ***
 ****
*****
```

## 5. Loop문 연습 4
아래 모양대로 출력을 해 보세요.
```
    **
   ****
  ******
 ********
**********
 ********
  ******
   ****
    **
```   

## 6. Loop문 연습 5
- 20 의 약수들을 모은 어떤 리스트를 만들어봅시다.
- 다음과 같은 skeleton code를 이용해도 됩니다.
	```python
	factors_of_20 = []
	for i in range(?, ?, ?):
	    if ???:
	        ????
	print(factors_of_20)
	```

## 7. Loop문 연습 6
- 구구단 출력하기.
```
1 * 1 = 1
1 * 2 = 2
....
9 * 9 = 81
```
이 출력 되도록 해 보세요.

- 힌트) loop 문 안에 loop문이 들어갈 수 있습니다.


## 8. loop문 연습 1

- 숫자로 구성된 리스트가 주어져 있을 때, 리스트 내 값들의 평균을 구해보기.<br>
  예를 들어, lst = [1, -2, 5, 4, -3] 일 때 1을 프린트 해 보세요.
- 아래와 같은 skeleton code를 사용해도 됩니다.
	```python
	lst = [1, -2, 5, 4, -3]

	sum_of_elements = 0 # lst 의 원소의 합이라는 뜻
	num_of_elements = 0 # lst 의 원소의 개수라는 뜻

	idx = 0 # index 라는 뜻
	while idx < ???:
	    ???
	    idx = idx + 1

	avg_of_elements = sum_of_elements / num_of_elements

	print(avg_of_elements)
	```
	
	```python
	lst = [1, -2, 5, 4, -3]

	sum_of_elements = 0 # lst 의 원소의 합이라는 뜻
	num_of_elements = 0 # lst 의 원소의 개수라는 뜻

	for e in ???:
	    ???

	avg_of_elements = sum_of_elements / num_of_elements

	print(avg_of_elements)
	```



## 9. string 연습 1
- 스트링으로 된 문장 내부에 특정 word가 몇 번 포함되는지 찾기.
- 예를 들어, sss 와 같은 문장이 주어져 있고, 'an' 이라는 단어가 sss 내부에 몇 번 나타나는지 찾기.
    - sss = 'Love is an open door! Love is an open door! Life can be so much more!'<br>
  일 때, an 이 두 개 있으니 2를 프린트하게 해 보세요.
- str을 ' ' (띄어쓰기) 기준으로 잘라 list에 보관할 수 있습니다.
    + 예) lst = sss.split(' ') 을 하게 되면<br>
		lst 는 ['Love', 'is', 'an', ...] 이 됩니다.
- 아래의 skeleton code를 사용해도 됩니다.
    ```python
    sss = 'Love is an open door! Love is an open door! Life can be so much more!'
    lst = sss.split(' ')

    idx = 0 # lst의 index 라는 뜻
    num = 0 # 'an'의 개수라는 뜻
    while ???:
        if ???:
            num = num + 1
        idx = idx + 1
    print(num)
    ```


## 10. string 연습 2
- 스트링으로 된 문장 내부에 특정 문구가 몇 번 포함되는지 찾기.
- 예를 들어, sss 와 같은 문장이 주어져 있고, 'an'이 들어간 단어가 sss 내부에 몇 번 나타나는지 찾기.
    - sss = 'Love is an open door! Love is an open door! Life can be so much more!'<br>
  일 때, an 이 들어간 단어는 3개가 있습니다.<br>
    - 세 번의 an 은 아래와 같이 검색됩니다. <br>
	Love is ``an`` open door!<br>
	Love is ``an`` open door!<br>
	Life c``an`` be so much more!<br>
	
