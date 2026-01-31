# Retail_Sales_Analytics.PY
import pandas as pd
import matplotlib.pyplot as plt


data = {
    "order_id": [101,102,103,104,105,106,107],
    "order_date": pd.to_datetime([
        "2024-01-01","2024-01-02","2024-01-03",
        "2024-01-04","2024-01-05","2024-01-06","2024-01-07"
    ]),
    "product": ["Laptop","Mobile","Shoes","TV","Jeans","Laptop","Shoes"],
    "category": ["Electronics","Electronics","Fashion","Electronics","Fashion","Electronics","Fashion"],
    "region": ["South","North","East","West","South","North","West"],
    "sales": [50000,30000,5000,40000,7000,52000,6000]
}

df = pd.DataFrame(data)
df

df.groupby("category")["sales"].sum()
df.groupby("region")["sales"].sum()
df.groupby("product")["sales"].sum().sort_values(ascending=False).head(3)

df.groupby(["category", "product"])["sales"].sum().reset_index() \
  .sort_values(["category", "sales"], ascending=[True, False]) \
  .groupby("category").head(1)

df.groupby("order_date")["sales"].sum()
df.groupby("category")["sales"].sum().plot(kind="bar", title="Sales by Category")
plt.show()


