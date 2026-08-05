Here is the full content formatted as a **README.md cell** (pure Markdown, ready to paste into GitHub README or a Jupyter Markdown cell):

````markdown
# Scikit-Learn Cheat Sheet: 21 Essential Tools for Professional ML Workflows (Part 1)

A practical reference guide covering pipelines, preprocessing, feature selection, and dimensionality reduction techniques in Scikit-Learn.

---

# 📋 Chapter 1: Building Professional ML Workflows

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

# 📋 Chapter 2: Data Preprocessing Essentials

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

# 📋 Chapter 3: Feature Selection & Dimensionality Reduction

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

# 🚀 Most Common Pipeline Patterns

## Pattern 1: Simple Classification Pipeline

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

---

## Pattern 2: Mixed Numerical + Categorical Data

```python
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.pipeline import Pipeline
from sklearn.linear_model import LogisticRegression

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

---

## Pattern 3: Feature Selection Pipeline

```python
from sklearn.feature_selection import SelectKBest, f_classif

pipeline = Pipeline([
    ("imputer", SimpleImputer(strategy="median")),
    ("scaler", StandardScaler()),
    ("selector", SelectKBest(f_classif, k=10)),
    ("classifier", LogisticRegression())
])
```

---

## Pattern 4: Polynomial Features Pipeline

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import LinearRegression

pipeline = Pipeline([
    ("poly", PolynomialFeatures(
        degree=2,
        include_bias=False
    )),
    ("scaler", StandardScaler()),
    ("model", LinearRegression())
])
```

⚠️ Always scale polynomial features because generated values can have very different magnitudes.

---

## Pattern 5: PCA Pipeline

```python
from sklearn.decomposition import PCA

pipeline = Pipeline([
    ("scaler", StandardScaler()),
    ("pca", PCA(n_components=0.95)),
    ("classifier", LogisticRegression())
])
```

`n_components=0.95` keeps enough components to preserve 95% of the variance.

---

# ⚠️ Golden Rules

## 1. Always Use Pipelines

### ✅ Good

```python
pipeline.fit(X_train, y_train)
```

### ❌ Bad (Data Leakage Risk)

```python
scaler.fit(X)
```

Always fit preprocessing steps only on training data.

---

## 2. Never Fit Transformers Before Train-Test Split

### ❌ Wrong

```python
scaler.fit_transform(X)

train_test_split()
```

The transformer has already seen information from the test set.

---

### ✅ Correct

```python
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)

scaler.fit(X_train)

X_train_scaled = scaler.transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

---

## 3. Use Double Underscores for Nested Parameters

### ✅ Good

```python
pipeline.get_params()["classifier__C"]
```

### ❌ Bad

```python
pipeline.get_params()["classifier_C"]
```

---

## 4. Never Use LabelEncoder on Features

### ✅ Correct

```python
OneHotEncoder() → features (X)

LabelEncoder() → target (y)
```

### ❌ Wrong

```python
LabelEncoder() on categorical features
```

---

## 5. Always Scale Before PCA

### ✅ Correct

```text
StandardScaler()
        ↓
       PCA()
```

### ❌ Wrong

```text
PCA()
without scaling
```

---

# 🔧 Parameter Tuning Quick Reference

| Model | Parameter | Example Values | Purpose |
|------|-----------|----------------|---------|
| Logistic Regression | `C` | 0.001–10 | Regularization strength |
| Logistic Regression | `max_iter` | 100, 500, 1000 | Training iterations |
| Random Forest | `n_estimators` | 50, 100, 200 | Number of trees |
| Random Forest | `max_depth` | 5, 10, None | Tree depth |
| SVM | `C` | 0.1, 1, 10 | Regularization |
| SVM | `kernel` | linear, rbf | Kernel function |

---

# 📊 Scaler Decision Guide

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

---

# 🎯 Feature Selection Decision Guide

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

---

# 💡 Pro Tips

## Tip 1: Visualize Pipelines

```python
from sklearn import set_config

set_config(display="diagram")
```

---

## Tip 2: Handle Unknown Categories

```python
OneHotEncoder(handle_unknown="ignore")
```

---

## Tip 3: Avoid Polynomial Bias Features

```python
PolynomialFeatures(
    degree=2,
    include_bias=False
)
```

---

## Tip 4: Keep Sparse Matrices for Memory Efficiency

```python
encoded = encoder.fit_transform(data)
```

Avoid converting sparse matrices unless necessary:

```python
encoded.toarray()
```

---

# 📦 Required Imports

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
from sklearn.ensemble import RandomForestClassifier

# Model Selection
from sklearn.model_selection import train_test_split, GridSearchCV
```

---

# 📝 Summary: When to Use What

| Task | Best Tool |
|------|-----------|
| Build reusable workflows | `Pipeline()` |
| Quick prototypes | `make_pipeline()` |
| Mixed data preprocessing | `ColumnTransformer()` |
| Custom transformations | `FunctionTransformer()` |
| Find parameters | `get_params()` |
| Update parameters | `set_params()` |
| Handle missing values | `SimpleImputer()` |
| Scale normal data | `StandardScaler()` |
| Scale data with outliers | `RobustScaler()` |
| Encode categories | `OneHotEncoder()` |
| Encode targets | `LabelEncoder()` |
| Create polynomial features | `PolynomialFeatures()` |
| Remove constant features | `VarianceThreshold()` |
| Select top features | `SelectKBest()` |
| Model-based selection | `SelectFromModel()` |
| Recursive selection | `RFE()` / `RFECV()` |
| Reduce dimensions | `PCA()` |
| Search feature subsets | `SequentialFeatureSelector()` |

---

## 🚀 Final Takeaway

Building strong machine learning models is not only about choosing the right algorithm.

A professional workflow requires:

✅ Clean preprocessing  
✅ Proper feature selection  
✅ Avoiding data leakage  
✅ Reproducible pipelines  
✅ Efficient model optimization  

Use the right Scikit-Learn tool for the right problem, and focus on the features that truly matter.

**Part 2 Coming Soon: Model Evaluation, Cross-Validation, Hyperparameter Tuning & Ensemble Methods 📊**
````
