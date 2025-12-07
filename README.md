### 30 Most Asked JavaScript LeetCode Problems  
(Optimized, clean, modern ES6+ solutions – ready for interviews)

#### 1. Two Sum  
**Difficulty:** Easy  
**Explanation:** Given an array of numbers and a target, return indices of two numbers that add up to target.  
**Solution:**  
```javascript
const twoSum = (nums, target) => {
    const map = new Map();
    for (let i = 0; i < nums.length; i++) {
        const complement = target - nums[i];
        if (map.has(complement)) return [map.get(complement), i];
        map.set(nums[i], i);
    }
};
```
**Complexity:** Time O(n) | Space O(n)  
**Logic:** Use hash map to store seen numbers and their indices.

#### 2. Valid Anagram  
**Difficulty:** Easy  
**Explanation:** Check if two strings have the same characters with same frequency.  
**Solution:**  
```javascript
const isAnagram = (s, t) => {
    if (s.length !== t.length) return false;
    const count = Array(26).fill(0);
    for (let i = 0; i < s.length; i++) {
        count[s.charCodeAt(i) - 97]++;
        count[t.charCodeAt(i) - 97]--;
    }
    return count.every(c => c === 0);
};
```
**Complexity:** Time O(n) | Space O(1)

#### 3. Contains Duplicate  
**Difficulty:** Easy  
**Explanation:** Return true if any value appears at least twice.  
**Solution:**  
```javascript
const containsDuplicate = nums => new Set(nums).size < nums.length;
```
**Complexity:** Time O(n) | Space O(n)

#### 4. Best Time to Buy and Sell Stock  
**Difficulty:** Easy  
**Explanation:** Find max profit from buying low and selling high (one transaction).  
**Solution:**  
```javascript
const maxProfit = prices => {
    let min = Infinity, profit = 0;
    for (const p of prices) {
        min = Math.min(min, p);
        profit = Math.max(profit, p - min);
    }
    return profit;
};
```
**Complexity:** Time O(n) | Space O(1)

#### 5. Valid Parentheses  
**Difficulty:** Easy  
**Explanation:** Check if brackets are properly closed.  
**Solution:**  
```javascript
const isValid = s => {
    const stack = [];
    const pairs = { ')':'(', '}':'{', ']':'[' };
    for (const c of s) {
        if (!(c in pairs)) stack.push(c);
        else if (stack.pop() !== pairs[c]) return false;
    }
    return stack.length === 0;
};
```
**Complexity:** Time O(n) | Space O(n)

#### 6. Merge Two Sorted Lists  
**Difficulty:** Easy  
**Explanation:** Merge two sorted linked lists.  
**Solution:**  
```javascript
const mergeTwoLists = (l1, l2) => {
    const dummy = new ListNode();
    let curr = dummy;
    while (l1 && l2) {
        if (l1.val <= l2.val) {
            curr.next = l1; l1 = l1.next;
        } else {
            curr.next = l2; l2 = l2.next;
        }
        curr = curr.next;
    }
    curr.next = l1 || l2;
    return dummy.next;
};
```
**Complexity:** Time O(n+m) | Space O(1)

#### 7. Majority Element  
**Difficulty:** Easy  
**Explanation:** Find element that appears more than n/2 times.  
**Solution (Boyer-Moore):**  
```javascript
const majorityElement = nums => {
    let candidate, count = 0;
    for (const n of nums) {
        if (count === 0) candidate = n;
        count += (n === candidate) ? 1 : -1;
    }
    candidate;
};
```
**Complexity:** Time O(n) | Space O(1)

#### 8. Move Zeroes  
**Difficulty:** Easy  
**Explanation:** Move all zeros to end while keeping relative order.  
**Solution:**  
```javascript
const moveZeroes = nums => {
    let i = 0;
    for (let j = 0; j < nums.length; j++) {
        if (nums[j] !== 0) nums[i++] = nums[j];
    }
    while (i < nums.length) nums[i++] = 0;
};
```
**Complexity:** Time O(n) | Space O(1)

