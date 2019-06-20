# EI332
SJTU EI332 实验部分的完整代码和实验报告  
建议先熟悉quartus II的使用，阅读王赓老师给出的my first fpga.pdf
了解下列操作：
新建project,创建.bdf文件，创建.v文件并生成相应的symbol(.bsf)文件。
在.bdf文件中插入相应的symbol,连接输入和输出，命名输出和输出
分析后，手动分配管脚(pin planner)，或者利用执行.tcl文件自动分配管脚
开始编译
烧录至SOC-DE1。
上传的文件，每一个实验，都可以直接编译通过，烧录到板子上，完成相应的功能，同时有一定的注释和实验报告。

关于实验考试：
要求扩展一条指令，比如hads rd,rs,rt。计算rs和rt的汉明距离即rs和rt有几位数不同（比如rs为0100，rt为1100，那么对应位有2个不同，则rd为2）.
首先写出这条指令的格式，hads rd,rs,rt。为它设置32位机器码是多少，R型指令，opcode为000000，rs、rt、rd字段为相应的5位五位二进制，而shamt字段为00000，func字段，可以自由设置，比如为111111.所以32位机器码是000000rsrtrd00000111111。
同时，需要考虑，如果是hads指令，那么控制信号应该如何设置，这里由于hads信号相当于R型指令，执行算术操作，所以它的指令设置和add和sub指令非常类似，不同的地方在于aluc的设置。根据我的设计，1000指示alu进行hads运算。
接下来，在cu中增加i_hads信号来指示当前指令是否是hads指令，相应地设置控制信号。
在alu中，如果aluc是1000，那么进行hads的相应运算，我的想法是rs和rt做异或后，利用for循环统计1的数量或者把结果的32位全部加起来[result[0]+result[1]+……+result[31])。
这里还有的考点就是I/O扩展，我指定哪几个开关作为输入，比如sw[9]到sw[1]作为rs，而rt是我给定的；同时要求把结果显示在HEX2或者HEX5上。
