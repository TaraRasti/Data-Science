# Scikit-Learn Cheat Sheet: 21 Essential Tricks (Part 1)

## 📋 Quick Reference: Chapter 1 - Building Professional ML Workflows

| # | Tool | Purpose | Key Parameters | When to Use |
|---|------|---------|----------------|-------------|
| 1 | Pipeline() | Chain preprocessing + model | List of (name, transformer) tuples | Production workflows with custom step names |
| 2 | make_pipeline() | Quick pipeline shortcut | List of transformers | Prototyping, simple workflows |
| 3 | ColumnTransformer() | Apply different transforms to different columns | (name, transformer, columns) | Mixed numeric + categorical data |
| 4 | FunctionTransformer() | Wrap custom Python functions | func | Custom preprocessing logic |
| 5 | get_params() | View all configurable parameters | None | Finding parameter names for tuning |
| 6 | set_params() | Update pipeline parameters | step__param=value | Applying best parameters from tuning |
| 7 | set_config(display="diagram") | Visualize pipeline in Jupyter | display="diagram" | Debugging, teaching, documentation |

---

## 📋 Quick Reference: Chapter 2 - Data Preprocessing Mastery

| # | Tool | Purpose | Key Parameters | Best For |
|---|------|---------|----------------|----------|
| 8 | SimpleImputer() | Handle missing values | strategy='mean'/'median'/'most_frequent' | Real-world datasets with missing values |
| 9 | StandardScaler() | Standardize to mean=0, std=1 | None | Distance-based models (SVM, KNN, Logistic Regression) |
| 10 | MinMaxScaler() | Scale to [0, 1] range | feature_range=(0, 1) | Neural networks, bounded features |
| 11 | RobustScaler() | Scale using median & IQR | None | Data with outliers |
| 12 | OneHotEncoder() | One-hot encode categories | handle_unknown='ignore' | Categorical features (X) |
| 13 | LabelEncoder() | Encode target labels | None | Target variables (y) ONLY |
| 14 | PolynomialFeatures() | Create polynomial features | degree=2, include_bias=True | Non-linear relationships |

---

## 📋 Quick Reference: Chapter 3 - Feature Selection & Dimensionality Reduction

| # | Tool | Purpose | Key Parameters | When to Use |
|---|------|---------|----------------|-------------|
| 15 | VarianceThreshold() | Remove low-variance features | threshold=0 | Constant/near-constant features |
| 16 | SelectKBest() | Select top K features by statistical test | score_func, k | Hundreds of features, need fast selection |
| 17 | SelectFromModel() | Select features using model importance | estimator, threshold | Model-based importance ranking |
| 18 | RFE() | Recursive feature elimination | estimator, n_features_to_select | Small datasets, interpretability matters |
| 19 | PCA() | Dimensionality reduction | n_components | High-dimensional data, visualization, compression |
| 20 | RFECV() | RFE with cross-validation | estimator, cv, scoring | Unknown optimal feature count |
| 21 | SequentialFeatureSelector() | Greedy feature subset search | estimator, n_features_to_select, direction | Dozens of features, want best combination |

---

## 🚀 Most Common Pipeline Patterns

### Pattern 1: Simple Classification Pipeline
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('classifier', LogisticRegression())
])

pipeline.fit(X_train, y_train)
pipeline.score(X_test, y_test)

### Pattern 2: Mixed Data Types Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.pipeline import Pipeline

numeric_features = ['age', 'income']
categorical_features = ['department', 'country']

preprocessor = ColumnTransformer([
    ('num', StandardScaler(), numeric_features),
    ('cat', OneHotEncoder(handle_unknown='ignore'), categorical_features)
])

pipeline = Pipeline([
    ('preprocessor', preprocessor),
    ('classifier', LogisticRegression())
])

### Pattern 3: Full Preprocessing Pipeline
pipeline = Pipeline([
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler()),
    ('selector', SelectKBest(f_classif, k=10)),
    ('classifier', LogisticRegression())
])

### Pattern 4: Polynomial Features Pipeline
from sklearn.preprocessing import PolynomialFeatures

pipeline = Pipeline([
    ('poly', PolynomialFeatures(degree=2, include_bias=False)),
    ('scaler', StandardScaler()),  # ⚠️ Important!
    ('model', LinearRegression())
])

### Pattern 5: PCA for Dimensionality Reduction
from sklearn.decomposition import PCA

pipeline = Pipeline([
    ('scaler', StandardScaler()),  # ⚠️ Always scale before PCA!
    ('pca', PCA(n_components=0.95)),  # Keep 95% variance
    ('classifier', LogisticRegression())
])

---

## ⚠️ Golden Rules

### 1. Always Use Pipelines
# ✅ GOOD
pipeline = Pipeline([...])
pipeline.fit(X_train, y_train)

# ❌ BAD (Risk of data leakage)
scaler.fit(X)
X_scaled = scaler.transform(X)

### 2. Fit on Train Only, Transform Test
# ✅ GOOD
pipeline.fit(X_train, y_train)
pipeline.transform(X_test)  # or pipeline.predict(X_test)

