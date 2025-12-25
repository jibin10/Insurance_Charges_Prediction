# Medical Insurance Charges Prediction

This project predicts **medical insurance charges** from basic customer information (age, sex, BMI, smoking status, children, and region). It is written as a full workflow: define the problem, choose a dataset, prepare the data, train models, validate properly, and explain conclusions in plain language.

---

## Background

Healthcare spending has been rising for decades. A big part of the work here is to understand whether a small set of common factors (like age, BMI, and smoking) can explain and predict the final insurance charges for an individual.

---

## Problem Statement

Given a person’s profile (age, sex, BMI, smoking status, number of children, and region), predict the **medical charges billed by the insurer**.

### Hypothesis
Basic personal and lifestyle features (especially smoking) contain enough signal to predict insurance charges reasonably well.

---

## Objectives

- Build a deep learning regression model to predict insurance charges.
- Use validation methods to avoid underfitting and overfitting.
- Select a final model that generalizes well to unseen data.

**Out of scope**
- Using non–deep learning algorithms (the focus is neural networks only).

---

## Dataset

A public “Medical Cost / Insurance” dataset (CSV format) is used.  
It contains individual-level records with features such as:

- age
- sex
- BMI
- children
- smoker
- region
- charges (target)

The dataset also shows a strong real-world pattern: **smokers tend to have higher medical costs**.

---

## Data Preparation (Preprocessing)

The dataset is prepared with simple checks and cleanup steps:

- Load the CSV and review basic statistics (min/max/mean, etc.).
- Check for missing values (null/empty) and confirm the data is usable.
- Check for duplicate rows and remove duplicates (keep one copy).
- Review whether categories are reasonably distributed (gender/region balance).
- Convert categorical fields (sex, smoker, region) into numeric form using encoded columns so they can be used for training.

---

## Measure of Success

This is a **regression** task (predicting a number). Two standard metrics are used:

- **MSE (Mean Squared Error)**: penalizes larger errors more strongly.
- **MAE (Mean Absolute Error)**: easier to interpret because it is the average absolute difference.

MAE is treated as the main metric for comparing models because it is more directly readable.

---

## Validation Strategy

Two validation methods are used to make sure model performance is not accidental:

### Hold-out validation
Split the dataset into training / validation / test sets.  
Validation data helps tune decisions during development, while the test set is kept untouched until the end.

### K-Fold validation
K-Fold is used because the dataset is not very large.  
The data is split into K parts; each part becomes the validation set once, and the remaining parts are used for training. This gives a more stable estimate of performance.

---

## Methodology (Workflow)

The workflow follows a standard deep learning development loop:

1. **Prepare the dataset**
   - Encode categorical features
   - Scale/normalize values so features stay in a similar numeric range

2. **Create a baseline**
   - Start with a simple model to set a minimum performance bar.
   - Also use a “common sense” baseline idea to sanity-check whether the model is learning something meaningful.

3. **Improve the model**
   - Increase model capacity and compare against the baseline.
   - Watch training vs validation behavior to detect underfitting or overfitting.

4. **Create an overfitting example (on purpose)**
   - Build a model that clearly overfits to understand what “too complex” looks like on this dataset.

5. **Tune hyperparameters**
   Tuning focuses on the most important knobs that affect learning and generalization:
   - batch size and training epochs
   - optimizer choice
   - learning rate
   - weight initialization
   - activation functions
   - dropout regularization
   - L1/L2 regularization
   - hidden layer size and number of layers

6. **Pick a final balanced model**
   The final model is chosen using a “simple is better” approach:
   - prefer the simplest model that still performs well
   - avoid unnecessary complexity that increases overfitting risk

---

## Final Evaluation

After model selection and validation, the final model is trained using the available development data and then evaluated on the **unseen test set** to estimate real-world performance.

(Exact numbers are intentionally not included in this README.)

---

## Conclusions

- The selected features provide enough signal to predict insurance charges to a useful level.
- Dataset size matters: smaller datasets make deep learning harder to tune and easier to overfit.
- A simpler model is often the safest choice when data is limited (Occam’s razor idea).

---

## Further Development

- Deploy as part of a simple web or mobile app for cost estimation.
- Watch for **concept drift** (real-world data changes over time).
- Collect fresh data after deployment and retrain periodically to prevent performance decay.

---

## References

The report cites sources discussing long-term healthcare spending trends and factors driving cost growth, and uses standard regression validation practices (holdout + K-Fold).
