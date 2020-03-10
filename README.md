# Coro_infection_2.0__in_Denmark  
  
This model is updated from my Coro_infection_1.0__Wuhan_Infection. Part of the data has been coor

Orientation in English:  
Model Assumption:  
[1].Basing on the Lancet dissertation, assuming that the infection period for each person as 8 days, from which, 3 days (T_delay) for generating the virus inside their body without infecting the others + 5 days (T_infect) infecting the others. After 8 days, the infected person was isolated into the hospital and lose the contagious.  
  
[2].The number of patient_zero is assumed as 1. Assuming that, each people in Denmark can meet up 50 persons a day, and 20% probability to have a close talk with these 50 persons, and 15% probability to infect and get infected in these close talk.Basing on all these, can calculate the infection corfficient q.  
  
Model Theory:  
From the perspective of mathematics, this model is made to predict the real & potential amount of people that has been infected by this Coro_2019 virus. The model carrier is the __Geometric series__, and by applying the higher algebra and recrusive algorithm, the most critical term in this entire algorithm, the __'weight_calculated'vector__ can be derived and utilized further.  
  
Model Functionality:  
Can be used to predict that, without any serious precautions from the government, how many people can be infected by this Coro_2019, from the first danish patient_zero shows up in 2020-02-24, to __NOW (In line_29, you can just change the time to say how this infection will go in the future).__ Since I believe in western world, there may not be any __serious__ precautiions always, so in principle, you can always use this model for prediction.  
  
Model Orientation:  
In line_38-43, are the hyperparameters that you can tuned in this model.    
[1].__nr_patient_zero__       : How many patient_zero there are.（__variable_0__）  
[2].__nr_people_meet_a_day__  : How many different people you can meet up in a day.（__variable_1__）    
[3].__percent_close_talking__ : The probability of having a close talk with them.（__variable_2__）  
[4].__percent_infect__        : The probability of getting infected by these close talks.（__variable_3__）    
  
Before we get started, I need to answer a most generalized question that I was asked when I uploaded my model_1.0. The question is: 'Your model, seems does not have a differnece when dealing with differernt countries, which is not scientific'. So let me put this into clear from two perspectives:  
(1). First of all, since the __nr_patient_zero__ for a certain country is always a small number (such as 1-10), which is truly a extrmnely small number compard with the while population. So in the beginning of this virus transmission, the initial condition can be always treated as similar.  
(2). Secondly, during the virus transmission, according to the difference in country population, or population density, there should be a difference in the virus transmission situation. I would like to take a little 'extreme' example to explain, like the difference between Denmark and Russia:  
As we know, the population density in Russia is quite low (9 person/km^2), compared with Denmark (138 person/Km^2), which means, their __variable_1__ can be quite different. On the other hand, the citizens' enthusiasm are quite different in these two countries, which makes a difference in if people usuallly wanna a close talk or not. This can somehow effect the __variable_2__. At last, since the citizen's fitness in Denmark is quite high compared with Russia, so the probability of getting infected can be dramatically different, which makes __variable_3__ different. In summary, the difference in countries, can show up in all those hyperparameters.  
  
The line_64-85 is the core of this model. This complicated strcuture is to realize, a periodic appearing & disappearing Geometric series tracking problem. What used here is also where the recrusive algorithm applied. I will help you realize where need to be tracking, and why it is complicated in doing this prediction. Please open the 'important_image_1.jpg' I left, read my __Model Assumption__ twice, and let me take an example to explain:  


零号病人出现在第0天，按照上述模型假设，前3天病毒在其体内繁殖，不具有传染性。但是到了第4天，病毒开始传播直到其第8天住院。零号感染者所传播的时间为第4天到第8天结束.我称此轮为第一轮，因为零号感染者感染的人数就是 零号病人的数量*感染因子q。特别是，此时q的指数为1。  
但这时重点来了，细心的朋友可能注意到了，在第7天时，传播的除了零号病人自己本身，第一轮的被感染者也开始传播病毒感染别人了。这种复杂的情况在后期随着天数增加愈演愈烈！如果你观察图片，看到我画紫色线的地方，你会发现，在第15天时，第二轮感染刚刚结束，第三轮感染在进行中，而第四轮感染已经开始了。图中写的q的系数，是当时推导递推规律时留下的。可以看出，想要准确计算括号中的参数，并不是这么简单。所以我先找到了这些系数的组成规律，然后用递推算法搞定了这些系数，并存在了 'weight_calculated' vector. 代码 line_64-85 的复杂结构就是为了实现这个功能所做。关于递推算法, 请参考我留下的'important_image_2.jpg',通过推倒前几轮感染出现时，不同的q^1 or q^2 or q^3 所乘的指数，就可以轻松的找出递推的规律，在这里我就不赘述了。非常有兴趣但推不出来的朋友可以联系我，有空可以当面推，比较好懂。





