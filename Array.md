# Array

## Tips
- Understand the problem requirements and constraints.
- Consider edge cases such as empty arrays, single-element arrays, and arrays with duplicate elements.
- Use two-pointer technique for problems involving pairs or subarrays.
- Utilize sorting for problems where order matters.
- Take advantage of hash maps for quick lookups.

## Notes
- Arrays are a collection of elements identified by index or key.
- They provide fast access to elements but can be costly for insertion and deletion operations.
- Arrays can be single-dimensional or multi-dimensional.

## Frequently Asked Questions
1. **How do you find the maximum product of two integers in an array?**
   - Sort the array and multiply the two largest numbers.
   - Alternatively, iterate through the array to find the two largest numbers.

2. **How do you find the missing number in an array of integers from 1 to n?**
   - Use the formula for the sum of the first n natural numbers and subtract the sum of the array elements from it.

3. **How do you remove duplicates from a sorted array?**
   - Use two pointers to overwrite duplicates in place.

## Common Tricks to Identify Patterns
- **Sliding Window:** Useful for problems involving subarrays or substrings.
- **Two Pointers:** Effective for problems involving pairs or when you need to traverse the array from both ends.
- **Hash Map:** Great for problems requiring quick lookups or counting elements.
- **Sorting:** Helps in problems where order or comparison is needed.

## Example Problems and Solutions

### 1. Two Sum
**Problem:** Given an array of integers, return indices of the two numbers such that they add up to a specific target.

**Solution in C#:**
```csharp
public int[] TwoSum(int[] nums, int target) {
    Dictionary<int, int> map = new Dictionary<int, int>();
    for (int i = 0; i < nums.Length; i++) {
        int complement = target - nums[i];
        if (map.ContainsKey(complement)) {
            return new int[] { map[complement], i };
        }
        map[nums[i]] = i;
    }
    throw new ArgumentException("No two sum solution");
}
```

### 2. Maximum Subarray
**Problem:** Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

**Solution in C#:**
```csharp
public int MaxSubArray(int[] nums) {
    int maxSoFar = nums[0];
    int maxEndingHere = nums[0];
    for (int i = 1; i < nums.Length; i++) {
        maxEndingHere = Math.Max(nums[i], maxEndingHere + nums[i]);
        maxSoFar = Math.Max(maxSoFar, maxEndingHere);
    }
    return maxSoFar;
}
```

### 3. Merge Sorted Array
**Problem:** Merge two sorted arrays into one sorted array.

**Solution in C#:**
```csharp
public void Merge(int[] nums1, int m, int[] nums2, int n) {
    int i = m - 1;
    int j = n - 1;
    int k = m + n - 1;
    while (i >= 0 && j >= 0) {
        if (nums1[i] > nums2[j]) {
            nums1[k--] = nums1[i--];
        } else {
            nums1[k--] = nums2[j--];
        }
    }
    while (j >= 0) {
        nums1[k--] = nums2[j--];
    }
}
```

### 4. Find the Duplicate Number
**Problem:** Given an array of integers containing n + 1 integers where each integer is between 1 and n (inclusive), find the duplicate number.

**Solution in C#:**
```csharp
public int FindDuplicate(int[] nums) {
    int slow = nums[0];
    int fast = nums[0];
    do {
        slow = nums[slow];
        fast = nums[nums[fast]];
    } while (slow != fast);
    
    fast = nums[0];
    while (slow != fast) {
        slow = nums[slow];
        fast = nums[fast];
    }
    return slow;
}
```

### 5. Rotate Array
**Problem:** Rotate an array of n elements to the right by k steps.

**Solution in C#:**
```csharp
public void Rotate(int[] nums, int k) {
    k = k % nums.Length;
    Reverse(nums, 0, nums.Length - 1);
    Reverse(nums, 0, k - 1);
    Reverse(nums, k, nums.Length - 1);
}

private void Reverse(int[] nums, int start, int end) {
    while (start < end) {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
}
```
