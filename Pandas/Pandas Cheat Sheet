# 🐼 ULTIMATE PANDAS MASTERY CHEAT SHEET
### *The Battle-Tested Toolkit for Data Wrangling Warriors*

---

## 📍 PAGE 1: Advanced Indexing & Selection

| Method | Vibe 💫 | Pro Tip 🎯 | Code Snippet ⚡ |
|--------|---------|------------|-----------------|
| `df.set_index('col')` | *Your DataFrame's new identity* | Use `inplace=True` only when memory matters; else chain | `df.set_index('date', inplace=True)` |
| `df.reset_index()` | *The "take me back" button* | Use `drop=True` to discard old index entirely | `df.reset_index(drop=True, inplace=True)` |
| `df.reindex(new_labels)` | *Match the new guest list* | Perfect for aligning time-series to uniform dates | `df.reindex(pd.date_range('2024-01-01', periods=10))` |
| `df.reindex_like(other_df)` | *Mirror, mirror on the wall* | Great for aligning two DataFrames before operations | `df1.reindex_like(df2, method='ffill')` |
| `df.xs(key, level=1)` | *X-ray vision for MultiIndex* | The level parameter is your best friend here | `df.xs('2024', level='year', axis=0)` |
| `df.swaplevel(i,j)` | *MultiIndex level shuffle* | Useful before `sort_index()` for reorganization | `df.swaplevel(0,1).sort_index()` |
| `df.droplevel(level)` | *Lose the baggage* | Clean up MultiIndex columns before export | `df.droplevel(1, axis=1)` |
| `df.sort_index()` | *Alphabetical order for your labels* | `ascending=False` for reverse chronological | `df.sort_index(axis=1, ascending=True)` |
| `df.take(indices)` | *Pick by position, not label* | Faster than `.iloc` for known positions | `df.take([0,2,4], axis=0)` |
| `df.lookup(row, col)` | ⚠️ DEPRECATED - *Read the room* | Use `.loc` with arrays instead | `df.loc[row, col]` |
| `df.first_valid_index()` | *The first light in the tunnel* | Great for finding data start dates | `df.first_valid_index()` |
| `df.last_valid_index()` | *The last stand* | Find where your data ends | `df.last_valid_index()` |

---

## 📍 PAGE 2: Advanced Missing Data Handling

| Method | Vibe 💫 | Pro Tip 🎯 | Code Snippet ⚡ |
|--------|---------|------------|-----------------|
| `df.fillna(value)` | *The great imputator* | Use `limit` parameter to avoid over-filling | `df.fillna(method='ffill', limit=2)` |
| `df.ffill()` | *Forward march!* | Also `.fillna(method='ffill')` - cleaner syntax | `df.ffill(axis=1)` |
| `df.bfill()` | *Back from the future* | Great for filling leading NAs | `df.bfill(axis=0)` |
| `df.interpolate()` | *The smooth talker* | `method='time'` for time-series interpolation | `df.interpolate(method='cubic')` |
| `df.combine_first(other)` | *The priority merge* | NaN in df1? Fill with df2 values | `df1.combine_first(df2)` |
| `df.dropna()` | *The bouncer* | `how='all'` removes only fully empty rows | `df.dropna(subset=['col'], thresh=5)` |
| `df.isna()` | *The truth serum* | Combine with `.sum()` for missing data dashboard | `df.isna().sum().sort_values(ascending=False)` |
| `df.notna()` | *The positive detective* | Negation of `isna()` | `df[df['col'].notna()]` |
| `df.replace(old, new)` | *The find-and-replace wizard* | Use dict for multiple replacements | `df.replace({'A':1, 'B':2})` |
| `df.mask(condition, value)` | *The conditional shroud* | Opposite of `where()` | `df.mask(df > 100, 0)` |
| `df.where(condition, value)` | *The conditional guardian* | Keep what's true, replace false | `df.where(df < 0, -1)` |
| `df.infer_objects()` | *The type whisperer* | Let pandas detect better dtypes | `df = df.infer_objects()` |

---

## 📍 PAGE 3: Sorting & Ranking

