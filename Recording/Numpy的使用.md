# **Numpy的使用**

```python
# 导入numpy模块
import numpy as np
```

## 1. 将列表转换为矩阵

```python
array = np.array([[1, 2, 3], [2, 3, 4]])
```



```python
# 查看维度：array.ndim
# 查看每一维的大小： array.shape
# 查看一共有多少个元素： array.size

print('维度：', array.ndim)
print('形状：', array.shape)
print('数量：', array.size)
```

## 2.创建array

```python
a = np.array([2, 23, 4], dtype = np.float_)
a.dtype  # 查看a数组的数据类型
```

```python
# 定义3行4列的零矩阵
a = np.zeros((3, 4))

# 定义3行4列的单位矩阵
b = np.ones((3, 4), dtype=np.int16)

# 生成空矩阵（每一个元素接近零）
c = np.empty((3, 4), dtype=np.float_)

# 生成从10 - 20之间的数，步长为2
d = np.arange(10, 20, 2)

# 从新定义行列数，这里为3行4列
e = np.arange(12).reshape((3, 4))

# 从固定区间进行取数(这里是从1 - 10 之间取6个数)
f = np.linspace(1, 10, 6)
# 重新定义矩阵形状
g = np.linspace(1, 10, 6).reshape((2, 3))



# 进行输出
print('a=', a, end = '\n\n')
print('b=', b, end = '\n\n')
print('c=', c, end = '\n\n')
print('d=', d, end = '\n\n')
print('e=', e, end = '\n\n')
print('f=', f, end = '\n\n')
print('g=', g)
```

## 3.numpy的基础运算

```python
# a+b  a-b  a*b  a**2
a = np.array([[1, 2, 3], [2, 3, 4]])
b = np.array([[2, 2, 3], [3, 3, 4]])

print('a + b = ', a+b, end = '\n\n')   # 对应相加
print('a - b = ', a-b, end = '\n\n')   # 对应相减
print('a * b = ', a*b, end = '\n\n')   # 对应相乘
print('a ** 2 = ', a**2, end = '\n\n')   # 每一项取平方
```

```python
print('a =', a)
print()
# 返回a中的列表，其中小于3的为True，否则为False
print(a<3)
```

```python
# 矩阵运算
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.array([[2],[2],[2]])
print('a = ', a, '\n\nb = ', b, end = '\n\n')
c = np.dot(a,b)
print('c = a * b.T \n', c, end = '\n\n')
c = a.dot(b)
print('c = a * b.T \n', c)
```

```python
# 矩阵的转置
print('A的转置为：\n', A.T)
print('A的转置为：\n', np.transpose(A))
# 矩阵乘法
print('矩阵乘法：\n', (A.T).dot(A))
```

## 4.矩阵的整体操作

```python
# 通过本函数可以返回一个或一组服从标准正态分布的随机样本值
a = np.random.randn(2, 4)
```

```python
# 在0 - 1 之间随机取数，生成2行4列矩阵
a = np.random.random((2, 4))
```

```python
# 求矩阵中的所有数之和
c = np.sum(a)
print('矩阵中的所有数之和：', c)

# 求矩阵中的最小值
c = np.min(a)
print('矩阵中的最小值：', c)

# 求矩阵中的最大值
c = np.max(a)
print('矩阵中的最大值：', c)

# 返回每一行中的所有数之和
c = np.sum(a, axis = 1)
print('每一行的所有数之和：', c)
# 返回每一列中的最小值
c = np.min(a, axis = 0)
print('每一列中的最小值：', c)
# 返回每一行中的最大值
c = np.max(a, axis = 1)
print('每一行中的最大值：', c)
```

```python
# 重新设定A 为从 2 - 14 (左闭右开) 中选取数，步长为1 一共12个数，并设定形状为3行4列
A = np.arange(2, 14).reshape((3, 4))
```

