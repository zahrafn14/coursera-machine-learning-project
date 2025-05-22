# Coursera Practical Machine Learning 
**Name:** Zahra Fitriana

This submission is the project of coursera assignment on Practical Machine learning course. The dataset is part of the Practical Machine Learning course in coursera.

### Data sources:
[Training data] (https://d396qusza40orc.cloudfront.net/predmachlearn/pml-training.csv)
[Testing data] (https://d396qusza40orc.cloudfront.net/predmachlearn/pml-testing.csv)

---
```markdown
### Load libraries and data

```r
library(rpart)
library(rpart.plot)
library(ggplot2)

set.seet(123)

## Load data
train_url <- "https://d396qusza40orc.cloudfront.net/predmachlearn/pml-training.csv"
test_url <- "https://d396qusza40orc.cloudfront.net/predmachlearn/pml-testing.csv"

train_data <- read.csv(train_url, na.strings = c("NA", "", "#DIV/0!"))
test_data <- read.csv(test_url, na.strings = c("NA", "", "#DIV/0!"))

### Data Cleaning
## Remove near-zero variance predictors
nzv <- nearZeroVar(train_data)
train_data <- train_data[, -nzv]

## Remove columns with too many NAs (keep columns with no NAs)
train_data <- train_data[, colSums(is.na(train_data)) == 0]

## Remove ID and timestamps columns (first 5)
train_data <- train_data[, -(1:5)]

## Make sure 'classe' is a factor
train_data$classe <- factor(train_data$classe)

## Apply some cleaning steps to test_data
test_data <- test_data[, names(test_data) %in% names(train_data)]
## test_data should not contain 'classe' column
test_data <- test_data[, names(train_data)[names(train_data) != "classe"]]

## Check final columns
print(paste("Number of columns in training data", ncol(train_data)))
