### [All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/)

Naive solution
Use recursion
```java
class Solution {
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        return allPathsCurrentTarget(0,graph);
    }
    
    public List<List<Integer>> allPathsCurrentTarget(int curr, int[][] graph){
        List<List<Integer>> result = new LinkedList<>();
        //if end of graph, check target
        if(curr == graph.length - 1){
                List<Integer> path = new LinkedList<Integer>();
                path.add(curr);
                result.add(path);
        }else{
            if(graph[curr].length != 0){
                for(int i : graph[curr]){
                    result.addAll(allPathsCurrentTarget(i,graph));
                }
                for(List p : result){
                    p.add(0,curr);
                }
            }
        }
        
        return result;
    }
}
```
Improved solution
```python
class Solution:
    def allPathsSourceTarget(self, graph: List[List[int]]) -> List[List[int]]:
        end = len(graph)-1
        frontier = [[0]]
        paths = []
        while frontier:
            curr_path = frontier.pop(0)
            neighbors = graph[curr_path[-1]]
            for n in neighbors:
                if end == n:
                    paths.append(curr_path+[n])
                else:
                    frontier.append(curr_path+[n])
        return paths
```
