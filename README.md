# Sequential-sentence-classification
<b> Objective</b>: Building Deep learning Model for Sequential Sentence Classification, for Converting “Harder to Read” text into “Easier to Read ” text.

<b>Dataset details: </b>

PubMed 20k RCT is dataset based on PubMed for sequential sentence classification. The dataset consists of approximately 20,000 abstracts of randomized controlled trials. Each sentence of each abstract is labelled with their role in the abstract using one of the following classes: background, objective, method, result, or conclusion. The purpose of releasing this dataset is twofold.  First, the majority of datasets for sequential short-text classification i.e., classification of short texts that appear in sequences. Second, from an application perspective, researchers need better tools to efficiently skim through the literature. Automatically classifying each sentence in an abstract would help researchers read abstracts more efficiently, especially in fields where abstracts may be long, such as the medical field
The dataset is taken from following link: https://github.com/Franck-Dernoncourt/pubmed-rct/tree/master/PubMed_20k_RCT_numbers_replaced_with_at_sign

Sample abstract:![image](https://github.com/user-attachments/assets/09e65f7f-4de9-4bcd-af48-6b8dd6991f6a)
![image](https://github.com/user-attachments/assets/8ba41605-e9b4-4f96-8836-1949cdf49082)

<b>Dataset Analysis</b>

Fig 1:  Distribution of sentences per abstract ![image](https://github.com/user-attachments/assets/8a659efe-8553-4db1-9e27-a077d056e041)

Fig 2:  Distribution of number of tokens in a sentence ![image](https://github.com/user-attachments/assets/8c5547e7-f77c-445b-bbda-e0ce804e7992)

Fig 3:  Distribution of character sequence lengths

![image](https://github.com/user-attachments/assets/6bfd7f53-a86b-41e9-9050-0886e9e5e5ed)

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
1. Naïve Bayes with TF-IDF encoder(baseline model)
2. Conv1D with token embedding
3. Pretrained feature extractor (using Universal Sentence Encoder)
4. Conv1D with character encoding

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

![image](https://github.com/user-attachments/assets/fe8cf090-b1dc-4d72-ad35-18d19a15875b) 

Fig 7:  F1 score comparison on validation set for different models 

![image](https://github.com/user-attachments/assets/5152a678-4ca6-4c91-9e4c-ea2807964a7f)

Fig 8:  F1 score comparison on test set for different models

Figure 7 and 8 show the comparison of the f1 score on validation and  test set for different classifier models sorted based on their f1 scores .The conv1d  with token embedding model has the highest f1 score among all the models and it outperforms other models by quite a good margin on both validation and test sets. A high F1 score indicates both high precision and high recall, suggesting that a model that makes accurate positive predictions and captures a large portion of actual positive instances. On comparing our best performing model to that of   PubMed 200k RCT: a Dataset for Sequential Sentence Classification in Medical Abstracts paper , the conv1d with token embedding model underperforms ( the paper’s model f1 score was around 90% as compared to our models 81.8%). As there was currently no metrics published for PubMed20K RCT dataset so the comparison has been made with the PubMed200K dataset

![image](https://github.com/user-attachments/assets/7b6c65c9-4dd6-4d4d-9ae6-81d7fe65370e)
Fig 9: Confusion matrix for best performing model(conv1d with token embedding)


![image](https://github.com/user-attachments/assets/91f4e6b7-6c92-442c-8bf4-11de55df8f7c)

Table 4:  Classification metrics for Conv1d with token embedding model

So lets check more into our best performing model(conv1d with token embedding) by inspecting the classification metrics( Table 4) and Confusion matrix(Fig 9).
On inspecting the classification metrics table carefully, we can infer below observations:
Examining the model's f1-score reveals its proficiency in discerning abstract lines associated with Conclusions, Methods, and Results. However, the model encounters challenges in distinguishing between lines categorized as Background or Objective. This difficulty may stem from the comparatively lower number of samples available for these two classes in comparison to others.
An additional factor contributing to this challenge is the potential similarity in embeddings for abstract texts from these two classes. This similarity could be attributed to the encoder generating embeddings that are too alike, prompting consideration for trying an alternative encoder or transformer. Alternatively, misclassification during dataset creation or the presence of noise within the texts might be influencing the model's difficulty in accurately classifying these instances, potentially indicating bias.
The confusion matrix also reveals more or less a similar inference to that of classification metrics. Rows show actual labels and columns show predicted labels. Our model is confused between Background and objective classes (343 background sentences classified as objective and 777 objective sentences classified as background). Similar behavior is also noticed with the Methods and Results classes, and this consistency might be attributed to the factors discussed above in the examination of classification metrics.


![image](https://github.com/user-attachments/assets/cdbe8551-7966-48a4-9348-50d7d7b0dc1a)

Fig 10: Most 50 Inaccurate predictions 

In order to understand the model performance better, let us check the part which gives information regarding the most inaccurate predictions given by our model which will help us to gauge to understand the scenarios in which the  model is not able to make a prediction correctly.

Fig 10 shows the details regarding the top 50 inaccurate predictions given by our model. It can be observed that the model encounters difficulties when making predictions on instances at the edges of the data spectrum. This challenge might stem from inherent biases within the model or characteristics of the dataset, such as insufficient samples or imbalances in class distribution. Addressing this issue would involve strategies such as increasing the training dataset size, exploring alternative encoders or transformers, and considering the application of cross-validation techniques during model training.

<b>Conclusion </b>

1. Conv1D model with token embedding is the best performing model on validation as well as test dataset 

2. The model encounters challenges arise when distinguishing between lines categorized as Background or Objective, possibly due to a lower number of available samples for these classes and potential embedding similarities. This similarity issue prompts consideration for alternative encoders or transformers to enhance model performance.

3. The confusion matrix aligns with these findings, revealing notable confusion between Background and Objective classes, as well as consistent behavior in the Methods and Results classes. This reinforces the challenges faced by the model in certain classifications.





