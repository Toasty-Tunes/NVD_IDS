# NVD Dataset link from 2021-2025
https://drive.google.com/drive/folders/15eHfWNd9Li8Gb55iETe5YZ9a2iUc8j4y?usp=sharing

# CVE Severity Prediction using Machine Learning and NLP

## 1. Introduction

This project aims to predict the severity of software vulnerabilities (CVEs) using a combination of natural language processing and machine learning techniques. The system leverages vulnerability descriptions along with structured CVSS metrics from the National Vulnerability Database (NVD) to classify vulnerabilities into severity categories.

The objective is to automate vulnerability assessment and assist security analysts in prioritizing risks effectively.

---

## 2. Dataset

The dataset consists of CVE records collected from NVD JSON feeds for the years 2021 to 2025.

- Total records: 152,551  
- Source: National Vulnerability Database (NVD)  

### Features Used:
- Description (text)
- Attack Vector
- Attack Complexity
- Privileges Required
- User Interaction
- Scope
- Base Score  

### Labeling Strategy:
- High severity: baseScore ≥ 7  
- Low severity: baseScore < 7  

---

## 3. Methodology

### 3.1 Data Extraction and Preprocessing

- JSON files were parsed to extract relevant fields  
- Missing or malformed entries were skipped  
- Data was stored in a structured DataFrame  
- Categorical features were encoded using Label Encoding  

---

### 3.2 Feature Engineering

#### Text Features (BERT Embeddings)

- Pretrained model: `bert-base-uncased`  
- Vulnerability descriptions were converted into embeddings  
- Mean pooling was applied to obtain fixed-length vectors  

#### Structured Features

- CVSS attributes were numerically encoded  

#### Feature Combination

- BERT embeddings were concatenated with CVSS features  
- This created a hybrid feature vector combining semantic and structured data  

---

### 3.3 Model Training

- Model: Random Forest Classifier  
- Number of estimators: 200  
- Train-test split: 80:20  
- Random state: 42  

The model was trained on the combined feature set.

---

## 4. Workflow

1. Load NVD JSON datasets (2021–2025)  
2. Extract CVE descriptions and CVSS metrics  
3. Clean and preprocess the data  
4. Encode categorical features  
5. Generate BERT embeddings  
6. Combine text and structured features  
7. Split data into training and testing sets  
8. Train Random Forest classifier  
9. Evaluate model performance  

---

## 5. Results

### 5.1 Model Performance

- Accuracy: **82.22%**

---

### 5.2 Classification Report

| Class | Precision | Recall | F1-score |
|------|----------|--------|----------|
| Low Severity (0) | 0.82 | 0.85 | 0.83 |
| High Severity (1) | 0.82 | 0.80 | 0.81 |

- Macro Avg F1-score: 0.82  
- Weighted Avg F1-score: 0.82  

---

### 5.3 Confusion Matrix
[[13637 2495]
[ 2929 11450]]


- True Positives: 11,450  
- True Negatives: 13,637  
- False Positives: 2,495  
- False Negatives: 2,929  

The model performs slightly better in identifying low-severity vulnerabilities.

---

## 6. Key Observations

- Hybrid features (BERT + CVSS) significantly improve performance  
- Text descriptions carry strong semantic signals  
- Structured CVSS metrics enhance prediction reliability  
- Balanced performance across both classes  

---

## 7. Limitations

- Binary classification oversimplifies severity levels  
- Medium and critical classes are not included  
- BERT embeddings are computationally expensive  
- No explainability mechanism included  

---

## 8. Future Work

- Extend to multi-class classification (Low, Medium, High, Critical)  
- Optimize embedding generation  
- Add explainability (e.g., SHAP)  
- Deploy as a web application  
- Integrate threat intelligence data  

---

## 9. Conclusion

This project demonstrates that combining NLP with structured cybersecurity data can effectively predict vulnerability severity. With an accuracy of 82.22%, the model shows strong potential for real-world vulnerability prioritization and risk assessment.
