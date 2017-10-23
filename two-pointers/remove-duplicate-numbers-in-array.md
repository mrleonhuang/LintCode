## 521. Remove Duplicate Numbers in Array \[LintCode\]

> Given an array of integers, remove the duplicate numbers in it.
>
> You should:  
> 1. Do it in place in the array.  
> 2. Move the unique numbers to the front of the array.  
> 3. Return the total number of the unique numbers.
>
> ##### Notice
>
> You don't need to keep the original order of the integers.
>
> **Example**
>
> Given _nums_=`[1,3,1,4,4,2]`, you should:
>
> 1. Move duplicate integers to the tail of _nums _=&gt; _nums=_`[1,3,4,2,?,?]`.
> 2. Return the number of unique integers in _nums _=&gt;`4`.
>
> Actually we don't care about what you place in`?`, we only care about the part which has no duplicate integers.

要把所有unique的元素顶到数组的最前面，这种情况肯定不能数组整体移动！！

两种方法：

1. O\(n\)时间 + O\(n\)空间：遍历数组元素加进HashSet，自动得到所有unique元素，再拷贝回原数组。

2. O\(nlogn\)时间： 将数组排序，所以重复元素会挤在一起。用一根指针index代表unique元素的最后位置，用for循环的i走在前面跟index元素作比较，如果一样，则i继续走，否则将i元素拷贝到index指针的下一位（方法巧妙没想到！！）。**根本思想是2根指针，一根作为先锋去探寻，第二根标记checked过的元素；类似于partition array和sort colors的思想。**

```java
// solution 1
public class Solution {
    /**
     * @param nums an array of integers
     * @return the number of unique integers
     */
    public int deduplication(int[] nums) {
        // Write your code here
        if (nums == null || nums.length == 0) {
            return 0;
        }
        Set<Integer> set = new HashSet<Integer>();
        for (int i = 0; i < nums.length; i++) {
            set.add(nums[i]);
        }
        int index = 0;
        for (int number : set) {
            nums[index++] = number;
        }
        return index;
    }
}

// solution 2
public class Solution {
    /**
     * @param nums an array of integers
     * @return the number of unique integers
     */
    public int deduplication(int[] nums) {
        // Write your code here
        if (nums == null || nums.length == 0) {
            return 0;
        }
        Arrays.sort(nums);
        int index = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != nums[index]) {
                nums[++index] = nums[i];
            } 
        }
        return index + 1;
    }
}
```