#### 9. Group Anagrams  
**Difficulty:** Medium  
**Solution:**  
```javascript
const groupAnagrams = strs => {
    const map = new Map();
    for (const s of strs) {
        const key = [...s].sort().join('');
        map.set(key, [...(map.get(key) || []), s]);
    }
    return Array.from(map.values());
};
```
**Complexity:** Time O(n × k log k) | Space O(n)

#### 10. Valid Palindrome  
**Difficulty:** Easy  
**Solution:**  
```javascript
const isPalindrome = s => {
    s = s.toLowerCase().replace(/[^a-z0-9]/g, '');
    let [l, r] = [0, s.length - 1];
    while (l < r) if (s[l++] !== s[r--]) return false;
    return true;
};
```

#### 11. Longest Common Prefix  
**Difficulty:** Easy  
**Solution:**  
```javascript
const longestCommonPrefix = strs => {
    let prefix = strs[0];
    for (let i = 1; i < strs.length; i++) {
        while (strs[i].indexOf(prefix) !== 0) {
            prefix = prefix.slice(0, -1);
            if (!prefix) return "";
        }
    }
    return prefix;
};
```

#### 12. Linked List Cycle  
**Difficulty:** Easy  
**Solution (Floyd’s Tortoise & Hare):**  
```javascript
const hasCycle = head => {
    let [slow, fast] = [head, head];
    while (fast && fast.next) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow === fast) return true;
    }
    return false;
};
```

#### 13. Reverse Linked List  
**Difficulty:** Easy  
**Solution (Iterative):**  
```javascript
const reverseList = head => {
    let [prev, curr] = [null, head];
    while (curr) {
        [curr.next, prev, curr] = [prev, curr, curr.next];
    }
    return prev;
};
```

#### 14. Binary Search  
**Difficulty:** Easy  
**Solution:**  
```javascript
const search = (nums, target) => {
    let [l, r] = [0, nums.length - 1];
    while (l <= r) {
        const mid = (l + r) >> 1;
        if (nums[mid] === target) return mid;
        nums[mid] < target ? l = mid + 1 : r = mid - 1;
    }
    return -1;
};
```

#### 15. Maximum Subarray (Kadane’s)  
**Difficulty:** Medium  
```javascript
const maxSubArray = nums => {
    let max = -Infinity, curr = 0;
    for (const n of nums) {
        curr = Math.max(n, curr + n);
        max = Math.max(max, curr);
    }
    return max;
};
```

#### 16. Climbing Stairs  
**Difficulty:** Easy  
**Solution (DP bottom-up):**  
```javascript
const climbStairs = n => {
    if (n <= 2) return n;
    let [a, b] = [1, 2];
    for (let i = 3; i <= n; i++) [a, b] = [b, a + b];
    return b;
};
```

#### 17. Plus One  
**Difficulty:** Easy  
```javascript
const plusOne = digits => {
    for (let i = digits.length - 1; i >= 0; i--) {
        if (digits[i] < 9) {
            digits[i]++;
            return digits;
        }
        digits[i] = 0;
    }
    return [1, ...digits];
};
```

#### 18. Roman to Integer  
**Difficulty:** Easy  
```javascript
const romanToInt = s => {
    const map = {I:1,V:5,X:10,L:50,C:100,D:500,M:1000};
    let total = 0;
    for (let i = 0; i < s.length; i++) {
        if (map[s[i]] < map[s[i+1]]) total -= map[s[i]];
        else total += map[s[i]];
    }
    return total;
};
```

#### 19. Palindrome Number  
**Difficulty:** Easy  
```javascript
const isPalindrome = x => x < 0 ? false : x === +x.toString().split('').reverse().join('');
```

#### 20. Remove Duplicates from Sorted Array  
**Difficulty:** Easy  
```javascript
const removeDuplicates = nums => {
    let i = 0;
    for (let j = 1; j < nums.length; j++) {
        if (nums[j] !== nums[i]) nums[++i] = nums[j];
    }
    return i + 1;
};
```

