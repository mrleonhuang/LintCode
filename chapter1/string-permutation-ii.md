# 10. String Permutation II

> Given a string, find all permutations of it without duplicates.
>
> **Example**
>
> Given`"abb"`, return`["abb", "bab", "bba"]`.
>
> Given`"aabb"`, return`["aabb", "abab", "baba", "bbaa", "abba", "baab"]`.

* **类似于Permutation II，不同点在于全排列不是List是String**

* **将String排序的方法：str.toCharArray\(\) → Arrays.sort\(charArr\)**

* **dfs遍历，将char临时存在List&lt;Character&gt;中，最后再用StringBuilder构建String**

      **`dfs(char[]arr,boolean[]used,List<Character>permutation,List<String>results)`**

* **去重机制与Permutation II一样，用boolean数组记录元素是否使用，并且用去重三要素杀手锏（排序+startIndex+比较）**

* **错误：String为null和长度为0情况不一样，dfs搜索易错点**

```java
public class Solution {
    /*
     * @param str: A string
     * @return: all permutations
     */
    public List<String> stringPermutation2(String str) {
        // write your code here
        List<String> results = new ArrayList<String>();
        if (str == null) {
            return results;
        }
        if (str.length() == 0) {
            results.add(new String(""));
            return results;
        }
        char[] arr = str.toCharArray();
        Arrays.sort(arr);
        List<Character> permutation = new ArrayList<Character>();
        boolean[] used = new boolean[arr.length];
        dfs(arr, used, permutation, results);
        return results;
    }

    private void dfs(char[] arr, boolean[] used, List<Character> permutation, List<String> results) {
        if (permutation.size() == arr.length) {
            StringBuilder sb = new StringBuilder();
            for (Character c : permutation) {
                sb.append(c);
            }
            results.add(new String(sb.toString()));
            return;
        }
        for (int i = 0; i < arr.length; i++) {
            if (used[i]) {
                continue;
            }
            if (i != 0 && arr[i] == arr[i - 1] && !used[i - 1]) {
                continue;
            }
            permutation.add(arr[i]);
            used[i] = true;
            dfs(arr, used, permutation, results);
            permutation.remove(permutation.size() - 1);
            used[i] = false;
        }
    }
}
```



