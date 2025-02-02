    
关于AI的胡说八道

这段时间AlphaGo的新闻在到处刷屏，好多人在说，计算机要战胜人类了。个人觉得这种提
法有点莫名其妙，马跑赢人，你不说马战胜人类，火车跑赢马，你不说火车战胜人类。好
脑筋不如硬笔头，你不说笔头战胜人类。用Python计算20位的乘法可以秒算，你不说
Python战胜人类。怎么弄个对围棋的模式匹配出来，你就觉得这玩意儿就战胜人类了呢？

大抵上，大部分人都没有“圣人”那种“以人之有以为己之有”的觉悟，没有“以天下之至柔驰
骋天下之至坚”的胸怀。什么都要认为是自己的，用个篱笆围起来，标上“私人财产”才会满
足。所以，“五音令人目盲，难得之货令人行妨”实在是把这些人描绘得栩栩如生。

那么最近AI的发展，到底踩了这些人的什么“私人区域”呢？估计是“直觉”。个位相加进位
到十位，十位再相加到百位，这种动作是有逻辑的，有“理智”的，有“道理”的，这种东西
你计算机算得快，咱不敢跟你争，但你计算机有“直觉”吗？你可以看到一只猫就可以得到“
猫”这个词吗？你可以冥冥中知道面对特定的棋局的时候，“感受”到下一步应该是“飞”还是
“刺”吗？这说起来是好像是人类最后的自尊心似的。

但这个其实也不算什么，因为似乎现在热炒的神经网络就是解决类似问题的其中一种方法
。

关于神经网络，我原来问过不少人，好多都说得不名不白的，我这里做一个归纳，懂的跳
过这一段吧。

所谓神经网络，是一个数学概念，和我们现实中的网络没有什么关系。它的概念来自对动
物神经元网络的研究。据说，Once up a time，有一群邪恶的科学家，躲在一个戒备深严
的黑暗基地中，把一些可爱的小花猫绑起来，在脑袋后面开了一个脑洞，然后让它看不同
的图片，研究它大脑皮层神经元的电极变化。

![](_static/神经元.png)
  
最后他们有这么一个结论：视神经传递进来不同的信息，进入边缘的神经元，每个神经元
会受到一个简单的刺激，然后把这个刺激传递给下一层的神经元，这样会在整个网络上形
成不同的电平分布和聚集。这被认为是一种“抽象”的过程——人或者动物在得到大量的信息
后，会通过神经网络抽象为简单的“概念”（比如“猫”，“煞笔”之类的）。

