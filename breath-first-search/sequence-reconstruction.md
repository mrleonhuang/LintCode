# 605. Sequence Reconstruction \[LintCode\]

> Check whether the original sequence  org  can be uniquely reconstructed from the sequences in  seqs .The org sequence is a permutation of the integers from 1 to n, with 1 ≤ n ≤ 10^4. Reconstruction means building a shortest common supersequence of the sequences in  seqs  \(i.e., a shortest sequence so that all sequences in  seqs  are subsequences of it\). Determine whether there is only one sequence that can be reconstructed from  seqs  and it is the  org  sequence.
>
> **Example**
>
> ```
> Given org = [1,2,3], seqs = [[1,2],[1,3]]
> Return false
> Explanation:
> [1,2,3] is not the only one sequence that can be reconstructed, because [1,3,2] is also a valid sequence that can be reconstructed.
>
> Given org = [1,2,3], seqs = [[1,2]]
> Return false
> Explanation:
> The reconstructed sequence can only be [1,2].
>
> Given org = [1,2,3], seqs = [[1,2],[1,3],[2,3]]
> Return true
> Explanation:
> The sequences [1,2], [1,3], and [2,3] can uniquely reconstruct the original sequence [1,2,3].
>
> Given org = [4,1,5,2,6,3], seqs = [[5,2,6,3],[4,1,5,2]]
> Return true
> ```

思路和Course Schedule是一样的，seqs中定义了序列的先后顺序要求（类似于Course Schedule中先修课关系）。通常情况下可以用两组HashMap来维护关系：

```java
Map<Integer, Set<Integer> map = new HashMap<>();
Map<Integer, Integer> preCounts = new HashMap<>();
```

但是因为数据本身是Integer，所以可以和Course Schedule一样用数组来表示，可以用数字本身就是index。BFS的Queue中如果每一层有大于1个的数字，说明有大于1个选择，序列则不唯一，返回false；如果最终序列长度和原始序列不一样也返回false

注意的易错点：

* 数字是从1 - n，所以数组要开org.length + 1个，并且数据从index为1开始填入

* 这道题edge cases特别多！初始化preCounts数组为-1，代表该数没有在seqs中出现，确定该下标的数字在seqs中出现了再初始化为0；防止edge case of

```
org = [1], seqs = [[],[]]
```

* 计算preCounts中每个数字的前序数字长度时，要判断seqs中的数字是否outOfBound，防止edge case of

```
org = [1, 2, 3, 4, 5], seqs = [[1,2] .... [1, 10000]];
```

```java
// solution 1
public class Solution {
    /*
     * @param org: a permutation of the integers from 1 to n
     * @param seqs: a list of sequences
     * @return: true if it can be reconstructed only one or false
     */
    public boolean sequenceReconstruction(int[] org, int[][] seqs) {
        // write your code here
        if (org == null || seqs == null) {
            return false;
        }
        int[] preCounts = new int[org.length + 1];
        List[] edges = new ArrayList[org.length + 1];
        for (int i = 1; i < edges.length; i++) {
            edges[i] = new ArrayList<Integer>();
        }
        Arrays.fill(preCounts, -1);
        for (int i = 0; i < seqs.length; i++) {
            int[] seq = seqs[i];
            for (int j = 0; j < seq.length; j++) {
                if (seq[j] <= 0 || seq[j] > org.length) {
                    return false;
                }
                preCounts[seq[j]] = preCounts[seq[j]] == -1 ? 0 : preCounts[seq[j]];
            }
            for (int j = 0; j < seq.length - 1; j++) {
                edges[seq[j]].add(seq[j + 1]);
                preCounts[seq[j + 1]]++;
            }
        }
        Queue<Integer> queue = new LinkedList<Integer>();
        int length = 0;
        for (int i = 1; i < preCounts.length; i++) {
            if (preCounts[i] == 0) {
                queue.offer(i);
            }
        }
        while (!queue.isEmpty()) {
            if (queue.size() > 1) {
                return false;
            }
            int head = (int) queue.poll();
            length++;
            for (int i = 0; i < edges[head].size(); i++) {
                int next = (int) edges[head].get(i);
                preCounts[next]--;
                if (preCounts[next] == 0) {
                    queue.offer(next);
                }
            }
        }
        return length == org.length;
    }
}

// solution 2
public class Solution {
    /*
     * @param org: a permutation of the integers from 1 to n
     * @param seqs: a list of sequences
     * @return: true if it can be reconstructed only one or false
     */
    public boolean sequenceReconstruction(int[] org, int[][] seqs) {
        // write your code here
        if (org == null || seqs == null) {
            return false;
        }
        Map<Integer, Set<Integer>> map = new HashMap<>();
        Map<Integer, Integer> preCounts = new HashMap<Integer, Integer>();
        for (int num : org) {
            map.put(num, new HashSet<Integer>());
            preCounts.put(num, 0);
        }
        int n = org.length;
        int count = 0;
        for (int[] seq : seqs) {
            count += seq.length;
            for (int num : seq) {
                if (num <= 0 || num > n) {
                    return false;
                }
            }
            for (int i = 1; i < seq.length; i++) {
                if (map.get(seq[i - 1]).add(seq[i])) {
                    preCounts.put(seq[i], preCounts.get(seq[i]) + 1);
                }
            }
        }
        // case: [1], []
        if (count < n) {
            return false;
        }
        Queue<Integer> queue = new LinkedList<Integer>();
        for (Map.Entry<Integer, Integer> entry : preCounts.entrySet()) {
            if (entry.getValue() == 0) {
                queue.offer(entry.getKey());
            }
        }
        int cnt = 0;
        while (queue.size() == 1) {
            int head = queue.poll();
            for (int next : map.get(head)) {
                preCounts.put(next, preCounts.get(next) - 1);
                if (preCounts.get(next) == 0) {
                    queue.offer(next);
                }
            }
            if (head != org[cnt]) {
                return false;
            }
            cnt++;
        }
        return cnt == org.length;
    }
}
```



