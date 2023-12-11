# calculator-for-89c51

本项目是一个用89c51制作计算器的练习项目，可以作为参考学习的资料。有计算显示和蜂鸣器警告功能，当然还存在一些问题。
关于其中的函数：
screen（）：输入一个数字，将其显示在数码管上。他有一个返回值，因为在显示过程中
使用了一个无限循环，当键盘再次有有效输入的时候会终止这个循环，并且返回输入的键值，
这样可以解决显示市场的问题（在之前的版本中使用的是 200 次的 for 循环，在长时间不输
入的情况下会产生乱码）

scanKeyboard():从键盘中读取输入。P0 口在不停的检测，当没有输入时返回 0xff,有输入
时会根据行号和列号返回对应的键值。缺点是需要使用 while（1）来不停的检测输入。为
了解决这个问题，又使用了 meaningfulKey（）函数，即有有效输入的时候进行赋值。
在后续的修改中有添加了定时器开关，来实现蜂鸣器的效果，每个按键对应不同的音调。

delay（）：延时函数。

warning（）：检测到非法输入或按置零键的时候会调用这个函数，蜂鸣器响起并且重置单
片机。但是由于蜂鸣器现在还有问题，所以只是重置他。（重置原理是把 P1.7 和 RST 相连，
有非法输入时将 P1.7 置为 1）

controlSystem():控制函数，是输入和计算逻辑。由于位数较少，所以采用了 if else
嵌套的方式进行讨论，缺点是非常冗杂。
calculate():作为 controlSystem()的一部分，接受三个参数，两个作为运算一个作
为符号。

当然项目也存在很多问题，比如为了偷懒，将P1^7直接连接到了rst来实现置零，这在实际操作中是不允许的。
欢迎交流提问学习
