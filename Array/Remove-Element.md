## Remove Element
```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int i = 0;
        int n = nums.length;
        while (i < n) {
            if (nums[i] == val) {
                nums[i] = nums[n - 1];
                // reduce array size by one
                n--;
            } else {
                i++;
            }
        }
        return n;
    }
}

// Method 2: Maintain Order
class Solution {
    public int removeElement(int[] nums, int val) {
        int shift = 0;
        for (int i = 0; i < nums.length; i++) {
            nums[i - shift] = nums[i];
            if (nums[i] == val) {
                shift++;
            }
        }
        return nums.length - shift;
    }
}

```