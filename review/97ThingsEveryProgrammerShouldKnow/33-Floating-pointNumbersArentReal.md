# 浮点数不是实数

[Floating-point Numbers Aren't Real](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_33/)

在数学科学种，浮点数不是“实数(real)”，尽管他们在很多编程语言中被成为`real`，比如Pascal和Fortran。实数是无限精度并连续无损的；浮点数被限制了精度，所以它们是有限的，类似于“四舍五入”的整数，因为它们在整个范围没有均匀间隔。

举个例子，把2147483647(32位int的最大值)分配给一个32位float变量(名为x)，然后打印。你会得到2147483648。现在打印`x - 64`，仍然是2147483648。现在打印`x - 65`你将得到2147483520！为什么？因为这两个浮点数之间的间隔是128，浮点运算会舍入到最近的浮点数。

(译注：类似于分辨率，128是浮点类型在内存中能表现的最小单位——间隔)

IEEE浮点数是基于基数为2的科学记数法的固定精度数：1.d1d2…dp-1x2e，p代表精度(float是24，double是53)。两个连续的数之间的间隔应为2的(1-p+e)，可以安全近似于ε|x|，ε表示机器的epsilon(2的1-p次方)。

知道相邻浮点数的间隔可以帮你避免数字类型的错误。比如，你要处理迭代计算，例如搜索方程的根，要求找出比超过系统能表达精度更高的数字是没有意义的。确保你要求得的差值没回比间隔更小，否则会进入死循环。