| Method | Vibe 💫 | Pro Tip 🎯 | Code Snippet ⚡ |
|--------|---------|------------|-----------------|
| `df.sort_values('col')` | *The master organizer* | `ascending=False` and `inplace=True` | `df.sort_values(['col1','col2'], ascending=[True,False])` |
| `df.rank()` | *The class ranking* | `method='dense'` for no gaps in ranks | `df['rank'] = df['score'].rank(method='dense')` |
| `df.nlargest(n, 'col')` | *The podium getter* | Faster than sorting then slicing | `df.nlargest(5, 'revenue')` |
| `df.nsmallest(n, 'col')` | *The bottom feeder* | Perfect for finding outliers | `df.nsmallest(3, 'price')` |
| `df.argsort()` | *The order revealer* | Returns indices that would sort | `df['col'].argsort()` |
| `df.idxmax()` | *The champion locator* | Find index of max value | `df['sales'].idxmax()` |
| `df.idxmin()` | *The underdog finder* | Find index of min value | `df['cost'].idxmin()` |
| `df.searchsorted(value)` | *The insertion point* | Only works on sorted Series | `df['date'].searchsorted('2024-06-01')` |
| `pd.factorize(df['col'])` | *The categorizer* | Returns (codes, unique_values) | `codes, uniques = pd.factorize(df['category'])` |

---

## 📍 PAGE 4: GroupBy Mastery

**Mental Model: The Split-Apply-Combine Dance** 🕺
```
DataFrame → [SPLIT by groups] → Apply Function → [COMBINE] → Result
          ↑                      ↑              ↑
    groupby()              .agg/.transform   New DataFrame
```

| Method | Vibe 💫 | Pro Tip 🎯 | Code Snippet ⚡ |
|--------|---------|------------|-----------------|
| `.groupby().agg()` | *The Swiss Army knife* | Pass dict for different aggs per column | `df.groupby('cat').agg({'num':'sum','col':'mean'})` |
| `.groupby().transform()` | *The broadcaster* | Same shape as original - great for normalization | `df['norm'] = df.groupby('cat')['val'].transform('mean')` |
| `.groupby().filter()` | *The bouncer* | Keep groups that meet a condition | `df.groupby('cat').filter(lambda x: x['val'].mean() > 100)` |
| `.groupby().apply()` | *The power user* | Run any custom function per group | `df.groupby('cat').apply(lambda x: x.nlargest(2, 'val'))` |
| `.groupby().cumcount()` | *The counter* | Use for ranking within groups | `df['rank'] = df.groupby('cat').cumcount()` |
| `.groupby().cumsum()` | *The rolling tide* | Running total per group | `df['running'] = df.groupby('cat')['val'].cumsum()` |
| `.groupby().cummax()` | *The all-time high* | Track peak values per group | `df['peak'] = df.groupby('cat')['val'].cummax()` |
| `.groupby().cummin()` | *The low tracker* | Track minimums per group | `df['bottom'] = df.groupby('cat')['val'].cummin()` |
| `.groupby().cumprod()` | *The multiplier* | Running product per group | `df['growth'] = df.groupby('cat')['factor'].cumprod()` |
| `.groupby().ngroup()` | *The group identifier* | Assigns group numbers | `df['group_id'] = df.groupby(['cat1','cat2']).ngroup()` |
| `.groupby().size()` | *The count'em up* | Includes all groups, even empty | `df.groupby('cat').size()` |
| `.groupby().value_counts()` | *The frequency king* | Multi-level counts in one shot | `df.groupby('cat')['subcat'].value_counts()` |
| `.groupby().rolling()` | *The moving target* | Rolling stats per group | `df.groupby('cat')['val'].rolling(3).mean()` |
| `.groupby().expanding()` | *The growing window* | Expanding stats per group | `df.groupby('cat')['val'].expanding().mean()` |

---

## 📍 PAGE 5: Reshaping Data

**Mental Model: The Tidy Data Tango** 💃
```
pivot()   → Widen data (rows → columns)
melt()    → Narrow data (columns → rows)
stack()   → Pivot columns to rows (MultiIndex)
unstack() → Pivot rows to columns (MultiIndex)
explode() → Unroll list-like entries
```

