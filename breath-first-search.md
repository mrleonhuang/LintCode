### **典型的图题的构成：**

1. Queue（heap）用 LinkedList实现
2. 如果需要计算长度或者次数之类，每次循环判断Queue长度（分层）
3. 自定义Coordinate类 / Magic数组代替坐标
4. InBound判断不要越界
5. boolean数组标记 / HashSet / HashMap / 改动原数组（图）来标记防止重复

### 关于BFS 图题类型的细分：

1. 首先判断start point有几个，**one or multiple**。
2. 如果是multiple，则有两个维度去继续细分：
   1. **时间上是同时还是分时**。同时的例子是Zombie in Matrix，需要两层for循环Search & Queue所有的Zombie，然后同时吃人；分时的例子是Build Post Office II，有不同的start point但是每次针对其中一个start point 进行BFS。
   2. **去重判断是共享空间还是不共享空间**。共享空间的例子是Number of Islands，共同mark一片空间；不共享空间的例子是Build Post Office II，针对每一个start point开一个新visited数组。



### 图题需要注意的问题：

1. 在加入Queue的时候就要马上mark点去重
2. 判断图为树：node == edge + 1 && all nodes are connected



