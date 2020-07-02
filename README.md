
@[toc]
# 引言
&#8195;主要是大三的课设，结合的是之前做的SE   IR同时相较之前加入了一些改进。
# 课程设计内容
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624195210770.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1plbmdtZW5nMTk5OA==,size_16,color_FFFFFF,t_70)

# 建模过程
## 符号约定
S 表示易  感   者； 
E 表示潜伏者；
I 表示感  染 者；
R 表示康  复  者；
D 表示死   亡者；


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200702085433385.png)


## 模型假设
* 期间不考虑人口的流   入与流出对模型的影响；
* 不考期间的自然  死  亡率与人口的   自然增长  率；
* 不考虑   无  症状   感   染  者的影响；
* 康复人群R具有抗    体，不在染病·。
## 模型的仿真过程

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200702085709459.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1plbmdtZW5nMTk5OA==,size_16,color_FFFFFF,t_70)


&#8195;首先是以wh在12月31日发现第一例患者为参考的时间，以1月24日wh开始f城作为采取强制措施的参考时间，因此，根据参考时间，我们假定第一天开始迭代的时间是12月31日，这是的迭代符合自然传播，规律到大约1月24日时候，开始采取隔离措施，外地医疗增援也开始陆续赶到，这时我们减少患者（I）与潜伏者（E）的传播  系数也是就这里c接触人数与有效的传播率（感  染）β，同时有关方开始将部分潜伏者与接触者放到某地   隔   离，假定隔   离  比例为q，这时这些的无转    播    能力，和被传    播   的风险，同时解除传    播的速率记为λ；假定由于医   疗   增   援可以提高患者的康复率r同时减少死亡率α。
## 模型的数学形式表达
&#8195;依据前面的假设，可以建立出如下的数学微分方程：
* 自然传播状态下的SE  IR微分形式为：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200702134431246.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1plbmdtZW5nMTk5OA==,size_16,color_FFFFFF,t_70)

由此可得其差分形式：


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200702134807315.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1plbmdtZW5nMTk5OA==,size_16,color_FFFFFF,t_70)


* 采取隔离措施后的SIER模型引入了隔离的潜伏者与隔离的易感染者这类群体不会感染其他人同时也无被感染的风险，故同理可得隔离措施模型的微分形式




建模过程相较上次，做了一些小小的改进，（让他看起来像真的一样，其实还是假的y y出来的）
# 建模结果
&#8195;根据上述的建模过程，笔者将Matlab   R20  16b作为编程环境并在其中实现。
##  仿真与现实情况的拟合
* 首先是先看看自然条件的SEIR模型的模拟过程：


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624194832271.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1plbmdtZW5nMTk5OA==,size_16,color_FFFFFF,t_70)


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624195303405.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1plbmdtZW5nMTk5OA==,size_16,color_FFFFFF,t_70)


* 由模型不难看出，如果放着肺炎不管的话，按照模型的推算会有很多人  患   病和死   亡。于是我们尝试加入隔离措施得到下图：


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624195529492.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1plbmdtZW5nMTk5OA==,size_16,color_FFFFFF,t_70)


![在这里插入图片描述](https://img-blog.csdnimg.cn/2020062521300488.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1plbmdtZW5nMTk5OA==,size_16,color_FFFFFF,t_70)


* 由于问题给出了附件数据，对附件尝试进行清洗，开始尝试对拟合，拟合方式主要为SE  IR差分式的迭代和采取隔  离措施后的参数调整，主要调整的参数为接触率C与有效接触比例b作为（同时增加了治愈率）不同城市采取隔 离措施后的改变体现。（外部增援后续治疗跟进，采取隔  离后人与人间的接触减少同时又更多比例的  人被隔 离）
拟合效果如下：


![在这里插入图片描述](https://img-blog.csdnimg.cn/2020062420043258.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1plbmdtZW5nMTk5OA==,size_16,color_FFFFFF,t_70)


* 同时将模型推广，比如选取哈儿滨市做模型的推广结果进行尝试得到：


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624200529697.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1plbmdtZW5nMTk5OA==,size_16,color_FFFFFF,t_70)


## 灵敏度分析
* 最后进行灵敏度的测试与分析,笔者这里主要对采取隔离的时间与强度进行相关的灵敏度分析，结果如下：


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624200705700.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1plbmdtZW5nMTk5OA==,size_16,color_FFFFFF,t_70)


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624200724822.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1plbmdtZW5nMTk5OA==,size_16,color_FFFFFF,t_70)


# 小结
&#8195;根据建模本文的结果，不难看出：提前采取隔离措施、增大隔离的力度，医疗资源的及时跟进，都是减少I者数量与D者的比较关键的几个因素，因此，此模型的参考意义与价值可以在此得到体现，也可以反映出我们早期的决策者决策的远见与正确。（以人为本的防疫策略可以取得更好的结果）。
# 模型的不足的展望

（1）现今yiqing已经走入下半阶段，防范外来的输入病例成为比较重要环节，因此加入外来su入病例的因素可以增加模型的准确性与真实性；
（2）SE  IR模型是一个相对理想条件下的拟合模型，因此引入一些智能算法如神经网络可以增加模型拟合真实数据时的准确性；
（3）当前yiqing对人民生活的影响可以切实感受，将SE  IR应用于其他相关模型的研究有待进一步尝试。

# 参考
* [之前的博客基于  2019-nCo  V的  SEIR  模型的建立与改进](https://blog.csdn.net/Zengmeng1998/article/details/104231869)
* 知网论文只要是浙江大学学报
