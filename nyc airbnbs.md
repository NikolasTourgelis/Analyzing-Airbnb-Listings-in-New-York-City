```python
import pandas as pd
import sqlite3
import matplotlib.pyplot as plt
import seaborn as sns
df = pd.read_csv('AB_NYC_2019.csv')
df.head()
conn = sqlite3.connect('airbnb_nyc.db')
df.to_sql('listings', conn, if_exists='replace', index=False)
query = """
SELECT neighbourhood_group, AVG(price) as average_price
FROM listings
GROUP BY neighbourhood_group
ORDER BY average_price DESC;
"""
avg_price = pd.read_sql_query(query, conn)
avg_price
query = """
SELECT room_type, COUNT(*) as count
FROM listings
GROUP BY room_type
ORDER BY count DESC;
"""
room_counts = pd.read_sql_query(query, conn)
room_counts
sns.barplot(data=avg_price, x='neighbourhood_group', y='average_price')
plt.title('Average Price by Neighborhood Group')
plt.ylabel('Average Price ($)')
plt.xlabel('Neighborhood Group')
plt.show()
sns.barplot(data=room_counts, x='room_type', y='count')
plt.title('Number of Listings by Room Type')
plt.ylabel('Count')
plt.xlabel('Room Type')
plt.show()

```

    C:\Users\Maria\anaconda3\lib\site-packages\pandas\core\computation\expressions.py:21: UserWarning: Pandas requires version '2.8.4' or newer of 'numexpr' (version '2.7.3' currently installed).
      from pandas.core.computation.check import NUMEXPR_INSTALLED
    C:\Users\Maria\anaconda3\lib\site-packages\pandas\core\arrays\masked.py:61: UserWarning: Pandas requires version '1.3.6' or newer of 'bottleneck' (version '1.3.2' currently installed).
      from pandas.core import (
    C:\Users\Maria\anaconda3\lib\site-packages\scipy\__init__.py:146: UserWarning: A NumPy version >=1.16.5 and <1.23.0 is required for this version of SciPy (detected version 1.26.4
      warnings.warn(f"A NumPy version >={np_minversion} and <{np_maxversion}"
    


    
![png](output_0_1.png)
    



    
![png](output_0_2.png)
    



```python

```
