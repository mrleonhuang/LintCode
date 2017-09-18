# 211. String Permutation \[LintCode\]

> Given two strings, write a method to decide if one is a permutation of the other.
>
> **Example**
>
> `abcd`is a permutation of`bcad`, but`abbe`is not a permutation of`abe`

用数组来记录第一个String中每一个char的出现频率，然后遍历第二个String把出现的char的从数组中减去。如果刚好数组中每一个char的频率都是0，说明是permutation.

```java
public class Solution {
    /**
     * @param A a string
     * @param B a string
     * @return a boolean
     */
    public boolean stringPermutation(String A, String B) {

        if (A == null  || B == null) {
            return false;
        }    
        int[] counter = new int[200];

        for (int i = 0; i < A.length(); i++) {
            counter[A.charAt(i)]++;
        }
        for (int j = 0; j < B.length(); j++) {
            counter[B.charAt(j)]--;
        }
        for (int count : counter) {
            if (count != 0) {
                return false;
            }
        }
        return true;
    }
}
```



