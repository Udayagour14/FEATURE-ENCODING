Feature encoding transforms categorical variables into numerical representations suitable for machine learning algorithms.
Several techniques are available in Python using Pandas and Scikit-learn but here we are using two `1.Label encoding 2.One hot encoding`
# Using pandas only
### 1️⃣ Label Encoding
### Label encoding converts categorical values into integer values. Useful for ordinal data (e.g., low < medium < high).
```python
import pandas as pd

# Sample Data
df = pd.DataFrame({'Category': ['Red', 'Blue', 'Green', 'Blue', 'Red']})

# Assign unique integer values
df['Category_Encoded'] = df['Category'].astype('category').cat.codes

print(df)
```
| Category | Category_Encoded |
|----------|-----------------|
| Red      | 2               |
| Blue     | 0               |
| Green    | 1               |
| Blue     | 0               |
| Red      | 2               |
```


