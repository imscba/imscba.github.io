# Pandas练习_1_3


# Ex1_3 - Getting and Knowing your Data

This time we are going to pull data directly from the internet. Special thanks to: https://github.com/justmarkham for sharing the dataset and materials.

### Step 1. Import the necessary libraries  / 导入必要的包

```python
import pandas as pd 
import numpy as np 
```



### Step 2. Import the dataset from this [address](https://raw.githubusercontent.com/justmarkham/DAT8/master/data/u.user). / 从该地址导入数据集



### Step 3. Assign it to a variable called users and use the 'user_id' as index / 将数据集命名为'users'，并将‘user_id’作为索引

```python
# Solution 1
url = ('https://raw.githubusercontent.com/justmarkham/DAT8/master/data/u.user')
users = pd.read_table(url, sep = '|', index_col= 'user_id') # 注意这里使用的是read_table,我是看了答案才知道使用table.
```



```python
# Solution 2 上面的答案可以简化,我是受上一篇文章的影响,多定义了url变量
users = pd.read_table('https://raw.githubusercontent.com/justmarkham/DAT8/master/data/u.user',sep = '|', index_col = 'user_id') # sep分隔符需要自己看数据集得到'|'
```



### Step 4. See the first 25 entries / 查看前25行记录

```python
users.head(25)
```



```outcome
	age	gender	occupation	zip_code
user_id				
1	24	M	technician	85711
2	53	F	other	94043
3	23	M	writer	32067
4	24	M	technician	43537
5	33	F	other	15213
6	42	M	executive	98101
7	57	M	administrator	91344
8	36	M	administrator	05201
9	29	M	student	01002
10	53	M	lawyer	90703
11	39	F	other	30329
12	28	F	other	06405
13	47	M	educator	29206
14	45	M	scientist	55106
15	49	F	educator	97301
16	21	M	entertainment	10309
17	30	M	programmer	06355
18	35	F	other	37212
19	40	M	librarian	02138
20	42	F	homemaker	95660
21	26	M	writer	30068
22	25	M	writer	40206
23	30	F	artist	48197
24	21	F	artist	94533
25	39	M	engineer	55107
```



### Step 5. See the last 10 entries / 查看倒数10行记录

```python
user.head(-10) # 我想当然认为这样可以,结果如下,显示的是全部数据
```

```outcome
	age	gender	occupation	zip_code
user_id				
1	24	M	technician	85711
2	53	F	other	94043
3	23	M	writer	32067
4	24	M	technician	43537
5	33	F	other	15213
...	...	...	...	...
929	44	M	scientist	53711
930	28	F	scientist	07310
931	60	M	educator	33556
932	58	M	educator	06437
933	28	M	student	48105

933 rows × 4 columns
```

```python
users.tail(10) #正确写法
```

```outcome
	age	gender	occupation	zip_code
user_id				
934	61	M	engineer	22902
935	42	M	doctor	66221
936	24	M	other	32789
937	48	M	educator	98072
938	38	F	technician	55038
939	26	F	student	33319
940	32	M	administrator	02215
941	20	M	student	97229
942	48	F	librarian	78209
943	22	M	student	77841
```



### Step 6. What is the number of observations in the dataset? / 数据集一共多少观测记录

```python
# Solution 1
users.shape[0]
```

```outcome
943
```



```python
# Solution 2
users.shape
```

```outcome
(943, 4)
```

```python
# Solution 3
users.info()
```

```outcome
<class 'pandas.core.frame.DataFrame'>
Int64Index: 943 entries, 1 to 943
Data columns (total 4 columns):
age           943 non-null int64
gender        943 non-null object
occupation    943 non-null object
zip_code      943 non-null object
dtypes: int64(1), object(3)
memory usage: 76.8+ KB
```



### Step 7. What is the number of columns in the dataset? / 数据集共有多少列

```python
# Solution 1
users.shape[1]
```

```outcome
4
```



```python
# Solution 2
users.shape
```

```outcome
(943, 4)
```



