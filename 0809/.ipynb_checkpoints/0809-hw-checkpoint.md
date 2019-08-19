## 1. List 연습 1
- list 내 최대값 구하기. 
- `lst = [2, 3, 6, 2, -1, 0, 6, 2, 3]` 이 주어져 있을 때 최대값인 6을 출력해보세요.
- 힌트1) 간단하게 `max(lst)` 로도 구할 수 있지만, `max()`를 쓰지 않고 loop로 해결해 보세요.
- 힌트2) skeleton code를 이용해도 좋습니다. ??? 을 채워 넣으면 됩니다.

```python
# Target list
lst = [2, 3, 6, 2, -1, 0, 6, 2, 3]

# Initialize max_val
max_val = -999

# Get the maximum value in lst
for v in lst:
    # if max_val is no longer the maximum value
    #  because of v that is larger than max_val
    if ????: 
        # v should be the new maximum value
        ???

print(max_val)
```

## 2. List 연습 2
- list 내 최대값을 갖는 원소가 몇 개인지 구해보세요.
- `lst = [2, 3, 6, 2, -1, 0, 6, 2, 3]` 이 주어져 있을 때, 최대값인 6은 2개 있습니다. 여기서 6의 개수인 2를 출력해 보세요.
- 이 때 다음과 같은 포맷으로 출력해 보세요: 'max = 6, num_max = 2'.

## 3. Dictionary 연습 1
- word_freqs 함수를 구현해 보세요.
    - **input**: 어떤 string. string 내 각 단어는 space로 구분되어 있음.
    - **output**: 어떤 dictionary. 이 때 key는 input내 각 단어를 말하고 value는 key 의 등장 횟수(frequency) 를 말함.
- 예) 다음과 같이 동작하는 함수를 만들어 봅시다.
    ```python
    s = "I am a boy you are a girl"
    freq_dict = word_freqs(s)
    print(freq_dict)
    ```
    출력 결과
    ```
    {'girl': 1, 'a': 2, 'you': 1, 'are': 1, 'I': 1, 'boy': 1, 'am': 1}
    ```
- **힌트)** 다음과 같은 뼈대코드를 사용해도 됩니다.
    ```python
    def word_freqs(sentence):

        # sentence 를 띄어쓰기 단위로 나누어, 
        # words 라는 리스트에 저장한다.
        words = ???

        # freq_dict 라는 새로운 dictionary를 만든다. 우리의 output이 될 것이다.
        # - key: a word
        # - val: # of the key in the sentence
        freq_dict = dict()

        # 각 word 를 살펴보면서 등장횟수를 count up 한다 (1씩 올려줌).
        for word in words:
        	???

        # freq_dict를 리턴한다.
        ???
    ```
    
## 4. Dictionary 연습 2
- 단어들을 시작 알파벳별로 분류하는 함수를 만들어 보자.
- **함수 이름**: classify_words
- **input**: 단어(string)들의 list
- **output**: 어떤 dictionary
    - key: 어떤 알파벳
    - val: input 내의 단어들 중 key로 시작하는 것들을 모은 list
- 예)
    ```python 
    word_lst = ["apple", "bear", "person", "aurora", "print", "boy"]
    classifier = classify_words(word_lst)
    print(classifier)
    ```
    출력 결과 (dictionary 내의 key나 value의 순서는 달라도 됨.)
    ```
    {'p': ['print', 'person'], 'a': ['apple', 'aurora'], 'b': ['bear', 'boy']}
    ```
- 힌트1) 리스트는 dictionary 의 value가 될 수 있습니다.
- 힌트2) 아래 skeleton code를 사용해도 됩니다.
    ```python
    def classify_words(word_lst):
        # Initialize a word dictionary, whose
        #   - key: an alphabet
        #   - val: list of words starting from the key
        classifier = dict()

        for word in word_lst:
            ???

        # Retrun the dictionary
        return ????
    ```

