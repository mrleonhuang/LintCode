# 613. High Five

> There are two properties in the node student
>
> `id`and `scores`, to ensure that each student will have at least 5 points, find the average of 5 highest scores for each person.
>
> **Example**
>
> ```
> Given results = [[1,91],[1,92],[2,93],[2,99],[2,98],[2,97],[1,60],[1,58],[2,100],[1,61]]
>
> Return
> ```

```java
/**
 * Definition for a Record
 * class Record {
 *     public int id, score;
 *     public Record(int id, int score){
 *         this.id = id;
 *         this.score = score;
 *     }
 * }
 */
public class Solution {
    /**
     * @param results a list of <student_id, score>
     * @return find the average of 5 highest scores for each person
     * Map<Integer, Double> (student_id, average_score)
     */
    public Map<Integer, Double> highFive(Record[] results) {
        // Write your code here
        if (results == null || results.length == 0) {
            return new HashMap<Integer, Double>();
        }
        HashMap<Integer, PriorityQueue<Integer>> minHeapMap = new HashMap<Integer, PriorityQueue<Integer>>();
        for (Record record : results) {
            if (!minHeapMap.containsKey(record.id)) {
                PriorityQueue<Integer> minHeap = new PriorityQueue<Integer>(6);
                minHeap.offer(record.score);
                minHeapMap.put(record.id, minHeap);
            } else {
                PriorityQueue<Integer> minHeap = minHeapMap.get(record.id);
                minHeap.offer(record.score);
                if (minHeap.size() == 6) {
                    minHeap.poll();
                }
            }
        }
        Map<Integer, Double> highFiveMap = new HashMap<Integer, Double>();
        for (Map.Entry<Integer, PriorityQueue<Integer>> entry : minHeapMap.entrySet()) {
            int id = entry.getKey();
            PriorityQueue<Integer> minHeap = entry.getValue();
            int size = minHeap.size();
            int sum = 0;
            while (!minHeap.isEmpty()) {
                sum += minHeap.poll();
            }
            highFiveMap.put(id, (double) sum / size);
        }
        return highFiveMap;
    }
}
```