```python
# 返回A中最小值的索引
minIdx = np.argmin(A)
print('A中最小值的索引：', minIdx)
minIdx = A.argmin()
print('A中最小值的索引：', minIdx)
# 返回A中每一行中最小值的索引
minIdx = np.argmin(A, axis = 1)
print('A中每一行中的最小值索引：', minIdx)

# 返回A中最大值
maxIdx = np.argmax(A)

maxIdx = A.argmax()


# 求平均值
print('A的平均值：', np.mean(A))
print('A的平均值：', A.mean())

# 求中位数
print('A的中位数：', np.median(A))
# 求前n项和
print('A的前n项和：', np.cumsum(A))
print('A的前n项和：', A.cumsum())

# 返回每两个数之间的差
print('每两个数之间的差：', np.diff(A))

# 返回不是0的索引
nZeroIdx = np.nonzero(A)
print('A中值不为0的索引：', nZeroIdx)
nZeroIdx = A.nonzero()
print('A中值不为0的索引：', nZeroIdx)

# 对列表逐行进行排序
print('逐行排序后的结果：\n', np.sort(A))
```

```python
# 矩阵整体转换
# 将矩阵A中所有小于5的都转换为5，大于9的都转换为9
print('矩阵的转换：\n', np.clip(A, 5, 9))
```

## 5. 矩阵的索引与切片

```python
a = np.arange(1, 17, 1).reshape(4, 4)
print('a = ', a, end = '\n\n')
# 一维索引输出第4个位置，二维输出第4行
temp = a[3]
print('二维第4行：', temp)
print('一维第4个位置：', temp[3])
# 索引第2行第2个位置
print('第2行第2个位置：', a[1][1])

# 第2行所有列
print('第2行所有列', a[1, :])
# 第2列所有行
print('第2列所有行', a[:, 1])

# 第2行的2 - 3 列
print('第2行的2 - 3 列', a[1, 1:3])
```

## 6. 对矩阵进行迭代

```python
a = np.arange(1, 17, 1).reshape(4, 4)
print('a = ', a, end = '\n\n')
# 直接进行迭代输出(首先是输出每一行)
for rows in a:
#     print(rows)
    for elem in rows:
        print(elem)
        
print('-' * 50)
# 将A的所有元素变为1行(这里返回的是一个迭代器)
for elemt in A.flat:
    print(elemt)
    
# 将A的所有元素变为1行（这里返回的是一个numpy.ndarray类型多为数组）
aFlatten = a.flatten()
print(aFlatten, type(aFlatten))
```

## 7. array的合并

```python
A = np.array([1, 1, 1])
B = np.array([2, 2, 2])

 # 将A, B 进行上下合并
C = np.vstack((A, B))  
print('A, B 进行上下合并\n', C)
# 将A, B 进行左右合并
C = np.hstack((A, B))  
print('A, B 进行左右合并\n', C)
# 将A添加维度转换为列向量
C = A[:, np.newaxis]   
print('将A添加维度转换为列向量:\n', C)

# 将A, B 进行上下合并
C = np.concatenate((A, B, B, A), axis = 0)
print('A, B 进行上下合并', C)
```

## 8.array分割

```python
A = np.array([[1, 1, 1, 1], [2, 2, 2, 2]])
B = np.array([2, 2, 2])

# 将A分成两块，按行进行分割，切割X轴
print('将A按行分成两块: ', np.split(A, 2, axis = 0))

# 将A按列进行不等分割(切割y轴)
print('将A按列分为三块：\n', np.array_split(A, 3, axis = 1))

# 将A横向分割为3块
print(np.vsplit(A, 2))
# 将A纵向分为2块
print(np.hsplit(A, 2))
```

## 9.赋值操作

```python
a = np.arange(4)
print('a= \n', a)
b= a    # 这里的b只是指向了a
print('b = a\n', b)
c = a   # 这里的c只是指向了a
print('c = a\n', c)
a[0] = 11
# 改变了a的同时，b和c也被改变了
print('a =', a, 'b =', b, 'c =', c)
```

```python
# 将a进行拷贝给b
a = np.arange(4)
# 这里的b是一片新的内存空间，将a进行了拷贝
b = a.copy()
print('a =', a, 'b =', b)
# 改变了a但是b没有改变
a[0] = 100
print('a =', a, 'b =', b)
```