Orientation in Chinese:  
模型假设：  
[1].根据‘柳叶刀’论文，假设平均每个感染者周期为8天,其中3天(T_delay)产病毒不传染 + 5天(T_infect)传染。感染者感染后8天住院丧失感染性。  
[2].零号感染者假定为1人。传播按每人每天接触50人，20% 近距离说话，15%传染给近距离讲话的人。通过以上数据，可以计算感染因子q。
  
模型原理：  
该模型意在实现传染病模型的纯数学模型。模型载体为几何级数, 通过使用高等代数和递归算法推导出本算法最关键的'weight_calculated'vector. 由于缺少准确数据，所以该模型预测无法使用ML/DL。
  
模型功能：  
可预测从2020-02-24第一例丹麦感染病患，到现在(NOW)，没有太大政府管控时，病毒的传播效率。可以通过调整line_29的'NOW'来更新日子，从而得到相应的感染人数预测。（讲实话，我觉得让丹麦政府封城啥的真的是做梦，民主自由，怎么可能？？？所以讲道理这模型你可能可以一直用...  :P）

模型orientation:  
代码的 line_38-43行 为本模型超参数。  
[1].多少个patient_zero  （__variable_0__）   
[2].您一天能见到多少个活人 （__variable_1__）  
[3].您有多大几率跟他们近距离说话 （__variable_2__）  
[4].您有多大几率在近距离说话时传染给他们（__variable_3__）  
然后这里update一个认知，有好多老铁在model_1.0时曾经问过我一个灵魂问题，那就是：‘你的模型听起来似乎针对不同国家（人口不同地理因素不同）预测的方式是一样的，这听起来似乎不太科学’。的确，没有解释清楚是我的问题，所以我想从两个方面详细解释一下这个问题:    
(1).首先我的patient_zero一般设置的是1-3个人，这种初始条件对于任何国家的总人口来说无异于水滴之于大海。所以在传播初始各个国家的初始条件可以认为是相同的。  
(2).其次，是在病毒传播过程中，不同人口密度，地理便利程度的不同国家传播理应也不同。这个问题我想聚个例子说明，比如 丹麦和俄罗斯：    
众所周知，毛子的领土真tmd是地广人稀，你一天根本可能除了你家人见不到几个新的活人。但是相反的，丹麦cph的人口密度可谓是相当大的,尼玛抢个鞋有时还要挤得头破血流的，所以两个国家根据实际情况 variable_1 会变得很不同。同时，丹麦人高冷，毛子热情，所以 variable_2 （近距离说话的概率）两国又不一样。最后，丹麦人身体好，毛子都tm酒鬼，近距离讲话染病概率 variable_3 也会存在很大不同。综上,国家之间的差异就体现出来了。  
  
  
代码的 line_64-85行 为本模型核心。该复杂结构意在实现一个针对具有【周期性出现消失的几何级数追踪问题】。该结构也是本模型所用递归算法的体现。可能有的数学还没忘干净的朋友会说：‘几何级数？不就是他妈等比数列，不是很简单么？？？’ 然而我想说，并没有tm这么简单。

首先请打开我留下的图片文件：important_image_1.jpg， 然后重新阅读我的模型假设两遍，接着听我举个例子：  
零号病人出现在第0天，按照上述模型假设，前3天病毒在其体内繁殖，不具有传染性。但是到了第4天，病毒开始传播直到其第8天住院。零号感染者所传播的时间为第4天到第8天结束.我称此轮为第一轮，因为零号感染者感染的人数就是 零号病人的数量*感染因子q。特别是，此时q的指数为1。  
但这时重点来了，细心的朋友可能注意到了，在第7天时，传播的除了零号病人自己本身，第一轮的被感染者也开始传播病毒感染别人了。这种复杂的情况在后期随着天数增加愈演愈烈！如果你观察图片，看到我画紫色线的地方，你会发现，在第15天时，第二轮感染刚刚结束，第三轮感染在进行中，而第四轮感染已经开始了。图中写的q的系数，是当时推导递推规律时留下的。可以看出，想要准确计算括号中的参数，并不是这么简单。所以我先找到了这些系数的组成规律，然后用递推算法搞定了这些系数，并存在了 'weight_calculated' vector. 代码 line_64-85 的复杂结构就是为了实现这个功能所做。关于递推算法, 请参考我留下的'important_image_2.jpg',通过推倒前几轮感染出现时，不同的q^1 or q^2 or q^3 所乘的指数，就可以轻松的找出递推的规律，在这里我就不赘述了。非常有兴趣但推不出来的朋友可以联系我，有空可以当面推，比较好懂。

在代码运行之后，可以观测到人数变化的动态曲线，以及在 console window 输出的最终预测值。

Enjoy! :)


                                                                                               yihaosun94@gmail.com
                                                                                                          Yihao Sun
                                                                                                         07.03.2020
