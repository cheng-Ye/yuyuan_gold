# 豫园（老庙）黄金智能补货项目

心得：做这个项目最大的收获就是之前把算法仅仅局限于AI,真正领会到算法其实真的是一门交叉学科。本项目偏向于模型可解释性以及业务，所以AI在这里用的不是很多。

# 背景：
豫园黄金珠宝智能补货项目，旨在帮助豫园集团完善过去纯以经验补货的策略，建立一个对历史数据分析并构建算法给出补货建议的平台。

# 项目简介
平台使用flask框架，主要包括历史数据分析和补货算法两个功能。
**补货算法涉及方法：**
自适应控制系统、间断时间序列预测conston法、带约束条件的线性回归、粒子群算法、聚合分解法以及指数平滑法。
# 1、历史数据分析：
包括月畅销排行、动销率排行、月各品种销售情况、SKU级月销量走势、节假日销量统计情况。
# 2、补货算法：
采用ABC分类法，A类即交易量大和交易量相对较小但是存在供不应求的物品；B类即种类繁多、交易量小物品、C类即滞销品，交易量和次数非常小；

A类商品补货方式：
构建自适应控制系统，系统包括参考模型、调节器和自适应机构三个部分；当系统运行时，自适应机构不断调整调节器的参数，使得系统随时间变化趋于稳定，当系统稳定时（商品预测销量与实际销量相等且商品库存为设定值），调节器的参数不再变化；其中参考模型为指数平滑法和带约束条件的线性拟合（拟合销量相关因子，粒子群算法确定拟合参数）的加权集成；调节器为本期调节系数Kt，系数由上一期的自适应机构调整得到，调节系数乘以上一期销量与参考模型的输出之和构成了商品本期预测销量；自适应机构会滞后一个周期，根据本期实际销量实际库存情况调节Kt系数大小，调整后的结果作为下一个周期调节系数Kt+1。

B类商品补货方式：
B类商品交易量分为平稳时间序列和间断时间序列，平稳序列使用指数平滑法，而对于间断时间序列，使用conston法和聚合分解法预测下一期销量；聚合分解就是将相似商品的销量相加，作为该类商品的本期销量，预测出的下一期销量按照每件商品的本期销量占比进行合理分配。

C类商品补货方式：
当C类商品本期库存低于安全库存，则考虑进货。

# 补货方式
最终每件商品补货量由预测销量、在途库存和人员行为操作计算得出，给出本期物品的合理补货订单。


# 注
项目具体细节可以参见 智能补货算法细节.pdf；因为项目是给公司做的，所以代码就不开源了，如有兴趣可以加我微信18018590558索要代码；
