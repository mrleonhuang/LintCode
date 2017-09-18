# 349. Intersection of Two Arrays \[LeetCode\]

> Given two arrays, write a function to compute their intersection.
>
> **Example:**  
> Givennums1=`[1, 2, 2, 1]`,nums2=`[2, 2]`, return`[2]`.
>
> **Note:**
>
> * Each element in the result must be unique.
> * The result can be in any order.

1. 用两个HashSet，第二个HashSet用来去重 O\(m + n\) 
2. Sort 2 Arrays + Two Pointers O\(nlogn + mlogm + m + n\)
3. Sort 1 Array + Binary Search O\(nlogn + mlogn\)

* 注意开结果数组的长度为确定的intersection的长度，而不是nums1或者nums2或者temp的长度，因为多余的长度会被默认值0填充！
* 方法2当pt1和pt2所指向的数相等时，要判断是否和temp里前一个数相同，来保证不重复。

```java
// solution 1
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        if (nums1 == null || nums2 == null || nums1.length == 0 || nums2.length == 0) {
            return new int[0];
        }
        Set<Integer> set = new HashSet<Integer>();
        Set<Integer> intersection = new HashSet<Integer>();
        for (int num : nums1) {
            set.add(num);
        }
        for (int num : nums2) {
            if (set.contains(num)) {
                intersection.add(num);
            }
        }
        int[] results = new int[intersection.size()];
        int index = 0;
        for (Integer num : intersection) {
            results[index++] = (int) num;
        }
        return results;
    }
}

// solution 2
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        if (nums1 == null || nums2 == null || nums1.length == 0 || nums2.length == 0) {
            return new int[0];
        }
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int[] temp = new int[Math.min(nums1.length, nums2.length)];
        int index = 0;
        int pt1 = 0;
        int pt2 = 0;
        while (pt1 < nums1.length && pt2 < nums2.length) {
            if (nums1[pt1] < nums2[pt2]) {
                pt1++;
            } else if (nums1[pt1] > nums2[pt2]) {
                pt2++;
            } else {
                if (index == 0 || temp[index - 1] != nums1[pt1]) {
                    temp[index++] = nums1[pt1];    
                }
                pt1++;
                pt2++;
            }
        }
        int[] results = new int[index];
        index = 0;
        while (index < results.length) {
            results[index] = temp[index];   
            index++;
        }
        return results;
    }
}

// solution 3
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        if (nums1 == null || nums2 == null || nums1.length == 0 || nums2.length == 0) {
            return new int[0];
        }
        Arrays.sort(nums1);
        Set<Integer> set = new HashSet<Integer>();
        for (int num : nums2) {
            if (set.contains(num)) {
                continue;
            }
            if (binarySearch(nums1, num)) {
                set.add(num);
            }
        }
        int[] results = new int[set.size()];
        int index = 0;
        for (Integer num : set) {
            results[index++] = (int) num;
        }
        return results;
    }
    
    private boolean binarySearch(int[] nums, int target) {
        int start = 0;
        int end = nums.length - 1;
        int mid;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (nums[mid] < target) {
                start = mid;
            } else if (nums[mid] > target) {
                end = mid;
            } else {
                return true;
            }
        }
        if (nums[start] == target || nums[end] == target) {
            return true;
        }
        return false;
    }
}
```



