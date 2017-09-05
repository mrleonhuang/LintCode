# 447. Search in a Big Sorted Array

> Given a big sorted array with positive integers sorted by ascending order. The array is so big so that you can not get the length of the whole array directly, and you can only access the kth number by`ArrayReader.get(k)`\(or ArrayReader-&gt;get\(k\) for C++\). Find the first index of a target number. Your algorithm should be in O\(log k\), where k is the first index of the target number.
>
> Return -1, if the number doesn't exist in the array.
>
> ##### Notice
>
> If you accessed an inaccessible index \(outside of the array\), ArrayReader.get will return`2,147,483,647`.
>
> **Example**
>
> Given`[1, 3, 6, 9, 21, ...]`, and target =`3`, return`1`.
>
> Given`[1, 3, 6, 9, 21, ...]`, and target =`4`, return`-1`.

```java
/**
 * Definition of ArrayReader:
 * 
 * class ArrayReader {
 *      // get the number at index, return -1 if index is less than zero.
 *      public int get(int index);
 * }
 */
public class Solution {
    /**
     * @param reader: An instance of ArrayReader.
     * @param target: An integer
     * @return : An integer which is the index of the target number
     */
    public int searchBigSortedArray(ArrayReader reader, int target) {
        // write your code here
        if (reader == null) {
            return -1;
        }
        int k = 1;
        while (reader.get(k) < target) {
            k *= 2;
        }
        int left = k / 2;
        int right = k;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (reader.get(mid) < target) {
                left = mid;
            } else {
                right = mid;
            }
        }
        if (reader.get(left) == target) {
            return left;
        }
        if (reader.get(right) == target) {
            return right;
        }
        return -1;
    }
}
```



