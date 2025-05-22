# Coursera Practical Machine Learning 
**Name:** Zahra Fitriana

This submission is the project of coursera assignment on Practical Machine learning course. The dataset is part of the Practical Machine Learning course in coursera.

### Data sources:
[Training data] (https://d396qusza40orc.cloudfront.net/predmachlearn/pml-training.csv)
[Testing data (https://d396qusza40orc.cloudfront.net/predmachlearn/pml-testing.csv)

---

## **Method**

### Data Preprocessing
- Removed near-zero variance predictors
- Removed columns with missing values (`NA`, `#DIV/0!`, etc.)
- Removed irrelevant ID and timestamps columns
- Converted the target `classe` variable into a factor

### Data Partitioning
- Splot the cleaned training data into:
  - **Training set** (70%)
  - **Validation set** (30%) using `createDataPartition()` from `caret`

### Model
- **Algorithm:** Random Forest (`caret::train()`)
- **Cross-validation:** 5-fold CV (`trainControl(method = "cv", number = 5)`)
- Model was trained to predict `classe` based on all remaining features

---

## **Results**

### Model Performance on Validation Set

```r
Accuracy : 0.9962
95% CI : (0.9934, 0.9979)
Kappa : 0.9952
