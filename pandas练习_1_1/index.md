# Pandas练习_1_1


# Ex1 - Getting and Knowing your Data

### Step 1. Go to https://www.kaggle.com/openfoodfacts/world-food-facts/data  / 从该网址下载源数据，我已经上传至百度网盘，方便没有kaggle账号的朋友下载。

```
链接：https://pan.baidu.com/s/1UUwCazrWudx6q_RYs4mHww 
提取码：3fmq
```



### Step 2. Download the dataset to your computer and unzip it.  / 下载数据集并解压，上面百度网盘已经是解压的数据集。



### Step 3. Use the tsv file and assign it to a dataframe called food / 读取tsv文件到dataframe，并命名为food

```python
import pandas as pd 
import numpy as np 

food = pd.read_csv('D:/Python/pandas_exercises/01_Getting_&_Knowing_Your_Data/World Food Facts/en.openfoodfacts.org.products.tsv', sep ='\t')
# 使用的是read_csv, 括号中是数据集存储的路径，sep为分隔符
```



### Step 4. See the first 5 entries 读取前5行数据

```python
food.head(5)
```

[food.head](https://raw.githubusercontent.com/imscba/PicGoimg/master/img/head.png)



### Step 5. What is the number of observations in the dataset? / 数据集一共有多少条记录

```python
# Solution 1
food.shape[0]

356027
```

```python
# Solution 2
food.shape

(356027, 163)
```



### Step 6. What is the number of columns in the dataset? /  数据集一共多少列

```python
# Solution 1
food.shape[1]

163
```

```python
# Solution 2
food.shape

(356027, 163)
```

```python
# Solution 3
food.info()

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 356027 entries, 0 to 356026
Columns: 163 entries, code to water-hardness_100g
dtypes: float64(107), object(56)
memory usage: 442.8+ MB
```



### Step 7. Print the name of all the columns. / 输出所有列名

```python
food.columns

Index(['code', 'url', 'creator', 'created_t', 'created_datetime',
       'last_modified_t', 'last_modified_datetime', 'product_name',
       'generic_name', 'quantity',
       ...
       'fruits-vegetables-nuts_100g', 'fruits-vegetables-nuts-estimate_100g',
       'collagen-meat-protein-ratio_100g', 'cocoa_100g', 'chlorophyl_100g',
       'carbon-footprint_100g', 'nutrition-score-fr_100g',
       'nutrition-score-uk_100g', 'glycemic-index_100g',
       'water-hardness_100g'],
      dtype='object', length=163)
```



### Step 8. What is the name of 105th column? / 第105列的列名

```python
food.columns[104]

'-glucose_100g'
```



### Step 9. What is the type of the observations of the 105th column? / 第105列观测值的数据类型

```python
# Solution 1
food.dtypes[''-glucose_100g'']

dtype('float64')
```

```python
# Solution 2
food.dtypes[food.columns[104]]

dtype('float64')
```



### Step 10. How is the dataset indexed? / 数据集是如何索引的

```python
food.index
```

```
RangeIndex(start=0, stop=356027, step=1)
```



### Step 11. What is the product name of the 19th observation? / 第19条观测值的商品名称

```python
food.values[18][7] #第19条记录第8列的内容，解决方案是根据前五条记录寻找商品名的列数在第8列，然后查找第19行，第8列的内容
```

```
'Lotus Organic Brown Jasmine Rice'
```


