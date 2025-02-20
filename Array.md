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

## Key Operations & Their Complexities
| Operation                  | Time Complexity (Best/Average/Worst) | Notes                                      |
|----------------------------|--------------------------------------|--------------------------------------------|
| Access (arr[i])            | O(1)                                 | Direct index-based access                  |
| Search (Linear Search)     | O(N)                                 | Scans the array sequentially               |
| Search (Binary Search)     | O(log N)                             | Only works on sorted arrays                |
| Insert (End - Dynamic Array)| O(1) amortized                      | If resizing isn’t needed                   |
| Insert (Middle)            | O(N)                                 | Shifts elements to the right               |
| Delete (End)               | O(1)                                 | Last element removal is fast               |
| Delete (Middle)            | O(N)                                 | Shifts elements to the left                |

## Types of Arrays
1. **Static Array**: Fixed size (e.g., `int arr[10]` in C/C++).
2. **Dynamic Array**: Resizable (e.g., `List<int>` in C#).
3. **Multi-Dimensional Array**: Used for matrices (e.g., `int[,] matrix = new int[3,3]`).
4. **Jagged Array**: Array of arrays (e.g., `int[][] jaggedArr = new int[3][]`).
5. **Sparse Array**: Mostly empty, stored efficiently using lists or hash tables.

## Important Algorithms & Questions on Arrays

### Searching in an Array

**Linear Search (O(N))**
```csharp
int LinearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.Length; i++) {
        if (arr[i] == target) return i;
    }
    return -1;
}
```
✅ Works for unsorted arrays but is slow.

**Binary Search (O(log N), Sorted Array Only)**
```csharp
int BinarySearch(int[] arr, int target) {
    int left = 0, right = arr.Length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```
✅ Efficient but only for sorted arrays.

### Sorting Algorithms
| Algorithm       | Time Complexity (Best/Average/Worst) | Space Complexity |
|-----------------|--------------------------------------|------------------|
| Bubble Sort     | O(N) / O(N²) / O(N²)                 | O(1)             |
| Selection Sort  | O(N²) / O(N²) / O(N²)                | O(1)             |
| Insertion Sort  | O(N) / O(N²) / O(N²)                 | O(1)             |
| Merge Sort      | O(N log N) / O(N log N) / O(N log N) | O(N)             |
| Quick Sort      | O(N log N) / O(N log N) / O(N²)      | O(log N)         |

### Array Problems & Solutions

**1. Find the Maximum Subarray Sum (Kadane’s Algorithm)**
👉 Problem: Find the contiguous subarray with the maximum sum in an array.
👉 Solution: Use Kadane’s Algorithm (O(N)).
```csharp
int MaxSubarraySum(int[] arr) {
    int maxSum = arr[0], currentSum = arr[0];
    for (int i = 1; i < arr.Length; i++) {
        currentSum = Math.Max(arr[i], currentSum + arr[i]);
        maxSum = Math.Max(maxSum, currentSum);
    }
    return maxSum;
}
```
✅ Efficient (O(N)), handles negatives.

**2. Two Sum (Find Two Numbers That Add to Target)**
👉 Problem: Given an array and a target, find two numbers that sum to the target.
👉 Solution: Use a HashSet (O(N)).
```csharp
int[] TwoSum(int[] nums, int target) {
    Dictionary<int, int> map = new Dictionary<int, int>();
    for (int i = 0; i < nums.Length; i++) {
        int complement = target - nums[i];
        if (map.ContainsKey(complement)) {
            return new int[] { map[complement], i };
        }
        map[nums[i]] = i;
    }
    return new int[] {};
}
```
✅ Faster than brute force O(N²), runs in O(N).

**3. Find the Missing Number (1 to N)**
👉 Problem: An array contains numbers from 1 to N with one missing number. Find it.
👉 Solution 1: Use Sum Formula (O(N), O(1) space).
```csharp
int MissingNumber(int[] arr) {
    int n = arr.Length + 1;
    int expectedSum = n * (n + 1) / 2;
    int actualSum = arr.Sum();
    return expectedSum - actualSum;
}
```
✅ Uses Math trick, very efficient.

👉 Solution 2: Use XOR Trick (O(N), O(1) space).
```csharp
int MissingNumberXOR(int[] arr) {
    int xorAll = 0, xorArr = 0;
    for (int i = 1; i <= arr.Length + 1; i++) xorAll ^= i;
    foreach (int num in arr) xorArr ^= num;
    return xorAll ^ xorArr;
}
```
✅ Uses Bitwise XOR, avoids integer overflow.

**4. Rotate Array by K Places**
👉 Problem: Rotate an array nums to the right by k steps.
👉 Solution: Use Reverse Trick (O(N)).
```csharp
void Rotate(int[] nums, int k) {
    k %= nums.Length;
    Array.Reverse(nums, 0, nums.Length - k);
    Array.Reverse(nums, nums.Length - k, k);
    Array.Reverse(nums);
}
```
✅ No extra space, O(N) time.

## Common Tricks to Identify Patterns in Array Problems

### 1. Hashing (Use HashSet or HashMap for O(1) Lookup)
✅ When to Use?
- Checking for duplicates
- Finding missing numbers
- Finding frequency/count of elements
- Storing prefix sums

**Example: Two Sum (O(N))**
```csharp
int[] TwoSum(int[] nums, int target) {
    Dictionary<int, int> map = new Dictionary<int, int>();
    for (int i = 0; i < nums.Length; i++) {
        int complement = target - nums[i];
        if (map.ContainsKey(complement)) return new int[] { map[complement], i };
        map[nums[i]] = i;
    }
    return new int[] {};
}
```
✅ O(N) time, O(N) space.

### 2. Sliding Window (For Subarray/Substring Problems)
✅ When to Use?
- Fixed Window Size (e.g., maximum sum of subarray of size k)
- Variable Window Size (e.g., smallest subarray with sum >= target)

**Example: Maximum Sum Subarray of Size K (O(N))**
```csharp
int MaxSumSubarray(int[] nums, int k) {
    int sum = 0, maxSum = int.MinValue;
    for (int i = 0; i < k; i++) sum += nums[i]; // First window
    for (int i = k; i < nums.Length; i++) {
        sum += nums[i] - nums[i - k]; // Slide window
        maxSum = Math.Max(maxSum, sum);
    }
    return maxSum;
}
```
✅ O(N) time, O(1) space.

### 3. Two Pointers (For Sorted Arrays, Pairs, and Partitions)
✅ When to Use?
- Finding pairs/triplets (e.g., two sum in sorted array, 3Sum)
- Sorting-based problems (e.g., Dutch National Flag, merging two sorted arrays)
- Partitioning problems (e.g., segregating odd/even, negatives/positives)

**Example: Two Sum in Sorted Array (O(N))**
```csharp
int[] TwoSumSorted(int[] nums, int target) {
    int left = 0, right = nums.Length - 1;
    while (left < right) {
        int sum = nums[left] + nums[right];
        if (sum == target) return new int[] { left, right };
        else if (sum < target) left++;
        else right--;
    }
    return new int[] {};
}
```
✅ O(N) time, O(1) space.

### 4. Kadane’s Algorithm (For Maximum Subarray Problems)
✅ When to Use?
- Finding the maximum sum subarray
- Problems where negative numbers may appear

**Example: Maximum Subarray Sum (O(N))**
```csharp
int MaxSubarraySum(int[] nums) {
    int maxSum = nums[0], currentSum = nums[0];
    for (int i = 1; i < nums.Length; i++) {
        currentSum = Math.Max(nums[i], currentSum + nums[i]);
        maxSum = Math.Max(maxSum, currentSum);
    }
    return maxSum;
}
```
✅ O(N) time, O(1) space.

### 5. Prefix Sum / Cumulative Sum (For Range Queries and Subarray Problems)
✅ When to Use?
- Range sum queries (sum of elements between i and j)
- Finding subarrays with a given sum

**Example: Range Sum Query (O(1) per Query after O(N) Preprocessing)**
```csharp
int[] PrefixSum(int[] nums) {
    int[] prefix = new int[nums.Length];
    prefix[0] = nums[0];
    for (int i = 1; i < nums.Length; i++) {
        prefix[i] = prefix[i - 1] + nums[i];
    }
    return prefix;
}

// Get sum of range [L, R]
int RangeSum(int[] prefix, int L, int R) {
    return L == 0 ? prefix[R] : prefix[R] - prefix[L - 1];
}
```
✅ O(N) preprocessing, O(1) per query.

### 6. XOR Trick (For Missing or Duplicated Elements)
✅ When to Use?
- Finding missing numbers
- Finding unique numbers when duplicates exist

**Example: Find the Missing Number (1 to N) Using XOR (O(N))**
```csharp
int MissingNumber(int[] arr) {
    int xorAll = 0, xorArr = 0;
    for (int i = 1; i <= arr.Length + 1; i++) xorAll ^= i;
    foreach (int num in arr) xorArr ^= num;
    return xorAll ^ xorArr;
}
```
✅ O(N) time, O(1) space.

### 7. Merge Intervals (For Overlapping Intervals)
✅ When to Use?
- Scheduling problems
- Overlapping meetings, booking systems

**Example: Merge Overlapping Intervals (O(N log N))**
```csharp
int[][] MergeIntervals(int[][] intervals) {
    if (intervals.Length <= 1) return intervals;
    Array.Sort(intervals, (a, b) => a[0] - b[0]);
    List<int[]> result = new List<int[]>();
    int[] current = intervals[0];
    foreach (int[] interval in intervals) {
        if (interval[0] <= current[1]) current[1] = Math.Max(current[1], interval[1]);
        else {
            result.Add(current);
            current = interval;
        }
    }
    result.Add(current);
    return result.ToArray();
}
```
✅ O(N log N) due to sorting.

### 8. Cyclic Sort (For Finding Missing and Duplicate Numbers in 1 to N Range)
✅ When to Use?
- Finding missing numbers
- Finding duplicate numbers

**Example: Find First Missing Positive (O(N))**
```csharp
int FirstMissingPositive(int[] nums) {
    int i = 0;
    while (i < nums.Length) {
        if (nums[i] > 0 && nums[i] <= nums.Length && nums[i] != nums[nums[i] - 1]) {
            (nums[i], nums[nums[i] - 1]) = (nums[nums[i] - 1], nums[i]); // Swap
        } else i++;
    }
    for (i = 0; i < nums.Length; i++) if (nums[i] != i + 1) return i + 1;
    return nums.Length + 1;
}
```
✅ O(N) time, O(1) space.

## Summary of Patterns & Techniques
| Technique                | Best For                                      | Complexity       |
|--------------------------|-----------------------------------------------|------------------|
| Hashing (HashSet/Dictionary) | Finding duplicates, two-sum                  | O(N)             |
| Sliding Window           | Fixed/variable-length subarrays               | O(N)             |
| Two Pointers             | Sorted arrays, pair problems                  | O(N)             |
| Kadane’s Algorithm       | Max sum subarrays                             | O(N)             |
| Prefix Sum               | Range sum queries                             | O(1) per query   |
| XOR Trick                | Finding missing/duplicate numbers             | O(N)             |
| Merge Intervals          | Overlapping intervals                         | O(N log N)       |
| Cyclic Sort              | Missing numbers in 1 to N                     | O(N)             |
