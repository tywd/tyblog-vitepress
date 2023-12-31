## 前言
阅读《学习JavaScript数据结构与算法（第3版）》有感
希望自己每次学习算法都能输出一篇博客，收入专栏，检查自身学习情况~ 文章有错欢迎各路大神指正，别喷，硬要喷的话，麻烦轻点，谢谢大神们~

> ps: 这书《学习JavaScript数据结构与算法（第3版）》居然没有讲希尔排序，只能自己整了

## 开始
希尔排序，也称递减增量排序算法，是插入排序（## 前端必会算法（三）：插入排序）的一种更高效的改进版本。是非稳定排序算法，插入排序只能移动一个相邻位置，希尔排序优化了这一点（希尔排序可以一次移动 gap 个距离），利用了插入排序在排序几乎已经排序好的数组的非常快的优点。
希尔排序是基于插入排序的以下两点性质而提出改进方法的：

插入排序在对几乎已经排好序的数据操作时，效率高，即可以达到线性排序 O(n) 的效率；
但插入排序一般来说是低效的，因为插入排序每次只能将数据移动一位；

### 思路
比如数组 `[9, 1, 2, 5, 7, 4, 8, 6, 3, 5]`


先将整个待排序的记录序列分割成为若干子序列分别进行插入排序，比如第一趟分成5个子序列（每一个子序列的索引是间隔为gap的值）
第二趟排序将取序列的间隔 gap/2 向下取整，再次进行插入排序
第三趟排序将取序列的间隔 gap = 1，此时整个序列中的记录“基本有序”，则对全体记录直接进行插入排序

### 实现
```js
function shellSort(array) {
  if (array.length <= 1) return array; // 如果数组长度为1，直接返回
  var gap = Math.floor(array.length / 2);
  while (gap > 0) {
    for (var i = gap; i < array.length; i++) {
      var j = i;
      var temp = array[j];
      while (j > 0 && array[j - gap] > temp) { // 若array[j - gap]>temp(即array[j]) 则互换位置
        array[j] = array[j - gap]; // 这里可看成是将 j-gap 后移一个 gap 位 //TODO 插入排序这里是后移一位
        array[j - gap] = temp; // 由于不像插入排序那样需要比较很多个元素，而是两个数的比较，此处将大得值往前移一个 gap 位即可
        j -= gap; // 跳出循环的条件
      }
    }
    gap = Math.floor(gap / 2); // 减小增量
  }
  return array;
}
var arr = [9, 1, 2, 5, 7, 4, 8, 6, 3, 5];
console.log(shellSort(arr))
```
### 优化
希尔排序则是插入排序的优化
暂无其他优化想法，欢迎各路大神评论
## 复杂度

- 时间复杂度
单次直接插入排序不会改变相同元素之间的相对顺序，是稳定的。
但在希尔排序多次不同的插入排序过程中, 相同的元素可能在各自的插入排序中移动，可能导致相同元素相对顺序发生变化。因此希尔排序并不稳定。
最佳情况：T(n) = O(n logn)。 最差情况：T(n) = O(nlog2n)。 平均情况：T(n) = 取决于间隙序列。
- 空间复杂度
希尔排序过程中，只涉及相邻数据的交换操作，只需要常量级的临时空间，空间复杂度为 「O(1)」

## 其他
[# 前端算法学习-算法复杂度](https://juejin.cn/post/7034077582584709150)\
[# 前端必会算法（一）：冒泡排序](https://juejin.cn/post/7034765646390886437)\
[# 前端必会算法（二）：选择排序](https://juejin.cn/post/7034819462687621133)\
[# 前端必会算法（三）：插入排序](https://juejin.cn/post/7036181901022855175)\
[# 前端必会算法（四）：归并排序](https://juejin.cn/post/7036277115905540103)\
[# 前端必会算法（五）：快速排序](https://juejin.cn/post/7037137749387771940)
## 最后
渣渣一个，欢迎各路大神多多指正，不求赞，只求监督指正