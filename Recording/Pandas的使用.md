# **Pandas的使用**

```python
# 导入pandas
import pandas as pd
import numpy as np
```

## 1.创建序列

```python
s = pd.Series([1, 3, 6, np.nan, 44, 1])
print('s =', s)
```

```python
# 生成6个数据的序列(日期类型)
dates = pd.date_range('20231225', periods=6)
print('dates =', dates)
```

```python
# 创建表格型数据
df = pd.DataFrame(np.random.randn(6, 4), index = dates, columns=['a', 'b', 'c', 'd'])
# randn返回一个或一组服从标准正态分布的随机样本值（6行4列）。并且以dates为索引，a, b, c, d为字段名
df
```

```python
# 创建3行4列的表格，默认索引号为1， 2， 3， ...
df1 = pd.DataFrame(np.arange(12).reshape((3, 4)))
print('df1 =', df)
```

```python
# 以字典作为数据，字典中：key为列名，value为一列数据
df2 = pd.DataFrame({'A': 1.,
                   'B': pd.Timestamp('20130102'),
                   'C': pd.Series(1, index=list(range(4)), dtype = 'float32'),
                   'D': np.array([3] * 4, dtype = 'int32'),
                   'E': pd.Categorical(['test', 'train', 'test', 'train']),
                   'F': 'foo'})
print('df2 =', df2)
```

## 2. 表格的数据特征

```python
# df2的数据类型
print('df2的数据类型：\n', df2.dtypes)
print()

# 输出索引
print('df2的索引：\n', df2.index, end='\n\n')

# 输出所有字段
print('df2的字段：\n', df2.columns, end='\n\n')

# 按行输出所有数据
print('df2的所有数据：\n', df2.values, end='\n\n')

# 输出数据特征（如：平均值，方差等）
print(df2.describe(), end='\n\n')

# 进行转置
print('转置后的结果：\n', df2.T, end='\n\n')

# 按字段进行排序，（倒序）
print('倒序排序为：\n', df2.sort_index(axis = 1, ascending=False), end='\n\n')
# 按照字段‘E’ 进行排序
print('按照字段‘E’ 进行排序：\n', df2.sort_values(by = 'E'), end='\n\n')
```

## 3.选择数据

```python
# df = df2.copy()
dates = pd.date_range('20130102', periods=6)
df = pd.DataFrame(np.random.randn(6, 4), index = dates, columns=['A', 'B', 'C', 'D'])
print('df =', df)
```

```python
# 选择某一字段数据
print('A:\n', df['A'] , end='\n\n')
print('A:\n', df.A, end='\n\n')
```

```python
# 切片：
# 输出df的前三行
print('0 - 3: \n', df[0:3], end='\n\n')
# 输出20130102 - 20130104 之间的所有行
print('20130102 - 20130104: \n', df['20130102':'20130104'], end='\n\n')

# 标签筛选
# 选择行名为20130102的行
print('20130102行: \n', df.loc['20130102'], end='\n\n')
# 选择A. B列
print('[A, B] = \n', df.loc[:, ['A', 'B']])

# 索引筛选
# 第3行数据
print('第3行数据：\n', df.iloc[3], end='\n\n')

# 第3行第1位数据
print('第3行第1位数据：\n', df.iloc[3, 1], end='\n\n')
# 第3行到第5行，第1列到第3列
print('3-5, 1-3: \n', df.iloc[3:5, 1:3], end='\n\n')
# 第1， 3， 5 行， 1 - 3 列
print('1, 3, 5 : 1 - 3\n', df.iloc[[1, 3, 5], 1:3], end='\n\n')

# 筛选出A列中大于8的数据
print('A > 0.2:\n',df.A > 0.2)
```

## 4. 设置值

```python
print(df, end='\n\n')

# 将第3列第3行的值改为1111
df.iloc[2, 2] = 1111
print(df, end='\n\n')
df.loc['20130102', 'B'] = 2222
print(df, end='\n\n')

# 将A列中大于4的行赋值为0
df[df.A > 4] = 0
print(df, end='\n\n')

# 添加'F' 列， 值为空
df['F'] = np.nan

# 添加'E' 列， 并且序列中的行标签与原列表一致
df['E'] = pd.Series([1, 2, 3, 4, 5, 6], index=pd.date_range('20130101', periods=6))
print(df, end='\n\n')
```

## 5. 处理丢失数据

