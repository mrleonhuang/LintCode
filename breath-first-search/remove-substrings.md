## 624. Remove Substrings \[LintCode\]

> Given a string`s`and a set of `n`substrings. You are supposed to remove every instance of those n substrings from s so that s is of the minimum length and output this minimum length.
>
> **Example**
>
> Given s =`ccdaabcdbb`, substrs =`["ab", "cd"]`  
> Return`2`
>
> Explanation:  
> `ccdaabcdbb`-&gt;`ccdacdbb`-&gt;`cabb`-&gt;`cb`\(length = 2\)

宽度优先搜索Queue + HashSet去重，对于每一层（放进queue的每一个长度的）的String，用尽dictionary中的每一个substring；对于每一个substring，从当前String中的每一个可能的start index中尽可能搜索到。查找当前String中是否存在substring的方法：

```java
str.indexOf(String sub, int fromIndex)
```

```java
public class Solution {
    /**
     * @param s a string
     * @param dict a set of n substrings
     * @return the minimum length
     */
    public int minLength(String s, Set<String> dict) {
        // Write your code here
        if (s == null || s.length() == 0) {
            return 0;
        }
        if (dict == null || dict.size() == 0) {
            return s.length();
        }
        Queue<String> queue = new LinkedList<String>();
        Set<String> set = new HashSet<String>();
        int min = s.length();
        queue.offer(s);
        set.add(s);
        while (!queue.isEmpty()) {
            String str = queue.poll();
            for (String sub : dict) {
                int start = str.indexOf(sub);
                while (start != -1) {
                    String newStr = str.substring(0, start) + str.substring(start + sub.length(), str.length());
                    if (!set.contains(newStr)) {
                        min = Math.min(min, newStr.length());
                        queue.offer(newStr);
                        set.add(newStr);
                    }
                    start = str.indexOf(sub, start + 1);
                }
            }
        }
        return min;
    }
}
```



