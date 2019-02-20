## 缺失值
1. 直接使用：模型支持缺失值，决策树
2. 删除特征： 某特征大多数是缺失值，可删除特征
3. 补全： 
* 均值填充： 值都一样
* 众数
* 插值法
* 聚类，同类均值补充
* 建模预测：如果缺失属性与其他属性无关，那么预测结果无意义。如果高度相关，那么可以删除特征
* 高维映射：最准确的做法，因为完全保留了信息，也不增加任何信息；样本量大才可以

实例
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
pd.set_option('display.max_columns',10)
raw=pd.read_csv('winequality-red.csv')
```

## 异常值
指一组测定值中与平均值的偏差超过两倍标准差的测定值。与平均值的偏差超过三倍标准差的测定值，称为高度异常的异常值
1. 确认方法：画box图检查；用3倍std检查

```python 
plt.boxplot(raw.chlorides)
plt.show()
```

2. 解决方法：
* 空值：视为空值待后期对空值进行处理，填补；但填补方式的不同会不同程度的改变原有的数据分布；
* 盖帽法：重新设定数据边界，也会改变数据的分布，但异常值往往很少的话可以采用；整行替换数据框里99%以上和1%以下的点，将99%以上的点值=99%的点值；小于1%的点值=1%的点值。即
把3sigma之外的数据定为sigma

```python
mu=raw.chlorides.mean()
sigma=raw.chlorides.std()
lb=mu-3*sigma
hb=mu+3*sigma
tmp[tmp<lb]=lb
tmp[tmp>hb]=hb
plt.boxplot(raw.chlorides)
plt.show()
```

* 取对数：
```python
raw.chlorides.hist(figsize=(8,4),bins=40)
plt.show()
raw['chlorides_expd']=np.log(tmp+1)
raw.chlorides_expd.hist(figsize=(8,4),bins=40)
plt.show()
```


* 分类建模：把干扰变量变成分类变量（异常为1，不异常为0）
* 离散化：例如做成 高、中、低，三种字段。
* 剔除 ：整行剔除，整列剔除
* 变量转换：通过一定的变换改变原有数据的分布，使得异常值不在异常；（对比上面的取对数）
对严重右偏的数据非常有用，变换后的数据能够更接近正态分布；
![https://pic3.zhimg.com/80/v2-f8b7c166c351fd3a036b69a888ec1132_hd.jpg][标记1]

## 冗余值
* 删除冗余值：drop_duplicates()

## 模型反馈
1. 数据清洗有没有问题
2. 数据抽样有没有问题
3. 数据理解有没有问题：主成分分析，聚类看一下
4. 模型选择有没有问题
5. 参数调整有没有问题

[标记1][https://pic3.zhimg.com/80/v2-f8b7c166c351fd3a036b69a888ec1132_hd.jpg]