```python
# 丢掉存在数据为空的行
ddf1 = df.dropna(axis=0, how='any')  # 若how的值为all， 则丢掉所有数据为空的行
print(ddf1)

# 将空数据填充为0
ddf2 = df.fillna(value=0)
print(ddf2)

# 若有空数据，则改为False，否则为True
ddf3 = df.isnull()
print(ddf3, end='\n\n')

# 若存在空数据（丢失数据）则返回True
print(np.any(df.isnull()) == True)
```

## 6. 导入导出数据

```python
# 导入数据
# path = ''
# pd.read_csv(path, sep='\t', header=None, names=['列1','列2'], index_col=False)
'''解释：
path: 文件路径
sep: 指定分割符为'\t'，默认为','
header: 指定表头
names: 指定字段名
index_col: 指定索引列，如index_col = 0, 指定第0列为索引
'''

# 同样还有:read_excel, read_hdf, read_sql, read_json, read_html, read_pickle等
```

```python
# 导出数据
# data.to_pickle('student.pickle')
'''导出名为student.pickle的文件''' 
# 同样还有：to_csv, to_excel, to_sql, to_hdf等
```

## 7. 合并

```python
# concat方法
df1 = pd.DataFrame(np.arange(20).reshape(4, 5), index = None, columns=['A', 'B', 'C', 'D', 'E'])
df2 = pd.DataFrame(np.arange(20, 30).reshape(2, 5), index = None, columns=['A', 'B', 'C', 'D', 'G'])
df3 = pd.DataFrame(np.arange(30, 50).reshape(4, 5), index = None, columns=['A', 'B', 'C', 'D', 'E'])
print('df1:\n', df1)
print('df2:\n', df2)
print('df3:\n', df3)

# 合并df1， df2, df3, 纵向合并，忽略各个表格中的索引
res1 = pd.concat([df1, df2, df3], axis=0, ignore_index=True) 
print('res1:\n',res1)

# 纵向合并df1与df2 ,将df1 与 df2中互相没有的数据填充为NAN
res2 = pd.concat([df1, df2], join='outer')
print('res2:\n',res2)

# 纵向合并df1与df2，将df1与df2中互相没有的列进行裁剪
res3 = pd.concat([df1, df2], join='inner')
print('res3:\n', res3)

# 横向合并df1 与 df2 ，并且按照df1的索引为基准，df2 中若没有则添加为NAN，多余的进行裁剪
res4 = pd.concat([df1, df2], axis=1).reindex(df1.index)
print('res4:\n', res4)

# 将df2添加在df1上
res5 = df1._append(df2, ignore_index=True)
print('res5:\n', res5)

# 将序列添加到列表中
sl = pd.Series([1, 3, 44, 1])
res6 = df1._append(sl, ignore_index=True)
print('res6:\n', res6)
```

```python
# merge方法
left = pd.DataFrame(np.arange(20).reshape(4, 5), index = None, columns=['A', 'B', 'C', 'D', 'E'])
right = pd.DataFrame(np.arange(10, 30).reshape(4, 5), index = None, columns=['A', 'B', 'C', 'D', 'G'])
print('left:\n', left)
print('right:\n', right)
print('\n\n')
# 将left 与 right 表格进行合并，以相同的B列为基准，左右合并
res7 = pd.merge(left, right, on='B')
print('res7:\n', res7, end='\n\n')

# 合并表left与right，将列名为A，B的两列分别相同的进行合并，how默认为'inner'
res8 = pd.merge(left, right, on=['A', 'B'])
print('res8:\n', res8, end='\n\n')

# how也可以= 'outer', 若how = 'left',则基于left的A，B进行合并，此时，right中没有的用NAN进行填充，how也可以为right
res9 = pd.merge(left, right, on=['A', 'B'], how='inner')
print('res9:\n', res9, end='\n\n')

# indicator:显示如何合并，即合并的方式，其值可以自己设定，设定的即为合并方式列的名称。
res10 = pd.merge(left, right, on='A', how='outer', indicator='indicator_column')
print('res10:\n', res10, end='\n\n')

# 指定左右索引分别为left，和right的索引，相同的直接合并，不相同的，添加NAN再合并（左右合并）
res11 = pd.merge(left, right, left_index=True, right_index=True, how='outer')
print('res11:\n', res11, end='\n\n')

# 将表格left与right进行合并，按照D进行，区分两个表格的数据，在left的数据标签中加_left, 在right的数据列标签加_right
res12 = pd.merge(left, right, on='D', suffixes=['_left', '_right'], how='outer')
print('res12:\n', res12)
```

