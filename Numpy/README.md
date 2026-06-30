```markdown
# 📊 NumPy Quick Reference Table (50 Essential Commands)

A concise reference of 50 important NumPy functions grouped by category.

| # | Command | Category | Description |
|---:|---------|----------|-------------|
| 1 | `np.ufunc.reduce()` | Universal Functions | Apply ufunc reduction along an axis |
| 2 | `np.max()` | Statistics | Find maximum value in an array |
| 3 | `np.min()` | Statistics | Find minimum value in an array |
| 4 | `np.argmax()` | Statistics | Return indices of maximum values |
| 5 | `np.argmin()` | Statistics | Return indices of minimum values |
| 6 | `np.nanmax()` | Statistics | Find maximum while ignoring NaN values |
| 7 | `np.nanmin()` | Statistics | Find minimum while ignoring NaN values |
| 8 | `np.mean()` | Statistics | Compute arithmetic mean |
| 9 | `np.median()` | Statistics | Compute median |
| 10 | `np.std()` | Statistics | Compute standard deviation |
| 11 | `np.var()` | Statistics | Compute variance |
| 12 | `np.sum()` | Statistics | Sum array elements |
| 13 | `np.prod()` | Statistics | Product of array elements |
| 14 | `np.cumsum()` | Statistics | Compute cumulative sum |
| 15 | `np.cumprod()` | Statistics | Compute cumulative product |
| 16 | `np.einsum()` | Advanced | Einstein summation convention |
| 17 | `np.einsum_path()` | Advanced | Optimize computation path for `einsum()` |
| 18 | `np.matmul()` | Linear Algebra | Matrix multiplication |
| 19 | `np.dot()` | Linear Algebra | Dot product of arrays |
| 20 | `np.linalg.det()` | Linear Algebra | Compute matrix determinant |
| 21 | `np.linalg.inv()` | Linear Algebra | Compute matrix inverse |
| 22 | `np.linalg.eig()` | Linear Algebra | Compute eigenvalues and eigenvectors |
| 23 | `np.linalg.svd()` | Linear Algebra | Singular Value Decomposition (SVD) |
| 24 | `np.linalg.solve()` | Linear Algebra | Solve systems of linear equations |
| 25 | `np.random.rand()` | Random | Generate random numbers in `[0, 1)` |
| 26 | `np.random.randint()` | Random | Generate random integers |
| 27 | `np.random.normal()` | Random | Generate values from a normal distribution |
| 28 | `np.random.seed()` | Random | Set the random seed |
| 29 | `np.random.choice()` | Random | Randomly sample from an array |
| 30 | `np.random.permutation()` | Random | Generate a random permutation |
| 31 | `np.ma.masked_array()` | Masked Arrays | Create a masked array |
| 32 | `np.ma.masked_where()` | Masked Arrays | Apply a mask based on a condition |
| 33 | `np.ma.masked_invalid()` | Masked Arrays | Mask invalid values (`NaN`, `Inf`) |
| 34 | `np.r_` | Indexing | Concatenate along the first axis |
| 35 | `np.c_` | Indexing | Concatenate along the second axis |
| 36 | `np.s_` | Indexing | Build slice/index tuples |
| 37 | `np.nonzero()` | Indexing | Return indices of non-zero elements |
| 38 | `np.where()` | Indexing | Conditional element selection |
| 39 | `np.ix_()` | Indexing | Construct an open mesh from sequences |
| 40 | `np.delete()` | Manipulation | Delete elements, rows, or columns |
| 41 | `np.insert()` | Manipulation | Insert elements, rows, or columns |
| 42 | `np.reshape()` | Manipulation | Change the shape of an array |
| 43 | `np.transpose()` | Manipulation | Permute array dimensions |
| 44 | `np.concatenate()` | Manipulation | Join multiple arrays |
| 45 | `np.split()` | Manipulation | Split an array into multiple sub-arrays |
| 46 | `np.broadcast_to()` | Broadcasting | Broadcast an array to a new shape |
| 47 | `np.broadcast()` | Broadcasting | Broadcast multiple arrays together |
| 48 | `np.result_type()` | Type Casting | Determine the resulting data type |
| 49 | `np.promote_types()` | Type Casting | Safely promote compatible data types |
| 50 | `np.copy()` | Utilities | Create a copy of an array |

---

## 📚 Categories

| Category | Commands |
|----------|----------|
| Universal Functions | 1 |
| Statistics | 2–15 |
| Advanced | 16–17 |
| Linear Algebra | 18–24 |
| Random | 25–30 |
| Masked Arrays | 31–33 |
| Indexing | 34–39 |
| Manipulation | 40–45 |
| Broadcasting | 46–47 |
| Type Casting | 48–49 |
| Utilities | 50 |

---

**Total Commands:** **50**  
**Library:** NumPy  
**Language:** Python
```
