## 471. Top K Frequent Words \[LintCode\]

> Given a list of words and an integer k, return the top k frequent words in the list.
>
> ##### Notice
>
> You should order the words by the frequency of them in the return list, the most frequent one comes first. If two words has the same frequency, the one with lower alphabetical order come first.
>
> **Example**
>
> Given
>
> ```
> [
>     "yes", "lint", "code",
>     "yes", "code", "baby",
>     "you", "baby", "chrome",
>     "safari", "lint", "code",
>     "body", "lint", "code"
> ]
> ```
>
> for k =`3`, return`["code", "lint", "baby"]`.
>
> for k =`4`, return`["code", "lint", "baby", "yes"]`,

方法1：HashMap计数 + maxHeap排序, 用HashMap统计每一个单词的频率。然后组建一个Pair扔进PriorityQueue来进行排序。

* 如果频率不同，则按照频率排序；如果频率相同，则按照alphabetical order排序

```java
       Comparator<Pair> pairComparator = new Comparator<Pair>() {
        public int compare(Pair x, Pair y) {
            if (x.count != y.count) {
                return y.count - x.count;
            }
            return x.word.compareTo(y.word);    
        }
    }
```

* 如果自定义的class中的attributes设置为private的话，在comparator中就不能访问到，所以如果需要访问attribute来构建comparator的话，atrribute不能设置为private

* 遍历Map的Entry的时候用Map.Entry&lt;String, Integer&gt;

```java
// solution 1
class Pair {
    String word;
    int count;
    public Pair(String word, int count) {
        this.word = word;
        this.count = count;
    }
}

public class Solution {
    /**
     * @param words an array of string
     * @param k an integer
     * @return an array of string
     */
    public String[] topKFrequentWords(String[] words, int k) {
        // Write your code here
        if (words == null || words.length == 0 || words.length < k) {
            return new String[0];
        }
        HashMap<String, Integer> counter = new HashMap<String, Integer>();
        for (String word : words) {
            if (counter.containsKey(word)) {
                counter.put(word, counter.get(word) + 1);
            } else {
                counter.put(word, 1);
            }
        }
        PriorityQueue<Pair> maxHeap = new PriorityQueue<Pair>(words.length, new Comparator<Pair>(){
            public int compare(Pair x, Pair y) {
                if (x.count != y.count) {
                    return y.count - x.count;
                }
                return x.word.compareTo(y.word);
            }
        });
        for (Map.Entry<String, Integer> entry : counter.entrySet()) {
            Pair newPair = new Pair(entry.getKey(), entry.getValue());
            maxHeap.offer(newPair);
        }
        String[] results = new String[k];
        for (int i = 0; i < k; i++) {
            results[i] = maxHeap.poll().word;
        }
        return results;
    }
}
```

方法2：HashMap计数 + minHeap排序

* Comparator需要改变顺序

* Reverse Array:

```java
     Collections.reverse(Arrays.asList(array));
```

```java

```

方法3： HashMap计数 + TreeMap + TreeSet

* 按照频率，把相同频率的word放在一个TreeSet里

* 易错点：如果Map&lt;String, Integer&gt;需要修改value的时候需要用map.put\(key, map.get\(key\) + 1\)的方法来实现；但是如果Map&lt;String, List&gt;需要修改value的时候直接map.get\(key\).add\(word\)即可。

```java




// solution 3
public class Solution {
    /**
     * @param words an array of string
     * @param k an integer
     * @return an array of string
     */
    public String[] topKFrequentWords(String[] words, int k) {
        // Write your code here
        if (words == null || words.length == 0 || words.length < k) {
            return new String[0];
        }
        HashMap<String, Integer> counter = new HashMap<String, Integer>();
        for (String word : words) {
            if (counter.containsKey(word)) {
                counter.put(word, counter.get(word) + 1);
            } else {
                counter.put(word, 1);
            }
        }
        TreeMap<Integer, TreeSet<String>> treeMap = new TreeMap<Integer, TreeSet<String>>();
        for (Map.Entry<String, Integer> entry : counter.entrySet()) {
            int freq = entry.getValue();
            String word = entry.getKey();
            if (!treeMap.containsKey(freq)) {
                TreeSet<String> treeSet = new TreeSet<String>();
                treeSet.add(word);
                treeMap.put(freq, treeSet);
            } else {
                treeMap.get(freq).add(word);
            }
        }
        String[] results = new String[k];
        int index = 0;
        while (index < k) {
            Map.Entry<Integer, TreeSet<String>> lastEntry = treeMap.pollLastEntry();
            while (index < k && lastEntry != null && lastEntry.getValue().size() > 0) {
                results[index] = lastEntry.getValue().pollFirst();
                index++;
            }
        }
        return results;
    }
}
```



