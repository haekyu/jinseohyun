## 1. 함수 연습
- 어떤 단어의 시작 알파벳 구하기.
- **함수 이름**: get_1st_alpha
- **input**: 어떤 string 한 개
- **output**: input의 가장 앞 알파벳
- 예) 
    ```python
    word = "apple"
    alpha = get_1st_alpha(word)
    print(alpha)
    ```
    출력 결과
    ```
    a
    ```

## 2. dictionary 연습
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

## 3. Palindrome
- Palindrome을 판단하는 **함수**를 만들어 보세요.
    - **input**: 어떤 string
    - **output**: input이 palindrome인지 아닌지 (True or False)
- Palindrome이란?
    - 앞에서부터 읽으나 뒤에서부터 읽으나 동일한 단어나 구를 말합니다.
    - 예) "소주만병만주소", "noon", "Wow", "My gym", "No lemon, no melon"
    - 규칙
        - 대소문자 구분하지 않음
        - 띄어쓰기, 쉼표 등 알파벳이 아닌 문자는 무시
        - 영어 단어만 있다고 가정
- **힌트 1)** 대소문자 구분하지 않기
    - 대소문자 구분하지 않는 방법 중 하나는 모든 문자를 대문자로 만들거나 모든 문자를 소문자로 만드는 것입니다.
    - lower() 함수나 upper() 함수를 사용해보세요. lower()는 어떤 스트링의 모든 문자를 소문자로 만드는 함수입니다. upper()는 모든 문자를 대문자로 만드는 함수입니다.
    - lower() 함수 예시
        ```python
        s = "No lemon, no melon"
        ss = s.lower()
        print(ss)
        ```
        출력 결과
        ```
        'no lemon, no melon'
        ```
- **힌트 2)** 알파벳만 걸러내기
    - 어떤 string의 알파벳만 filtering 하는 기능을 사용해 봅시다. 
    - filter() 함수를 사용합니다.
        - filter(input1, input2) 는 두 개의 input을 받습니다.
            - input1: 필터 (== 함수)
            - input2: 필터링 될 대상 (== sequence, 가령 string이나 list 등)
        - filter(f, seq) 는 seq안의 원소 각각을 f 라는 필터로 거릅니다. 이 때 f(원소) 가 True인 원소는 남기고, f(원소)가 False 인 원소는 다 버립니다.
        - filter 예시 1)
            ```python
            # 짝수인지 아닌지를 리턴하는 함수
            def is_even(n):
                if n % 2 == 0:
                    return True
                else:
                    return False

            filtered_evens = list(filter(is_even, [1, 2, 3, 4, 5]))
            print(filtered_evens)
            ```
            출력 결과 
            ```
            [2, 4]
            ```
        - filter 예시 2)
            ```python
            ss = 'no lemon, no melon'
            filtered_alphas = list(filter(str.isalpha, ss))
            print(filtered_alphas)
            ```
            출력 결과
            ```
            ['n', 'o', 'l', 'e', 'm', 'o', 'n', 'n', 'o', 'm', 'e', 'l', 'o', 'n']
            ```

## 4. 함수 연습
- rank 함수를 구현해 보세요.
    - **input**: 두 개의 list를 인풋으로 받습니다.
        - names: 학생들의 이름을 보관하는 리스트입니다.
        - scores: 각 학생들의 점수를 보관하는 리스트입니다. 모두 숫자입니다.
    - **output**: 
        - 각 학생들의 등수를 순서대로 보관하는 리스트를 리턴합시다.
- 예) 우리가 구현하는 함수를 get_ranks 라고 가정.
    ```python
    name_lst = ['이', '얼', '산', '쓰', '우']
    score_lst = [30, 42, 51, 18, 23]

    ranks = get_ranks(name_lst, score_lst)

    for name, score, rank in zip(name_lst, score_lst, ranks):
        print('{}번째 학생: 이름={}, 점수={}, 등수={}등'.format(name, score, rank))
    ```
    출력 결과
    ```
    0번째 학생: 이름=이, 점수=30, 등수=3등
    1번째 학생: 이름=얼, 점수=42, 등수=2등
    2번째 학생: 이름=산, 점수=51, 등수=1등
    3번째 학생: 이름=쓰, 점수=18, 등수=5등
    4번째 학생: 이름=우, 점수=23, 등수=4등
    ```
    
- 힌트) 학생 A의 등수는 "A의 점수보다 높은 다른 사람들의 명 수 + 1" 이 됩니다.


