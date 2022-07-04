# Plagiarism-detector-in-programming-assignments-
Plagiarism detector ( in programming assignments )
## Use some AI to get the plagiarism between the files to get similarity answers

# Install requirements :
    pip install -U scikit-learn
    pip install os
    import os
    from sklearn.feature_extraction.text import TfidfVectorizer
    from sklearn.metrics.pairwise import cosine_similarity
    
# Code to get the files and read them :
    # Enter the path of files and the files extension(I use .java files)
    student_files = [doc for doc in os.listdir("../../..") if doc.endswith('.java')]
    student_notes =[open(File).read() for File in student_files]

# Use AI to prepare the files for measuring the palagrism detection :
    vectorize = lambda Text: TfidfVectorizer().fit_transform(Text).toarray()
    similarity = lambda doc1, doc2: cosine_similarity([doc1, doc2])
    #print(vectorize)
    vectors = vectorize(student_notes)
    s_vectors = list(zip(student_files, vectors))

# Define the Function to detect the plagiarism and Get the Allowed_similarity_ratio from supervisor :
    Allowed_similarity_ratio = input("Enter the allowed similarity ratio:")
    def check_plagiarism():
        plagiarism_results = set()
        global s_vectors
        for student_a, text_vector_a in s_vectors:
            new_vectors =s_vectors.copy()
            current_index = new_vectors.index((student_a, text_vector_a))
            del new_vectors[current_index]
            for student_b , text_vector_b in new_vectors:
                sim_score = (similarity(text_vector_a, text_vector_b)[0][1])*100
                if sim_score > eval(Allowed_similarity_ratio) :
                  student_pair = sorted((student_a, student_b))
                  score = (student_pair[0], student_pair[1],sim_score)
                  plagiarism_results.add(score)
        return plagiarism_results
    
    # To print similar answers and the plagiarism ratio between them
    for data in check_plagiarism():
        print(data)
        
#The complete code :

    pip install -U scikit-learn
    pip install os
    import os
    from sklearn.feature_extraction.text import TfidfVectorizer
    from sklearn.metrics.pairwise import cosine_similarity
    
    student_files = [doc for doc in os.listdir() if doc.endswith('.java')]
    student_notes =[open(File).read() for File in student_files]
    
    #print(student_files)
    #print(student_notes)
    
    vectorize = lambda Text: TfidfVectorizer().fit_transform(Text).toarray()
    similarity = lambda doc1, doc2: cosine_similarity([doc1, doc2])
    
    print(vectorize)
    
    vectors = vectorize(student_notes)
    s_vectors = list(zip(student_files, vectors))
    
    Allowed_similarity_ratio = input("Enter the allowed similarity ratio: ")
    
    def check_plagiarism():
        plagiarism_results = set()
        global s_vectors
        for student_a, text_vector_a in s_vectors:
            new_vectors =s_vectors.copy()
            current_index = new_vectors.index((student_a, text_vector_a))
            del new_vectors[current_index]
            for student_b , text_vector_b in new_vectors:
                sim_score = (similarity(text_vector_a, text_vector_b)[0][1])*100
                if sim_score > eval(Allowed_similarity_ratio) :
                  student_pair = sorted((student_a, student_b))
                  score = (student_pair[0], student_pair[1],sim_score)
                  plagiarism_results.add(score)
        return plagiarism_results

    for data in check_plagiarism():
        print(data)



   
