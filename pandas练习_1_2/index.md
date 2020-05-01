# Pandas练习_1_2


# Ex2 - Getting and Knowing your Data

This time we are going to pull data directly from the internet. Special thanks to: https://github.com/justmarkham for sharing the dataset and materials.

### Step 1. Import the necessary libraries / 导入必要的包

```python
import pandas as pd
import numpy as np
```

### Step 2. Import the dataset from this [address](https://raw.githubusercontent.com/justmarkham/DAT8/master/data/chipotle.tsv). / 导入数据

### Step 3. Assign it to a variable called chipo. 数据命名为chipo

```python
url = "https://raw.githubusercontent.com/justmarkham/DAT8/master/data/chipotle.tsv"
chipo = pd.read_csv(url, sep = '\t')
```

### Step 4. See the first 10 entries / 查看前10条记录

```python
chipo.head(10)
```

|      | order_id | quantity | item_name                             | choice_description                                | item_price |
| ---- | -------- | -------- | ------------------------------------- | ------------------------------------------------- | ---------- |
| 0    | 1        | 1        | Chips and Fresh Tomato Salsa          | NaN                                               | $2.39      |
| 1    | 1        | 1        | Izze                                  | [Clementine]                                      | $3.39      |
| 2    | 1        | 1        | Nantucket Nectar                      | [Apple]                                           | $3.39      |
| 3    | 1        | 1        | Chips and Tomatillo-Green Chili Salsa | NaN                                               | $2.39      |
| 4    | 2        | 2        | Chicken Bowl                          | [Tomatillo-Red Chili Salsa (Hot), [Black Beans... | $16.98     |
| 5    | 3        | 1        | Chicken Bowl                          | [Fresh Tomato Salsa (Mild), [Rice, Cheese, Sou... | $10.98     |
| 6    | 3        | 1        | Side of Chips                         | NaN                                               | $1.69      |
| 7    | 4        | 1        | Steak Burrito                         | [Tomatillo Red Chili Salsa, [Fajita Vegetables... | $11.75     |
| 8    | 4        | 1        | Steak Soft Tacos                      | [Tomatillo Green Chili Salsa, [Pinto Beans, Ch... | $9.25      |
| 9    | 5        | 1        | Steak Burrito                         | [Fresh Tomato Salsa, [Rice, Black Beans, Pinto... | $9.25      |

### Step 5. What is the number of observations in the dataset? / 一共多少条数据

```python
# Solution 1
chipo.shape[0] 
```

```
4622
```



```python
# Solution 2
chipo.info()
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 4622 entries, 0 to 4621
Data columns (total 5 columns):
order_id              4622 non-null int64
quantity              4622 non-null int64
item_name             4622 non-null object
choice_description    3376 non-null object
item_price            4622 non-null object
dtypes: int64(2), object(3)
memory usage: 180.7+ KB
```

### Step 6. What is the number of columns in the dataset?  / 数据集一共有几列

```python
chipo.shape[1]
```

```
5
```

### Step 7. Print the name of all the columns. / 输出所有列名

```python
chipo.columns
```

```
Index(['order_id', 'quantity', 'item_name', 'choice_description',
       'item_price'],
      dtype='object')
```

### Step 8. How is the dataset indexed?  /数据集是如何索引的

```python
chipo.index
```

```
RangeIndex(start=0, stop=4622, step=1)
```

### Step 9. Which was the most-ordered item? / 购买最多的商品

```python
c = chipo.groupby(item_name)
c = c.sum()
c = c.sort_values('quantity', ascending = False)
c.head(1)
```

|               | order_id | quantity | item_price |
| :-----------: | :------: | :------: | :--------: |
| **item_name** |          |          |            |
| Chicken Bowl  |  713926  |   761    |  7342.73   |

### Step 10. For the most-ordered item, how many items were ordered?  / 购买最多的商品共有多少

```python
c = chipo.groupby('item_name')
c = c.sum()
c = c.sort_value('quantity', ascending = False)
c.head(1)
```

|               | order_id | quantity | item_price |
| :-----------: | :------: | :------: | :--------: |
| **item_name** |          |          |            |
| Chicken Bowl  |  713926  |   761    |  7342.73   |

### Step 11. What was the most ordered item in the choice_description column?  /  有choice_description列的商品,购买最多的是什么

```python
c = chipo.groupby('choice_description')
c = c.sum()
c = c.sort_values('choice_description', ascending = False)
c.head(1)
```

|                        | order_id | quantity |
| :--------------------: | :------: | :------: |
| **choice_description** |          |          |
|      [Diet Coke]       |  123455  |   159    |

### Step 12. How many items were ordered in total? / 一共购买了多少商品

```python
item_ordered = chipo.quantity.sum()
item_ordered
```

```
4972
```

### Step 13. Turn the item price into a float /将商品价格转换为浮点型

#### Step 13.a. Check the item price type / 首先检查原价格的数据类型

```python
chipo.item_price.dtype
```

```
dtype('0')
```

#### Step 13.b. Create a lambda function and change the type of item price / 创建lambda函数来转换价格的数据类型

```python
dollarizer = lambda x: float(x)
chipo.item_price = chipo.item_price.apply(dollarizer)
```

#### Step 13.c. Check the item price type 再次检查价格的数据类型

```python
chipo.item_price.dtype
```

```
dtype('float64')
```

### Step 14. How much was the revenue for the period in the dataset? /当前数据集中的总收入是多少

```python
revenue = (chipo['quantity']* chipo['item_price']).sum()
print('Revenue is $' + str(round(revenue, 2))
```



```
Revenue is $39237.02
```

### Step 15. How many orders were made in the period? /当前数据集中一共有多少订单

```python
orders = chipo.order_id.value_counts().count()
orders
```

```
1834
```

### Step 16. What is the average revenue amount per order?  / 每单的平均收入

```python
# Solution 1
revenue = (chipo['quantity']* chipo['item_price']).sum()
order_in_total = chipo.order_id.value_counts().count()
revenue_avg = revenue/order_in_total
revenue_avg
# 自己想出来的最原始的办法
```

```python
# Solution 2
chipo['revenue'] = chipo['quantity'] * chipo['item_price']
order_grouped = chipo.groupby(by=['order_id']).sum()
order_gouped.mean()['revenue']
# 我自己还没搞懂
```

```python
# Solution 3
chipo.groupby(by=['order_id']).sum().mean()['revenue']
```

```python
21.394231188658654
```

### Step 17. How many different items are sold? /一共订购了多少不同种类的商品

```
chipo.item_name.value_counts().count()
```

```
50
```


