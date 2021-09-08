# Sort an array of 0’s 1’s 2’s

## Approach 1 [ O(N\*log(n)) ]

```cpp
void sortColors(vector<int>& nums) {
    sort(nums.begin(), nums.end());
}
```
## Approach 2 [ O(2*N) ]

```cpp
void sortColors(vector<int>& nums) {
    int zero=0, one=0, two=0, n=nums.size();
    for(int i=0; i<n; i++) {
        switch(nums[i]) {
            case 0 : zero++; break;
            case 1 : one++; break;
            case 2 : two++; break;
        }
    }
    for(int i=0; i<n; i++) {
        if(zero > 0)
            nums[i] = 0, zero--;
        else if(one > 0)
            nums[i] = 1, one--;
        else if(two > 0)
            nums[i] = 2, two--;
    }
}
```


## Approach 3 [ O(N) ]

```cpp
void sortColors(vector<int>& nums) {
    int n = nums.size(), l = 0, r = n-1, m=0;
    while(m <= r) {
        if(nums[m] == 0) {
            swap(nums[l], nums[m]);
            l++, m++;
        } else if (nums[m] == 2) {
            swap(nums[m], nums[r]);
            r--;
        } else {
            m++;
        }
    }
}
```
