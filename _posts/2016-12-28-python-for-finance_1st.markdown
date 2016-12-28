---
layout:     post
title:      "Python股票数据分析系列（1）——数据读取及初步处理"
subtitle:   "Stock Market Data Analysis with Python——Reading and Processing Data "
date:       2016-12-28
author:     "Cai"
header-img: "img/post-bg-py-fin.png"
catalog:    true
tags:
    - Python
    - 股票数据分析
    - 量化投资
    - 金融
---

**写在前面的话**

博客搭起来还没来得及写篇简单介绍或者卷首语，就直接进入了技术内容，单纯直接我喜欢。就直接进入正题吧，那些吹逼的话什么时候空了想起来再写，不是重点。

本系列是《Python股票数据分析系列》，主要用Python处理和分析股票数据，会涉及数据读取、可视化、投资组合、量化投资的内容，全部内容需要一点金融基础、统计基础和Python基础，但不用很多，因为本系列的内容还都比较小白。

全部代码基于Python3.5，如果遇到Python2.X和Python3.5内容不一样的地方，文中尽量标注说明。另外，需要安装numpy/pandas/pandas_datareader（Python3.5）/matplotlib等模块。

本文是系列的第一篇，主要涉及股票数据的读取和初步处理——描述统计、可视化等。

> **注！** 本系列写作风格比较随意和口头话，因为尽量撒干活而不用太在意文字的正式和规范，尽量活泼不艰涩又能把问题说明白。

---

好，进入主题吧。

### 获取股票数据

先加载pandas模块。

```python
from pandas import Series, DataFrame
import pandas as pd
```

利用Python读取股票数据常用两种方法
- 读取已经从行情软件或者其他地方下载存放在Excel、CSV等格式文件里的股票数据
- 从yahoo财经，Google 财经，world bank等网站数据接口直接读取

###### 读取CSV数据

这里只以读取CSV格式的上证综指数据为例，其他格式类似。

```Python
path = 'D:\GitHub\python-for-finance'
print(path + '/szzz.csv')
szzz = pd.read_csv(path + '/szzz.csv', index_col = 0)
print(szzz.head())
```

结果就是读出来啦。数据包括了上证综指开盘价、最高价、最低价、收盘价和成交量。只显示前面五行。

![img](/img/in-post/past_py_fin/read_csv.jpg)

###### 从Yahoo、Google等网站直接读取

pandas（Python2.X）/pandas_datareader（Python3.5）可通过API直接获取yahoo财经，Google 财经，world bank等数据接口提供的股票数据。前段时间万科在风口，那这里就以从yahoo财经的股票数据接口获取万科A股票数据为例吧。

```Python
import pandas as pd
import pandas_datareader.data as web #python3.5
import datetime  #日期时间处理模块
start = datetime.datetime(2010, 1, 1) #数据读取开始日期
end = datetime.date.today() #数据读取结束日期
vanke = web.DataReader("000002.SZ", 'yahoo', start, end)
```

就是如此简单，获得了2010-1-1至今天（2016-12-27日）的万科A股票开盘价、最高价、最低价、收盘价、成交量、调整后收盘价等股本数据。

>注意：000002.SZ表示在深市上市的万科A，其中000002为股票代码，SZ表示上市所在交易所代码，在深市上市的股票加SZ，在沪市上市的股票加SS，即股票代码加沪深SS或SZ。

```Python
print(len(vanke))
1801
```

```Python
print(vanke.head())
print(vanke.tail())
```

![img](/img/in-post/past_py_fin/yahoo_data.jpg)


**参考文献**