```python
# Solution 3
user.info()
```

```outcome
<class 'pandas.core.frame.DataFrame'>
Int64Index: 943 entries, 1 to 943
Data columns (total 4 columns):
age           943 non-null int64
gender        943 non-null object
occupation    943 non-null object
zip_code      943 non-null object
dtypes: int64(1), object(3)
memory usage: 76.8+ KB
```



### Step 8. Print the name of all the columns. / 输出列名

```python
users.columns
```

```outcome
Index(['age', 'gender', 'occupation', 'zip_code'], dtype='object')
```



### Step 9. How is the dataset indexed?  / 数据集的索引方式

```python
users.index
```

```outcome
Int64Index([  1,   2,   3,   4,   5,   6,   7,   8,   9,  10,
            ...
            934, 935, 936, 937, 938, 939, 940, 941, 942, 943],
           dtype='int64', name='user_id', length=943)
```



### Step 10. What is the data type of each column? / 每一列数据的数据类型

```python
users.dtypes
```

```outcome
age            int64
gender        object
occupation    object
zip_code      object
dtype: object
```

### Step 11. Print only the occupation column / 仅输出'occupation'列

```python
users.occupation
```

```outcome
user_id
1         technician
2              other
3             writer
4         technician
5              other
           ...      
939          student
940    administrator
941          student
942        librarian
943          student
Name: occupation, Length: 943, dtype: object
```



### Step 12. How many different occupations there are in this dataset? / 数据集中共有多少不同职业(occupation)

```python
users.occupation.nunique() # 确实不知道这种用法, 还想用计数的办法,也没想出来
```

```outcome
21
```



### Step 13. What is the most frequent occupation? / 最多的职业

> 开始的思路是使用groupby来分组，但是没有结果，也没搞清楚原因

```python
users.occupation.value_counts()
```

```outcome
student          196
other            105
educator          95
administrator     79
engineer          67
programmer        66
librarian         51
writer            45
executive         32
scientist         31
artist            28
technician        27
marketing         26
entertainment     18
healthcare        16
retired           14
lawyer            12
salesman          12
none               9
homemaker          7
doctor             7
Name: occupation, dtype: int64
```

```python
# 精确输出出现频次最高的职业
users.occupation.value_counts().head(1)
```

```outcome
student    196
Name: occupation, dtype: int64
```



### Step 14. Summarize the DataFrame. /  概述数据集

```python
users.describe() # 有数据的列才会返回结果
```

```outcome
        age
count	943.000000
mean	34.051962
std	    12.192740
min	    7.000000
25%	    25.000000
50%	    31.000000
75%	    43.000000
max	    73.000000
```



### Step 15. Summarize all the columns / 概述每一列

> 没有太理解这题，反正记住这个操作就好了

```python
users.describe(include = 'all')  # 有数据的列才会返回结果
```

```outcome
        age	        gender	occupation	zip_code
count	943.000000	943	         943	943
unique	NaN	        2	          21	795
top	    NaN	        M	     student	55414
freq	NaN	        670	         196	9
mean	34.051962	NaN	         NaN	NaN
std	    12.192740	NaN	         NaN	NaN
min	    7.000000	NaN	         NaN	NaN
25%	    25.000000	NaN	         NaN	NaN
50%	   31.000000	NaN	         NaN	NaN
75%	   43.000000	NaN	         NaN	NaN
max	   73.000000	NaN	         NaN	NaN
```



### Step 16. Summarize only the occupation column / 概述occupation列

```python
users.occupation.describe()
```

```outcome
count         943
unique         21
top       student
freq          196
Name: occupation, dtype: object
```



### Step 17. What is the mean age of users? / 用户的平均年龄

```python
users.age.mean()
```

```outcome
34.05196182396607
```



### Step 18. What is the age with least occurrence? / 出现次数最少的年龄

```python
users.age.value_counts().tail()
```

```outcome
11    1
10    1
73    1
66    1
7     1
Name: age, dtype: int64
```


