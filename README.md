# Data-Wrangling-Final-

title: "Will Lynch Data Wrangling Final"
format: html

```{python}
import pandas as pd
import numpy as np
import statsmodels.api as sm
import seaborn as sns
import matplotlib.pyplot as plt
df = pd.read_csv('~/Downloads/Amazon.csv')
```

```{python}
sns.histplot(
    data=df,
    x="TotalAmount",    
    bins=40,
    kde=True,
    color="royalblue",
    alpha=0.5,
    edgecolor="white"
)

plt.title("Distribution of Customer Spending (TotalAmount)", fontsize=14)
plt.xlabel("Total Amount Spent")
plt.ylabel("Number of Orders")

plt.tight_layout()
plt.show()
```

```{python}

revenue_by_category = (
    df.groupby("Category")["TotalAmount"]
      .sum()
      .reset_index()
)


revenue_by_category["Revenue_Millions"] = revenue_by_category["TotalAmount"] / 1_000_000


plt.figure(figsize=(12,6))

sns.barplot(
    data=revenue_by_category,
    x="Revenue_Millions",
    y="Category",
    palette=["#E39A27", "#2C6B9A", "#0F1419"]  
)

plt.title("Total Revenue by Product Category", fontsize=14)
plt.xlabel("Total Revenue (USD, Millions)")
plt.ylabel("Category")

plt.tight_layout()
plt.show()
```


```{python}


purchase_share = (
    df['Category']
    .value_counts(normalize=True)
    .sort_values(ascending=False)
)

purchase_share
```

```{python}
plt.figure(figsize=(12,6))

sns.regplot(
    data=df,
    x="Quantity",
    y="TotalAmount",
    scatter_kws={"alpha": 0.6, "s": 40},
    line_kws={"color": "orange"}
)

plt.title("Does Buying More Items Increase Customer Spending?", fontsize=14)
plt.xlabel("Quantity Purchased")
plt.ylabel("Total Amount Spent ($)")

plt.tight_layout()
plt.show()
```
