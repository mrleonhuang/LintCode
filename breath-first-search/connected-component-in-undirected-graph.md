# 431. Connected Component in Undirected Graph

> Find the number connected component in the undirected graph. Each node in the graph contains a label and a list of its neighbors. \(a connected component \(or just component\) of an undirected graph is a subgraph in which any two vertices are connected to each other by paths, and which is connected to no additional vertices in the supergraph.\)
>
> ##### Notice
>
> Each connected component should sort by label.
>
> **Clarification**
>
> [Learn more about representation of graphs](http://www.lintcode.com/help/graph)
>
> **Example**
>
> Given graph:
>
> ```
> A------B  C
>  \     |  | 
>   \    |  |
>    \   |  |
>     \  |  |
>       D   E
>
> ```
>
> Return`{A,B,D}, {C,E}`. Since there are two connected component which is`{A,B,D}, {C,E}`

```java
/**
 * Definition for Undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
    /**
     * @param nodes a array of Undirected graph node
     * @return a connected set of a Undirected graph
     */
    public List<List<Integer>> connectedSet(ArrayList<UndirectedGraphNode> nodes) {
        // Write your code here
        
        List<List<Integer>> result = new ArrayList();
        if(nodes == null)
            return result;
            
        Map<UndirectedGraphNode, Boolean> visited = new HashMap();
        for(UndirectedGraphNode node : nodes){
            visited.put(node, false);
        }
        
        for(UndirectedGraphNode node : nodes){
            if(visited.get(node) == false){
                helper(node, visited, result);
            }
        }
        
        return result;
    }
    
    private void helper(UndirectedGraphNode node, Map<UndirectedGraphNode, Boolean> visited, 
                            List<List<Integer>> result){
        
        ArrayList<Integer> row = new ArrayList();
        Queue<UndirectedGraphNode> queue = new LinkedList<UndirectedGraphNode>();
        queue.offer(node);
        visited.put(node, true);
        
        while(!queue.isEmpty()){
            UndirectedGraphNode head = queue.poll();
            row.add(head.label);
            for(UndirectedGraphNode nei : head.neighbors){
                if(visited.get(nei) == false){
                    queue.offer(nei);
                    visited.put(nei, true);
                }
            }
        }
        
        Collections.sort(row);
        result.add(row);
    }
}
```



