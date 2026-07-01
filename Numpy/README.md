# 🚀 NumPy Unleashed: 50 Essential Commands Every Data Scientist Must Know

*A comprehensive quick-reference guide to the most powerful NumPy functions for data science and scientific computing.*

---

[![Medium](https://img.shields.io/badge/Medium-@tararasti-black?style=for-the-badge&logo=medium)](https://medium.com/@tararasti)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-@tararasti-blue?style=for-the-badge&logo=linkedin)](https://linkedin.com/in/tararasti)
[![NumPy](https://img.shields.io/badge/NumPy-v1.24+-013243?style=for-the-badge&logo=numpy)](https://numpy.org/)
[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python)](https://python.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

---

## 📖 Table of Contents

- [🎯 Why This Guide?](#-why-this-guide)
- [📊 Quick Reference Table](#-quick-reference-table)
- [📚 Categories Overview](#-categories-overview)
- [💡 Pro Tips](#-pro-tips)
- [🔗 Connect With Me](#-connect-with-me)

---

## 🎯 Why This Guide?

Most data scientists use only **20%** of NumPy's capabilities — the basics like `array()`, `reshape()`, and `mean()`. But the **real power** lies in the remaining 80%: advanced indexing, broadcasting, linear algebra, and sophisticated reductions that can turn your code from **"good enough"** to **"lightning fast."**

### What You'll Find Here

- ✅ **50 carefully curated commands** — each one battle-tested in real data science projects
- ✅ **Clear categorization** — find the right function when you need it
- ✅ **Practical descriptions** — understand what each command does at a glance
- ✅ **Common use cases** — know when to reach for each function

### Who This Is For

| Level | What You'll Gain |
|-------|------------------|
| 🐣 **Beginners** | A roadmap of what to learn next |
| 👩‍💻 **Intermediate** | Bridge the gap between "knowing" and "mastering" |
| 🏆 **Advanced** | A quick reference for those rarely-used-but-powerful functions |

---

## 📊 Quick Reference Table

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

## 📚 Categories Overview

| # | Category | Commands | Use Cases |
|---|----------|----------|-----------|
| 1 | **Universal Functions** | 1 | Element-wise operations with reduction capabilities |
| 2 | **Statistics** | 2–15 | Data summarization, analysis, and exploration |
| 3 | **Advanced** | 16–17 | Complex tensor operations and optimization |
| 4 | **Linear Algebra** | 18–24 | Matrix operations, ML algorithms, physics simulations |
| 5 | **Random** | 25–30 | Simulation, random sampling, reproducibility |
| 6 | **Masked Arrays** | 31–33 | Handling missing data elegantly |
| 7 | **Indexing** | 34–39 | Advanced data selection and extraction |
| 8 | **Manipulation** | 40–45 | Reshaping and transforming arrays |
| 9 | **Broadcasting** | 46–47 | Efficient operations without loops |
| 10 | **Type Casting** | 48–49 | Type safety and optimization |
| 11 | **Utilities** | 50 | Creating independent copies |

---

## 💡 Pro Tips

### ⚡ Performance Optimization
```python
# ✅ DO THIS: Use vectorized operations
result = arr1 + arr2

# ❌ DON'T DO THIS: Use Python loops
result = [arr1[i] + arr2[i] for i in range(len(arr1))]
```

### 🎲 Reproducibility
```python
# Always set the seed for reproducible random results
np.random.seed(42)
```

### 🛡️ Handling Missing Data
```python
# Use masked arrays instead of deleting data
masked = np.ma.masked_where(arr < 0, arr)
```

### 🧠 Memory Efficiency
```python
# Use broadcasting instead of creating large arrays
broadcasted = np.broadcast_to(arr, (1000, 1000))
```

---

## 🔗 Connect With Me

### 📝 **Medium Articles**
I write practical tutorials on **Data Science, Machine Learning, Python, and NumPy**. Follow me for hands-on guides and real-world projects.

👉 **[Read my articles on Medium](https://medium.com/@tararasti)**

### 🤝 **LinkedIn**
Let's connect! I share daily insights, project updates, and learning resources for the data science community.

👉 **[Connect with me on LinkedIn](https://linkedin.com/in/tararasti)**

### 📂 **GitHub**
Explore my repositories for more guides, notebooks, and cheat sheets.

👉 **[Follow me on GitHub](https://github.com/tararasti)**

---

## 📋 How to Use This Repository

1. **Bookmark this page** — you'll come back to it often!
2. **Share with your team** — make it your team's NumPy reference
3. **Practice each command** — try them in your own projects
4. **Customize for your needs** — add your own frequently used commands

---

## 🤝 Contributing

Found a mistake? Have a suggestion for a command that should be included?

1. Open an issue
2. Submit a pull request
3. Star this repository ⭐

---

## 📄 License

This project is open source and available under the **MIT License**.

---

## 🙏 Acknowledgments

- **NumPy Team** — for creating this incredible library
- **The Data Science Community** — for continuous knowledge sharing
- **You** — for reading and using this guide!

---

## ⭐ If you found this helpful...

- ⭐ **Star this repository** on GitHub
- 📝 **Share it** with your data science colleagues
- 🔔 **Follow me** on Medium and LinkedIn for more content

---

## 🚀 Summary

| Metric | Value |
|--------|-------|
| **Commands Covered** | 50 |
| **Categories** | 11 |
| **Use Cases** | Data Science, ML, Scientific Computing |
| **Language** | Python 3.8+ |
| **Library** | NumPy 1.24+ |

---

> 💬 *"NumPy is not just a library — it's a way of thinking about data. Master these commands, and you master computational thinking."*

---

**Happy NumPy Coding! 🚀**

---

[![GitHub](https://img.shields.io/badge/GitHub-@tararasti-181717?style=for-the-badge&logo=github)](https://github.com/tararasti)
[![Medium](https://img.shields.io/badge/Medium-@tararasti-black?style=for-the-badge&logo=medium)](https://medium.com/@tararasti)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-@tararasti-blue?style=for-the-badge&logo=linkedin)](https://linkedin.com/in/tararasti)