| Method | Vibe 💫 | Pro Tip 🎯 | Code Snippet ⚡ |
|--------|---------|------------|-----------------|
| `df.pivot()` | *The spreadsheet maker* | Only one value per cell | `df.pivot(index='date', columns='var', values='val')` |
| `df.pivot_table()` | *The pivot with personality* | Aggregates duplicates with `aggfunc` | `pd.pivot_table(df, values='val', index='cat', aggfunc='mean')` |
| `df.melt()` | *The melter* | Wide → Long format | `df.melt(id_vars=['id'], value_vars=['col1','col2'])` |
| `df.stack()` | *The compression* | Columns → MultiIndex rows | `df.stack(level=0)` |
| `df.unstack()` | *The expansion* | MultiIndex rows → Columns | `df.unstack(level=-1)` |
| `df.explode('col')` | *The popcorn maker* | Expand list-like entries | `df.explode(['col1','col2'])` |
| `pd.wide_to_long()` | *The dedicated widener* | For complex wide formats | `pd.wide_to_long(df, stubnames=['score'], i='id', j='year')` |
| `pd.get_dummies()` | *The categorical converter* | One-hot encoding | `pd.get_dummies(df['cat'], prefix='cat')` |
| `pd.crosstab()` | *The contingency creator* | Pivot with counts/aggs | `pd.crosstab(df['cat1'], df['cat2'], normalize='index')` |
| `pd.cut()` | *The binner* | Convert continuous to categorical bins | `pd.cut(df['age'], bins=5, labels=['Young','...'])` |
| `pd.qcut()` | *The quantile binner* | Equal-frequency bins | `pd.qcut(df['value'], q=4, labels=['Q1','Q2','Q3','Q4'])` |
| `MultiIndex.from_product()` | *The Cartesian maker* | Create all combos of iterables | `idx = pd.MultiIndex.from_product([['A','B'], [1,2]])` |
| `MultiIndex.from_tuples()` | *The tuple transformer* | Create MultiIndex from tuples | `idx = pd.MultiIndex.from_tuples([('A',1), ('A',2)])` |

---

## 📍 PAGE 6: Combining DataFrames

| Method | Vibe 💫 | Pro Tip 🎯 | Code Snippet ⚡ |
|--------|---------|------------|-----------------|
| `pd.merge(df1, df2)` | *The SQL master* | `how='outer'` to keep all keys | `pd.merge(df1, df2, on='id', how='left')` |
| `df1.join(df2)` | *The neighbor* | Index-based merge by default | `df1.join(df2, how='inner')` |
| `pd.concat([df1, df2])` | *The stacker* | `axis=0` for rows, `axis=1` for columns | `pd.concat([df1, df2], axis=0, ignore_index=True)` |
| `df1.combine(df2, func)` | *The element-wise warrior* | Great for row-wise operations | `df1.combine(df2, lambda x,y: x if x>y else y)` |
| `df1.update(df2)` | *The in-place patcher* | Updates df1 with df2 values (aligns on index) | `df1.update(df2, overwrite=True)` |
| `df1.append(df2)` | ⚠️ DEPRECATED - *The old way* | Use `pd.concat()` instead | `pd.concat([df1, df2])` |
| `df1.align(df2)` | *The synchronizer* | Align two DataFrames to same shape | `df1.align(df2, join='outer')` |
| `pd.merge_asof()` | *The time traveler* | Nearest-time merge | `pd.merge_asof(df1, df2, on='time', direction='forward')` |
| `pd.merge_ordered()` | *The chronological merger* | Merge and sort by key | `pd.merge_ordered(df1, df2, on='date')` |
| `df1.compare(df2)` | *The spot-the-difference* | Show what changed between DataFrames | `df1.compare(df2, align_axis=0)` |

---

## 📍 PAGE 7: Time-Series Operations

**Mental Model: The Temporal Toolkit** ⏰
```
time-series → [RESAMPLE] → New frequency → [FFILL/BFILL] → Clean series
           → [SHIFT]     → Lag/Lead      → [PCT_CHANGE] → Returns
           → [ROLLING]   → Moving stats  → [EWM]        → Exponential weights
```

| Method | Vibe 💫 | Pro Tip 🎯 | Code Snippet ⚡ |
|--------|---------|------------|-----------------|
| `df.rolling(window)` | *The moving wave* | `min_periods` to handle early NAs | `df['rolling_mean'] = df['val'].rolling(7).mean()` |
| `df.expanding()` | *The growing perspective* | Running stats from start | `df['expanding_max'] = df['val'].expanding().max()` |
| `df.ewm(span)` | *The exponential weight* | More weight to recent observations | `df['ewma'] = df['val'].ewm(span=30).mean()` |
| `df.shift(periods)` | *The time machine* | ± periods in time | `df['lag_1'] = df['val'].shift(1)` |
| `df.diff(periods)` | *The change detector* | Difference from previous periods | `df['change'] = df['val'].diff()` |
| `df.pct_change(periods)` | *The growth rate* | Percentage change over periods | `df['returns'] = df['price'].pct_change()` |
| `df.resample('M')` | *The frequency changer* | Aggregates to new frequency | `df.resample('M').mean()` |
| `df.asfreq('D')` | *The fill with frequency* | Set frequency without aggregation | `df.asfreq('D', method='ffill')` |
| `df.between_time('09:00','17:00')` | *The business hours filter* | Filter rows by time | `df.between_time('09:00', '17:00')` |
| `df.at_time('12:00')` | *The exact time picker* | Grab rows at specific time | `df.at_time('12:00:00')` |
| `df.tz_localize('UTC')` | *The time zone setter* | Assign timezone | `df.tz_localize('US/Eastern')` |
| `df.tz_convert('US/Pacific')` | *The time zone converter* | Convert to another timezone | `df.tz_convert('Europe/London')` |
| `pd.infer_freq(df.index)` | *The frequency detective* | Guesses the frequency | `pd.infer_freq(df.index)` |