## 5. Bubble sort
- 숫자들을 오름차순으로 정렬하는 (즉, sorting 하는) 알고리즘중 하나인 Bubble sort를 구현해 보자.
- **input**: unsorted list
- **output**: sorted list
- Bubble sort 설명
    - 주어진 lst의 맨 끝에 maximum 값을 채워 넣는 식으로 구현할 수 있다.
    - 이 때 크기 2짜리인 sliding window 가 움직이는 것으로 생각하고, window 안에서 원하는 조건일 때 원소를 swap (두 개의 원소를 자리바꿈) 한다.
        - window는 아래 예시에서 [..., ```원소1, 원소2```, ...] 처럼 표시한다.
    - 예시) 
        + [5, 1, 2, 6, 2, 1] 가 주어졌다. 
        + stage 0: [5, 1, 2, 6, 2, 1] 에서 최대값은 6이다. 목표는 6을 맨 뒤로 밀어 넣는 것.
            * [```5, 1```, 2, 6, 2, 1]: {5, 1} 에서 5가 크니까 뒤로 보낸다. 즉, 5와 1의 순서를 바꾼다.
            * [```1, 5```, 2, 6, 2, 1]: 이 되었다.
            * [1, ```5, 2```, 6, 2, 1]: {5, 2} 에서 5가 크니까 뒤로 보낸다. 즉, 5와 2의 순서를 바꾼다.
            * [1, ```2, 5```, 6, 2, 1]: 이 되었다.
            * [1, 2, ```5, 6```, 2, 1]: {5, 6} 에서 6이 크니까 그대로 둔다.
            * [1, 2, 5, ```6, 2```, 1]: {6, 2} 에서 6이 크니까 뒤로 보낸다. 즉, 6과 2의 순서를 바꾼다.
            * [1, 2, 5, ```2, 6```, 1]: 이 되었다.
            * [1, 2, 5, 2, ```6, 1```]: {6, 1} 에서 6이 크니까 뒤로 보낸다. 즉, 6과 1의 순서를 바꾼다.
            * [1, 2, 5, 2, ```1, 6```]: 이 되었다. 끝에 도달했으니 stage 0은 끝이 난다.
        + stage 1: [1, 2, 5, 2, 1, **6**] 에서 마지막 6을 제외하고 최대값은 5이다. 목표는 5를 6 바로 앞까지 뒤로 밀어 넣는 것.
            * [```1, 2```, 5, 2, 1, **6**]: {1, 2} 에서 순서가 잘 맞으니 그대로 둔다.
            * [1, ```2, 5```, 2, 1, **6**]: {2, 5} 에서 순서가 잘 맞으니 그대로 둔다.
            * [1, 2, ```5, 2```, 1, **6**]: {5, 2} 에서 순서가 뒤바뀌었으니 순서를 바꾼다.
            * [1, 2, ```2, 5```, 1, **6**]: 가 되었다.
            * [1, 2, 2, ```5, 1```, **6**]: {5, 1} 에서 순서가 뒤바뀌었으니 순서를 바꾼다.
            * [1, 2, 2, ```1, 5```, **6**]: 가 되었다. 끝에 도달했으니 stage 1은 끝이 난다.
        + stage 2: [1, 2, 2, 1, **5, 6**] 에서 목표는 2를 뒤로 밀어 넣는 것. 아래에는 자세한 설명을 생략하고 lst의 변화 양상만을 포함. 
            * [```1, 2```, 2, 1, **5, 6**]
            * [1, ```2, 2```, 1, **5, 6**]
            * [1, 2, ```2, 1```, **5, 6**]: Swap 필요
            * [1, 2, ```1, 2```, **5, 6**]: 가 되었다. 끝에 도달했으니 stage 2는 끝이 난다.
        + stage 3: [1, 2, 1, **2, 5, 6**] 에서 목표는 2를 뒤로 밀어 넣는 것.
            * [```1, 2```, 1, **2, 5, 6**]
            * [1, ```2, 1```, **2, 5, 6**]: Swap 필요
            * [1, ```1, 2```, **2, 5, 6**]: 가 되었다. 끝에 도달했으니 stage 3은 끝이 난다.
        + stage 4: [1, 1, **2, 2, 5, 6**]: 에서 목표는 1을 가장 뒤에 두는 것.
            * [```1, 1```, **2, 2, 5, 6**]: Swap 필요 없고, 끝에 도달했으니 stage 4는 끝이 난다.
        + 끝!
