# Big O Notation

## Introduction
Big O notation is used to describe the performance or complexity of an algorithm. It specifically describes the worst-case scenario and helps to understand the upper limits of an algorithm.

## Common Big O Notations
- **O(1)**: Constant time
- **O(log n)**: Logarithmic time
- **O(n)**: Linear time
- **O(n log n)**: Linearithmic time
- **O(n^2)**: Quadratic time
- **O(2^n)**: Exponential time
- **O(n!)**: Factorial time

## Tips
- Focus on the part of the code that runs the most times.
- Ignore constants and lower-order terms.
- Nested loops often indicate O(n^2) complexity.
- Recursive algorithms can often be analyzed using recurrence relations.

## Notes
- Big O notation helps in comparing the efficiency of different algorithms.
- It is crucial for optimizing code and improving performance.
- Understanding the time and space complexity of algorithms is essential for writing efficient code.

## Amortized Analysis
Amortized analysis is used to average the time complexity of an algorithm over a sequence of operations, providing a more accurate measure of its performance in practice.

### Example
Consider a dynamic array (e.g., `List` in C#) that doubles its size when it runs out of space. The `Add` operation is generally O(1), but occasionally it will be O(n) when resizing is required. Amortized analysis helps to show that the average time complexity of `Add` is still O(1).

### Tips
- Amortized analysis is useful for understanding the average performance of operations that have occasional expensive costs.
- It is often used in data structures like dynamic arrays, hash tables, and splay trees.

### Example in C#

#### Dynamic Array - Amortized O(1)
```csharp
public class DynamicArray {
    private int[] arr;
    private int count;
    private int capacity;

    public DynamicArray() {
        arr = new int[2];
        count = 0;
        capacity = 2;
    }

    public void Add(int item) {
        if (count == capacity) {
            Resize();
        }
        arr[count++] = item;
    }

    private void Resize() {
        capacity *= 2;
        int[] newArr = new int[capacity];
        for (int i = 0; i < count; i++) {
            newArr[i] = arr[i];
        }
        arr = newArr;
    }
}
```

## Frequently Asked Questions

### What is Big O notation?
Big O notation is a mathematical representation used to describe the efficiency of an algorithm in terms of time and space.

### Why is Big O notation important?
It helps in understanding the scalability of an algorithm and comparing the performance of different algorithms.

### How do you calculate Big O notation?
By analyzing the number of operations an algorithm performs relative to the input size.

## Common Tricks to Identify Patterns

### Constant Time - O(1)
- Accessing an array element by index.
- Performing a simple arithmetic operation.

### Logarithmic Time - O(log n)
- Binary search in a sorted array.
- Operations on balanced trees (e.g., AVL trees).

### Linear Time - O(n)
- Iterating through all elements of an array.
- Finding the maximum or minimum element in an array.

### Linearithmic Time - O(n log n)
- Efficient sorting algorithms like Merge Sort and Quick Sort.

### Quadratic Time - O(n^2)
- Nested loops iterating over the same range.
- Bubble Sort, Insertion Sort, and Selection Sort.

### Exponential Time - O(2^n)
- Solving the Tower of Hanoi problem.
- Recursive algorithms that solve subproblems multiple times.

### Factorial Time - O(n!)
- Generating all permutations of a set.
- Solving the Traveling Salesman Problem using brute force.

## Example in C#

### Linear Search - O(n)
```csharp
public int LinearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.Length; i++) {
        if (arr[i] == target) {
            return i;
        }
    }
    return -1;
}
```

### Binary Search - O(log n)
```csharp
public int BinarySearch(int[] arr, int target) {
    int left = 0, right = arr.Length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            return mid;
        }
        if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;
}
```

### Bubble Sort - O(n^2)
```csharp
public void BubbleSort(int[] arr) {
    int n = arr.Length;
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j + 1]
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
