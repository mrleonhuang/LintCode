1. 二分查找要非常注意关键词：first, last ...
2. 注意当每个循环**mid的值等于target**的时候，**坐标调整关系**和**最后判断的先后顺序**。如果把left = mid了，说明整体指针是向右靠的，因此最后判断的时候先判断left，再判断right。反之亦然。特殊情况例如找last index，坐标整体向右边靠，但是最后先判断right指针的值，再判断left指针
3. 注意返回下标index还是值本身！
4. Rotated Sorted Array遇到duplicate的问题要把**等于**的情况单独拿出来处理，前或者后指针一格一格移动，最终达到把duplicate元素堆到序列的其中一边的目的



