# Sequential-sentence-classification
Objective: Building Deep learning Model for Sequential Sentence Classification, for Converting “Harder to Read” text into “Easier to Read ” text.

<b>Dataset details: </b>

PubMed 20k RCT is dataset based on PubMed for sequential sentence classification. The dataset consists of approximately 20,000 abstracts of randomized controlled trials. Each sentence of each abstract is labelled with their role in the abstract using one of the following classes: background, objective, method, result, or conclusion. The purpose of releasing this dataset is twofold.  First, the majority of datasets for sequential short-text classification i.e., classification of short texts that appear in sequences. Second, from an application perspective, researchers need better tools to efficiently skim through the literature. Automatically classifying each sentence in an abstract would help researchers read abstracts more efficiently, especially in fields where abstracts may be long, such as the medical field
The dataset is taken from following link: https://github.com/Franck-Dernoncourt/pubmed-rct/tree/master/PubMed_20k_RCT_numbers_replaced_with_at_sign

Sample abstract:![image](https://github.com/user-attachments/assets/09e65f7f-4de9-4bcd-af48-6b8dd6991f6a)
![image](https://github.com/user-attachments/assets/8ba41605-e9b4-4f96-8836-1949cdf49082)

<b>Dataset Analysis</b>
Fig 1:  Distribution of sentences per abstract ![image](https://github.com/user-attachments/assets/8a659efe-8553-4db1-9e27-a077d056e041)

Fig 2:  Distribution of number of tokens in a sentence ![image](https://github.com/user-attachments/assets/8c5547e7-f77c-445b-bbda-e0ce804e7992)

Fig 3:  Distribution of character sequence lengths ![image](https://github.com/user-attachments/assets/6bfd7f53-a86b-41e9-9050-0886e9e5e5ed)

Table 1: Dataset overview 
![image](https://github.com/user-attachments/assets/d1ec1212-218c-479f-99f4-7a262546b37d)

Table 1 provides an overview of the dataset. The column labeled |V| represents the vocabulary size. In the context of the training, validation, and test sets, the details specify the number of abstracts, followed by the number of sentences in parentheses. For instance, 15k(80k) means there are 15,000 abstracts with a total of 80,000 sentences. This information is crucial for understanding the scope and scale of the dataset.Furthermore to understand the distribution of various features in the dataset, let us check distributions into more detail.

Fig 1 depicts the distribution of number of sentences per abstract. By looking at the distribution it can be inferred that most of the sentences in abstract have length in between 7 to 15 .
Fig 2 shows the distribution of number of tokens per sentence. On analyzing it was found the majority of the tokens are between 0 to 55 tokens in length. 
Fig 3 shows the  distribution of character sequence lengths. By checking the distribution it seems that the most of the sequences are between 0 to 200 characters long.

![image](https://github.com/user-attachments/assets/b609dad7-5427-409a-b74c-ddc471c12e33)

Fig 4 shows the number of sentences per label in train , test and validation sets. It can be observed that the least common label (objective) is nearly 4 times less frequent than the most commonly occurring label (results). This observation suggests that while there is some variability in label frequencies, the dataset does not exhibit an extreme imbalance.


<b>Performance Benchmarks</b>

Following experiments were performed on the PubMed 20k RCT dataset.
Naïve Bayes with TF-IDF encoder(baseline model)
Conv1D with token embedding
Pretrained feature extractor (using Universal Sentence Encoder)
Conv1D with character encoding

![image](https://github.com/user-attachments/assets/0a4fdb79-14f1-4bab-9d19-c1612a11e287)
Fig 5:  Bar chart comparison on validation set for model metrics for different models

The first baseline classifier (Naïve Bayes with TF-IDF encoder) uses the TfidfVectorizer class to convert abstract sentences to numbers using the TF-IDF (term frequency-inverse document frequency) algorithm and then learns to classify the sentences using the MultinomialNB aglorithm.

The second classifier(Conv1D with token embedding) consists of vectorizing text inputs ,turning them into numerical sequences using token embedding and then applying a 1D Convolution layer to create the required model. 

Vectorizing text input is like converting words into numbers so that a computer can understand and process them more easily. It's similar to creating a numerical representation of the words in a document.

The third classifier (pretrained feature extractor using USE) is similar to second classifier except that it uses pretrained embedding (Universal Sentence encoder from TFHub) which takes care of tokenization part which is then passed to convolution layer.

The fourth classifier( Conv1D with character embedding) consists of splitting  sequences into  character and creating feature vector for each character using TextVectorization and passing the resulting sequence into character embedding layer.

![image](https://github.com/user-attachments/assets/6225e116-badc-42fb-b0ac-a4de8f417b32)

Table 2: Model metrics for different models on  validation dataset  

Table 2 shows the model metrics for different models wrt validation dataset.  The baseline model(Naïve Bayes with TF-IDF encoder) performs poorly on validation set(f1 score :69.89 ). Based on the comparison across all metrics, the Conv1D model with token embedding consistently outperforms the baseline Naïve Bayes model and other models . This is evident by looking at the  bar chart figure 5  which compares model metrics of all different models and clearly Conv1D with token outperforms the rest. This conclusion is drawn considering the higher values in accuracy(82.45), precision(82.22), recall(82.45), and F1 score(82.15), indicating better overall performance in classification tasks.


![image](https://github.com/user-attachments/assets/56c5a984-bab8-489b-9aa3-3215b0228d3d)

Fig 6:  Bar chart comparison on test set for model metrics for different models

![image](https://github.com/user-attachments/assets/aca44bdc-13b1-4cd8-bf7c-bc30fdbd34de)

Table 3: Model metrics for different models on  test  dataset  

Table no 3 shows the model metrics for different models wrt test  dataset. The baseline model(Naïve Bayes with TF-IDF encoder) performs poorly on test set(f1 score :69.25 ) similar to its validation test result where f1 score was 69.89 .As we can see from the bar chart(fig 6),the other 3 models nearly similar on test set as compared to the results on the validation set.  Here also, the  Conv1D with token embedding outperforms the baseline as well as other models  and is evident on inspecting the accuracy, precision, recall and f1 score. So the conv1d is out best performing model on validation as well as test set.


