```java
//naive: hashset
class Solution {
    public int firstUniqChar(String s) {
        if(s == "")return -1;
        HashSet set = new HashSet();
        ArrayList list = new ArrayList();
        for(int i = 0; i < s.length(); i++ ){
            Character c = s.charAt(i);
            if(!set.add(c)){
                list.remove(c);
            }else{
                list.add(c);
            }
        }
        return list.isEmpty()?-1:s.indexOf(list.get(0).toString());
    }
}

//method 1: hashmap;
class Solution {
    public int firstUniqChar(String s) {
        if(s == null) return -1;
        int n = s.length();
        HashMap<Character, Integer> hm = new HashMap<>();
        for(int i = 0; i < n; i++){
            char c = s.charAt(i);
            if(!hm.containsKey(c)) hm.put(c, 1);
            else hm.put(c, hm.get(c) + 1);
        }
        
        for(int i = 0; i < n; i++){
            char d = s.charAt(i);
            if(hm.get(d) == 1) return i;
        }
    }
}    

//method 2: indexOf(char) == lastIndexOf(char);
class Solution {
    public int firstUniqChar(String s) {
        int n =s.length();
        for(int first = 'a'; first <= 'z'; first++){
            int i = s.indexOf(first);
            if(i != -1 && i == s.lastIndexOf(first)){
                //because we scan from a to z, so there is some case that i is equal to the second unique char's index, that's why we need to store the min one to n, which means n is the first uniqe char.
                //we use n to store the index because the index of the chars couldn't be greater or equal to n, so once the program goes here, we will get the i we want. 
                n = Math.min(n, i); 
            }
        }
        //if n hasn't changed, means there are no unique char
        return n == s.length() ? -1 : n;
    }
}
```