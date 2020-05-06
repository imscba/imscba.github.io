# Pandas练习_2_1


# Ex2_1 - Filtering and Sorting Data

This time we are going to pull data directly from the internet. Special thanks to: https://github.com/justmarkham for sharing the dataset and materials.

### Step 1. Import the necessary libraries / 导入必要的包

```python
import pandas as pd 
```

### Step 2. Import the dataset from this [address](https://raw.githubusercontent.com/justmarkham/DAT8/master/data/chipotle.tsv). / 从该网址导入数据集

### Step 3. Assign it to a variable called chipo. / 数据集命名为"chipo"

```python
url = ('https://raw.githubusercontent.com/justmarkham/DAT8/master/data/chipotle.tsv')
chipo = pd.read_csv(url, sep = '\t')
```

### Step 4. How many products cost more than $10.00?

```python
# 首先将item_price转换为float
prices = [float(value[1:-1]) for value in chipo.item_price] # float(value[1:-1])，value[1:-1]截取其中第2位到最后一位（不包含）——因为最前含有$符号、最后有空格

# 转换后的价格重新分配到原来的item_price中
chipo.item_price = prices

# 去除重复商品名、数量
chipo_filtered = chipo.drop_duplicates(['item_name','quantity'])

# 筛选数量为1的商品(我是没有想明白这一步的操作的合理性)
chipo_one_prod = chipo_filtered[chipo_filtered.quantity == 1]

chipo_one_prod[chipo_one_prod['item_price']>10].item_name.nunique()
```

```outcome
12
```

### Step 5. What is the price of each item?

###### print a data frame with only two columns item_name and item_price

```python
# 删除重复商品名、数量
chipo_filtered = chipo.drop_duplicates(['items_name','quantity'])

# 仅选择数量为1的商品
chipo_one_prod = chipo_filtered[chipo_filtered.quantity == 1]

# 选择商品名称列和商品价格列
price_per_item = chipo_one_prod[['item_name','item_price']]

# 价格从高到低排序
price_per_item_sorted = price_per_item.sort_values(by = 'item_price', ascending = False)

price_per_item_sorted
```

```outcome
	item_name	item_price
606	Steak Salad Bowl	11.89
1229	Barbacoa Salad Bowl	11.89
1132	Carnitas Salad Bowl	11.89
7	Steak Burrito	11.75
168	Barbacoa Crispy Tacos	11.75
39	Barbacoa Bowl	11.75
738	Veggie Soft Tacos	11.25
186	Veggie Salad Bowl	11.25
62	Veggie Bowl	11.25
57	Veggie Burrito	11.25
250	Chicken Salad	10.98
5	Chicken Bowl	10.98
8	Steak Soft Tacos	9.25
554	Carnitas Crispy Tacos	9.25
237	Carnitas Soft Tacos	9.25
56	Barbacoa Soft Tacos	9.25
92	Steak Crispy Tacos	9.25
664	Steak Salad	8.99
54	Steak Bowl	8.99
3750	Carnitas Salad	8.99
21	Barbacoa Burrito	8.99
27	Carnitas Burrito	8.99
33	Carnitas Bowl	8.99
11	Chicken Crispy Tacos	8.75
12	Chicken Soft Tacos	8.75
44	Chicken Salad Bowl	8.75
1653	Veggie Crispy Tacos	8.49
16	Chicken Burrito	8.49
1694	Veggie Salad	8.49
1414	Salad	7.40
510	Burrito	7.40
520	Crispy Tacos	7.40
673	Bowl	7.40
298	6 Pack Soft Drink	6.49
10	Chips and Guacamole	4.45
1	Izze	3.39
2	Nantucket Nectar	3.39
674	Chips and Mild Fresh Tomato Salsa	3.00
111	Chips and Tomatillo Red Chili Salsa	2.95
233	Chips and Roasted Chili Corn Salsa	2.95
38	Chips and Tomatillo Green Chili Salsa	2.95
3	Chips and Tomatillo-Green Chili Salsa	2.39
300	Chips and Tomatillo-Red Chili Salsa	2.39
191	Chips and Roasted Chili-Corn Salsa	2.39
0	Chips and Fresh Tomato Salsa	2.39
40	Chips	2.15
6	Side of Chips	1.69
263	Canned Soft Drink	1.25
28	Canned Soda	1.09
34	Bottled Water	1.09
```

