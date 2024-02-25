# [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

## Description

You are given two non-empty linked lists representing two non-negative integers.

The digits are stored in reverse order, and each of their nodes contains a single digit.

Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number `0` itself.

#### Example

    Input: l1 = [2,4,3], l2 = [5,6,4]
    Output: [7,0,8]
    Explanation: 342 + 465 = 807.

## Iterative solution

1. Initialize a dummy head node to anchor the resulting list and a carry variable for handling the carry-over during addition.
2. Loop through both input lists `l1` and `l2`, adding corresponding digits along with the carry, creating new nodes for each sum.
3. Handle cases where the lists are of unequal lengths by continuing the addition with the remaining digits of the longer list.
4. After processing both lists, check for any remaining carry and create an additional node if necessary.
5. Delete the initial dummy node and return the resulting linked list that starts from the next node, which contains the sum of the two numbers.

```C++
class Solution 
{
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) 
    {
        ListNode* dummyHead = new ListNode(0);
        ListNode* tail = dummyHead;
        int carry = 0;

        // Iterate through every node
        while (l1 != nullptr || l2 != nullptr || carry != 0) 
        {
            // Get digits of current nodes (l1 and l2)
            int digit1 = (l1 != nullptr) ? l1->val : 0;
            int digit2 = (l2 != nullptr) ? l2->val : 0;

            // Sum digits and carry
            int sum = digit1 + digit2 + carry;
            int digit = sum % 10;
            carry = sum / 10;

            // Create new node and append it to the linked list
            ListNode* newNode = new ListNode(digit);
            tail->next = newNode;
            
            // Move to next node if there is one
            l1 = (l1 != nullptr) ? l1->next : nullptr;
            l2 = (l2 != nullptr) ? l2->next : nullptr;
            tail = tail->next;
        }

        ListNode* result = dummyHead->next;
        delete dummyHead;
        return result;
    }
};
```
#### Complexity

- Time complexity: $O(n)$;
- Space Complexity: $O(n)$;
