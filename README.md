# Sequential-sentence-classification
Building Deep learning Model for Sequential Sentence Classification, for Converting “Harder to Read” text into “Easier to Read ” text.

Dataset details: 
PubMed 20k RCT is dataset based on PubMed for sequential sentence classification. The dataset consists of approximately 20,000 abstracts of randomized controlled trials. Each sentence of each abstract is labelled with their role in the abstract using one of the following classes: background, objective, method, result, or conclusion. The purpose of releasing this dataset is twofold.  First, the majority of datasets for sequential short-text classification i.e., classification of short texts that appear in sequences. Second, from an application perspective, researchers need better tools to efficiently skim through the literature. Automatically classifying each sentence in an abstract would help researchers read abstracts more efficiently, especially in fields where abstracts may be long, such as the medical field
The dataset is taken from following link: https://github.com/Franck-Dernoncourt/pubmed-rct/tree/master/PubMed_20k_RCT_numbers_replaced_with_at_sign
Sample abstract:![image](https://github.com/user-attachments/assets/09e65f7f-4de9-4bcd-af48-6b8dd6991f6a)
![image](https://github.com/user-attachments/assets/8ba41605-e9b4-4f96-8836-1949cdf49082)

Dataset Analysis
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
![image](https://github.com/user-attachments/assets/6225e116-badc-42fb-b0ac-a4de8f417b32)

Table 2: Model metrics for different models on  validation dataset  

Table 2 shows the model metrics for different models wrt validation dataset.  The baseline model(Naïve Bayes with TF-IDF encoder) performs poorly on validation set(f1 score :69.89 ). Based on the comparison across all metrics, the Conv1D model with token embedding consistently outperforms the baseline Naïve Bayes model and other models . This is evident by looking at the  bar chart figure 5  which compares model metrics of all different models and clearly Conv1D with token outperforms the rest. This conclusion is drawn considering the higher values in accuracy(82.45), precision(82.22), recall(82.45), and F1 score(82.15), indicating better overall performance in classification tasks.

