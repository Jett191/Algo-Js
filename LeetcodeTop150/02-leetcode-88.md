# Lettcode-88

### 题目

给你两个按 **非递减顺序** 排列的整数数组 `nums1` 和 `nums2`，另有两个整数 `m` 和 `n` 

，分别表示 `nums1` 和 `nums2` 中的元素数目。



请你 **合并** `nums2` 到 `nums1` 中，使合并后的数组同样按 **非递减顺序** 排列。

**注意：**最终，合并后数组不应由函数返回，而是存储在数组 `nums1` 中。为了应对这种情

况，`nums1` 的初始长度为 `m + n`，其中前 `m` 个元素表示应合并的元素，后 `n` 个元素

为 `0` ，应忽略。`nums2` 的长度为 `n` 。



输入：nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3

输出：[1,2,2,3,5,6]

解释：需要合并 [1,2,3] 和 [2,5,6] 。

合并结果是 [1,2,2,3,5,6] ，其中斜体加粗标注的为 nums1 中的元素。





### 解题思路

- 先将数组进行合并
- 进行排序
- 根据 `m`、`n` 将合并后的数组的0元素排除，

- 两个数组需要合并后按非递减顺序排列，因为最后是返回 `nums1` ,并且它的初始长度

  为 `m+n` 。在 `nums1` 中有n个 `0` 元素，在 `nums2` 中一共有n个元素，相当于将 

  `nums2` 的元素与 `nums1` 的 `0` 元素进行替换。 合并后的数组不应有值为 `0` 的元素

  



### 代码



JS方法

```js
const merge = function (nums1, m, nums2, n) {
//将 nums1 从 m 开始切断后面的n个 0 元素，并将nums2拼接上去
    nums1.splice(m, n, ...nums2);
//将合并好的数组进行排序
    nums1.sort((a, b) => a - b);
};
```





手写

```js
const merge = function(nums1, m, nums2, n) {
  
    // 初始化两个指针，分别指向nums1和nums2的有效元素的末尾
    let p1 = m - 1;
    let p2 = n - 1;

    // 初始化一个指针，指向nums1数组的末尾，用于存放合并后的元素
    let p = m + n - 1;

    // 从后向前遍历，将两个数组中较大的元素放入nums1的末尾
    while (p1 >= 0 && p2 >= 0) {
        if (nums1[p1] > nums2[p2]) {
            nums1[p--] = nums1[p1--];
        } else { 
            nums1[p--] = nums2[p2--];
        }
    }

    // 如果nums2中还有元素未处理，将其复制到nums1中
    while (p2 >= 0) {
        nums1[p--] = nums2[p2--];
    }

};

```



