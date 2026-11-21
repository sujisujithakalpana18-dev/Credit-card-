# Credit Card Default Prediction

## Project Overview

This project explores customer credit-card information and builds
machine-learning classification models to predict whether a customer
will default on their payment in the next month.

The target variable is **`default payment next month`**: - `0` -- No
default - `1` -- Default

## Dataset

The notebook loads the dataset from an Excel file named
`creditcard.xls`.

Place `creditcard.xls` in the same directory as the notebook before
running it. The dataset is expected to contain customer details and
payment information, including fields such as:

-   `LIMIT_BAL` -- Credit limit
-   `SEX`, `EDUCATION`, `MARRIAGE` -- Customer demographic categories
-   `AGE` -- Customer age
-   `PAY_0` / `PAY_1` and subsequent `PAY` fields -- Repayment status
-   `BILL_AMT1` to `BILL_AMT6` -- Bill statement amounts
-   `PAY_AMT1` to `PAY_AMT6` -- Previous payment amounts
-   `default payment next month` -- Prediction target

The `ID` field is excluded from the model predictors because it is an
identifier.

## Technologies and Libraries

-   Python
-   Jupyter Notebook
-   NumPy
-   pandas
-   Matplotlib
-   Seaborn
-   scikit-learn
-   xlrd (for reading legacy `.xls` Excel files)

## Project Workflow

1.  **Load the data** -- Read the Excel dataset into a pandas DataFrame.
2.  **Inspect the data** -- Review sample rows, dimensions, column
    names, data types, descriptive statistics, missing values and
    duplicates.
3.  **Clean the data** -- Promote the first data row to column headers,
    remove unnamed/extra columns and convert columns to numeric values.
4.  **Explore the data** -- Examine summary statistics and the
    distribution of the target classes.
5.  **Handle outliers** -- Apply the Interquartile Range (IQR) method
    with clipping to selected numerical columns.
6.  **Encode categorical data** -- Apply one-hot encoding to the
    `MARRIAGE` column. The modelling section also identifies `SEX`,
    `EDUCATION` and `MARRIAGE` as categorical predictors.
7.  **Visualize patterns** -- Create plots for default distribution,
    age, credit limits, default rates by sex and education, and feature
    correlations.
8.  **Prepare model data** -- Separate the predictors (`X`) and target
    (`y`), then split the data into training and testing sets using an
    80:20 ratio and stratification.
9.  **Select features** -- Use `SelectKBest` with the ANOVA F-test
    (`f_classif`) to rank predictors and select the top 20 features.
10. **Train classifiers** -- Fit Logistic Regression, Decision Tree and
    Random Forest models.
11. **Evaluate models** -- Compare accuracy, precision, recall and
    F1-score on the test set.

## Machine Learning Models

The notebook evaluates these classification algorithms:

-   **Logistic Regression**
-   **Decision Tree Classifier**
-   **Random Forest Classifier** (100 estimators)

## Evaluation Metrics

  -----------------------------------------------------------------------
  Metric                              Meaning
  ----------------------------------- -----------------------------------
  Accuracy                            Overall proportion of correct
                                      predictions

  Precision                           Proportion of predicted defaults
                                      that are actual defaults

  Recall                              Proportion of actual defaults
                                      correctly identified

  F1-score                            Harmonic mean of precision and
                                      recall
  -----------------------------------------------------------------------

The notebook prints a comparison table containing accuracy, precision,
recall and F1-score for each model. Actual scores depend on the dataset
and execution environment.

## How to Run

1.  Install Python and Jupyter Notebook.

2.  Save `creditcard.xls` in the project directory.

3.  Install the required libraries:

    ``` bash
    pip install numpy pandas matplotlib seaborn scikit-learn xlrd openpyxl jupyter
    ```

4.  Open the notebook:

    ``` bash
    jupyter notebook
    ```

5.  Open the project notebook and run the cells in order.

## Notes and Potential Improvements

-   The notebook currently applies feature selection before the
    train/test split. For a more reliable evaluation, fit feature
    selection using only the training data (preferably inside a
    scikit-learn pipeline).
-   The scaling section calls `fit_transform` separately on the training
    and test sets. Fit the scaler on the training data and use
    `transform` on the test data to avoid data leakage.
-   The final model loop trains on the original `X_train` data, rather
    than the scaled arrays or the previously defined preprocessing
    pipeline. Consider integrating imputation, encoding, scaling,
    feature selection and the classifier into a single pipeline.
-   The notebook imports K-Nearest Neighbors but does not include it in
    the final `models` dictionary, so it is not evaluated.
-   Review the dataset's first-row/header structure before running the
    cleaning cells. The notebook assumes the first row contains the
    column names.

## Project Goal

The goal is to understand patterns associated with credit-card payment
defaults and compare baseline classification algorithms that may help
identify customers at risk of defaulting.
