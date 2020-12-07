```java
class Solution {
    public List<String> generateParenthesis(int n) {
        return generate(n,n,"");
    }
    
    public List<String> generate(int l, int r, String s){
        List<String> res = new LinkedList<String>();
        if(l == 0 && r == 0){
            res.add(s);
            return res;
        }
        if(l == 0){
            return generate(l, r-1, s+')');
        }
        if (l == r){
            return generate(l-1, r, s+'(');
        } else{
            res = generate(l-1, r, s+'(');
            res.addAll(generate(l, r-1, s+')'));
            return res;
        }
    } 
}
```