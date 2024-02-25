#[1. Two Sum](https://leetcode.com/problems/two-sum)

## Description

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

#### Example

    Input: nums = [2,7,11,15], target = 9
    Output: [0,1]
    Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

## 1. Brute force approach

1. Use nested loops and iterate through every possible pair.
2. If a pair of elements is found that add up to the target sum, return their indices.

```C++
class Solution 
{
public:
    vector<int> twoSum(vector<int>& nums, int target) 
    {
        for (int i = 0; i < nums.size(); ++i) 
        {
            for (int j = i + 1; j < nums.size(); ++j) 
            {
                if (nums[i] + nums[j] == target) 
                {
                    return {i, j};
                }
            }
        }
        return {}; // No solution found
    }
};
```

#### Complexity

- Time complexity: $O(n^2)$;
- Space Complexity: $O(1)$;

## 2. Two-pass hash table

1. Create an empty hash table to store the elements and their indices.
2. Iterate through the input array to populate the hash table with elements and their indices in the first pass.
3. In the second pass, iterate through the array again:
4. For each element, calculate the complement needed to reach the target sum.
5. Check if the complement exists in the hash table.
    1. If found, return the indices of the current element and the complement.
    2. If no two elements are found that add up to the target sum, return an empty array.

```C++
class Solution 
{
public:
    vector<int> twoSum(vector<int>& nums, int target) 
    {
        unordered_map<int, int> mp;
        int n = nums.size();
        // Populate the hash table:
        for (int i = 0; i < n; ++i) 
        {
            mp[nums[i]] = i;
        }

        // Find the complement:
        for (int i = 0; i < n; ++i) 
        {
            int complement = target - nums[i];
            if (mp.count(complement) && mp[complement] != i) 
            {
                return {i, mp[complement]};
            }
        }
        return {}; // No solution found
    }
};
```

#### Complexity

- Time complexity: $O(n)$;
- Space Complexity: $O(n)$; 
  
## 3. One-pass hash table

1. Create an empty hash table to store the elements and their indices.
2. Iterate through the input array, for each element:
   1. Calculate the complement needed to reach the target sum.
   2. Check if the complement exists in the hash table.
   3. If found, return the indices of the current element and the complement.
   4. If not found, add the current element to the hash table.
3. If no two elements are found that add up to the target sum, return an empty array.

```C++
class Solution 
{
public:
    vector<int> twoSum(vector<int>& nums, int target) 
    {
        unordered_map<int, int> mp;
        for (int i = 0; i < nums.size(); ++i) 
        {
            int complement = target - nums[i];
            if (mp.count(complement))  // Check if the complement exists in the hash map
            {
                // If yes, return the indices of the current number and its complement
                return {i, mp[complement]};
            }
            // If not, add the current number and its index to the hash map
            mp[nums[i]] = i;
        }
        return {}; // No solution found
    }
};
```

#### Complexity

- Time complexity: $O(n)$;
- Space Complexity: $O(n)$;

## 4. Two-pointer approach

1. Create a sorted copy of the input array.
2. Initialize two pointers, one at the beginning and one at the end of the sorted array.
3. Use a loop to iterate through the array and adjust the pointers based on the sum of elements at the pointers.
4. When the sum equals the target, return the indices of the elements in the original unsorted array.

```C++
class Solution 
{
public:
    vector<int> twoSum(vector<int>& nums, int target) 
    {
        vector<pair<int, int>> sortedNums;
        for (int i = 0; i < nums.size(); i++) 
        {
            sortedNums.push_back({nums[i], i});
        }
        sort(sortedNums.begin(), sortedNums.end());

        // Declare 2 pointers 
        int l = 0;
        int r = nums.size() - 1;

        while (l < r) 
        {
            int sum = sortedNums[l].first + sortedNums[r].first;
            if (sum == target) 
            {
                return {sortedNums[l].second, sortedNums[r].second};
            } 
            else if (sum < target) 
            {
                ++l;  // Left pointer moves to the right
            } 
            else // sum > target
            {
                --r; // Right pointer moves to the left
            }
        }
        return {}; // No solution found!
    }
};
```

#### Complexity

- Time complexity: $O(n \times log(n))$
- Space Complexity: $O(n)$
