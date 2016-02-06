Welcome to Debuging and Profiling Worlding!!!

Debug的几个要素：
- 收集信息：要有合理的手机信息的方法。
- 重现错误：要使得错误可以有规律的重现
- 逻辑推断：不要瞎猜，要根据事实进行推断。
- 重复试验：如果想到的解决办法没有解决问题，那么应该回退之前的更改，重新试验。
- 要有耐心：bug很难修复，所以要有耐心，一味的求快，从长久来看，是浪费时间。
- 记录心得：问题解决之后，要对问题，以及解决这个问题的方案有详细的记录。

Debug的技术：
- 使用console.info，打印代码执行的过程。需要注意的是，之后要及时删除这些用于打印的代码。避免引起视觉干扰。
- 分析崩溃的日志（crash log）。
- 使用转么的IDE，设置breakpoint去跟踪代码的执行过程。

Debug和Testing
Debug和Testing是不一样的，主要有以下区别：
- Testing是在软件发布或者使用之前，对软件的代码进行测试
- Debug是在软件发布之后或者使用之后，对软件崩溃信息尽心分析

iOS中查看系统log的步骤：
- 使用Spotlight或者Alfred呼出Console.app
- 在左边的导航栏，展开iOS Simulator
- 选择跟你的simulator对应的版本

TODO：Android查看log的步骤

TODO：使用Studio进行breakpoint等的调试方法，查看memory leak。（有时间安装Studio试一下）
