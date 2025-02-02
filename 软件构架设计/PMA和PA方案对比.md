    
PMA和PA方案对比
本文对比一下RISC-V的Physical Memory Attribute方案，和ARM的Page Attribute方案在
不同场合下的优劣。

我们用鲲鹏920的总线结构作为我们讨论这个问题的基础：

  source/认识鲲鹏920：一个服务器SoC/总线.rst · Kenneth-Lee-2012/从鲲鹏920了解现代服务器实现和应用_公开 - 码云 Gitee.com，

（其中内存部分的行为可以进一步看这里：

  source/计算子系统/内存访问模型.rst · Kenneth-Lee-2012/从鲲鹏920了解现代服务器实现和应用_公开 - 码云 Gitee.com

）。

但这只是保证我们有一个想象的基础，实际上现在的服务器大部分和这个结构大同小异，
所以我们的结论和是不是这个平台无关。

RISC-V的PMA和ARM的Page Attribute背后体现了一个不同的取向：RISC-V认为，一片内存
是否可以原子操作，是否进行Cache算法，应该体现在物理地址上，所以对这个属性的设置
，属于物理区域（所谓Physical Memory），甚至是硬件设计决定的，不可更改。

而ARM的设计认为，对一片内存是否使用原子操作和Cache行为，是CPU一方主动决定的，你
要我用Cache，我就用Cache，你让我不要用，我就不用，这是我的行为，不是你对端内存
的行为。参考一下前面引用材料中这幅图：

![](_static/Cache同步.jpg)

任何一个CPU看到的语义的实现，背后都是这些节点之间的复杂通讯。

RISCV的设计好处在于，大部分时候，我没有给你设计相关的Cache同步，原子更新等协议
，你根本就没有办法保证你的协议，所以，假惺惺在每个页表上都设计一个Cache操作协议
，这毫无必要。所以这个属性应该属于物理地址区域。

而ARM的设计好处在于，即使你设计了Cache互操作协议，我也可以选择不同的协议实现我
不同的目标，比如你设计了Cache协议，但我希望可以直通，我仍可以要求直通。这提高了
自由度。

这说起来各有优势，但在每个页上都放一些控制要素，而大部分时候这些控制要素都用不
上，不像很有价值的样子。

这个微小的差别，可以导致很多设计上的区别，比如ARM上可以通过MMU关掉Cache，那么如
果系统中断进入安全态，安全态的MMU不开Cache，那么在一般状态通过Cache保证的被
ld.ex等指令设置的标记就无法被感知，ARM方案需要通过切换状态的时候清除ld.ex的标记
保证内存语义Consistent。

所以，如果条件只有这么多，我个人觉得还是RISCV的设计更进步一些：）
