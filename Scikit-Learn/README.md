
# Scikit-Learn Cheat Sheet: 50 Essential Tools for Professional ML Workflows

A comprehensive reference guide covering pipelines, preprocessing, feature selection, evaluation, cross-validation, hyperparameter tuning, ensemble methods, and advanced model improvement techniques.

---

## 📋 Chapter 1: Building Professional ML Workflows

| # | Tool | Purpose | Key Parameters | When to Use |
|---|------|---------|----------------|-------------|
| 1 | `Pipeline()` | Chain preprocessing steps and models together | List of `(name, transformer)` tuples | Production workflows with custom step names |
| 2 | `make_pipeline()` | Quickly create pipelines | List of transformers | Prototyping and simple workflows |
| 3 | `ColumnTransformer()` | Apply different transformations to different columns | `(name, transformer, columns)` | Mixed numerical + categorical datasets |
| 4 | `FunctionTransformer()` | Wrap custom Python functions | `func` | Custom preprocessing logic |
| 5 | `get_params()` | View available parameters | None | Finding parameters for tuning |
| 6 | `set_params()` | Update pipeline parameters | `step__parameter=value` | Applying tuned hyperparameters |
| 7 | `set_config(display="diagram")` | Visualize pipelines | `display="diagram"` | Debugging and documentation |

---

## 📋 Chapter 2: Data Preprocessing Essentials

| # | Tool | Purpose | Key Parameters | Best For |
|---|------|---------|----------------|----------|
| 8 | `SimpleImputer()` | Handle missing values | `strategy="mean"` / `"median"` / `"most_frequent"` | Real-world datasets |
| 9 | `StandardScaler()` | Standardize features (mean=0, std=1) | None | Scale-sensitive models (SVM, KNN, Logistic Regression, Neural Networks) |
| 10 | `MinMaxScaler()` | Scale features to a fixed range | `feature_range=(0,1)` | Neural networks and bounded features |
| 11 | `RobustScaler()` | Scale using median and IQR | None | Datasets with outliers |
| 12 | `OneHotEncoder()` | Convert categories into binary features | `handle_unknown="ignore"` | Categorical features (`X`) |
| 13 | `LabelEncoder()` | Convert labels into integers | None | Target variables (`y`) only |
| 14 | `PolynomialFeatures()` | Create polynomial and interaction features | `degree=2` | Non-linear relationships |

---

## 📋 Chapter 3: Feature Selection & Dimensionality Reduction

| # | Tool | Purpose | Key Parameters | When to Use |
|---|------|---------|----------------|-------------|
| 15 | `VarianceThreshold()` | Remove constant or low-variance features | `threshold=0` | Removing useless features |
| 16 | `SelectKBest()` | Select top K features using statistical tests | `score_func`, `k` | Large feature spaces |
| 17 | `SelectFromModel()` | Select features using model importance | `estimator`, `threshold` | Model-based feature ranking |
| 18 | `RFE()` | Recursive feature elimination | `estimator`, `n_features_to_select` | Smaller datasets and interpretability |
| 19 | `RFECV()` | RFE with cross-validation | `estimator`, `cv`, `scoring` | Finding optimal feature count |
| 20 | `SequentialFeatureSelector()` | Search feature combinations | `direction`, `n_features_to_select` | Finding the best feature subset |
| 21 | `PCA()` | Reduce dimensionality by creating new components | `n_components` | High-dimensional data and visualization |

---

## 📋 Chapter 4: Model Evaluation & Performance Metrics

| # | Tool | Purpose | Key Parameters | When to Use |
|---|------|---------|----------------|-------------|
| 22 | `accuracy_score()` | Measure classification accuracy | `y_true`, `y_pred` | Balanced classification problems |
| 23 | `precision_score()` | Measure precision | `average`, `pos_label` | When false positives matter |
| 24 | `recall_score()` | Measure recall/sensitivity | `average`, `pos_label` | When false negatives matter |
| 25 | `f1_score()` | Balance precision and recall | `average` | Imbalanced classification |
| 26 | `confusion_matrix()` | Show classification errors | `labels` | Understanding prediction errors |
| 27 | `classification_report()` | Generate multiple classification metrics | `target_names`, `digits` | Quick model evaluation |
| 28 | `mean_squared_error()` | Measure squared regression error | `y_true`, `y_pred` | Regression evaluation |
| 29 | `mean_absolute_error()` | Measure average absolute error | `y_true`, `y_pred` | Interpretable regression errors |
| 30 | `r2_score()` | Measure explained variance | `y_true`, `y_pred` | Regression model comparison |

