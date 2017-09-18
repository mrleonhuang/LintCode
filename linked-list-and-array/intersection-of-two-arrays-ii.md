# 350. Intersection of Two Arrays II \[LeetCode\]

> Given two arrays, write a function to compute their intersection.
>
> **Example:**  
> Givennums1=`[1, 2, 2, 1]`,nums2=`[2, 2]`, return`[2, 2]`.
>
> **Note:**
>
> * Each element in the result should appear as many times as it shows in both arrays.
> * The result can be in any order.
>
> **Follow up:**
>
> * What if the given array is already sorted? How would you optimize your algorithm?
> * What if nums1's size is small compared to nums2's size? Which algorithm is better?
> * What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

1. 对比前一题solution1，本题要记录重复个数，所以需要HashMap + List的数据结构
2. 对比前一题solution2， 本题不用判断重复即可

* 如果一个大数组和一个小数组，则采用大数组里二分搜索小数组里的数！
* 总结结论：不计数用2 HashSet，计数用HashMap + List

```java
// solution 1
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        if (nums1 == null || nums2 == null || nums1.length == 0 || nums2.length == 0) {
            return new int[0];
        }
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int num : nums1) {
            if (map.containsKey(num)) {
                map.put(num, map.get(num) + 1);
            } else {
                map.put(num, 1);
            }
        }
        List<Integer> list = new ArrayList<Integer>();
        for (int num : nums2) {
            if (map.containsKey(num) && map.get(num) > 0) {
                list.add(num);
                map.put(num, map.get(num) - 1);
            }
        }
        int[] results = new int[list.size()];
        for (int i = 0; i < results.length; i++) {
            results[i] = list.get(i);
        }
        return results;
    }
}
```



