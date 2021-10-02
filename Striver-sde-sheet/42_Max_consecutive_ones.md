# Max consecutive ones

## Problem statement

Given a binary array `nums`, return the maximum number of consecutive `1's` in the array.

## Solution (Two pointer)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
int findMaxConsecutiveOnes(vector<int>& nums) {
    int c=0, res=0;
    for(int i=0; i<nums.size(); i++) {
        if(nums[i] == 1) {
            c++;
        } else {
            res = max(res, c);
            c=0;
        }
    }
    res = max(res, c);
    return res;
}
```