---

## 📍 PAGE 8: Advanced String Operations

| Method | Vibe 💫 | Pro Tip 🎯 | Code Snippet ⚡ |
|--------|---------|------------|-----------------|
| `df['col'].str.contains()` | *The pattern finder* | `na=False` handles NAs gracefully | `df[df['text'].str.contains('pandas', case=False)]` |
| `df['col'].str.extract()` | *The pattern grabber* | Captures first match | `df['url'].str.extract(r'(https?://[^\s]+)')` |
| `df['col'].str.extractall()` | *The pattern scooper* | Captures all matches | `df['text'].str.extractall(r'(\w+)')` |
| `df['col'].str.findall()` | *The list maker* | Returns list of all matches | `df['text'].str.findall(r'\d+')` |
| `df['col'].str.replace()` | *The text replacer* | Regex support | `df['name'].str.replace(r'\s+', '_')` |
| `df['col'].str.split()` | *The splitter* | `expand=True` creates new DataFrame | `df['name'].str.split(' ', expand=True, n=1)` |
| `df['col'].str.get(i)` | *The indexer* | Get element at position i | `df['list_col'].str.get(0)` |
| `df['col'].str.cat()` | *The concatenator* | Join strings with separator | `df['str1'].str.cat(df['str2'], sep='-')` |

---

## 📍 PAGE 9: Performance & Data Cleaning

| Method | Vibe 💫 | Pro Tip 🎯 | Code Snippet ⚡ |
|--------|---------|------------|-----------------|
| `df.astype('category')` | *The memory saver* | Reduces memory for categorical data | `df['cat'] = df['cat'].astype('category')` |
| `df.convert_dtypes()` | *The smart converter* | Best possible dtypes | `df = df.convert_dtypes()` |
| `df.memory_usage()` | *The memory meter* | Check memory per column | `df.memory_usage(deep=True)` |
| `df.select_dtypes(include=[])` | *The type picker* | Filter columns by dtype | `df.select_dtypes(include=['float64', 'int64'])` |
| `df.pipe(func)` | *The pipeline builder* | Chain custom functions cleanly | `df.pipe(lambda x: x[x['val'] > 0]).pipe(log_transform)` |
| `df.eval('new_col = col1 + col2')` | *The expression evaluator* | Faster than Python operations | `df.eval('total = price * qty')` |
| `df.query('col > 100')` | *The SQL-style filter* | More readable than boolean indexing | `df.query('age > 21 and city == "NYC"')` |
| `df.sample(n)` | *The random sampler* | `frac=0.1` for 10% sample | `df.sample(frac=0.1, random_state=42)` |
| `df.duplicated()` | *The duplicate detector* | `keep='first'`/`'last'`/`False` | `df[df.duplicated(subset=['id'], keep=False)]` |

---

## 🥋 PAGE 10: BLACK BELT BONUS - The Advanced Arsenal

