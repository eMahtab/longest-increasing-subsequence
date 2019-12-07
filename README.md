# Longest Increasing Subsequence

Given a non-empty array of integers, write a function that returns the longest strictly-increasing subsequence of the array. A subsequence is defined as a set of numbers that are not necessarily adjacent but that are in the same order as they appear in the array. Assume that there will only be one longest increasing subsequence.

e.g.

Input: [5, 7, -24, 12, 10, 2, 3, 12, 5, 6, 35]

Output: [-24, 2, 3, 5, 6, 35]


```java
public static List<Integer> longestIncreasingSubsequence(int[] nums) {
		List<Integer> list = new ArrayList<Integer>();
		if (nums == null || nums.length == 0) {
			return list;
		}
		int length = nums.length;
		int[] dpTable = new int[length];
		Arrays.fill(dpTable, 1);
		int i = 0;
		int index = 0;
		int answer = 1;
		for (int j = 1; j < length; j++) {
			i = 0;
			while (i < j) {
				if (nums[j] > nums[i]) {
					dpTable[j] = Math.max(dpTable[j], dpTable[i] + 1);
				}
				i++;
			}
			if (dpTable[j] > answer) {
				index = j;
				answer = dpTable[j];
			}
		}

		list.add(nums[index]);

		int loc = index;
		for (int k = index - 1; k >= 0; k--) {
			if (dpTable[k] + 1 == dpTable[loc]) {
				list.add(nums[k]);
				loc = k;
			}
		}
		Collections.reverse(list);
		return list;
	}
```