### Step 6. Sort by the name of the item

```python
chipo.item_name.sort_values()

# 或

chipo.sort_values(by = 'item_name')
```

```outcome
	order_id	quantity	item_name	choice_description	item_price
3389	1360	2	6 Pack Soft Drink	[Diet Coke]	12.98
341		148	1	6 Pack Soft Drink	[Diet Coke]	6.49
1849	749	1	6 Pack Soft Drink	[Coke]	6.49
1860	754	1	6 Pack Soft Drink	[Diet Coke]	6.49
2713	1076	1	6 Pack Soft Drink	[Coke]	6.49
...	...	...	...	...	...
1395	567	1	Veggie Soft Tacos	[Fresh Tomato Salsa (Mild), [Pinto Beans, Rice...	8.49

4622 rows × 5 columns
```

### Step 7. What was the quantity of the most expensive item ordered?

```python
chipo.sort_values('item_price',ascending = False).head(1)
```

```outcome
		order_id	quantity	item_name			choice_description	item_price
3598	1443		15			Chips and Fresh Tomato Salsa	NaN		44.25
```

### Step 8. How many times were a Veggie Salad Bowl ordered?

```python
chipo_salad = chipo[chipo.item_name == 'Veggie Salad Bowl']
chipo_salad # 分步骤看一下，可以直接len(chipo_salad)
```

```outcome
	order_id	quantity	item_name	choice_description	item_price
186	83	1	Veggie Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Rice,...	11.25
295	128	1	Veggie Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Lettu...	11.25
455	195	1	Veggie Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Rice,...	11.25
496	207	1	Veggie Salad Bowl	[Fresh Tomato Salsa, [Rice, Lettuce, Guacamole...	11.25
960	394	1	Veggie Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Lettu...	8.75
1316	536	1	Veggie Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Rice,...	8.75
1884	760	1	Veggie Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Rice,...	11.25
2156	869	1	Veggie Salad Bowl	[Tomatillo Red Chili Salsa, [Fajita Vegetables...	11.25
2223	896	1	Veggie Salad Bowl	[Roasted Chili Corn Salsa, Fajita Vegetables]	8.75
2269	913	1	Veggie Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Rice,...	8.75
2683	1066	1	Veggie Salad Bowl	[Roasted Chili Corn Salsa, [Fajita Vegetables,...	8.75
3223	1289	1	Veggie Salad Bowl	[Tomatillo Red Chili Salsa, [Fajita Vegetables...	11.25
3293	1321	1	Veggie Salad Bowl	[Fresh Tomato Salsa, [Rice, Black Beans, Chees...	8.75
4109	1646	1	Veggie Salad Bowl	[Tomatillo Red Chili Salsa, [Fajita Vegetables...	11.25
4201	1677	1	Veggie Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Black...	11.25
4261	1700	1	Veggie Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Rice,...	11.25
4541	1805	1	Veggie Salad Bowl	[Tomatillo Green Chili Salsa, [Fajita Vegetabl...	8.75
4573	1818	1	Veggie Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Pinto...	8.75
```

```python
len(chipo)
```

```outcome
18
```

### Step 9. How many times people ordered more than one Canned Soda?

```python
chipo_Canned_Soda = chipo[(chipo.item_name == 'Canned Soda') & (chipo.quantity > 1)]

# chipo_Canned_Soda 可以分解步骤看一下
len(chipo_Canned_Soda)
```

```python
20
```


