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

## 4. 함수 연습
```python
def get_ranks(scores):
    ranks = []
    for score in scores:
        rank = 1
        for score_cmp in scores:
            if score < score_cmp:
                rank = rank + 1
        ranks.append(rank)
    return ranks 
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

## 6. k-means clustering
```python
import numpy as np

def kmeans(data, k):
    '''
    k-means clustering
    * input
        - data: the data points(vectors), np.array
        - k: the number of clusters
    * output
        - clusters: a dictionary, whose
            - key: center index
            - val: a list of data indices that belong to the cluster of the center (key)
    '''
    
    # Randomly pick k cluster centers
    centers = np.random.randint(0, len(data), k)
    
    # k-means iteration
    while True:
        
        # Clustering the data based on centers
        clusters = get_cluster(data, centers)

        # Get new centers
        new_centers = get_new_centers(clusters)

        # Check if all of the centers stay the same
        is_converged = centers_stayed(centers, new_centers)
        if is_converged:
            break
            
        # Update the center
        centers = new_centers[:]
        
    clusters = get_cluster(data, centers)
    return clusters
    
    
def centers_stayed(centers, new_centers):
    '''
    If all points in centers and new_centers are the same, return True
    The order of points in centers and new_centers could be different.
    '''
    
    for c in centers:
        if c not in new_centers:
            return False
        
    return True


def get_cluster(data, centers):
    '''
    Clusters the data for given centers
    * input
        - data: the data points(vectors), np.array
        - centers: list of centers(indices)
    * output
        - clusters: a dictionary, whose
            - key: center index
            - val: a list of data indices that belong to the cluster of the center (key)
    '''

    # Initialize clusters
    # clusters is a dictionary, whose
    #   - key: a center index
    #   - val: initially an empty list, but this will be 
    #          a list of data indices that belong to the cluster of the center index (key)
    clusters = {}
    for c in centers:
        clusters[c] = []
    
    # For every data point, map the data into one of the center point
    for data_idx, data_point in enumerate(data):
        
        center_for_this_data = 0
        dist_bw_d_center = 100000
        
        # Find out the center that has the minimum distance with the current data
        for center in centers:
            center_point = data[center]            
            square_distance = np.sum((data_point - center_point) ** 2)

            if square_distance < dist_bw_d_center:
                center_for_this_data = center
                dist_bw_d_center = square_distance
                
        clusters[center_for_this_data].append(data_idx)
    
    return clusters
    

def get_new_centers(clusters):
    '''
    Get new centers in every clusters
    * input
        - clusters: a dictionary, whose
            - key: center index
            - val: a list of data indices that belong to the cluster of the center (key)
    * output
        - new_centers: list of centers(indices)
    '''
    
    # Initialize new_centers
    new_centers = []
    
    # For every cluster, get cluster center
    for member_in_cluster in clusters.values():

        min_sum_distance = 100000
        center_of_cluster = 0

        # Get a new center (center_of_cluster) in this cluster
        for potential_center in member_in_cluster:

            # Calculate the sum of distance
            # between the potential center and other members in the clusters
            sum_distance = 0
            
            for other_member in member_in_cluster:
                
                # Get vectors of center point and the other member
                center_point = data[potential_center]
                member_point = data[other_member]
                
                # Get distance and add up into sum_distance
                distance = np.sum((center_point - member_point) ** 2)
                sum_distance = sum_distance + distance

            # If found out a better center, 
            # update min_sum_distance and center_of_cluster
            if sum_distance < min_sum_distance:
                center_of_cluster = potential_center
                min_sum_distance = sum_distance

        # Add the new center (center_of_cluster) to new_centers
        new_centers.append(center_of_cluster)
        
    return new_centers
    
data = np.array([[1, 2], [2, 3], [4, 1], [1, 2], [6, 6], [8, 1], [-9, -10], [-2, -3], [-2, -9], [-1, -3], [-2, -5], [-9, -3]])
clusters = kmeans(data, 2)
print(clusters)
```
출력 결과
```
{10: [6, 7, 8, 9, 10, 11], 2: [0, 1, 2, 3, 4, 5]}
```