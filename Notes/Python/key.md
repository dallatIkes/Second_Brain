The `key` parameter in [[Python]] functions like `min`, `max`, and `sorted` allows you to specify a function that transforms each element before comparison.

---

Example:
```python
import numpy as np

point = np.array([1.0, 2.0])
centroids = {
    0: np.array([0.5, 1.5]),
    1: np.array([3.0, 2.0]),
    2: np.array([1.2, 2.1])
}

nearest = min(centroids.keys(), key=lambda c: np.linalg.norm(point - centroids[c]))
print(nearest)  # Output: 2
```
