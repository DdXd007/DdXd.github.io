# STL:优先队列（priority_queue)

包含在头文件 `#include <queue>`中

与queue的区别在于priority_queue可以自定义数据的优先级，让优先级别高的排在队前，优先出队

优先队列包含普通队列的所有特征，是在普通队列的内部添加了一个排序，本质上是通过堆实现的

定义：`priority_queue<Type, Container, Functional>`

*Type* 就是数据类型，*Container* 就是容器类型（必须是用数组实现的容器，默认使用`vector`），`Functional`就是比较方式，当需要用自定义的数据类型时需要传入这三个参数，使用基本数据类型时只需要传入数据类型，默认是大顶堆。

一般是：

```c++
priority_queue<int, vector<int>, greater<int>> q;
// 升序排列
priority_queue<int, vector<int>, less<int>> q;
// 降序排列
```

