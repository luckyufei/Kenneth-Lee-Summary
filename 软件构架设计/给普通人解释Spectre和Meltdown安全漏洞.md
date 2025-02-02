    
给普通人解释Spectre和Meltdown安全漏洞

这次Spectre和Meltdown攻击闹得沸沸扬扬，很多不过用着手机的吃瓜群众，来问我这个到
底是个什么问题，很多人可能觉得是芯片做错了什么功能，无意中把重要的数据泄露出去
了，只要把这个代码修改一下，修补这个漏洞，这个问题就可以解决了……这个问题远没有
这么简单，我通过这段文字给群众们简单解释一下。

这次的问题比过去的那些安全漏洞严重得多。它是基于一种称为Cache Timing Side
Channel的方法来发起攻击的。我们用一个比喻来理解一下这种攻击手段是什么样的：

计算机是有权限这个概念的，权限分给不同的软件（程序），比如Android操作系统里面有
你的密码，微信里面有微信的密码，高德里有当前用户的位置。计算机硬件通过技术手段
保证了微信不能随便去读Android的密码，高德不能随便去读高德的位置。如果要读，就要
先问问人家那个程序行不行，那个程序同意了，就可以把数据按“正规”的渠道提供给你。

但现在人们发现了这样一个方法：微信可以直接去问Android：“你那个密码第一个数字是1
吗？”Android说：“这不关你的事”。这本来没有什么的，但Android好死不死，他虽然没有
回答，但他心里想了一把这件事，当对方问到一个正确的数字的时候，他回答的时候稍犹
豫了几个毫秒（在我们讨论的这个技术上其实是快了，但反正是不同，我们不关注细节）
，这个事情被微信注意到了。微信就可以用这种方法，通过反复的提问，最后猜到了密码
是什么。

你说这个事情恐怖不恐怖？惊喜不惊喜？虽然你严守规矩，坚决不透露一个字，但你回答
时的神态出卖了你！

那怎么解决这个问题呢？有几个手段，第一，严格按规矩办事，在没有确定这个人有没有
权限之前，连想都不要想它。已经有操作系统发行版用这种手段了，关闭CPU的指令预测功
能。让CPU本来能提前想的，不要提前想。这种手段，貌似执行性能可以下降90%——不是下
降到，是下降！——喔哈哈哈哈哈……

第二，就是现在Android用的手段——不让高速摄像机进场：你肉眼是看不到我表情的的一点
点变化的，你来参加我们的记者招待会，就不许带高速摄像机进场，你敢带我第一时间就
把你赶出去。这样你就偷不到我的信息了。但是有没有人很快发明一种让你看不见的手段
还能够捕获你的那点表情变化呢？另外，服务器上是用不了这个手段的，人家很多程序高
速摄像头（其实就是高精度时钟）是必备装备，你不能禁止。

第三，那就是就事论事了，这些具有保密信息的程序，也不是有问必答的，你得找到一些
安全的，不经意的问题来问我，我才有可能回答你。Spectre和Meltdown就是其中两种模式
，我们把和这两种模式有关的地方都改掉，这个问题就不存在了。比如针对Meltdown的攻
击，他们就用一种称为KAISER的技术来防止有人来读内核的密码，但和第一个问题类似，
这个东西对性能的影响，也可以大到30%乃至50%的。

恐怖不恐怖？惊喜不惊喜？

我们这些用手机的吃瓜群众，有可能泄密的地方有两个：

第一，你的手机上运行了一个有恶意的程序，你手机上的所有密码都可以被人用这种手段
取走，然后被黑客保存起来，过一段时间拿来用。

所谓“恶意程序”，包括你访问一个未知的网站。所以不要吃饱没事乱访问没有什么保证的
地址，看到一个链接就点进去看看的事情不能干。

第二，你在各个服务器厂家里面保存的信息，也可能被黑客在那些服务器上攻破，然后保
存起来，过一段时间拿来用。

而现在服务器厂家要升级，需要时间，而且都是仓猝应战，这段时间可能对黑客就是敞开
的了。

所以，在现在这个阶段，你除了赶紧升级，少去访问那些不清不楚的链接，就只能自求多
福了。这个问题就好像突然有人发明了透视摄像机一样，你的衣服再也保护不了你了。

恐怖不恐怖？惊喜不惊喜？

当然了，社会是个复杂的系统，每种攻击都有很多具体的限制，这些限制包括法律，流程
，成本等等，没有我这里说的这么简单，但这次的问题是影响深远的，等风平浪静以后，
大家还是把密码都改一改吧。

另外，相对来说，ARM平台这次除了A75，基本上对Meltdown攻击免疫，而Meltdown的攻击
是有成功攻击代码的，而Spectre我们只看到理论的代码，还没有见过真实可以对实际系统
发起攻击的例子。所以……也许吧，用手机还是比用电脑上网安全那么一点点的。
