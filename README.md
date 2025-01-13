# SMS Spam Classifier Using Word2Vec and Random Forest

## 1.  Objective
The primary goal of this project is to develop a machine learning model that classifies SMS messages as either **Spam** or **Not Spam** (Ham). This is done using a **Word2Vec** representation for the text data and a **Random Forest Classifier** for model training.

## 2. Requirements
To run this project, you need to install the following Python libraries:
- `gensim`: For word vectorization using Word2Vec.
- `nltk`: For natural language processing tasks like tokenization, lemmatization, etc.
- `sklearn`: For machine learning tasks, such as splitting the dataset and training the model.
- `pandas`: For handling and analyzing the dataset.
- `tqdm`: For progress bars during model training.
- `numpy`: For numerical computations.

To install all dependencies, run:

```bash
pip install gensim nltk scikit-learn pandas tqdm numpy
```

## 3.  Dataset
The dataset used in this project is the SMSSpamCollection dataset, which contains a collection of SMS messages that are labeled as either "ham" (not spam) or "spam". It includes two columns:

* label: A binary label indicating whether the message is spam (spam) or not spam (ham).
* message: The content of the SMS message.
The dataset is stored in a .csv file (SMSSpamCollection), and it is used for both training and testing the spam classifier.

## 4. Project Workflow
###  Step 1: Data Preprocessing
* The first step in the project is data preprocessing:

* Cleaning the text: All non-alphabetic characters are removed using regular expressions.
  * Lowercasing: All the text is converted to lowercase for uniformity.
  * Tokenization: The text is split into individual words (tokens).
  * Lemmatization: Words are lemmatized to ensure that the base or root form of the word is used (e.g., "running" becomes "run").
  * Stopword Removal: Although not shown in the code, it's typically useful to remove common words (like "is", "the", etc.) that do not add much value to the meaning of the text.
  
### Step 2: Word2Vec Embedding
* The Word2Vec model is trained on the cleaned text data:

* Word2Vec converts each word in the dataset into a vector representation that captures its meaning.
* The word2vec-google-news-300 model from the gensim library is loaded, which provides pre-trained embeddings for words.
* A custom Word2Vec model is also trained on the processed data to generate embeddings for words not present in the pre-trained model.
  
###  Step 3: Vectorization
* Each message is represented as a vector by averaging the word vectors for all the words in the message. This produces a fixed-length vector for each message.
  * avg_word2vec: This function computes the average Word2Vec embedding for each message.
* Training Word2Vec from scratch: The Word2Vec model is trained on the tokenized messages to capture the semantic meaning of the words.
### Step 4: Model Training
* Once the data is processed and vectorized, the next step is to train the classifier:
  * Random Forest Classifier is used for training the model. Random Forest is an ensemble learning method that creates multiple decision trees and aggregates their predictions.
  * Train-test split: The dataset is split into training (80%) and testing (20%) datasets using train_test_split from the sklearn library.
    
### Step 5: Model Evaluation
* The trained model is evaluated using the following metrics:
  *Accuracy: Measures the proportion of correct predictions made by the model.
  *Classification Report: Provides additional performance metrics such as precision, recall, and F1-score for each class (Spam or Ham).
    ```python
        print(accuracy_score(y_test, y_pred))
        print(classification_report(y_test, y_pred))
    ```
### Step 6: Result Interpretation
* Accuracy: A measure of how often the classifier makes the correct prediction.
* Precision: Measures the ability of the classifier to correctly identify positive samples (spam) out of all the samples it predicted as positive.
* Recall: Measures the ability of the classifier to correctly identify all positive samples (spam) out of all actual positive samples.
* F1-Score: A weighted average of precision and recall, balancing the two metrics.
  * Code Breakdown
      ```python
        #Word2Vec Model Loading and Training
        import gensim
        from gensim.models import Word2Vec
        import gensim.downloader as api
        
        # Load pre-trained Word2Vec model
        wv = api.load('word2vec-google-news-300')
      

        # Train a custom Word2Vec model
        model = gensim.models.Word2Vec(words)
        Preprocessing of Messages
        python
        Copy code
        import re
        import nltk
        from nltk.stem import WordNetLemmatizer
        from nltk.tokenize import word_tokenize
        nltk.download('stopwords')
        nltk.download('punkt')

        lemmatizer = WordNetLemmatizer()
        
        # Preprocessing the messages
        corpus = []
        for message in messages['message']:
            review = re.sub('[^a-zA-Z]', ' ', message)
            review = review.lower()
            review = review.split()
            review = [lemmatizer.lemmatize(word) for word in review]
            review = ' '.join(review)
        corpus.append(review)
        Training and Evaluation
        python
        Copy code
        from sklearn.model_selection import train_test_split
        from sklearn.ensemble import RandomForestClassifier
        from sklearn.metrics import accuracy_score, classification_report
        
        # Split the dataset
        X_train, X_test, y_train, y_test = train_test_split(X_new, y, test_size=0.2)
        
        # Train the Random Forest Classifier
        classifier = RandomForestClassifier()
        classifier.fit(X_train, y_train)
        
        # Make predictions
        y_pred = classifier.predict(X_test)

        # Evaluate the model
        print(accuracy_score(y_test, y_pred))
        print(classification_report(y_test, y_pred))
      ```
      
### 6. Future Improvements
* Deep Learning: Use deep learning models like LSTM or CNNs for better accuracy in text classification.
* Hyperparameter Tuning: The model's hyperparameters (like the number of trees in the Random Forest) can be tuned to improve performance.
* Handling Imbalanced Data: If the dataset is imbalanced (more ham messages than spam), techniques like oversampling, undersampling, or using class weights in the classifier can be applied.
  
### 7. Conclusion
This project demonstrates the ability to classify SMS messages as spam or ham using Word2Vec embeddings for text representation and a Random Forest classifier for the prediction task. The model performs well in distinguishing between spam and non-spam messages, but there is potential for further improvements using deep learning models.
* Deep Learning: Use deep learning models like LSTM or CNNs for better accuracy in text classification.
* Hyperparameter Tuning: The model's hyperparameters (like the number of trees in the Random Forest) can be tuned to improve performance.
* Handling Imbalanced Data: If the dataset is imbalanced (more ham messages than spam), techniques like oversampling, undersampling, or using class weights in the classifier can be applied.
### 8. Conclusion
* This project demonstrates the ability to classify SMS messages as spam or ham using Word2Vec embeddings for text representation and a Random Forest classifier for the prediction task. 
* The model performs well in distinguishing between spam and non-spam messages, but there is potential for further improvements using deep learning models.


