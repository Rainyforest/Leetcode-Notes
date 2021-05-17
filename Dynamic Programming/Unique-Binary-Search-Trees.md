### [Unique Binary Search Trees](https://leetcode.com/problems/unique-binary-search-trees/)
Naive solution
```java
class Solution {
    public int numTrees(int n) {
        if(n<=1) return 1;
        int sum = 0;
        for(int i = 1; i <= n; i++){
            sum += numTrees(i-1)*numTrees(n-i);
        }
        return sum;
    }
}
```
After realizing the importance of DP
```java
class Solution {
    int[] numArray = new int[19];
    public int numTrees(int n) {
        if(n<=1) return 1;
        if(numArray[n-1]!= 0)return numArray[n-1];
        int sum = 0;
        for(int i = 1; i <= n; i++){
            sum += numTrees(i-1)*numTrees(n-i);
        }
        numArray[n-1] = sum;
        return sum;
    }
}
```
Improved version: [Formula Simplification](https://leetcode.com/problems/unique-binary-search-trees/discuss/31666/DP-Solution-in-6-lines-with-explanation.-F(i-n)-G(i-1)-*-G(n-i))
```java
public int numTrees(int n) {
  int [] G = new int[n+1];
  G[0] = G[1] = 1;
    
  for(int i=2; i<=n; ++i) {
    for(int j=1; j<=i; ++j) {
      G[i] += G[j-1] * G[i-j];
    }
  }
  return G[n];
}
```
- Avoid declaration of global variables
- No recursions
