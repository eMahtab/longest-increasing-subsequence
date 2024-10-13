# Longest Increasing Subsequence
## https://leetcode.com/problems/longest-increasing-subsequence

Given a non-empty array of integers, write a function that **returns the longest strictly-increasing subsequence of the array**. A subsequence is defined as a set of numbers that are not necessarily adjacent but that are in the same order as they appear in the array. Assume that there will only be one longest increasing subsequence.

e.g.

Input: [5, 7, -24, 12, 10, 2, 3, 12, 5, 6, 35]

Output: [-24, 2, 3, 5, 6, 35]


## Implementation 1 : O(n^2)
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        int maxLIS = 1;
        int[] dp = new int[nums.length];
        dp[0] = 1;
        for(int i = 1; i < nums.length; i++) {
            int max = 1;
            for(int j = 0; j < i; j++) {
                if(nums[j] < nums[i]) {
                  max = Math.max(max, dp[j] + 1);   
                }
            }
            dp[i] = max;
            maxLIS = Math.max(maxLIS, dp[i]);
        }
        return maxLIS;
    }
}
```

## Implementation 2 : 
```java
public static List<Integer> longestIncreasingSubsequence(int[] nums) {
		if(nums == null || nums.length == 0) {
			return new ArrayList<Integer>();
		}
		int length = nums.length;
		int[] dpTable = new int[length];
		int[] sequence = new int[length];
		Arrays.fill(dpTable, 1);
		Arrays.fill(sequence, Integer.MIN_VALUE);
		int maxLengthIndex = 0;
		for(int i = 1; i < length; i++) {
			for(int j = 0; j < i; j++) {
				if(nums[j] < nums[i] && dpTable[j] + 1 > dpTable[i] ) {
					dpTable[i] = dpTable[j] + 1;
					sequence[i] = j;
				}
			}
			if(dpTable[i] > dpTable[maxLengthIndex]) {
				maxLengthIndex = i;
			}
		}
		
		List<Integer> result = buildSequence(nums, sequence, maxLengthIndex);
		return result;
}

public static List<Integer> buildSequence(int[] nums, int[] sequence, int maxLengthIndex) {
		List<Integer> list = new ArrayList<Integer>();
		while(maxLengthIndex != Integer.MIN_VALUE) {
			list.add(0, nums[maxLengthIndex]);
			maxLengthIndex = sequence[maxLengthIndex];
		}
		return list;
}
```

# References :
https://www.youtube.com/watch?v=odrfUCS9sQk (Hindi, very good explanation)
