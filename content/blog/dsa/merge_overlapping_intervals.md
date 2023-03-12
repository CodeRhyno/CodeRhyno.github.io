---
title: "Merge Overlapping Intervals"
date: 2023-03-12T09:55:47+05:30
draft: false
author: ['CodeRhyno']
tags: ['DSA', 'Arrays', 'Sorting']
---

### Leetcode problem link: [Merge Overlapping Intervals](https://leetcode.com/problems/merge-intervals/)

### Optimised Approach

1. Make copy of the input array (it's a good practice to not update the inputs provided).
2. Sort the copied input based upon the start of each interval.
3. Add the first interval from sorted list to the output.
4. For each element in the sorted list from index 1, if it is able to merge to the last interval in output then merge else add to the output list.
5. Return the output.

#### Time & Space Complexity
Time Complexity: __O(N)__

Space Complexity: __O(N)__

#### Java Code
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        int N = intervals.length;
        int[][] copyInterval = intervals.clone();
        ArrayList<int[]> output = new ArrayList<>();

        Arrays.sort(copyInterval, (firstInterval, secondInterval) -> Integer.compare(firstInterval[0], secondInterval[0]));
        output.add(copyInterval[0]);

        for (int i = 1; i < N; i++) {
            int[] firstInterval = output.get(output.size() - 1);
            int[] secondInterval = copyInterval[i];

            if (secondInterval[0] <= firstInterval[1]) {
                firstInterval[0] = Math.min(firstInterval[0], secondInterval[0]);
                firstInterval[1] = Math.max(firstInterval[1], secondInterval[1]);
            } else {
                output.add(secondInterval);
            }
        }

        return output.toArray(new int[output.size()][]);
    }
}
```
