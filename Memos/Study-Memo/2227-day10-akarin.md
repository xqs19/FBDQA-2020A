### 第10次课笔记
张心远 2018012227

#### 配对交易

***
原因：个股无平稳性，利用同一行业两只股票的协整性可以构建一个均值回复的策略
要素：对冲比例、spread、策略持有时间
步骤
* 找到可以配对的股票：协整性测试
	* 计算协整性：statmodels.coint 
		coint_t,pvalue,crit_value = coint(df[1],df[2])，看pvalue知置信度
* 持有比例/对冲比例
	* spread：多空价差
	* hedgeratio：把两只股票的beta（敏感度）变成一样的仓位之比 
	* model=OLS(df[1],df[2]) , results = model.fit()
	* hedgeratio = results.params，看价格差序列
* 计算持有时间/半衰期
	* 最佳持有时间随着使用这一策略的人的增加而减少，套利机会消失
	* EMH：信息传播 --> 套利机会消失
	* 外生冲击也会导致套利机会消失
	* 确定持有时间的统计方法：
		* Ornstein-Uhlenbeck公式: $dz(t)=-\theta(z(t)-\mu)dt+dW$  
		* $\mu$：随着时间推移的价格均值
		* dW：随机的高斯噪声
		* z的平均值意味着$\mu$指数衰减，半衰期为$ln(2)/\theta$
		* 用整个序列找出最好的$\theta$的估计
* 策略退出
* *平稳性：如果股价时间序列不偏离初始值，那么就是平稳的；
大多数股票价格序列不平稳，而表现出几何上的随机游走；*
* *协整性：long-short两只股票，portfolio的市值是稳定的*
*通常这两只股票来自同一个行业，常用于均值回归策略*
* *相关性：收益率的相关性，相关性不等于协整性*
	相关性：两只股票收益率同方向移动；协整性：两只股票价格的多空组合是平稳的；

#### 期权 part1

***
期权和期权合约
* 期权的定义：call & put
* 交易制度、行权制度
* 权利金、合约单位（10000）、交易日（到期月第四个周三）
持有期权合约到期时，标的价格和收益的图形：到期损益图
* 评估风险收益特征
* 计算损益平衡点
* 交易动作
	* 开仓/入场
	* 了解头寸/出场
		*	到期行权：美式/欧式
		*	到期归零/放弃行权
		*	提前平仓（T+0）：主要方式
* 四大基本交易策略：buy/sell call/put

##### 期权定价
三种状态：实值/平值/虚值、内在价值
期权价格 = 内在价值 + 时间价值
时间价值的衰减规律：随时间衰减速度加速，相当于未来价格波动的可能