### Classification Metrics Quick Reference

```python
from sklearn.metrics import (
    accuracy_score,
    precision_score,
    recall_score,
    f1_score,
    confusion_matrix,
    classification_report
)

# Basic usage
y_pred = model.predict(X_test)

accuracy = accuracy_score(y_test, y_pred)
precision = precision_score(y_test, y_pred)
recall = recall_score(y_test, y_pred)
f1 = f1_score(y_test, y_pred)

# Confusion matrix
cm = confusion_matrix(y_test, y_pred)

# Full report
print(classification_report(y_test, y_pred))
```

### Regression Metrics Quick Reference

```python
from sklearn.metrics import (
    mean_squared_error,
    mean_absolute_error,
    r2_score
)

mse = mean_squared_error(y_test, y_pred)
mae = mean_absolute_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)
```

---

## 📋 Chapter 5: Cross-Validation & Data Splitting

| # | Tool | Purpose | Key Parameters | When to Use |
|---|------|---------|----------------|-------------|
| 31 | `cross_val_score()` | Evaluate a model using cross-validation | `cv`, `scoring` | Quick model evaluation |
| 32 | `KFold()` | Create K-fold splits | `n_splits`, `shuffle`, `random_state` | Regression/general datasets |
| 33 | `StratifiedKFold()` | Create stratified K-fold splits | `n_splits`, `shuffle` | Classification |
| 34 | `LeaveOneOut()` | Use one sample as validation at a time | None | Very small datasets |
| 35 | `cross_validate()` | Evaluate multiple metrics and timing | `scoring`, `cv`, `return_train_score` | Detailed model evaluation |
| 36 | `train_test_split()` | Split data into training and testing sets | `test_size`, `random_state`, `stratify` | Basic train/test evaluation |

### Cross-Validation Quick Reference

```python
from sklearn.model_selection import (
    cross_val_score,
    cross_validate,
    KFold,
    StratifiedKFold,
    LeaveOneOut,
    train_test_split
)

# Quick CV
scores = cross_val_score(model, X, y, cv=5)

# Detailed CV
results = cross_validate(
    model, X, y, cv=5,
    scoring=['accuracy', 'f1'],
    return_train_score=True
)

# Custom splits
kf = KFold(n_splits=5, shuffle=True, random_state=42)
skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
loo = LeaveOneOut()

# Train/test split
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)
```

---

## 📋 Chapter 6: Hyperparameter Optimisation

| # | Tool | Purpose | Key Parameters | When to Use |
|---|------|---------|----------------|-------------|
| 37 | `GridSearchCV()` | Exhaustive hyperparameter search | `param_grid`, `cv`, `scoring` | Small parameter spaces |
| 38 | `RandomizedSearchCV()` | Random hyperparameter search | `param_distributions`, `n_iter`, `cv` | Large parameter spaces |
| 39 | `ParameterGrid()` | Generate parameter combinations | `param_grid` | Custom search loops |
| 40 | `validation_curve()` | Visualize hyperparameter effects | `param_name`, `param_range`, `cv` | Understanding model behavior |
| 41 | `learning_curve()` | Analyze data size effects | `train_sizes`, `cv` | Diagnosing bias/variance |

### Hyperparameter Tuning Quick Reference

```python
from sklearn.model_selection import (
    GridSearchCV,
    RandomizedSearchCV,
    ParameterGrid,
    validation_curve,
    learning_curve
)

# Grid Search
param_grid = {'C': [0.1, 1, 10], 'kernel': ['linear', 'rbf']}
grid = GridSearchCV(model, param_grid, cv=5)
grid.fit(X_train, y_train)

# Random Search
param_dist = {'n_estimators': [50, 100, 200]}
search = RandomizedSearchCV(model, param_dist, n_iter=10, cv=5)
search.fit(X_train, y_train)

# Validation Curve
train_scores, val_scores = validation_curve(
    model, X_train, y_train,
    param_name='n_estimators',
    param_range=[10, 50, 100, 200],
    cv=5
)

# Learning Curve
sizes, train_scores, val_scores = learning_curve(
    model, X_train, y_train,
    train_sizes=np.linspace(0.1, 1.0, 5),
    cv=5
)
```

---

## 📋 Chapter 7: Ensemble Learning Techniques

