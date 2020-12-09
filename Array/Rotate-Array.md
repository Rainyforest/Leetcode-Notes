## Rotate Array
-  Need 3 different ways
-  O(1) Extra Space in-place    
### 
Example:
```
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

Solution:
```java
// Brute Force
// Simply rotate array 1 place k times 
// O(kN)<O(N^2)
class Solution {
    public void rotate(int[] nums, int k) {
        k %= nums.length; //save time
        for(int i = 0; i < k; i++){
            int tail = nums[nums.length-1];
            for(int j = nums.length - 1; j > 0; j--){
                nums[j] = nums[j-1];
            }
            nums[0] = tail;
        }
    }
}

// Using Extra Array to place element to correct position directly
// O(N)
class Solution {
  public void rotate(int[] nums, int k) {
    int[] a = new int[nums.length];
    for (int i = 0; i < nums.length; i++) {
      a[(i + k) % nums.length] = nums[i];
    }
    for (int i = 0; i < nums.length; i++) {
      nums[i] = a[i];
    }
  }
}
```
Approach 3: [Cyclic Replacements](https://leetcode.com/problems/rotate-array/solution/)
```java
class Solution {
  public void rotate(int[] nums, int k) {
    k = k % nums.length;
    int count = 0;
    for (int start = 0; count < nums.length; start++) {
      int current = start;
      int prev = nums[start];
      do {
        int next = (current + k) % nums.length;
        int temp = nums[next];
        nums[next] = prev;
        prev = temp;
        current = next;
        count++;
      } while (start != current);
    }
  }
}
```
Approach 4: Using Reverse
```
n = 7, k = 3
Original List                   : 1 2 3 4 5 6 7
After reversing all numbers     : 7 6 5 4 3 2 1
After reversing first k numbers : 5 6 7 4 3 2 1
After revering last n-k numbers : 5 6 7 1 2 3 4 --> Result
```
```java
// Time O(n)
// Space O(1)
class Solution {
  public void rotate(int[] nums, int k) {
    k %= nums.length;
    reverse(nums, 0, nums.length - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, nums.length - 1);
  }
  public void reverse(int[] nums, int start, int end) {
    while (start < end) {
      int temp = nums[start];
      nums[start] = nums[end];
      nums[end] = temp;
      start++;
      end--;
    }
  }
}
```

## Intersection of Two Arrays II
```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int shorter[];
        int longer[]; 
        if(nums1.length > nums2.length){
            shorter = nums2;
            longer = nums1;
        }else{
            shorter = nums1;
            longer = nums2;
        }
        int[] common = new int[shorter.length];
        int count = 0;
        int j = 0;
        for(int i = 0; i < shorter.length; i++){
            while(shorter[i] > longer[j]){
                if(++j>=longer.length)return Arrays.copyOfRange(common, 0, count);
            }
            if(shorter[i]==longer[j]){
                common[count++] = shorter[i];
                if(++j>=longer.length)return Arrays.copyOfRange(common, 0, count);

            }
        }
        return Arrays.copyOfRange(common, 0, count);
    }
}
```