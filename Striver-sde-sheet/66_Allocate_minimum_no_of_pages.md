# Allocate books

## Problem statement

Given an array of integers `A` of size `N` and an integer `B`.

College library has `N` bags,the i<sup>th</sup> book has `A[i]` number of pages.

You have to allocate books to `B` number of students so that maximum number of pages alloted to a student is minimum.

- A book will be allocated to exactly one student.
- Each student has to be allocated at least one book.
- Allotment should be in contiguous order, for example: A student cannot be allocated book 1 and book 3, skipping book 2.

Calculate and return that minimum possible number. Return -1 if a valid assignment is not possible.

## Solution

Time complexity : O(N\*log(N))  
Space complexity : O(1)

```cpp
bool allocationPossible(vector<int> &A, int B, int limit) {
    int c = 1, sum = 0;
    for(auto it:A) {
        if(it > limit) return false;
        if(sum + it > limit) {
            c++;
            sum = 0;
        }
        sum += it;
    }
    return c <= B;
}
int Solution::books(vector<int> &A, int B) {
    if(A.size() < B) return -1;
    int low = A[0], high = 0, res = -1;
    for(auto it:A) {
        low = min(low, it);
        high += it;
    }
    while(low <= high) {
        int mid = (low + high)/2;
        if(allocationPossible(A, B, mid)) {
            res = mid;
            high = mid-1;
        } else {
            low = mid + 1;
        }
    }
    return res;
}
```
