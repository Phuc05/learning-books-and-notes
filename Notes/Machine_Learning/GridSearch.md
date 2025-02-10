`GridSearchCV` is a function in the `sklearn.model_selection` module of the Scikit-learn library. It is a powerful tool for performing hyperparameter tuning by systematically searching through a grid of hyperparameter combinations and selecting the one that optimizes the performance of a machine learning model.

---

### Key Features
1. **Grid Search**:
   - It performs an exhaustive search over a specified hyperparameter space for a given estimator (model).
   - Evaluates every combination of hyperparameter values specified in the grid.

2. **Cross-Validation**:
   - It evaluates the model's performance using cross-validation for each combination of hyperparameters, ensuring the model generalizes well to unseen data.

3. **Best Model Selection**:
   - It automatically identifies and fits the model with the best hyperparameter combination to the training data.

4. **Scoring Metrics**:
   - You can specify a custom scoring metric (e.g., accuracy, F1-score, mean squared error) to optimize the model.

---

### Syntax
```python
from sklearn.model_selection import GridSearchCV

grid_search = GridSearchCV(estimator, param_grid, scoring=None, cv=None, n_jobs=None)
```

### Parameters
1. **`estimator`**:
   - The machine learning model to be optimized (e.g., `RandomForestClassifier`, `SVC`, etc.).

2. **`param_grid`**:
   - A dictionary where keys are the hyperparameter names, and values are lists of possible values to try.

   Example:
   ```python
   param_grid = {
       'C': [0.1, 1, 10],
       'kernel': ['linear', 'rbf']
   }
   ```

3. **`scoring`**:
   - The metric to optimize (e.g., `'accuracy'`, `'roc_auc'`, `'neg_mean_squared_error'`).
   - Default: estimator's default score.

4. **`cv`**:
   - The number of cross-validation folds (e.g., `cv=5` for 5-fold cross-validation).

5. **`n_jobs`**:
   - Number of parallel jobs (-1 means using all processors).

---

### Example

#### Step 1: Import Libraries and Data
```python
from sklearn.datasets import load_iris
from sklearn.svm import SVC
from sklearn.model_selection import GridSearchCV

# Load dataset
data = load_iris()
X, y = data.data, data.target
```

#### Step 2: Define Model and Parameter Grid
```python
model = SVC()  # Support Vector Classifier
param_grid = {
    'C': [0.1, 1, 10],
    'kernel': ['linear', 'rbf'],
    'gamma': [1, 0.1, 0.01]
}
```

#### Step 3: Perform Grid Search
```python
grid_search = GridSearchCV(estimator=model, param_grid=param_grid, cv=5, scoring='accuracy', n_jobs=-1)
grid_search.fit(X, y)
```

#### Step 4: Best Parameters and Score
```python
print("Best Parameters:", grid_search.best_params_)
print("Best Score:", grid_search.best_score_)
```

---

### Output Example
If the best parameters were `C=1`, `kernel='rbf'`, and `gamma=0.1`, the output would look like:
```
Best Parameters: {'C': 1, 'gamma': 0.1, 'kernel': 'rbf'}
Best Score: 0.9733
```

---

### Use Case
Hyperparameter tuning is critical for improving model performance. `GridSearchCV` helps to:
1. Automate the tuning process.
2. Prevent overfitting by using cross-validation.
3. Evaluate a model's robustness with different hyperparameter combinations.

It is widely used in machine learning pipelines for optimizing models efficiently.