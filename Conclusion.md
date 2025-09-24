# Conclusion for Biomarkers in Neuronal Synuclein Disease (NSD)

## Logistic Regression Model <br>
The logistic regression model was found to have the highest level of accuracy.
### Key Metrics:
<b>Precision:</b><br>
Class 0 (Negative): 0.312 indicates that only 31.2% of the model's predictions for "negative" cases are correct.<br>
Class 1 (Positive): 0.995 means that when the model predicts someone is positive for neuronal synuclein disease, it is correct 99.5% of the time.<br>
<br>
<b>Recall:<br></b>
Class 0 (Negative): 0.909 indicates the model captures 90.9% of true negatives.<br>
Class 1 (Positive): 0.900 means the model correctly identifies 90% of those who actually have the disease.<br>
<br>
<b>F1-Score:<br></b>
Combines precision and recall: Class 0 (Negative): 0.465 indicates weaker performance for detecting true negatives.<br>
Class 1 (Positive): 0.945 suggests strong performance for detecting true positives.<br>
<br>
<b>Accuracy:<br></b>
Overall, the model correctly classifies 90% of cases.<br>
<b>ROC-AUC (0.959):<br></b>
This high value indicates excellent discrimination between positive and negative cases. verage Precision (0.998):<br>
This is the area under the precision-recall curve. A value of 0.591 suggests moderate precision across recall levels, particularly for the minority class (Class 2).<br>

<b>Confusion Matrix:<br></b>
True Negatives (TN): 10 – Correctly predicted negative cases (Class 0).<br>
False Negatives (FN): 1 – Predicted negative (Class 0) but actually positive (Class 1).<br>
True Positives (TP): 197 – Correctly predicted positive cases (Class 1).<br>
False Positives (FP): 22 – Predicted positive (Class 1) but actually negative (Class 0).<br>

<b>Strengths:<br></b>
The model excels at identifying positive cases (Class 1), with high precision and recall for this class. Overall accuracy and ROC-AUC are very high, indicating the model is generally effective.

<b>Weaknesses:<br></b>
The model struggles with the minority class (Class 0, negative cases), as seen in its low precision (31.2%) and F1-score (0.465). This issue arises because the dataset is imbalanced (Class 1 has 219 cases vs. 11 for Class 2). SMOTE helped improve recall for Class 2 (0.909), but precision remains low.

## Analysis of Results

Our first objective was to determine if we could predict incidence of neuronal synuclein disease (NSD) using logistic regression and the FMax and TTT variables. The logistic regression model performs exceptionally well in identifying positive cases of neuronal synuclein disease (Class 1), with high precision, recall, and overall accuracy (90%). However, it struggles with detecting negative cases (Class 0), reflected in low precision and F1-score. The model's strengths make it suitable for applications prioritizing correct identification of positive cases, but it has limitations in handling imbalanced data which should be addressed to improve negative case predictions. It will be difficult to improve upon this model with the current data, due to the significant imbalance in the testing results from participants in the study.

Our second objective was to further analyze if a prediction of NSD was possible, what would be the threshold to determine a positive or negative result. Looking at the FMax variable, we can predict at just a 5% threshold, the incidence of a correct positive diagnosis is 99%. However, the incidence of false positives is also high with a 35.9% precision level meaning nearly 36% of the people who would show as positive are actually negative. This would potentially be acceptable for a very early, first pass screening test, however, could not provide a definite diagnosis. Looking at just the Time to Threshold variable gave us inconclusive results because the prediction accuracy was only at about 50% for most of the data.

Ultimately, improving either the Logistic Regression model or the Threshold Model will be challenging without including more control subjects in the study. However, increasing control numbers is particularly difficult with cerebrospinal fluid due to the invasive nature of this medical test. Nevertheless, it is possible to see conclusive evidence that the presence of alpha-synuclein protein in cerebrospinal fluid serves as a strong indicator of the disease.

