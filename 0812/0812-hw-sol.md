## 1. 함수 연습
```python
def get_1st_alpha(word):
    return word[0]
```

## 2. dictionary 연습
```python
def classify_words(word_lst):
    # Initialize a word dictionary, whose
    #   - key: an alphabet
    #   - val: list of words starting from the key
    classifier = dict()

    for word in word_lst:
        alpahbet = word[0]
        if alpahbet not in classifier:
            classifier[alpahbet] = []
        classifier[alpahbet].append(word)

    # Retrun the dictionary
    return classifier
```

## 3. Palindrome
```python
def is_palindrome(word):
    alphabet_sequence = list(filter(str.isalpha, word.lower()))
    n = len(alphabet_sequence)
    
    for i, alphabet in enumerate(alphabet_sequence):

        # Check only half of the sequence
        if i == int(n / 2):
            break
        
        # Check if i-th word is matched with the last i-th word
        i_th_word = alphabet
        last_i_th_word = alphabet_sequence[n - i - 1]
        print(i_th_word, last_i_th_word)
        if i_th_word != last_i_th_word:
            return False
    return True
```

## 5. TF-IDF
```python
def tf_idf(input_path):

    '''
    Read documents
    '''
    
    f = open(input_path, 'r')
    documents = f.readlines()
    f.close()
    
    
    '''
    Parse documents (remove "\n" and "." in all document)
    '''
    
    for d, document in enumerate(documents):
        parsed_document = document.replace('\n', '').replace('.', '')
        documents[d] = parsed_document

        
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
        # word_freq_dict[w] = w가 document 안에서 나타난 횟수
        word_freq_dict = {}
        for w in words:
            if w not in word_freq_dict:
                word_freq_dict[w] = 0
            word_freq_dict[w] = word_freq_dict[w] + 1
        
        # Get max_freq_d
        max_freq_d = max(list(word_freq_dict.values()))
        
        # For all words, get tf(d, w) score, using word_freq_dict and max_freq_d
        # tf(d, w) = 0.5 + (0.5 * w가 d안에서 나타난 횟수) / (max_freq_d)
        for w in words:
            tf_dict[(d, w)] = 0.5 + (0.5 * word_freq_dict[w]) / max_freq_d
      

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
            if w not in document_count_dict:
                document_count_dict[w] = 0
            document_count_dict[w] = document_count_dict[w] + 1
    
    # Initialize idf_dict
    #  - key: w
    #  - val: idf(w)
    # idf(w) = log (N / w가 포함된 document의 개수)
    idf_dict = {}
    
    N = len(documents)
    for w in document_count_dict.keys():
        idf_dict[w] = np.log(N / document_count_dict[w])
        
        
    '''
    Get tf_idf score
    '''
    
    # Initialize tf_idf_dict
    #  - key: (d, w)
    #  - val: tf_idf(d, w) 
    # tf_idf(d, w) = tf(d, w) * idf(w)
    tf_idf_dict = {} 
    
    for d, w in tf_dict.keys():
        tf_idf_dict[(d, w)] = tf_dict[(d, w)] * idf_dict[w]
    
    return tf_idf_dict
```

```python
tf_idf_dict = tf_idf('./data/documents.txt')
print(tf_idf_dict)
```
실행 결과
```
{(0, 'I'): 0.719122666963206,
 (0, 'will'): 1.9237120180961527,
 (0, 'never'): 2.0604531856916184,
 (0, 'be'): 1.9237120180961527,
 (0, 'this'): 2.227810849177276,
    ...
 (77, 'reason'): 3.267531620017194,
 (77, 'for'): 1.619613187015029,
 (77, 'not'): 2.0604531856916184,
 (77, 'having'): 3.267531620017194,
 (77, 'time'): 2.4435724035161117,
 (77, 'join'): 3.267531620017194,
 (77, 'us'): 2.7476712345972345}
```