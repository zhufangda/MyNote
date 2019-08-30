# Confusion matrix

|True Positive(TP)|False Positive(FP)|
|------------|---------|
|False Negative(FN)|True Negative(TN)|

# Accuracy

Accuracy is the fraction of predictions our model got right. Formally, accuracy has the following definition:

$$\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}$$

# Precision 

Precision mesures the percentage of sentences flagged as positive that were corretly classified
$$\text{Precision} = \frac{TP}{TP + FP} = \frac{\text{Example identified as positive correctly}}{\text{Example identified}}$$

# Recall
Recall mesures the percentage of actual positive sentence that were correctly classified.
$\text{Recall} = \frac{TP}{TP + FN} = \frac{TP}{\text{Actual positive}}$

# F1 Score
$$\text{F1} = 2\times \frac{precision \times recall}{precision + recall}$$

A good F1 score means that we have low flase positives and low false negatives.