| # | Tool | Purpose | Key Parameters | When to Use |
|---|------|---------|----------------|-------------|
| 42 | `VotingClassifier()` | Combine multiple classifiers | `estimators`, `voting` | Different model types |
| 43 | `VotingRegressor()` | Combine multiple regressors | `estimators` | Different regression models |
| 44 | `RandomForestClassifier()` | Ensemble of decision trees | `n_estimators`, `max_depth` | Strong baseline |
| 45 | `GradientBoostingClassifier()` | Sequential error correction | `n_estimators`, `learning_rate` | High performance |
| 46 | `AdaBoostClassifier()` | Focus on difficult examples | `n_estimators`, `learning_rate` | Improving weak models |
| 47 | `StackingClassifier()` | Meta-model on base models | `estimators`, `final_estimator`, `cv` | Complex combinations |

### Ensemble Quick Reference

```python
from sklearn.ensemble import (
    VotingClassifier,
    VotingRegressor,
    RandomForestClassifier,
    GradientBoostingClassifier,
    AdaBoostClassifier,
    StackingClassifier
)
from sklearn.linear_model import LogisticRegression
from sklearn.svm import SVC

# Voting
voting = VotingClassifier([
    ('lr', LogisticRegression()),
    ('rf', RandomForestClassifier()),
    ('svc', SVC())
])
voting.fit(X_train, y_train)

# Soft voting (better with probabilities)
voting = VotingClassifier(estimators=[...], voting='soft')

# Random Forest
rf = RandomForestClassifier(n_estimators=100, max_depth=10)

# Gradient Boosting
gb = GradientBoostingClassifier(n_estimators=100, learning_rate=0.1)

# AdaBoost
ada = AdaBoostClassifier(n_estimators=100, learning_rate=0.5)

# Stacking
stacking = StackingClassifier(
    estimators=[('rf', RandomForestClassifier()), ('svc', SVC())],
    final_estimator=LogisticRegression(),
    cv=5
)
```

---

## 📋 Chapter 8: Advanced Model Improvement Techniques

| # | Tool | Purpose | Key Parameters | When to Use |
|---|------|---------|----------------|-------------|
| 48 | `CalibrationDisplay()` | Check probability calibration | `n_bins` | Probability-critical applications |
| 49 | `permutation_importance()` | Measure feature importance | `n_repeats`, `scoring` | Understanding feature impact |
| 50 | `joblib.dump()` / `joblib.load()` | Save and load models | None | Production deployment |

### Advanced Techniques Quick Reference

```python
from sklearn.calibration import CalibrationDisplay
from sklearn.inspection import permutation_importance
import joblib

# Calibration check
CalibrationDisplay.from_estimator(model, X_test, y_test, n_bins=10)

# Feature importance
result = permutation_importance(
    model, X_test, y_test,
    n_repeats=10, random_state=42
)

# Model persistence
joblib.dump(pipeline, "model.pkl")
loaded_pipeline = joblib.load("model.pkl")
```

---

## 🚀 Common Pipeline Patterns

### Pattern 1: Simple Classification Pipeline

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

pipeline = Pipeline([
    ("scaler", StandardScaler()),
    ("classifier", LogisticRegression())
])

pipeline.fit(X_train, y_train)
pipeline.score(X_test, y_test)
```

### Pattern 2: Mixed Numerical + Categorical Data

```python
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.pipeline import Pipeline

numeric_features = ["age", "income"]
categorical_features = ["department", "country"]

preprocessor = ColumnTransformer([
    ("num", StandardScaler(), numeric_features),
    ("cat", OneHotEncoder(handle_unknown="ignore"), categorical_features)
])

pipeline = Pipeline([
    ("preprocessor", preprocessor),
    ("classifier", LogisticRegression())
])
```

### Pattern 3: Feature Selection Pipeline

```python
from sklearn.feature_selection import SelectKBest, f_classif

pipeline = Pipeline([
    ("imputer", SimpleImputer(strategy="median")),
    ("scaler", StandardScaler()),
    ("selector", SelectKBest(f_classif, k=10)),
    ("classifier", LogisticRegression())
])
```

### Pattern 4: PCA Pipeline

```python
from sklearn.decomposition import PCA

pipeline = Pipeline([
    ("scaler", StandardScaler()),
    ("pca", PCA(n_components=0.95)),
    ("classifier", LogisticRegression())
])
```

### Pattern 5: Hyperparameter Tuning with Pipeline

```python
from sklearn.model_selection import GridSearchCV

param_grid = {
    "classifier__C": [0.1, 1, 10],
    "classifier__kernel": ["linear", "rbf"]
}

grid = GridSearchCV(pipeline, param_grid, cv=5)
grid.fit(X_train, y_train)
print(grid.best_params_)
```

---

## 📊 Decision Guides

### Scaler Decision Guide

```
Do you have outliers?

        Yes
         |
   RobustScaler()

        No
         |
