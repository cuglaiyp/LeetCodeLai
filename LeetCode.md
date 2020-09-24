# LeetCode

## 滑动窗口

[3. 无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

[209. 长度最小的子数组](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)

## 拓扑排序

[207. 课程表](https://leetcode-cn.com/problems/course-schedule/)

[210. 课程表 II](https://leetcode-cn.com/problems/course-schedule-ii/)

## 排序

[215. 数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)(堆排序、快排)

## 回溯算法

[216. 组合总和 III](https://leetcode-cn.com/problems/combination-sum-iii/)

## 动态规划

[221. 最大正方形](https://leetcode-cn.com/problems/maximal-square/)

##### 1. 完全背包问题

[322. 零钱兑换](https://leetcode-cn.com/problems/coin-change/)

[518. 零钱兑换 II](https://leetcode-cn.com/problems/coin-change-2/)

##### 2. 0-1背包问题

[416. 分割等和子集](https://leetcode-cn.com/problems/partition-equal-subset-sum/)

[474. 一和零](https://leetcode-cn.com/problems/ones-and-zeroes/)

##### 3. 股票买卖问题

[121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

[122. 买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

[123. 买卖股票的最佳时机 III](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)

[188. 买卖股票的最佳时机 IV](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iv/)

[309. 最佳买卖股票时机含冷冻期](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

[714. 买卖股票的最佳时机含手续费](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

##### 4. 打家劫舍问题

[198. 打家劫舍](https://leetcode-cn.com/problems/house-robber/)

[213. 打家劫舍 II](https://leetcode-cn.com/problems/house-robber-ii/)

[337. 打家劫舍 III](https://leetcode-cn.com/problems/house-robber-iii/)（**树形动态规划**）

##### 动态规划的一点思路

<img src="LeetCode.assets/image-20200923152848338.png" alt="image-20200923152848338" style="zoom:80%;" />

## 位运算

[231. 2的幂](https://leetcode-cn.com/problems/power-of-two/)

## 二叉树的遍历

[222. 完全二叉树的节点个数](https://leetcode-cn.com/problems/count-complete-tree-nodes/)

[230. 二叉搜索树中第K小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/)

[235. 二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

[236. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)

## Map的运用

[217. 存在重复元素](https://leetcode-cn.com/problems/contains-duplicate/)

[219. 存在重复元素 II](https://leetcode-cn.com/problems/contains-duplicate-ii/)

[220. 存在重复元素 III](https://leetcode-cn.com/problems/contains-duplicate-iii/)

## 栈

[232. 用栈实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/)

## 快慢指针

[234. 回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)

## 链表操作

[237. 删除链表中的节点](https://leetcode-cn.com/problems/delete-node-in-a-linked-list/)

## 子串查找算法

##### 1. KMP算法

[28. 实现 strStr()](https://leetcode-cn.com/problems/implement-strstr/)

~~~java
/**
 * 构建next数组。算法核心，必须理解。
*/
private int[] getNext(String needle) {
    int len = needle.length();
    int[] next = new int[len];
    // j就是遍历的下标。外循环每次都会+1
    // i很关键，表示应跳转的下标，也对应着needle的j下标前面匹配的对数。后面详解。
    int j = 0, i = -1;
    // 先初始化next[0] = -1。因为needle下标为0，不可能有匹配的。为什么要设置为-1，而不是0呢。在下面内循环中可以用i = -1作为退出循环的条件
    next[j] = i;
    while (j < len) {
        // i >= 0的时候说明还有匹配到的可能。所以判断一下两个字符是否相等。不相等就把i回退。这里需要画图理解。
        while (i >= 0 && needle.charAt(i) != needle.charAt(j)) {
            i = next[i];
        }
        // i代表的是上一次匹配成功的个数，所以这一次需要在上一次的基础上+1
        i++;
        // j代表的是上一次的needle下标，这里要更新为这次的
        j++;
        // 如果不越界，填充next数组的值
        if (j < len)
            next[j] = i;
    }
    return next;
}
~~~

上面的文字解析不是很清楚，下面我们画图抽丝剥茧把这个搞明白。

来一个needle字符串**`abaababb`**，一个数组**`int[] next`**。匹配的机制是j下标前的字符，前半段有多少与后半段相同。

1. 初始化：`next[j] = i;`

   

   <img src="LeetCode.assets/kmp-1.png" alt="kmp-1" style="zoom:50%;" />

   **注：**字符对应的数字（比如：1a对应的-1）表示的是：**到a这发生了不匹配，下标需要跳转到的位置**，同时也表示的是**a前面字符匹配的对数**

2. 遍历生成next

   <img src="LeetCode.assets/kmp-2-1600163087851.png" style="zoom:50%;" />

   1b对应为0，因为前面只有一个a，没有能够匹配的。

   <img src="LeetCode.assets/kmp-3.png" style="zoom:50%;" />

   2a对应为0，因为前面的a、b不匹配

   <img src="LeetCode.assets/kmp-4.png" style="zoom:50%;" />

   3a对应为1，因为前面0a和2a匹配上了，当在4a处与文本串发生不匹配时（此时3a已经匹配上了），模式串只需返回到下标为1处。判断1b能不能与文本串匹配，0a就不用管了，因为它与2a匹配上了，所以必定会与文本串匹配上。见下图：

   <img src="LeetCode.assets/kmp-5.png" style="zoom:50%;" />

   <img src="LeetCode.assets/kmp-6.png" style="zoom:50%;" />

   4b对应的下标或者说前面匹配的个数，分了两步，也就是内循环了一次。因为在找3a的时候，已经发现0a和2a匹配上了，所以那么再看一下1和3位置的字符能否匹配。如果匹配上了，也就是ab ab，那么4b对应的就为i+1 = 2了（i保存了上一次匹配对数或者下标的信息）。但是这时候没有匹配上，那么导致内循环一次，**`i = next[i]`。这句代码是什么意思呢？i 处与 j 处没匹配上，因为相当于自己匹配自己，所以 i 需要通过next数组回退，用尽量少的次数找一个能与 j 处字符匹配的地方 **

   <img src="LeetCode.assets/kmp-7.png" style="zoom:50%;" />

   在5a处，同理，因为 i 记录了上一次的1，正因为 i 又是记录着下标的信息，所以在正好判断 i 处字符（此处为1b）是否等于 j 处字符，而1b 与 4b相同，所以5a为2。

   <img src="LeetCode.assets/kmp-8.png" style="zoom:50%;" />

   同上

   <img src="LeetCode.assets/kmp-9.png" style="zoom:50%;" />

   同上

##### 2. sunday算法

需要用map记住每个元素最靠右的位置

## 堆

[295. 数据流的中位数](https://leetcode-cn.com/problems/find-median-from-data-stream/)

