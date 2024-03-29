# [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return the median of the two sorted arrays.

The overall run time complexity should be $O(log(m+n))$.

#### Example 1

    Input: nums1 = [1,3], nums2 = [2]
    Output: 2.00000
    Explanation: merged array = [1,2,3] and median is 2.
    Example 2:

#### Example 2

    Input: nums1 = [1,2], nums2 = [3,4]
    Output: 2.50000
    Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.

## Binary Search

- Calculate the sizes of both arrays and the midpoint where the arrays should be divided to form two equal halves.
- If the first array is larger, swap the arrays so the binary search is always done on the smaller array.
- Perform a binary search to find the correct position where the arrays can be split.
- Examine the values around the split to ensure that the largest number on the left is smaller than the smallest number on the right of both arrays.
- If the total number of elements is odd, the median is the larger of the two left-side values. If it's even, the median is the average of the two central values (the largest left-side value and the smallest right-side value). If a proper split isn't found, return an error or default value.

```C++
class Solution
{
public:
    double findMedianSortedArrays(std::vector<int>& nums1, std::vector<int>& nums2)
    {
        int n1 = nums1.size();
        int n2 = nums2.size();
        int total = n1 + n2;
        int half = (total + 1) / 2;

        if (n1 > n2) return findMedianSortedArrays(nums2, nums1); // ensure n1 <= n2

        int low = 0, high = n1;

        while (low <= high)
        {
            int partition1 = (low + high) / 2;
            int partition2 = half - partition1;

            int maxLeft1 = (partition1 == 0) ? INT_MIN : nums1[partition1 - 1];
            int minRight1 = (partition1 == n1) ? INT_MAX : nums1[partition1];

            int maxLeft2 = (partition2 == 0) ? INT_MIN : nums2[partition2 - 1];
            int minRight2 = (partition2 == n2) ? INT_MAX : nums2[partition2];

            if (maxLeft1 <= minRight2 && maxLeft2 <= minRight1)
            {
                if (total % 2 == 0)
                {
                    return (std::max(maxLeft1, maxLeft2) + std::min(minRight1, minRight2)) / 2.0;
                }
                else
                {
                    return std::max(maxLeft1, maxLeft2);
                }
            }
            else if (maxLeft1 > minRight2)
            {
                high = partition1 - 1;
            }
            else
            {
                low = partition1 + 1;
            }
        }

        return 0.0; // Arrays are not sorted or input is invalid
    }
};

```

#### Complexity

- Time complexity: $O(log(n))$;
- Space Complexity: $O(1)$;