Need values between 0 and 1?

     Yes       No
      |         |
MinMaxScaler StandardScaler
```

### Feature Selection Decision Guide

```
More than 1000 features?

        Yes
         |
SelectKBest()
or
SelectFromModel()

        No
         |
Need interpretability?

     Yes          No
      |            |
 RFE()        RFECV()
 SequentialFS
```

### Cross-Validation Decision Guide

```
Need a quick CV score?
        |
        ↓
cross_val_score()
        |
        ├── Classification
        │       ↓
        │  StratifiedKFold()
        │
        └── Regression
                ↓
             KFold()

Need multiple metrics?
        |
        ↓
cross_validate()

Very small dataset?
        |
        ↓
LeaveOneOut()
```

### Evaluation Metric Decision Guide

```
Classification
      |
      ├── Balanced classes
      │       ↓
      │   Accuracy
      │
      ├── False positives are costly
      │       ↓
      │   Precision
      │
      ├── False negatives are costly
      │       ↓
      │   Recall
      │
      └── Need balance
              ↓
             F1

Regression
      |
      ├── Penalize large errors
      │       ↓
      │      MSE
      │
      ├── Easy interpretation
      │       ↓
      │      MAE
      │
      └── Explained variance
              ↓
             R²
```

---

## ⚠️ Golden Rules

### 1. Always Use Pipelines

**✅ Good**
```python
pipeline.fit(X_train, y_train)
```

**❌ Bad (Data Leakage Risk)**
```python
scaler.fit(X)
```

### 2. Never Fit Transformers Before Train-Test Split

**❌ Wrong**
```python
scaler.fit_transform(X)
train_test_split()
```

**✅ Correct**
```python
X_train, X_test, y_train, y_test = train_test_split(...)
scaler.fit(X_train)
X_train_scaled = scaler.transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

### 3. Use Double Underscores for Nested Parameters

**✅ Good**
```python
pipeline.get_params()["classifier__C"]
```

**❌ Bad**
```python
pipeline.get_params()["classifier_C"]
```

### 4. Never Use LabelEncoder on Features

**✅ Correct**
```python
OneHotEncoder() → features (X)
LabelEncoder() → target (y)
```

**❌ Wrong**
```python
LabelEncoder() on categorical features
```

### 5. Always Scale Before PCA

**✅ Correct**
```text
StandardScaler() → PCA()
```

**❌ Wrong**
```text
PCA() without scaling
```

### 6. Never Tune on the Test Set

**❌ Wrong**
```text
Train → Test → Change Model → Test Again
```

**✅ Correct**
```text
Train → Cross-Validation → Tune & Select → Final Model → Test Once
```

### 7. Put Preprocessing Inside the Pipeline

**❌ Risky**
```python
X_scaled = StandardScaler().fit_transform(X)
cross_val_score(model, X_scaled, y, cv=5)
```

**✅ Correct**
```python
pipeline = Pipeline([("scaler", StandardScaler()), ("model", LogisticRegression())])
scores = cross_val_score(pipeline, X_train, y_train, cv=5)
```

---

## 📦 Complete Import Collection

```python
# Pipelines
from sklearn.pipeline import Pipeline, make_pipeline
from sklearn.compose import ColumnTransformer

# Preprocessing
from sklearn.preprocessing import (
    StandardScaler,
    MinMaxScaler,
    RobustScaler,
    OneHotEncoder,
    LabelEncoder,
    PolynomialFeatures,
    FunctionTransformer
)

# Imputation
from sklearn.impute import SimpleImputer

# Feature Selection
from sklearn.feature_selection import (
    VarianceThreshold,
    SelectKBest,
    SelectFromModel,
    RFE,
    RFECV,
    SequentialFeatureSelector
)

# Dimensionality Reduction
from sklearn.decomposition import PCA

# Models
from sklearn.linear_model import LogisticRegression, LinearRegression
from sklearn.ensemble import (
    RandomForestClassifier,
    GradientBoostingClassifier,
    AdaBoostClassifier,
    VotingClassifier,
    VotingRegressor,
    StackingClassifier
)
from sklearn.svm import SVC

# Model Evaluation
from sklearn.metrics import (
    accuracy_score,
    precision_score,
    recall_score,
    f1_score,
    confusion_matrix,
    classification_report,
    mean_squared_error,
    mean_absolute_error,
    r2_score
)

# Model Selection
from sklearn.model_selection import (
    train_test_split,
    cross_val_score,
    cross_validate,
    KFold,
    StratifiedKFold,
    LeaveOneOut,
    GridSearchCV,
    RandomizedSearchCV,
    ParameterGrid,
    validation_curve,
    learning_curve
)

# Calibration & Inspection
from sklearn.calibration import CalibrationDisplay
from sklearn.inspection import permutation_importance

# Configuration
from sklearn import set_config

# Persistence
import joblib

# Visualization
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
```

