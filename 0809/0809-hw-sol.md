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
    if max_val < v: 
        # v should be the new maximum value
        max_val = v

print(max_val)
```
출력 결과
```
6
```

## 2. List 연습 2
- list 내 최대값을 갖는 원소가 몇 개인지 구해보세요.
- `lst = [2, 3, 6, 2, -1, 0, 6, 2, 3]` 이 주어져 있을 때, 최대값인 6은 2개 있습니다. 여기서 6의 개수인 2를 출력해 보세요.
- 이 때 다음과 같은 포맷으로 출력해 보세요: 'max = 6, num_max = 2'.

```python
# Target list
lst = [2, 3, 6, 2, -1, 0, 6, 2, 3]

# Get the maximum values
max_val = max(lst)

# Count how many max_val are there in lst
num_max_val = 0
for v in lst:
    if v == max_val:
        num_max_val = num_max_val + 1
        
print('max = {}, num_max = {}'.format(max_val, num_max_val))
```
출력 결과
```
max = 6, num_max = 2
```

## 3. Dictionary 연습 1
- word_freqs 함수를 구현해 보세요.
    - **input**: 어떤 string. string 내 각 단어는 space로 구분되어 있음.
    - **output**: 어떤 dictionary. 이 때 key는 input내 각 단어를 말하고 value는 key 의 등장 횟수(frequency) 를 말함.
- sol
    ```python
    def word_freqs(sentence):
        words = sentence.split(' ')
        freqs = {}

        for word in words:
            if word not in freqs:
                freqs[word] = 0
            freqs[word] += 1

        return freqs

    s = "I am a boy you are a girl"
    freq_dict = word_freqs(s)
    print(freq_dict)
    ```
    출력 결과
    ```
    {'girl': 1, 'a': 2, 'you': 1, 'are': 1, 'I': 1, 'boy': 1, 'am': 1}
    ```
    
## 4. Dictionary 연습 2
- 단어들을 시작 알파벳별로 분류하는 함수를 만들어 보자.
- **함수 이름**: classify_words
- **input**: 단어(string)들의 list
- **output**: 어떤 dictionary
    - key: 어떤 알파벳
    - val: input 내의 단어들 중 key로 시작하는 것들을 모은 list
- sol
    ```python
    def classify_words(word_lst):
        classifier = {}
        for word in word_lst:
            fst_alphabet = word[0]
            if fst_alphabet not in classifier:
                classifier[fst_alphabet] = []
            classifier[fst_alphabet].append(word)
        return classifier

    word_lst = ["apple", "bear", "person", "aurora", "print", "boy"]
    classifier = classify_words(word_lst)
    print(classifier)
    ```
    출력 결과 (dictionary 내의 key나 value의 순서는 달라도 됨.)
    ```
    {'p': ['print', 'person'], 'a': ['apple', 'aurora'], 'b': ['bear', 'boy']}
    ```
    
## 5. Bubble sort
- 숫자들을 오름차순으로 정렬하는 (즉, sorting 하는) 알고리즘중 하나인 Bubble sort를 구현해 보자.
- **input**: unsorted list
- **output**: sorted list
- sol
    ```python
    def bubble_sort(lst):
        for stage in range(0, len(lst)):
            # lst[0: len(lst) - stage] 의 범위 내의 최대값을, 
            # lst[len(lst) - stage - 1] 에 넣는 것이 목표.

            for j in range(0, len(lst) - stage - 1):
                # j는 현재 window의 왼쪽 위치(index)를 의미한다.

                if lst[j] > lst[j + 1]:
                    # Swap lst[j] and lst[j + 1]
                    lst_j = lst[j]
                    lst[j] = lst[j + 1]
                    lst[j + 1] = lst_j
        return lst

    lst = [2, 3, 6, 2, -1, 0, 6, 2, 3]
    sorted_lst = bubble_sort(lst)
    print(sorted_lst)
    ```
    출력 결과
    ```
    [-1, 0, 2, 2, 2, 3, 3, 6, 6]
    ```

## 6. Insertion sort 짜기
- input: unsorted list
- output: sorted list
- sol
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

                # 삽입할 위치 확인 시
                if lst[j] > target_to_put_in:

                    # lst[j: rnd]를 한 칸씩 오른쪽으로 밀기
                    for k in range(rnd, j, -1):
                        lst[k] = lst[k - 1]

                    # 마지막으로 lst[j]에 target_to_put_in을 넣기
                    lst[j] = target_to_put_in

                    # 이번 라운드는 끝!
                    break

        return lst

    lst = [2, 3, 6, 2, -1, 0, 6, 2, 3]
    sorted_lst = insertion_sort(lst)
    print(sorted_lst)
    ```
    출력 결과
    ```
    [-1, 0, 2, 2, 2, 3, 3, 6, 6]
    ```