## 5. TF-IDF
- TF-IDF 설명
    - TF-IDF는 documents들이 주어져있을 때, 어떤 단어가 어떤 document 내에서 얼마나 중요한지를 나타내는 score입니다.
    - TF(단어 빈도, term frequency)는 특정한 단어가 특정 문서 내에 얼마나 자주 등장하는지를 나타내는 값입니다. 이 값이 높을 수록 해당 특정 단어가 그 문서에서 중요하다고 생각할 수 있습니다.
    - DF(문서 빈도, document frequency)는 특정 단어가 몇 개의 문서 내에 등장하는지를 나타내는 값입니다. 이 값이 높을 수록 그 단어의 중요도는 떨어집니다. (개나소나 아무 문서에나 등장하는 단어라면 그 단어는 중요하지 않음)
    - IDF(역문서 빈도, inverse document frequency)는 1/DF 로 계산합니다. 이 값이 높을 수록 단어의 중요도는 증가합니다.
    - TF-IDF는 TF와 IDF를 곱한 값으로, 이 점수가 높은 단어일수록 다른 문서에는 많지 않고 해당 문서에서 자주 등장하는 단어를 의미한다. 즉 해당 문서에서 그 단어가 얼마나 중요한지를 나타냅니다.
    - 참고: https://en.wikipedia.org/wiki/Tf–idf
    - TF 는 다음과 같이 계산됩니다.
        - w: word, d: document id 라고 가정합니다.
        - max_freq_d 는 d 안에 있는 모든 단어들에 대해, 가능한 최대 단어 빈도수를 나타냅니다.
            - 예)
                ```
                document = "A B C C C D" 일 때, 

                A 의 빈도수 = 1
                B 의 빈도수 = 1
                C 의 빈도수 = 3
                D 의 빈도수 = 1
                
                이므로 max_freq_d는 3이 됩니다.
                ```
        - tf(d, w) = 0.5 + (0.5 \* w가 d안에서 나타난 횟수) / (max_freq_d)
    - IDF 는 다음과 같이 계산됩니다.
        - N: document의 총 개수
        - idf(w) = log (N / w가 포함된 document의 개수)
    - TF-IDF 는 다음과 같이 계산됩니다.
        - tf_idf(d, w) = tf(d, w) * idf(w)
- tf_idf 함수를 구현해 보세요.
    - **input**: 
        - input_path: documents 를 나타내는 파일 경로
            - documents들은 하나의 txt파일로 주어집니다.
            - 이 txt파일에서 여러 문장들이 newline ('\n') 을 기준으로 구분됩니다.
            - 하나의 문장을 하나의 document라고 생각해봅시다.
    - **output**:
        - tf_idf_dict: 모든 단어의 tf_idf score를 저장한 딕셔너리
            - key: 
                - (d, w) pair (tuple 로 구현)
                - d: document의 id
                - w: 단어
            - val: d 내의 w의 tf_idf score
            - 예) 
                다음과 같이 3개의 documents가 존재한다고 해봅시다.
                여기서 각 document는 0, 1, 2로 표현됩니다.
                d=1이면 그 document는 "We need to rent a room for our party." 입니다.
                ```
                I will never be this young again. Ever. Oh damn I just got older.
                We need to rent a room for our party.
                I want more detailed information.
                ```
                여기서 `tf_idf_dict[(1, 'need')]` 는 "We need to rent a room for our party." 내에서 "need" 의 tf_idf score를 나타냅니다.
- 다음과 같은 뼈대코드를 사용하셔도 됩니다.
```python
def tf_idf(input_path):

    '''
    Read documents
    '''
    
    f = ???
    documents = f.readlines()
    f.close()
    
    
    '''
    Parse documents (remove "\n" and "." in all document)
    '''
    
    for d, document in enumerate(documents):
        parsed_document = document.replace('\n', '').replace('.', '')
        documents[d] = ???

        
    '''
    Get tf score
    '''

    # Initialize tf_dict
    #  - key: (d, w)
    #  - val: tf(d, w)
    tf_dict = {} 
    
    # Get tf scores
    for d, document in enumerate(documents):
        
        # Get all words in document
        words = document.split(' ')
        
        # For all words, get frequency of words
        '''
        word_freq_dict 의 예시
        document = "A B C C C D" 일 때, 
        word_freq_dict["A"] = 1
        word_freq_dict["B"] = 1
        word_freq_dict["C"] = 3
        word_freq_dict["D"] = 1
        '''
        word_freq_dict = {}
        ???
        
        # Get max_freq_d 
        max_freq_d = 0
        ????
        
        # For all words, get tf(d, w) score, using word_freq_dict and max_freq_d
        # tf(d, w) = 0.5 + (0.5 \* w가 d안에서 나타난 횟수) / (max_freq_d)
        for w in words:
            tf_dict[(d, w)] = ???
      

    '''
    Get idf score
    '''
    
    # Initialize document_count_dict
    #  - key: w
    #  - val: w가 포함된 document의 개수
    document_count_dict = {}
    
    for d, document in enumerate(documents):
        
        # Get all words in document
        words = document.split(' ')
        
        # Get document_count_dict
        for w in words:
            ???
    
    # Initialize idf_dict
    #  - key: w
    #  - val: idf(w)
    idf_dict = {}
    
    for w in document_count_dict.keys():
        idf_dict[w] = ????
        
        
    '''
    Get tf_idf score
    '''
    
    # Initialize tf_idf_dict
    #  - key: (d, w)
    #  - val: tf_idf(d, w)
    tf_idf_dict = {} 
    
    for d, w in tf_dict.keys():
        ???
    
    return tf_idf_dict
```
