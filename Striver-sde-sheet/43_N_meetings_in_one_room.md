# N meetings in one room

## Problem statement

There is one meeting room in a firm. There are `N` meetings in the form of `(start[i], end[i])` where `start[i]` is start time of meeting `i` and `end[i]` is finish time of meeting `i`.
What is the maximum number of meetings that can be accommodated in the meeting room when only one meeting can be held in the meeting room at a particular time?

**Note:** Start time of one chosen meeting can't be equal to the end time of the other chosen meeting.

## Solution

Time complexity : O(N\*log(N))  
Space complexity : O(N)

```cpp
int maxMeetings(int start[], int end[], int n) {
    vector<pair<int, int>> v(n);
    for(int i=0; i<n; i++)
        v[i] = {end[i], start[i]};
    sort(v.begin(), v.end());
    int prev = v[0].first, res=1;
    for(int i=1; i<n; i++) {
        if(v[i].second > prev) {
            res++;
            prev = v[i].first;
        }
    }
    return res;
}
```
