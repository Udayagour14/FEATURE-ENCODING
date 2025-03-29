Feature encoding transforms categorical variables into numerical representations suitable for machine learning algorithms.
Several techniques are available in Python using Pandas and Scikit-learn but here we are using two `1.Label encoding 2.One hot encoding`
# A.Using pandas only
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


## 2️⃣ One-Hot Encoding
# One-hot encoding creates separate binary (0/1) columns for each category.

### ✅ Example using pd.get_dummies()
```python
df_ohe = pd.get_dummies(df, columns=['Category'])
print(df_ohe)
```
`Removes the ordinal relationship between categories.
pd.get_dummies(df, drop_first=True) can be used to reduce dimensions and avoid multicollinearity. it drop last column as for example if two columns are 0 than third columns will be 1`

| Category_Blue | Category_Green | Category_Red |
|--------------|---------------|-------------|
| 0            | 0             | 1           |
| 1            | 0             | 0           |
| 0            | 1             | 0           |
| 1            | 0             | 0           |
| 0            | 0             | 1           |

# B.Using  Scikit-learn
### 1️⃣ Label Encoding
```python
import pandas as pd
from sklearn.preprocessing import LabelEncoder

# Sample Data
data = {'Category': ['Red', 'Blue', 'Green', 'Blue', 'Red']}
df = pd.DataFrame(data)

# Apply Label Encoding
encoder = LabelEncoder()
df['Category_Encoded'] = encoder.fit_transform(df['Category'])

print(df)
```
## 2️⃣ One-Hot Encoding
```python
from sklearn.preprocessing import OneHotEncoder

# Initialize OneHotEncoder
encoder = OneHotEncoder(sparse=False)  # sparse=False returns a NumPy array

# Fit and Transform Data
encoded_array = encoder.fit_transform(df[['Color']])  # Input must be 2D (DataFrame or array)

# Convert to DataFrame
df_encoded = pd.DataFrame(encoded_array, columns=encoder.get_feature_names_out(['Color']))

print(df_encoded)
```
| Color_Blue | Color_Green | Color_Red |
|------------|------------|-----------|
| 0.0        | 0.0        | 1.0       |
| 1.0        | 0.0        | 0.0       |
| 0.0        | 1.0        | 0.0       |
| 1.0        | 0.0        | 0.0       |
| 0.0        | 0.0        | 1.0       |

#### Avoiding Dummy Variable Trap (Drop First Column)
The dummy variable trap happens when one column is redundant because it can be derived from others.
`example`
If Color_Blue, Color_Green, and Color_Red exist, we only need two of them:
If Color_Blue = 0 and Color_Green = 0, then the color must be Red.
One column is unnecessary.

```python
encoder = OneHotEncoder(sparse=False, drop='first')
encoded_array = encoder.fit_transform(df)
df_encoded = pd.DataFrame(encoded_array, columns=encoder.get_feature_names_out(['Color', 'Size']))
print(df_encoded)
```