# ❌ BAD
pipeline.fit(X_train + X_test, y_train + y_test)

### 3. Use Double Underscores for Nested Parameters
# ✅ GOOD
pipeline.get_params()['logisticregression__C']

# ❌ BAD
pipeline.get_params()['logisticregression_C']

### 4. Never LabelEncoder on Features
# ✅ GOOD
OneHotEncoder() for features (X)
LabelEncoder() for target (y)

# ❌ BAD
LabelEncoder() on features (X)

### 5. Scale Before PCA
# ✅ GOOD
StandardScaler() → PCA()

# ❌ BAD
PCA() without scaling

---

## 🔧 Parameter Tuning Quick Reference

### Finding Parameter Names
# Get all parameter names
pipeline.get_params().keys()

# Get specific parameter
pipeline.get_params()['step_name__parameter_name']

# Update parameter
pipeline.set_params(step_name__parameter_name=value)

### Common Parameters to Tune

| Model | Parameter | Range | Description |
|-------|-----------|-------|-------------|
| LogisticRegression | C | [0.001, 0.01, 0.1, 1, 10] | Inverse regularization strength |
| LogisticRegression | max_iter | [100, 500, 1000] | Max iterations for convergence |
| RandomForest | n_estimators | [50, 100, 200] | Number of trees |
| RandomForest | max_depth | [5, 10, None] | Maximum tree depth |
| SVM | C | [0.1, 1, 10] | Regularization parameter |
| SVM | kernel | ['linear', 'rbf'] | Kernel type |

---

## 📊 Scaler Decision Tree

Does your data have outliers?
    ├── Yes → RobustScaler()
    └── No → Does your data need bounded range [0,1]?
        ├── Yes → MinMaxScaler()
        └── No → StandardScaler()

---

## 🎯 Feature Selection Decision Tree

Is your dataset huge (>1000 features)?
    ├── Yes → SelectKBest() or SelectFromModel()
    └── No → Does interpretability matter?
        ├── Yes → RFE() or SequentialFeatureSelector()
        └── No → RFECV() for automatic optimization

---

## 💡 Pro Tips

### Tip 1: Visualize Pipelines
from sklearn import set_config
set_config(display='diagram')  # HTML diagram in Jupyter

### Tip 2: Handle Unknown Categories
OneHotEncoder(handle_unknown='ignore')  # Always use this!

### Tip 3: Remove Bias Column from Polynomial Features
PolynomialFeatures(degree=2, include_bias=False)

### Tip 4: Use Sparse Matrices to Save Memory
# OneHotEncoder returns sparse by default - keep it that way!
encoded = encoder.fit_transform(data)  # Sparse
# encoded.toarray()  # Only if you need to see it

### Tip 5: Always Scale Polynomial Features
Pipeline([
    ('poly', PolynomialFeatures(degree=2)),
    ('scaler', StandardScaler()),  # ⚠️ Important!
    ('model', LinearRegression())
])

---

## 📦 Required Imports Cheat Sheet

# Pipelines
from sklearn.pipeline import Pipeline, make_pipeline
from sklearn.compose import ColumnTransformer

# Preprocessing
from sklearn.preprocessing import (
    StandardScaler, MinMaxScaler, RobustScaler,
    OneHotEncoder, LabelEncoder,
    PolynomialFeatures, FunctionTransformer
)

# Imputation
from sklearn.impute import SimpleImputer

# Feature Selection
from sklearn.feature_selection import (
    VarianceThreshold, SelectKBest, f_classif,
    SelectFromModel, RFE, RFECV, SequentialFeatureSelector
)

# Dimensionality Reduction
from sklearn.decomposition import PCA

# Models
from sklearn.linear_model import LogisticRegression, LinearRegression
from sklearn.ensemble import RandomForestClassifier, RandomForestRegressor

# Model Selection
from sklearn.model_selection import train_test_split, GridSearchCV

# Utilities
from sklearn import set_config

---

## 📝 Summary: When to Use What

| Task | Best Tool |
|------|-----------|
| Build a reusable workflow | Pipeline() |
| Quick prototype | make_pipeline() |
| Mixed numeric + categorical data | ColumnTransformer() |
| Custom transformations | FunctionTransformer() |
| Find parameter names | get_params() |
| Update parameters | set_params() |
| Visualize pipeline | set_config(display='diagram') |
| Handle missing values | SimpleImputer() |
| Scale features (no outliers) | StandardScaler() |
| Scale features (bounded) | MinMaxScaler() |
| Scale features (with outliers) | RobustScaler() |
| Encode categories | OneHotEncoder() |
| Encode target labels | LabelEncoder() |
| Create polynomial features | PolynomialFeatures() |
| Remove constant features | VarianceThreshold() |
| Select top K features | SelectKBest() |
| Model-based selection | SelectFromModel() |
| Recursive elimination | RFE() or RFECV() |
| Reduce dimensionality | PCA() |
| Search feature subsets | SequentialFeatureSelector() |

---

**Save this cheat sheet for quick reference!** 🚀

*Part 2 Coming Soon: Model Evaluation, Cross-Validation, Hyperparameter Tuning & Ensemble Methods* 📊