后来又有一些疯狂科学家，基于这个概念发明了一种所谓的人工的神经网络（ANN）。这个
东西本质是一种类似的数学结构，我们把输入的信息，首先经过简化，变成一个向量，然
后把这个向量输入到一个这样的网络中，让它产生波动，让它形成“抽象”，比如，一个40
岁，有洁癖，长头发，鼻梁高，反骨突，耳垂长的猥琐男人挑这款咖啡猫马桶坐垫的可能
性有多大呢？我们可以把这个作为一个向量A[40, 2（洁癖程度），30（头发长度）, 12（
鼻梁高度）, 3(反骨高度）, 2(耳垂长度），3（猥琐程度）, 1（男）]输入到神经网络中
，神经网络的每个节点接受其中一个参数，如图所示：

![](_static/神经网络.png)

每个输入要先进行标准化（比如每个参数都变成0-1之间的值，避免有一个参数特别重要，
类似高考的标准分），然后进行综合，比如v=a1w1+a2w2+a3w3+...，变成一个单一的值，
输入到下一层的神经元，每个神经元都做一个简单的运算（这个运算称为刺激函数：
y=f(v,si)），基于v和一个控制参数产生下一个输入。这样一层层计算下去，到最后一层
，就只有少数几个输出，比如“买咖啡猫马桶垫”和“不买咖啡猫马桶垫”。这样，我们就得
到一个模拟的“直觉思考”模型了。

这个东西类似巫术——找两个算筹，问问生辰八字，摆个玄而又玄的形状，然后扔上去，说
自己夺天地之造化，然后预测你明年会不会发财。当然，如果现代巫术还是这种水平，那
人类就太没有长进了。所以，概率论这种现代巫术也搬上来了。上面那个“直觉模型”，真
正决定输出的，其实是网络本身的结构，算法以及所有的Wi和Si，得到最后的“抽象”也不
准，但如果我们已经有十万个先验数据呢？也就是我们有一万个买还是不买这种坐垫圈的
实际数据对这个模型进行“训练”，让它“阅人无数”，每次如果算错了(Loss），就给网络一
个反馈（比如一种常见的算法叫梯度下降法），调整这些Wi和Si的值，如果这个事情确实
是具有规律的（特征），这个训练就有可能成功，比如，我们最后对于这十万个数据，正
确判断结果可以达到80%，这样这个模型就具有参考价值了。下次我们看到上面提到的猥琐
老男人，我们就告诉你，这个家伙有90%的可能买咖啡猫马桶垫。

这个功能非常实用，只要你有数据，你就是个现代巫师。AlphaGo只要有足够的棋谱去喂，
以及足够的计算资源，你的“直觉”远远不如。但是不是人类因此就没有存在价值呢？你这
样想，只能说是穷碧惯了，没有过过好日子。计算机吃电，你吃饭，你们有很多冲突吗？
要不要每件事都来“比一比”啊？人和计算机是无有入无间，你真的有必要什么都要拿在自
己手上吗？你买辆汽车回来不想着怎么快点到单位，想着有什么办法“战胜”汽车？脑子有
水啊？

当然，拉黄包车的还是要紧张的。比如我们这种做CPU的。上面神经网络那类的算法，是个
让人又喜又忧的现实。喜的是，计算机工业很长时间都聚焦在IO上，对“计算”的要求有比
较长一段时间内不怎么引起人们的注意了。所以，卖“计算”的人有出头之日了，钱又开始
投给“计算”了。但另一方面，CPU这种“理智计算”却不是重点，AI的运算大部分时候，是非
理智计算。它的要求可能是：

向量化的：比如前面算v=a1w1+a2w2+a3w3+...，cpu要先算a1*w1，然后算a2*w2，再算
a1w1+a2w2... 但如果你GPU算，可能一条指令就把整条公式给它算了。

低精度的：我们最后只是要一个“抽象”，根本没有必要让每个参数都是什么64位的，比如
，只支持8位的计算就可以了。

重复性的（模式化的）：每个神经元都是单一的简单计算，并不需要CPU这么复杂的指令集
和特定的流水线优化。

非精确的：上面的整个计算过程，也不需要精确的计算设计，你要算100*100，它就不需要
等于10000，等于9998之类的就差不多了，这也为“计算”的优化提供了机会

光向量化这一点就把CPU踢出了主演的列表了，GPU现在是主角，但如果考虑到精度和精确
这些要素，它的地位能否保持，见仁见智。新的计算单元迟早是要进入舞台的，叫不叫TPU
就难说了。

在这个游戏中，谁能赢呢？在水刚刚开始搅动的时候，谁能说这个水最终会流到哪里？但
水是摆在那里的，这一点倒是肯定的。把钱投在这上面，是有基础的理由的。

现在有三个注目的中心：算法方（研究算法的人），数据方（拥有训练数据的人），计算
方（提供计算基础设施的人）。钱最终流到哪里（注意，不是流向上面说的三个“方”，而
是三类“方”的无数个“方”中）？这是上帝都无法知道的事情——上帝也缺乏训练数据：（。

但我们知道的是，长江后浪推前浪，前浪死在沙滩上。所以，这个时世，抱哪个大腿，都
是死得快。我看到，某些做编译器的，想着基于编译器做自己的生态，某些做处理器的，
想着做自己专用的处理器，做GPU的，想着做自己的OS和驱动。想想这些，估计会活得很艰
难。以身为天下，方可以托天下。这个阶段，就是要成为所有方案的助力，善利万物而不
争，你成为别人的依托，最后别人就离不开你，你才会活下去。盈利点都十划没有一撇就
想着围一个园子出来自己玩的，迟早还是会玩死在自己的园子中的。

其实，你让我说，AI本质是巫术。现在搞这个行业的都太Navie，老想着弄什么图像识别啦
，语音识别啦，自动驾驶，下围棋啦。都是书生意气。弄这些个东西就应该回到真正的巫
术上来。你说你把什么马某云啦，王某林啦之类的生辰八字，掌纹面相，还有什么金木水
火土，五行方位的，搞个8层的神经网络给它算一算（不要问我为什么是八，据说是小崔说
的），以后丈母娘选女婿的时候，把这些东西往里一输，哗哗哗的数据就出来了。到时你
要卖手机可以卖手机，要卖云服务可以卖云服务。什么不比你动不动撞死人背锅的自动驾
驶要强？

就算你不信这一套，你做生意，做HR，阅人无数，每个人偷偷给他照个照片，存在你手机
的数据库中，标记上：此人可信，此人易骗，此人偏激，诸如此类的。让你的手机学习一
通。以后再遇到新的合作伙伴，照个照片就让他无所遁形。这不是甚好？

所以，你说搞什么“看电脑”，“听电脑”的啊，我们就应该搞什么“周易电脑”，“黄帝阴符先
天八卦电脑”，“圣母临凡星座电脑”。这才有商机的嘛……
