Initial Employee Attrition Model Evaluation

1. Overview

This report documents the initial predictive modelling experiment for the Employee Retention Intelligence & Attrition Early Warning System.

The objective was to establish a baseline model capable of identifying employees who may voluntarily leave the organisation within the next six months.

A Logistic Regression classifier was selected as the initial model.

 2. Dataset Preparation

The modelling dataset was prepared from the simulated monthly workforce history.

| Metric | Training | Testing |
|---|---:|---:|
| Observation period | Jan–Jun 2024 | Jan–Jun 2025 |
| Observations | 1,740 | 7,517 |
| Attrition observations | 59 | 312 |
| Attrition rate | 3.39% | 4.15% |

July–December 2024 was excluded as an embargo period to ensure that training labels had sufficient time to mature before the assumed deployment date of January 2025.

The test period was selected to evaluate performance on a later workforce period.

 3. Model Features

The initial model used eight features:

- Months at Company
- Tenure in Years
- Job Satisfaction
- Work-Life Balance
- Engagement Score
- Manager Relationship
- Workload Score
- Overtime Hours

StandardScaler was used to standardise numerical features, while Logistic Regression was configured with balanced class weights to address the minority attrition class.

 4. Model Performance

| Evaluation Metric | Result |
|---|---:|
| Accuracy | 50.59% |
| Precision | 4.15% |
| Recall | 49.36% |
| F1-Score | 7.66% |
| ROC-AUC | 0.5145 |
| PR-AUC | 0.0431 |

Confusion Matrix

| | Predicted: Stay | Predicted: Leave |
|---|---:|---:|
| Actual: Stay | 3,649 | 3,556 |
| Actual: Leave | 158 | 154 |

 5. Interpretation

The initial model identified approximately 49% of the actual attrition observations. However, its precision was only 4.15%, meaning that most observations classified as potential attrition cases were false positives.

The ROC-AUC of 0.5145 indicates that the model has very limited ability to distinguish between employees who leave and those who stay.

The PR-AUC of 0.0431 was only marginally above the test-set positive-class prevalence of approximately 4.15%.

Although the model used balanced class weights, its default classification threshold resulted in a large number of positive predictions.

These findings suggest that the initial model is not yet suitable for operational employee-retention decisions.

6. Limitations Identified

The initial experiment revealed several methodological concerns:

1. Monthly employee experience indicators were not sufficiently connected to the underlying employee-level risk factors used in generating exit records.
2. Several variables in the original monthly dataset were static values copied from the end of the simulation period, creating potential temporal leakage.
3. Training and testing observations differed substantially in workforce tenure and months at company.
4. The training dataset contained only 59 positive attrition observations.
5. Multiple monthly observations can belong to the same employee, and overlapping six-month prediction windows can produce correlated outcomes.

These limitations must be considered when interpreting the results.

. Next Steps

The next development phase will focus on:

- Improving the synthetic monthly workforce experience generation process.
- Establishing a more consistent relationship between employee experience and simulated attrition.
- Reassessing temporal integrity and data leakage.
- Developing and comparing additional classification models.
- Evaluating classification thresholds using validation data rather than the test set.
- Investigating model fairness and practical retention intervention strategies.

8. Conclusion

The initial Logistic Regression experiment established a baseline for the project but did not achieve satisfactory predictive performance.

Rather than treating this as a successful prediction system, the results provide a foundation for improving the dataset, refining the modelling approach and developing a more reliable employee attrition early-warning framework.

