# Network Traffic Classification using UNSW-NB15 Dataset

## Problem Summary
This project focuses on classifying network traffic records as either **normal** or **attack** (binary classification) using the UNSW-NB15 dataset. The dataset contains a hybrid of real modern normal traffic and contemporary synthesized attack activities, making it valuable for intrusion detection research.

## Dataset Description
The UNSW-NB15 dataset contains:
- **175,000+ network traffic records**
- **45 features** describing network flow characteristics
- **Binary labels**: 0 (normal) or 1 (attack)
- **9 attack categories** (e.g., Fuzzers, DoS, Exploits, Reconnaissance)
### Class Imbalance
The dataset exhibits significant class imbalance:
- **Normal (Class 0)**: 31.94%  
- **Attack (Class 1)**: 68.06%  

This imbalance necessitated specialized metrics and techniques to avoid biased model performance.

### Key Features:
| Feature Name | Description |
|-------------|-------------|
| `dur` | Record total duration |
| `proto` | Transaction protocol |
| `service` | Network service (http, ftp, ssh, etc.) |
| `spkts`/`dpkts` | Source/destination packet counts |
| `sbytes`/`dbytes` | Source/destination byte counts |
| `attack_cat` | Attack category (for attacks) |
| `label` | 0=normal, 1=attack |

## Methodology
1. **Exploratory Data Analysis (EDA)**
   - Analyzed feature distributions
   - Investigated class imbalance
   - Examined correlations between features

2. **Preprocessing**
#### Handling Data Challenges:

| Technique            | Reason                                                                                                                 |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **Robust Scaler**    | Mitigated outliers in flow durations (`dur`), packet counts (`spkts`, `dpkts`), and byte features (`sbytes`, `dbytes`) |
| **One-Hot Encoding** | Optimal for categorical features (`proto`, `service`, `state`) with non-ordinal relationships                          |

3. **Model Development**
   - **Baseline Models** (70-80% accuracy):
     - Logistic Regression
     - K-Nearest Neighbors (KNN)
     - Decision Trees
     - Naive Bayes
   
   - **Advanced Models** (85-90% accuracy):
     - Random Forest
     - XGBoost
     - AdaBoost
     - Balanced Random Forest (handling class imbalance)

4. **Model Optimization**
   - Hyperparameter tuning using GridSearchCV
   - Cross-validation (5-fold)
   - Ensemble methods (Voting Classifier)
   
5.  **Class Imbalance Mitigation**:
    - Evaluated **resampling techniques** (SMOTE, RandomUnderSampler)
    - Used **class-weighted models** (e.g., `class_weight='balanced'`)
    - Prioritized **imbalance-aware metrics** (F1, Precision-Recall, ROC-AUC)

## Results
The **Balanced Random Forest model** achieved the best performance:
- **Accuracy**: 90%
- **ROC AUC Score**: 0.89

## Conclusion
This project demonstrates that tree-based ensemble methods (particularly Balanced Random Forest) effectively classify network traffic in the UNSW-NB15 dataset, outperforming traditional machine learning models. The results suggest strong potential for real-world intrusion detection systems.

## Dataset Source
The UNSW-NB15 dataset is available [here](https://www.unsw.adfa.edu.au/unsw-canberra-cyber/cybersecurity/ADFA-NB15-Datasets/).