---

## 📝 Quick Summary: All 50 Tools

| # | Task | Best Tool |
|---|------|-----------|
| 1 | Build reusable workflows | `Pipeline()` |
| 2 | Quick pipelines | `make_pipeline()` |
| 3 | Mixed preprocessing | `ColumnTransformer()` |
| 4 | Custom transformations | `FunctionTransformer()` |
| 5 | Inspect parameters | `get_params()` |
| 6 | Update parameters | `set_params()` |
| 7 | Visualize pipelines | `set_config()` |
| 8 | Handle missing values | `SimpleImputer()` |
| 9 | Standard scaling | `StandardScaler()` |
| 10 | Min-max scaling | `MinMaxScaler()` |
| 11 | Robust scaling | `RobustScaler()` |
| 12 | Encode categories | `OneHotEncoder()` |
| 13 | Encode targets | `LabelEncoder()` |
| 14 | Create polynomial features | `PolynomialFeatures()` |
| 15 | Remove low-variance features | `VarianceThreshold()` |
| 16 | Select top features | `SelectKBest()` |
| 17 | Model-based selection | `SelectFromModel()` |
| 18 | Recursive feature elimination | `RFE()` |
| 19 | Recursive selection with CV | `RFECV()` |
| 20 | Sequential feature selection | `SequentialFeatureSelector()` |
| 21 | Reduce dimensionality | `PCA()` |
| 22 | Classification accuracy | `accuracy_score()` |
| 23 | Classification precision | `precision_score()` |
| 24 | Classification recall | `recall_score()` |
| 25 | Balance precision & recall | `f1_score()` |
| 26 | Analyze classification errors | `confusion_matrix()` |
| 27 | Classification summary | `classification_report()` |
| 28 | Penalize large regression errors | `mean_squared_error()` |
| 29 | Measure average regression error | `mean_absolute_error()` |
| 30 | Measure explained variance | `r2_score()` |
| 31 | Quick cross-validation | `cross_val_score()` |
| 32 | K-fold validation | `KFold()` |
| 33 | Stratified validation | `StratifiedKFold()` |
| 34 | Small-dataset validation | `LeaveOneOut()` |
| 35 | Multi-metric validation | `cross_validate()` |
| 36 | Train/test splitting | `train_test_split()` |
| 37 | Exhaustive hyperparameter search | `GridSearchCV()` |
| 38 | Random hyperparameter search | `RandomizedSearchCV()` |
| 39 | Generate parameter combinations | `ParameterGrid()` |
| 40 | Visualize hyperparameter effects | `validation_curve()` |
| 41 | Analyze data size effects | `learning_curve()` |
| 42 | Combine classifiers | `VotingClassifier()` |
| 43 | Combine regressors | `VotingRegressor()` |
| 44 | Random forest ensemble | `RandomForestClassifier()` |
| 45 | Gradient boosting | `GradientBoostingClassifier()` |
| 46 | AdaBoost | `AdaBoostClassifier()` |
| 47 | Stacking ensemble | `StackingClassifier()` |
| 48 | Check probability calibration | `CalibrationDisplay()` |
| 49 | Measure feature importance | `permutation_importance()` |
| 50 | Save and load models | `joblib.dump()` / `joblib.load()` |

---

## 🚀 Final Takeaway

A professional Scikit-Learn workflow goes beyond simply fitting a model.

**You need to know how to:**

1. **Build** → Reproducible pipelines with `Pipeline()` and `ColumnTransformer()`
2. **Prepare** → Clean data with imputation, scaling, and encoding
3. **Select** → Keep only the most informative features
4. **Split** → Separate train, validation, and test sets properly
5. **Train** → Fit models on training data only
6. **Validate** → Use cross-validation for reliable evaluation
7. **Evaluate** → Choose the right metrics for your problem
8. **Tune** → Optimize hyperparameters systematically
9. **Ensemble** → Combine models for better performance
10. **Deploy** → Save and load models for production

> **"Don't just build a model. Build a workflow that can be trusted."** 🚀

With these **50 Scikit-Learn tools**, you now have a complete foundation for preprocessing, feature engineering, feature selection, dimensionality reduction, model evaluation, cross-validation, hyperparameter tuning, ensemble learning, and production-ready deployment.
