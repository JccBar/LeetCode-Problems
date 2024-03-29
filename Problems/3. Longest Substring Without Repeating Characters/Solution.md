# [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Given a string `s`, find the length of the longest substring without repeating characters.

#### Example 1

    Input: s = "abcabcbb"
    Output: 3
    Explanation: The answer is "abc", with the length of 3.

#### Example 2

    Input: s = "bbbbb"
    Output: 1
    Explanation: The answer is "b", with the length of 1.

#### Example 3

    Input: s = "pwwkew"
    Output: 3
    Explanation: The answer is "wke", with the length of 3.
    Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

## Sliding window

- Use two pointers to track the `start` and `end` of the current substring.
- Use an auxiliary array to store the last index of each character encountered.
- Iterate through the input string `s` using the `end` pointer.
- Update the `start` pointer whenever a repeating character is encountered.
- Return the maximum result found.

```C++
class Solution
{
public:
    int lengthOfLongestSubstring(std::string s)
    {
        int result = 0;
        int start = 0;
        vector<int> lastIndex(256, -1);

        for (int end = 0; end < s.size(); ++end)
        {
            start = max(start, lastIndex[s[end]] + 1);
            result = max(result, end - start + 1);

            lastIndex[s[end]] = end;
        }
        return result;
    }
};
```

#### Complexity

- Time complexity: $O(n)$;
- Space Complexity: $O(1)$;
