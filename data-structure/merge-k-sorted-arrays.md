# 486. Merge k Sorted Arrays

> Given _k _sorted integer arrays, merge them into one sorted array.
>
> **Example**
>
> Given 3 sorted arrays:
>
> ```
> [
>   [1, 3, 5, 7],
>   [2, 4, 6],
>   [0, 8, 9, 10, 11]
> ]
>
> return[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11].
> ```

**与Merge K Sorted Lists类似。**

1. **Heap \(PriorityQueue\) + HashMap，HashMap中记录每一个array下一个插入元素的index**

2. **递归Merge Two Sorted Arrays**

3. **Merge Two By Two不好写，因为数组的长度是固定的，不好像list那样可以判断长度来决定merge与否。**

```java
// solution 1
class Pair {
    int value;
    int index;
    public Pair(int value, int index) {
        this.value = value;
        this.index = index;
    }
}

public class Solution {
    /**
     * @param arrays k sorted integer arrays
     * @return a sorted array
     */
    public List<Integer> mergekSortedArrays(int[][] arrays) {
        // Write your code here
        List<Integer> sorted = new ArrayList<Integer>();
        if (arrays == null || arrays.length == 0) {
            return sorted;
        }
        PriorityQueue<Pair> queue = new PriorityQueue<Pair>(arrays.length, new Comparator<Pair>(){
            public int compare(Pair x, Pair y) {
                return x.value - y.value;
            }
        });
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < arrays.length; i++) {
            if (arrays[i].length > 0) {
                map.put(i, 0);
            }
        }
        for (int ith : map.keySet()) {
            queue.offer(new Pair(arrays[ith][0], ith));
            map.put(ith, map.get(ith) + 1);
        }
        while (!queue.isEmpty()) {
            Pair minPair = queue.poll();
            sorted.add(minPair.value);
            if (map.get(minPair.index) < arrays[minPair.index].length) {
                int nextNumberIndex = map.get(minPair.index);
                queue.offer(
                    new Pair(arrays[minPair.index][nextNumberIndex], 
                            minPair.index)
                    );
                map.put(minPair.index, nextNumberIndex + 1);
            }
        }
        return sorted;
    }
}

// solution 2
public class Solution {
    /**
     * @param arrays k sorted integer arrays
     * @return a sorted array
     */
    public List<Integer> mergekSortedArrays(int[][] arrays) {
        // Write your code here
        List<Integer> sortedList = new ArrayList<Integer>();
        if (arrays == null || arrays.length == 0) {
            return sortedList;
        }
        int[] sortedArray = helper(arrays, 0, arrays.length - 1);
        for (int i = 0; i < sortedArray.length; i++) {
            sortedList.add(sortedArray[i]);
        }
        return sortedList;
    }
    
    private int[] helper(int[][] arrays, int start, int end) {
        if (start == end) {
            return arrays[start];
        }
        int mid = start + (end - start) / 2;
        int[] array1 = helper(arrays, start, mid);
        int[] array2 = helper(arrays, mid + 1, end);
        return mergeTwoArrays(array1, array2);
    }
    
    private int[] mergeTwoArrays(int[] array1, int[] array2) {
        if (array1.length == 0) {
            return array2;
        }
        if (array2.length == 0) {
            return array1;
        } 
        int[] sortedArray = new int[array1.length + array2.length];
        int i = 0;
        int j = 0;
        int index = 0;
        while (i < array1.length && j < array2.length) {
            if (array1[i] < array2[j]) {
                sortedArray[index++] = array1[i++];
            } else {
                sortedArray[index++] = array2[j++];
            }
        }
        while (i < array1.length) {
            sortedArray[index++] = array1[i++];
        }
        while (j < array2.length) {
            sortedArray[index++] = array2[j++];
        }
        return sortedArray;
    }
}
```