#### 21. Merge Sorted Array  
**Difficulty:** Easy  
```javascript
const merge = (nums1, m, nums2, n) => {
    let i = m - 1, j = n - 1, k = m + n - 1;
    while (j >= 0) {
        nums1[k--] = (i >= 0 && nums1[i] > nums2[j]) ? nums1[i--] : nums2[j--];
    }
};
```

#### 22. Search Insert Position  
**Difficulty:** Easy  
```javascript
const searchInsert = (nums, target) => {
    let [l, r] = [0, nums.length - 1];
    while (l <= r) {
        const mid = (l + r) >> 1;
        if (nums[mid] === target) return mid;
        nums[mid] < target ? l = mid + 1 : r = mid - 1;
    }
    return l;
};
```

#### 23. Length of Last Word  
**Difficulty:** Easy  
```javascript
const lengthOfLastWord = s => {
    const words = s.trim().split(' ');
    return words[words.length - 1].length;
};
```

#### 24. Longest Substring Without Repeating Characters  
**Difficulty:** Medium  
```javascript
const lengthOfLongestSubstring = s => {
    const set = new Set();
    let [l, max] = [0, 0];
    for (let r = 0; r < s.length; r++) {
        while (set.has(s[r])) set.delete(s[l++]);
        set.add(s[r]);
        max = Math.max(max, r - l + 1);
    }
    return max;
};
```

#### 25. Container With Most Water  
**Difficulty:** Medium  
```javascript
const maxArea = height => {
    let [l, r, max] = [0, height.length - 1, 0];
    while (l < r) {
        max = Math.max(max, Math.min(height[l], height[r]) * (r - l));
        height[l] < height[r] ? l++ : r--;
    }
    return max;
};
```

#### 26. 3Sum  
**Difficulty:** Medium  
```javascript
const threeSum = nums => {
    nums.sort((a,b) => a - b);
    const res = [];
    for (let i = 0; i < nums.length - 2; i++) {
        if (i > 0 && nums[i] === nums[i-1]) continue;
        let [l, r] = [i+1, nums.length - 1];
        while (l < r) {
            const sum = nums[i] + nums[l] + nums[r];
            if (sum === 0) {
                res.push([nums[i], nums[l], nums[r]]);
                while (nums[l] === nums[l+1]) l++;
                while (nums[r] === nums[r-1]) r--;
                l++; r--;
            } else if (sum < 0) l++;
            else r--;
        }
    }
    return res;
};
```

#### 27. Remove Nth Node From End of List  
**Difficulty:** Medium  
```javascript
const removeNthFromEnd = (head, n) => {
    const dummy = new ListNode(0, head);
    let [fast, slow] = [dummy, dummy];
    for (let i = 0; i <= n; i++) fast = fast.next;
    while (fast) {
        fast = fast.next;
        slow = slow.next;
    }
    slow.next = slow.next.next;
    return dummy.next;
};
```

#### 28. Product of Array Except Self  
**Difficulty:** Medium  
```javascript
const productExceptSelf = nums => {
    const n = nums.length;
    const res = Array(n).fill(1);
    let prefix = 1, postfix = 1;
    for (let i = 0; i < n; i++) {
        res[i] *= prefix;
        prefix *= nums[i];
        res[n-1-i] *= postfix;
        postfix *= nums[n-1-i];
    }
    return res;
};
```
**Complexity:** Time O(n) | Space O(1) (output array not counted)

#### 29. Find the Kth Largest Element  
**Difficulty:** Medium  
```javascript
const findKthLargest = (nums, k) => nums.sort((a,b)=>b-a)[k-1];
// Or use QuickSelect for O(n) average
```

#### 30. Implement Queue using Stacks  
**Difficulty:** Easy  
```javascript
class MyQueue {
    constructor() {
        this.in = [];
        this.out = [];
    }
    push(x) { this.in.push(x); }
    pop() {
        this.peek();
        return this.out.pop();
    }
    peek() {
        if (!this.out.length) {
            while (this.in.length) this.out.push(this.in.pop());
        }
        return this.out[this.out.length - 1];
    }
    empty() { return !this.in.length && !this.out.length; }
}
```