- 아래 skeleton code를 사용해도 됩니다.
    ```python
    def bubble_sort(lst):
        for stage in range(0, len(lst)):
            # lst[0: len(lst) - stage] 의 범위 내의 최대값을, 
            # lst[len(lst) - stage - 1] 에 넣는 것이 목표.
            
            for j in range(0, ???):
                # j는 현재 window의 왼쪽 위치(index)를 의미한다.

                if lst[j] ? lst[j + 1]:
                    # Swap lst[j] and lst[j + 1]
                    ????
        return ???
    ```

## 6. Insertion sort 짜기
- input: unsorted list
- output: sorted list
- Insertion sort 설명
    - lst 의 앞 부분에 sorted array를 완성시켜나가는 방식이다. 원소 하나씩 하나씩 앞 부분에 넣어간다.
    - 예시) 
        + [5, 1, 2, 6, 2, 1, 3, 0] 가 주어졌다. 
        + round 0: lst[0: 0 + 1] 부분을 sorted array로 만드는 것이 목표.
            - [```5```, 1, 2, 5, 2, 1, 3, 0] 에서 ```5```는 sorted 완료. round 0 완료.
        + round 1: lst[0: 1 + 1] 부분을 sorted array로 만드는 것이 목표.
            - [```5```, **1**, 2, 5, 2, 1, 3, 0] 에서 **1**을 sorted array 안에 넣는다.
            - [```1, 5```, 2, 5, 2, 1, 3, 0] 이 된다. round 1 완료.
        + round 2: lst[0: 2 + 1] 부분을 sorted array로 만드는 것이 목표.
            - [```1, 5```, **2**, 5, 2, 1, 3, 0] 에서 **2** 를 sorted array 안에 넣는다.
            - [```1, 2, 5```, 5, 2, 1, 3, 0] 이 된다. round 2 완료.
        + round 3: lst[0: 3 + 1] 부분을 sorted array로 만드는 것이 목표.
            - [```1, 2, 5```, **5**, 2, 1, 3, 0] 에서
            - [```1, 2, 5, 5```, 2, 1, 3, 0] 가 된다.
        + round 4: lst[0: 4 + 1] 부분을 sorted array로 만드는 것이 목표.
            - [```1, 2, 5, 5```, **2**, 1, 3, 0] 에서
            - [```1, 2, 2, 5, 5```, 1, 3, 0] 가 된다.
        + round 5: lst[0: 5 + 1] 부분을 sorted array로 만드는 것이 목표.
            - [```1, 2, 2, 5, 5```, **1**, 3, 0] 에서
            - [```1, 1, 2, 2, 5, 5```, 3, 0] 가 된다.
        + round 6: lst[0: 6 + 1] 부분을 sorted array로 만드는 것이 목표.
            - [```1, 1, 2, 2, 5, 5```, **3**, 0] 에서
            - [```1, 1, 2, 2, 3, 5, 5```, 0] 가 된다.
        + round 7: lst[0: 7 + 1] 부분을 sorted array로 만드는 것이 목표.
            - [```1, 1, 2, 2, 3, 5, 5```, **0**] 에서
            - [```0, 1, 1, 2, 2, 3, 5, 5```] 가 된다.

아래 skeleton code를 사용해도 됩니다.
```python
def insertion_sort(lst):
    for rnd in range(0, len(lst)):
        # Current rnd (round) 에서는
        # - lst[0: rnd] 가 현재로서는 sorted array이고
        # - lst[0: rnd + 1] 을 sorted array로 만들 예정이다.
        
        # sorted array에 새로 insert 할 target
        target_to_put_in = lst[rnd]
        
        # target_to_put_in 을 lst[0: rnd] 안에 잘 넣는다.
        # target을 앞 원소부터 비교해가며, 삽입할 위치를 찾는다.
        for j in range(0, rnd):
            if lst[j] > target_to_put_in:
                ????
        
        # target_to_put_in 을 적절한 위치에 넣는다.
        ????
    
    return ???
```
