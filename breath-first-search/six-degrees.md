# 531. Six Degrees \[LintCode\]

> Six degrees of separation is the theory that everyone and everything is six or fewer steps away, by way of introduction, from any other person in the world, so that a chain of "a friend of a friend" statements can be made to connect any two people in a maximum of six steps.
>
> Given a friendship relations, find the degrees of two people, return`-1`if they can not been connected by friends of friends.
>
> **Example**
>
> Gien a graph:
>
> ```
> 1------2-----4
>  \          /
>   \        /
>    \--3--/
> ```
>
> `{1,2,3#2,1,4#3,1,4#4,2,3}`and s =`1`, t =`4`return`2`
>
> Gien a graph:
>
> ```
> 1      2-----4
>              /
>            /
>           3
> ```
>
> `{1#2,4#3,4#4,2,3}`and s =`1`, t =`4`return`-1`

```java
/**
 * Definition for Undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     List<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { 
 *         label = x;
 *         neighbors = new ArrayList<UndirectedGraphNode>(); 
 *     }
 * };
 */
public class Solution {
    /**
     * @param graph a list of Undirected graph node
     * @param s, t two Undirected graph nodes
     * @return an integer
     */
    public int sixDegrees(List<UndirectedGraphNode> graph,
                          UndirectedGraphNode s,
                          UndirectedGraphNode t) {


        if(graph == null || s == null || t == null)
            return -1;

        int degree = 0;
        Set<UndirectedGraphNode> set = new HashSet<UndirectedGraphNode>();
        Queue<UndirectedGraphNode> queue = new LinkedList<UndirectedGraphNode>();
        queue.offer(s);
        set.add(s);
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i = 0; i < size; i++){
                UndirectedGraphNode node = queue.poll();
                if(node.label == t.label){
                    return degree;
                }
                for(UndirectedGraphNode nei : node.neighbors){
                    if(!set.contains(nei)){
                        queue.offer(nei);
                        set.add(nei);
                    }
                }
            }
            degree++;
        }
        return -1;
    }
}
```



