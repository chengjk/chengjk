---
title: 股票常见指标 
date: 2018-04-27 17:13:15
tags: [study]
---


## K线图
由阴阳烛组成，每个烛包含周期内开盘价，收盘价，最高值，最低值；颜色区分涨跌。 如果开盘价还没有产生，采用上一个周期的收盘价。
 
 
## Volumn 成交量
成交量，每天的成交量组成柱状图。

## MA (Moving Avg)
窗口期的平均值，窗口期随时间滑动。形成平滑曲线图。

$$MA=1/n\sum_{i=1}^n Price_i $$

Price 一般是收盘价，也可以是开盘价，最高级，最低价。

 
 
## EMA (Exponential Moving Average)  
指数加权平均

$$ EMA_{today} = α * Price_{today} + ( 1 - α ) * EMA_{yesterday} $$
 
其中，α为平滑指数，一般取作2/(N+1)。在计算MACD指标时，EMA计算中的N一般选取12和26天，因此α相应为2/13和2/27。
 权重基数2/(N+1)，N是天数。权重随时间的增长呈指数增长，影响越来越小。
 
## MACD (Moving Avg Convergence and Divergence)

MA发散收敛情况, 大于零适合买入，小于零适合卖出。
$$ MACD=2*(DIF-DEA)$$
其中：
Dif: 短线减去长线，短线一般12天，长线一般26天
$DIF=EMA_{12}-EMA_{26}$
DEA: DIF的9日加权移动均线
$DEA=DEA_{yesterday}×8/10+DIF_{today}×2/10$
 
## KDJ

以J值为主，80以上超买，20以下超卖。
KDJ 指标算法

$ K=2/3*K_{yesterday}+1/3*RSV_{today}$
$ D=2/3*D_{yesterday}+1/3*K_{today}$
$$J=3K-2D$$

>若无前一日K值与D值，则可分别用50来代替。

其中未成熟随机指标 RSV
$RSV=(收盘价-N日最低)/(N日最高-N日最低)$

## BOLL
通过计算股价的“标准差”，再求股价的“信赖区间”。
该指标在图形上画出三条线，其中上下两条线可以分别看成是股价的压力线和支撑线，而在两条线之间还有一条股价平均线，布林线指标的参数最好设为20。一般来说，股价会运行在压力线和支撑线所形成的通道中。

1. MB 中轨线 = MA(N)
2. UP 上轨线 = MB+2*MD
3. DN 下轨线 = MB-2*MD


>MD 标准差计算
过去n日的每日价格减去ma的平方和除以n。
$MD=\sqrt {1/n\sum_{i=1}^n (Price_i-MA_i)^2 } $