| Tool | Vibe 💫 | When to Use | Code Snippet ⚡ |
|------|---------|-------------|-----------------|
| `DataFrame.style` | *The beautifier* | Make DataFrames presentation-ready | `df.style.highlight_max(color='lightgreen')` |
| `Styler.format` | *The formatter* | Format numbers for display | `df.style.format('{:.2f}')` |
| `Styler.background_gradient` | *The heatmap maker* | Color-code by values | `df.style.background_gradient(cmap='Blues')` |
| `Styler.highlight_max` | *The spotlight* | Highlight maximum values | `df.style.highlight_max(axis=0)` |
| `pd.Grouper` | *The group timer* | Group by time frequencies | `df.groupby(pd.Grouper(key='date', freq='W'))` |
| `pd.IndexSlice` | *The index slicer* | Complex MultiIndex selection | `df.loc[pd.IndexSlice[:, '2024'], :]` |
| `SparseDtype` | *The memory miser* | Store sparse data efficiently | `df['sparse'] = pd.arrays.SparseArray(df['data'])` |
| `CategoricalDtype` | *The category definer* | Custom categorical order | `cat_type = pd.CategoricalDtype(['low','med','high'], ordered=True)` |
| `pd.IntervalIndex` | *The range marker* | Represent intervals | `pd.IntervalIndex.from_breaks([0, 10, 20])` |
| `pd.PeriodIndex` | *The period tracker* | Time periods (quarters, years) | `pd.PeriodIndex(['2024Q1','2024Q2'], freq='Q')` |
| `pd.DatetimeIndex` | *The datetime master* | Explicit datetime index | `pd.DatetimeIndex(df['date'])` |
| `pd.TimedeltaIndex` | *The duration keeper* | Time differences | `pd.TimedeltaIndex(['1 day','2 days'])` |
| `pd.NamedAgg` | *The named aggregator* | Name your aggregation columns | `df.groupby('cat').agg(mean_score=pd.NamedAgg('score', 'mean'))` |
| `.pipe()` | *The chaining master* | Clean code pipeline | `df.pipe(clean_data).pipe(transform_data)` |
| `explode()` with multiple columns | *The multi-unroller* | Explode multiple columns | `df.explode(['col1','col2'])` |
| `pd.json_normalize()` | *The JSON flatteners* | Unnest nested JSON | `pd.json_normalize(json_data, record_path='data')` |
| `df.to_records()` | *The record maker* | DataFrame → NumPy records | `df.to_records(index=True)` |
| `pd.from_records()` | *The record breaker* | Records → DataFrame | `pd.DataFrame.from_records(records)` |
| `df.to_xarray()` | *The dimension shifter* | For multi-dimensional data | `df.to_xarray()` |
| `df.convert_dtypes()` | *The dtype optimizer* | Re-run after operations | `df = df.convert_dtypes()` |

---

## 🎯 Quick Reference: Most Frequently Used Chains

```python
# Data Cleaning Pipeline
(df
 .pipe(load_data)
 .query('age > 0')
 .assign(age_group=lambda x: pd.cut(x['age'], bins=[0,18,65,100]))
 .groupby('age_group')
 .agg(mean_score=('score', 'mean'), count=('score', 'count'))
 .style.background_gradient(cmap='Blues')
)

# Time Series Pipeline
(df
 .set_index('date')
 .resample('D')
 .mean()
 .ffill(limit=5)
 .assign(rolling_mean=lambda x: x['value'].rolling(7).mean())
 .assign(pct_change=lambda x: x['value'].pct_change())
)
```

---

## 💡 The Pandas Philosophy Cheat Sheet

| Principle | Translation | Code Example |
|-----------|-------------|--------------|
| **Vectorization** | Never write Python loops | `df['col'] = df['col'] + 100` ❌ loops ✅ vectorized |
| **Chain It** | Use method chaining for readability | `df.query(...).assign(...).groupby(...).agg(...)` |
| **Dtype Awareness** | Right dtype = Right performance | `astype('category')` for ≤ 50% unique |
| **In-Place Caution** | In-place doesn't always save memory | Use `.copy()` if you mutate |
| **Index Power** | A good index solves 80% of problems | `set_index('date')` before time-series ops |

---

## 📋 Summary: Top 10 Most Important Pandas Methods

| Rank | Method | Why It's Essential |
|------|--------|-------------------|
| 🥇 | `.groupby().agg()` | The foundation of data analysis |
| 🥈 | `.merge()` | The SQL of Python |
| 🥉 | `.pivot_table()` | The Excel of Python |
| 4 | `.loc[]` | The most used indexing method |
| 5 | `.fillna()` | The most used data cleaning method |
| 6 | `.query()` | The readable filter |
| 7 | `.assign()` | The column creator |
| 8 | `.pipe()` | The pipeline builder |
| 9 | `.resample()` | The time-series MVP |
| 10 | `.style` | The report maker |

---

**Your Next Steps:**
1. Copy this markdown content (select all text above from the code block)
2. Use a markdown editor (Typora, Obsidian, or VS Code with markdown preview)
3. Export as PDF or HTML
4. Convert to images using your preferred tool
5. Print or share as visual cheat sheets

This cheat sheet contains **100+ methods** organized into logical categories with examples, pro tips, and mental models. The visual hierarchy and emojis make it scannable and memorable. 🚀
