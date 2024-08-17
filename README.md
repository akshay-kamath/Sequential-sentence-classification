# Sequential Sentence Classification

**Objective**: Building a Deep Learning Model for Sequential Sentence Classification, to convert “Harder to Read” text into “Easier to Read” text.

## Dataset Details

The [PubMed 20k RCT dataset](https://github.com/Franck-Dernoncourt/pubmed-rct/tree/master/PubMed_20k_RCT_numbers_replaced_with_at_sign) is based on PubMed for sequential sentence classification. The dataset consists of approximately 20,000 abstracts of randomized controlled trials. Each sentence of each abstract is labeled with its role in the abstract using one of the following classes: background, objective, method, result, or conclusion. This dataset aims to enhance tools for efficiently skimming through literature, particularly in the medical field.

### Sample Abstracts
![Sample Abstract 1](https://github.com/user-attachments/assets/09e65f7f-4de9-4bcd-af48-6b8dd6991f6a)
![Sample Abstract 2](https://github.com/user-attachments/assets/8ba41605-e9b4-4f96-8836-1949cdf49082)

## Dataset Analysis

### Fig 1: Distribution of Sentences per Abstract
![Distribution of Sentences](https://github.com/user-attachments/assets/8a659efe-8553-4db1-9e27-a077d056e041)

### Fig 2: Distribution of Number of Tokens in a Sentence
![Distribution of Tokens](https://github.com/user-attachments/assets/8c5547e7-f77c-445b-bbda-e0ce804e7992)

### Fig 3: Distribution of Character Sequence Lengths
![Distribution of Character Lengths](https://github.com/user-attachments/assets/6bfd7f53-a86b-41e9-9050-0886e9e5e5ed)

### Table 1: Dataset Overview
![Dataset Overview](https://github.com/user-attachments/assets/d1ec1212-218c-479f-99f4-7a262546b37d)

- **|V|** represents the vocabulary size.
- The training, validation, and test sets are detailed with the number of abstracts and sentences.

**Distribution Insights**:
- **Fig 1**: Most abstracts have between 7 to 15 sentences.
- **Fig 2**: Majority of tokens per sentence range between 0 to 55.
- **Fig 3**: Most character sequences are between 0 to 200 characters long.

### Fig 4: Number of Sentences per Label in Train, Test, and Validation Sets
![Sentences per Label](https://github.com/user-attachments/assets/b609dad7-5427-409a-b74c-ddc471c12e33)

## Performance Benchmarks

### Experiments Conducted:
1. Naïve Bayes with TF-IDF Encoder (Baseline Model)
2. Conv1D with Token Embedding
3. Pretrained Feature Extractor (Using Universal Sentence Encoder)
4. Conv1D with Character Encoding

### Fig 5: Bar Chart Comparison on Validation Set for Model Metrics
![Validation Set Metrics](https://github.com/user-attachments/assets/0a4fdb79-14f1-4bab-9d19-c1612a11e287)

- **Naïve Bayes with TF-IDF Encoder**: Uses TF-IDF to convert sentences to numbers and MultinomialNB for classification.
- **Conv1D with Token Embedding**: Converts text inputs into numerical sequences using token embedding and applies a 1D Convolution layer.
- **Pretrained Feature Extractor (USE)**: Uses Universal Sentence Encoder for tokenization and convolution layer.
- **Conv1D with Character Encoding**: Splits sequences into characters, creates feature vectors for each character, and applies character embedding layer.

### Table 2: Model Metrics for Different Models on Validation Dataset
![Validation Metrics Table](https://github.com/user-attachments/assets/6225e116-badc-42fb-b0ac-a4de8f417b32)

- **Conv1D with Token Embedding** consistently outperforms other models with higher accuracy (82.45), precision (82.22), recall (82.45), and F1 score (82.15).

### Fig 6: Bar Chart Comparison on Test Set for Model Metrics
![Test Set Metrics](https://github.com/user-attachments/assets/56c5a984-bab8-489b-9aa3-3215b0228d3d)

### Table 3: Model Metrics for Different Models on Test Dataset
![Test Metrics Table](https://github.com/user-attachments/assets/aca44bdc-13b1-4cd8-bf7c-bc30fdbd34de)

- **Conv1D with Token Embedding** is the top performer in the test set as well.

### Fig 7: F1 Score Comparison on Validation Set for Different Models
![Validation F1 Score](https://github.com/user-attachments/assets/fe8cf090-b1dc-4d72-ad35-18d19a15875b)

### Fig 8: F1 Score Comparison on Test Set for Different Models
![Test F1 Score](https://github.com/user-attachments/assets/5152a678-4ca6-4c91-9e4c-ea2807964a7f)

- **Conv1D with Token Embedding** shows the highest F1 score, indicating strong performance in both validation and test sets.

### Fig 9: Confusion Matrix for Best Performing Model (Conv1D with Token Embedding)
![Confusion Matrix](https://github.com/user-attachments/assets/7b6c65c9-4dd6-4d4d-9ae6-81d7fe65370e)

### Table 4: Classification Metrics for Conv1D with Token Embedding Model
![Classification Metrics](https://github.com/user-attachments/assets/91f4e6b7-6c92-442c-8bf4-11de55df8f7c)

**Observations**:
- The model excels in classifying Conclusions, Methods, and Results.
- Challenges in distinguishing Background and Objective may be due to fewer samples and potential similarities in embeddings.

### Fig 10: Most 50 Inaccurate Predictions
![Inaccurate Predictions](https://github.com/user-attachments/assets/cdbe8551-7966-48a4-9348-50d7d7b0dc1a)

- **Top 50 Inaccurate Predictions**: Highlights instances where the model struggles, potentially due to dataset biases or sample imbalances.

## Conclusion

1. **Conv1D with Token Embedding** is the best-performing model on both validation and test datasets.
2. Challenges include distinguishing Background and Objective categories, potentially due to sample size and embedding similarities.
3. The confusion matrix supports these findings, with notable confusion between Background and Objective classes, and consistent behavior in Methods and Results classes.

Feel free to explore the provided figures and tables for more detailed insights into the model performance and dataset characteristics.
