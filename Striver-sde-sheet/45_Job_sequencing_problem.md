# Job sequencing problem

## Problem statement

Given a set of `N` jobs where each `jobi` has a deadline and profit associated with it. Each job takes **1** unit of time to complete and only one job can be scheduled at a time. We earn the profit if and only if the job is completed by its deadline. The task is to find the number of jobs done and the **maximum profit**.

**Note:** Jobs will be given in the form (Jobid, Deadline, Profit) associated with that Job.

## Solution

Time complexity : O(N\*log(N) + N\*M)  
Space complexity : O(N)

```cpp
static bool comp(Job j1, Job j2) {
    return j1.profit > j2.profit;
}
vector<int> JobScheduling(Job arr[], int n) {
    sort(arr, arr+n, comp);
    int maxDead = arr[0].dead;
    for(int i=1; i<n; i++)
        maxDead = max(maxDead, arr[i].dead);
    vector<int> slot(maxDead+1, -1);
    int profit = 0, count = 0;
    for(int i=0; i<n; i++) {
        for(int j = arr[i].dead; j>0; j--) {
            if(slot[j] == -1) {
                slot[j] = arr[i].id;
                count++;
                profit += arr[i].profit;
                break;
            }
        }
    }
    return {count, profit};
}
```
