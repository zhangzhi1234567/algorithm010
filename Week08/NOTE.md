学习笔记

# LRU

LRU是Least Recently Used的缩写，即最近最少使用，是一种替换算法。

### cache

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1679669/1596034824355-85c8ea2b-0b9a-44b5-88e0-e3c89c1e8ca4.png?x-oss-process=image%2Fresize%2Cw_1500)

内存分三级缓存 L1 D-cache是处理速度最快的，也是容量最小的，如何往里面存数据，就需要用到替换算法。



### LRU cache

- 缓存是有限的，在缓存满的时候，删除哪些元素，就有不同的缓存删除策略
- 在缓存满的时候，删除缓存里最久未使用的数据，然后再放入新元素
- 数据的访问时间很重要，**访问时间距离现在最近**，就最不容易被删除。



![image.png](https://cdn.nlark.com/yuque/0/2020/png/1679669/1596034164539-ecf1b985-2ac8-4a6d-8bb0-2c98853de9ff.png?x-oss-process=image%2Fresize%2Cw_1500)



get实现：

判断hash 中Key是否存在，不存在返回-1 ； 存在则返回对应的值，并把节点添加到头部

put实现：

判断hash 中Key是否存在，不存在：1.添加新的节点到头部，添加到哈希，并size++，检查容量大小，容量大于cap时，删除尾部节点，删除哈希key，size--；

存在则更新的值，并把节点添加到头部。 

get put 操作时，只有

添加到头部

|---删除节点 （最小操作）

移动到头部--

|---添加到头部（最小操作）   全部都可以由这两个基本操作完成



删除尾部 --删除尾节点， 返回删除节点。



# bloom filter

### 简介

是一个很长的二进制向量和一系列随机映射函数

在很多场景下，我们都需要一个能迅速判断一个元素是否在一个集合中。譬如：

1. 网页爬虫对URL的去重，避免爬取相同的URL地址；
2. 反垃圾邮件，从数十亿个垃圾邮件列表中判断某邮箱是否垃圾邮箱（同理，垃圾短信）；
3. 缓存击穿，将已存在的缓存放到布隆中，当黑客访问不存在的缓存时迅速返回避免缓存及DB挂掉。

### Bloom Filter vs Hash Table

-  hash表不仅可以判断元素是否在集合中，还可以元素的各种额外信息。
-  bloom filter只是检索一个元素在还是不在，不能存其他的信息 

- - 优点，空间效率和查询效率都远远高于一般的算法 
  - 缺点，有一点的误识别率和删除困难



### 原理

布隆过滤器（Bloom Filter）的核心实现是一个超大的位数组和几个哈希函数。

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1679669/1595947322336-ef6e0e62-60b5-45e4-9eb7-5e27d6d799b3.png)

bloom filter会通过哈希函数把x, y, z一次映射到几个二进制位中，查x是否存在时，即查对应映射出来的二进制位是否都为1，都为1是则可能存在，

若有一个不为1，则一定不存在；（可能存在的原因是：查询的K个位置可能被其他的数据恰好都映射了1）

当数据可能存在时，需要进一步查存储结构。 布隆过滤器一般做最外层的缓存，为了降低数据库的查询率，当不存在时就不去查数据库，只有当某个数据可能存在时，才去进一步查数据库。

### 布隆过滤器添加元素

- 将要添加的元素给k个哈希函数（一个哈希函数只能映射到一个位置，所以多个位置就需要多个哈希函数）
- 得到对应于位数组上的k个位置
- 将这k个位置设为1

### 布隆过滤器查询元素

- 将要查询的元素给k个哈希函数
- 得到对应于位数组上的k个位置
- 如果k个位置有一个为0，则肯定不在集合中
- 如果k个位置全部为1，则可能在集合中

# 排序



### 快排 quick sort

排序算法的思想非常简单，在待排序的数列中，我们首先要找一个数字作为基准数（这只是个专用名词）。为了方便，我们一般选择第 1 个数字作为基准数（其实选择第几个并没有关系）。接下来我们需要把这个待排序的数列中小于基准数的元素移动到待排序的数列的左边，把大于基准数的元素移动到待排序的数列的右边。这时，左右两个分区的元素就相对有序了；接着把两个分区的元素分别按照上面两种方法继续对每个分区找出基准数，然后移动，直到各个分区只有一个数时为止。

- 首先从数列的右边开始往左边找，我们设这个下标为 i，也就是进行减减操作（i--），找到第 1 个比基准数小的值，让它与基准值交换；
- 接着从左边开始往右边找，设这个下标为 j，然后执行加加操作（j++），找到第 1 个比基准数大的值，让它与基准值交换；
- 然后继续寻找，直到 i 与 j 相遇时结束，最后基准值所在的位置即 k 的位置，也就是说 k 左边的值均比 k 上的值小，而 k 右边的值都比 k 上的值大
- 时间复杂度是nlogn



```c++
int partition(vector<int> &nums, int begin, int end) {
    int pivot = end, counter = begin;
    for (int i = begin; i < end; i++) {      // 不包括pivot
        if (nums[i] < nums[pivot]) {
            swap(nums[i], nums[counter]);    //快慢指针 i 快指针 counter 慢指针 相当于记录比pivot小的个数
            counter++;                       //当i > counter时，counter的位置就比pivot大了; 找到一个比pivot小的数，和counter换一下位置
        }                                    //当i = counter时，说明还没遇到比pivot大的数
        printArray(nums);
    }
    swap(nums[counter], nums[pivot]);        //counter之后的数都比pivot大，所以这里交换一下位置
    return counter;
}

void quickSort(vector<int> &nums, int begin, int end) {
    if (end <= begin) return;
    int pivot = partition(nums, begin, end);
    quickSort(nums, begin, pivot - 1);
    quickSort(nums, pivot + 1, end);
}
```



### 归并 merge sort

分治的思想

1. 把长度为n的输入序列分成两个长度为n/2的子序列;
2. 对这两个子序列分别采用归并排序;
3. 将两个排序好的子序列合并成一个最终的排序序列。

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1679669/1596377748803-3532ce43-42f4-4b53-b798-84c225f3f8c3.png?x-oss-process=image%2Fresize%2Cw_1500)

归并排序是稳定排序，它也是一种十分高效的排序，能利用完全二叉树特性的排序一般性能都不会太差。java中Arrays.sort()采用了一种名为TimSort的排序算法，就是归并排序的优化版本。

从上文的图中可看出，每次合并操作的平均时间复杂度为O(n)，而完全二叉树的深度为|log2n|。总的平均时间复杂度为O(nlogn)。而且，归并排序的最好，最坏，平均时间复杂度均为O(nlogn)。



```c++
void mergeSort(vector<int> &nums, int left, int right) {
    if (left >= right) return ;
    int mid = left + (right - left)/2;
    mergeSort(nums, left, mid);
    mergeSort(nums, mid + 1, right);
    
    merge(nums, left, mid, right);
}

void merge(vector<int> &nums, int left, int mid, int right) {   //合并两个有序数组：借用一个额外的数组，依次比较nums1, nums2把较小的填进去
    vector<int> tmp(right - left + 1, 0);
    int i = left, j = mid + 1, k = 0;
    while (i <= mid && j <= right) {                            //合并两个有序数组，三段式要记住
        tmp[k++] = nums[i] <= nums[j] ? nums[i] : nums[j];
    }
    while (i <= mid) tmp[k++] = nums[i++];
    while (j <= right) tmp[k++] = nums[j++];
    
    for (i = left, k = 0; i <= right;) nums[i++] = tmp[k++];
}
```























​														 