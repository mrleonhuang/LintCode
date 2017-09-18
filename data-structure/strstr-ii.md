# 594. strStr II \[LintCode\]

> Implement`strStr`function in O\(n + m\) time.
>
> `strStr`return the first index of the target string in a source string. The length of the target string is_m\_and the length of the source string is\_n_.  
> If target does not exist in source, just return -1.
>
> **Example**
>
> Given source =`abcdef`, target =`bcd`, return`1`.

维护一个HashMap&lt;Character, LinkedList&lt;Integer&gt;&gt;来记录source中所有char出现的index，如果target中的字母在HashMap里对应的queue中index是连续 +1 的，说明存在并返回第一个字母的index

错误：

* HashMap中存char用它对应的类Character

* 边界条件判断，如果target的长度是0，是所有String的subString，返回0，类似空集是所有集合的子集

* 每次遍历target的字母时候，在HashMap中找出对应queue，要看头元素是否比当前连续的index要小，如果小的话就poll出来

技巧：判断for循环是break出来的还是自然循环结束的，用 i 是否 == length来判断

```java
public class Solution {
    /**
     * @param source a source string
     * @param target a target string
     * @return an integer as index
     */
    public int strStr2(String source, String target) {
        // Write your code here
        if (source == null || target == null || source.length() < target.length()) {
            return -1;
        }
        if (target.length() == 0) {
            return 0;
        }
        HashMap<Character, LinkedList<Integer>> map = new HashMap<Character, LinkedList<Integer>>();
        for (int i = 0; i < source.length(); i++) {
            if (map.containsKey(source.charAt(i))) {
                LinkedList<Integer> queue = map.get(source.charAt(i));
                queue.offer(i);
            } else {
                LinkedList<Integer> queue = new LinkedList<Integer>();
                queue.offer(i);
                map.put(source.charAt(i), queue);
            }
        }
        if (!map.containsKey(target.charAt(0))) {
            return -1;
        }
        while (!map.get(target.charAt(0)).isEmpty()) {
            int start = map.get(target.charAt(0)).poll();
            int index = start;
            int i;
            for (i = 1; i < target.length(); i++) {
                if (!map.containsKey(target.charAt(i)) || map.get(target.charAt(i)).isEmpty()) {
                    return -1;
                }
                while (map.get(target.charAt(i)).peek() < index) {
                    map.get(target.charAt(i)).poll();
                }
                if (map.get(target.charAt(i)).peek() != index + 1) {
                    break;
                } 
                index = map.get(target.charAt(i)).poll();    
            }
            if (i == target.length()) {
                return start;
            }
        }
        return -1;    
    }
}
```



