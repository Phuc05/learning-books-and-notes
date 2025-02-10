### **Hyperparameters in K-Nearest Neighbors (KNN) Classification**

The **K-Nearest Neighbors (KNN)** algorithm is a simple and effective machine learning method for classification. It relies on hyperparameters to define its behavior and performance. These hyperparameters must be set before training the model, as they control the structure and working of the algorithm.

Below are the main hyperparameters in **KNN classification**:

---

### **1. Number of Neighbors (`k`)**
- **Description**: This is the most critical hyperparameter. It defines the number of neighbors to consider when making a prediction.
- **Effect**:
  - A smaller `k` (e.g., 1 or 3):
    - Model becomes highly sensitive to noise in the data.
    - It can lead to overfitting, as predictions rely heavily on the nearest neighbors.
  - A larger `k` (e.g., 15 or 20):
    - Model smoothens predictions and reduces sensitivity to noise.
    - It may lead to underfitting, as the prediction considers more distant neighbors, which might not be relevant.
- **Best Practice**:
  - Choose `k` using cross-validation. A typical starting point is `k = √n`, where `n` is the number of data points in the training set.

---

### **2. Distance Metric (`metric`)**
- **Description**: Determines how the distance between data points is calculated.
- **Common Options**:
  - **Euclidean Distance** (default in most libraries):
    - \( \sqrt{\sum (x_i - y_i)^2} \)
    - Works well in continuous, non-correlated feature spaces.
  - **Manhattan Distance**:
    - \( \sum |x_i - y_i| \)
    - Useful for high-dimensional or grid-like data.
  - **Minkowski Distance** (generalization of Euclidean and Manhattan):
    - \( \left( \sum |x_i - y_i|^p \right)^{1/p} \)
    - Controlled by the hyperparameter `p`.
  - **Cosine Similarity**:
    - Measures the angle between two vectors (not their magnitude).
    - Useful for text or high-dimensional sparse data.
- **Effect**:
  - Different metrics capture relationships between data differently, which can impact performance.
- **Best Practice**:
  - Test multiple distance metrics during hyperparameter tuning to identify the best one for your dataset.

---

### **3. Weighting of Neighbors (`weights`)**
- **Description**: Determines how the influence of each neighbor is weighted.
- **Common Options**:
  - **Uniform Weights**:
    - All neighbors contribute equally to the prediction.
    - Suitable when neighbors are equally relevant.
  - **Distance Weights**:
    - Closer neighbors have higher influence on the prediction.
    - Useful when nearby neighbors are more likely to share the same class.
- **Effect**:
  - Distance weighting can improve performance for datasets where closer neighbors are more important than distant ones.
- **Best Practice**:
  - Use `weights='distance'` when data points farther away are less likely to belong to the same class.

---

### **4. Algorithm for Nearest Neighbor Search (`algorithm`)**
- **Description**: Determines the method used to compute the nearest neighbors.
- **Options**:
  - **`'brute'`**: Exhaustive search. Useful for small datasets.
  - **`'kd_tree'`**: Tree-based method for low-dimensional data.
  - **`'ball_tree'`**: Similar to `kd_tree` but handles higher dimensions better.
  - **`'auto'`**: Automatically selects the best algorithm based on the dataset.
- **Effect**:
  - Impacts computation time but not the prediction accuracy.
- **Best Practice**:
  - Use `'auto'` unless you have specific knowledge about the dataset.

---

### **5. Leaf Size (`leaf_size`)**
- **Description**: Used in tree-based nearest neighbor algorithms (`kd_tree` or `ball_tree`) to control the size of leaf nodes.
- **Effect**:
  - Smaller leaf size increases precision but takes longer to compute.
  - Larger leaf size decreases computation time but may slightly reduce accuracy.
- **Default**: 30.
- **Best Practice**:
  - Tune this parameter if you're using a tree-based algorithm.

---

### **6. `p` (Power Parameter for Minkowski Distance)**
- **Description**: Determines the type of Minkowski distance metric.
  - \( p = 1 \): Manhattan Distance.
  - \( p = 2 \): Euclidean Distance.
- **Effect**:
  - Influences how distances are calculated.
  - Higher values of `p` make the model sensitive to larger differences.
- **Best Practice**:
  - Use cross-validation to determine the best value of `p`.

---

### **Tuning Hyperparameters**
Hyperparameters in KNN can be tuned using:
1. **Grid Search**:
   ```python
   from sklearn.model_selection import GridSearchCV
   from sklearn.neighbors import KNeighborsClassifier

   knn = KNeighborsClassifier()
   param_grid = {
       'n_neighbors': [3, 5, 7, 9],
       'weights': ['uniform', 'distance'],
       'metric': ['euclidean', 'manhattan', 'minkowski']
   }
   grid_search = GridSearchCV(knn, param_grid, cv=5)
   grid_search.fit(X_train, y_train)
   print(grid_search.best_params_)
   ```

2. **Random Search**:
   - Faster for larger parameter spaces.

---

### **Summary**
| **Hyperparameter**     | **Description**                                   | **Default Value**   |
|-------------------------|--------------------------------------------------|---------------------|
| `n_neighbors`           | Number of neighbors to consider (`k`).           | 5                   |
| `weights`               | Weighting method for neighbors.                 | `'uniform'`         |
| `metric`                | Distance metric (e.g., `'euclidean'`, `'manhattan'`). | `'minkowski'`       |
| `algorithm`             | Algorithm for nearest neighbor search.          | `'auto'`            |
| `leaf_size`             | Size of leaf nodes in tree-based algorithms.     | 30                  |
| `p`                     | Power parameter for Minkowski distance.          | 2                   |

By tuning these hyperparameters appropriately, you can significantly improve the performance of your KNN model.