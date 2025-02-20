# Heap

## Overview
A Heap is a specialized binary tree-based data structure that satisfies the heap property:
- **Max-Heap**: The parent node is always greater than or equal to its children.
- **Min-Heap**: The parent node is always less than or equal to its children.

## Common Heap Operations
1. **Insert**: Add an element to the heap while maintaining the heap property.
2. **Delete/Extract Min or Max**: Remove the root element (min or max) and restore the heap structure.
3. **Peek**: Return the minimum or maximum without removing it.
4. **Heapify**: Rearrange an array to satisfy the heap property.

## Heap Time Complexities
| Operation       | Time Complexity |
|-----------------|-----------------|
| Insert          | O(log N)        |
| Extract Min/Max | O(log N)        |
| Peek            | O(1)            |
| Heapify         | O(N)            |
| Build Heap      | O(N)            |

## Uses of Heaps in Algorithms
- **Priority Queues**: Heaps are used to implement efficient priority queues.
- **Dijkstra's Algorithm**: Min-heaps are used to efficiently find the next node with the shortest distance.
- **Median Finding**: Two heaps (min-heap and max-heap) can be used to maintain the median in a dynamic dataset.
- **Heap Sort**: An efficient, comparison-based sorting algorithm with O(N log N) time complexity.

## Types of Heaps
- **Binary Heap**: A complete binary tree that satisfies the heap property.
- **Fibonacci Heap**: Supports faster decrease-key operations, often used in advanced algorithms like Prim's and Dijkstra’s.
- **Binomial Heap**: A collection of binomial trees used for merging heaps efficiently.

## Common Problems Involving Heaps

### 1. Kth Largest/Smallest Element
**Problem**: Find the Kth largest or smallest element in an array.
**Solution**:
- Use a Min-Heap to maintain the K largest elements.
- Use a Max-Heap for the K smallest elements.
**Time Complexity**: O(N log K)

### 2. Merge K Sorted Lists
**Problem**: Merge K sorted linked lists into one sorted list.
**Solution**: Use a Min-Heap to store the smallest elements from each list and iteratively extract the minimum.
**Time Complexity**: O(N log K), where N is the total number of elements.

### 3. Top K Frequent Elements
**Problem**: Find the K most frequent elements in an array.
**Solution**:
- Use a frequency map to count element frequencies.
- Use a Min-Heap to keep track of the K most frequent elements.
**Time Complexity**: O(N log K)

### 4. Find Median from Data Stream
**Problem**: Given a stream of numbers, find the median at any point.
**Solution**:
- Maintain two heaps: a Max-Heap for the smaller half and a Min-Heap for the larger half.
- Balance both heaps after every insertion.
**Time Complexity**: O(log N) per insertion.

## Tricks to Identify Heap Problems
1. **Priority or Order**: Look for problems that involve selecting the top K elements or finding the minimum/maximum.
   - Example: "Find the Kth largest element" or "Select the smallest element from multiple groups."
2. **Continuous Stream or Dynamic Median**: If the problem involves dynamically adding numbers and finding the median, it’s a strong hint for a heap.
3. **Merge or Sorting Multiple Lists**: Merging multiple sorted lists or finding the smallest elements across multiple arrays often indicates heap usage.
4. **Greedy Selection**: Problems that require selecting the best option at every step may benefit from using heaps.
   - Example: Huffman coding uses a Min-Heap to construct optimal prefix codes.

## Heap Tricks and Optimization Tips
- **Heapify in O(N)**: Use the bottom-up heap construction method to build a heap in O(N) instead of O(N log N).
  - This is often useful when converting an entire array into a heap.
- **Dual Heaps for Median**: For median problems, maintaining a balance between two heaps is more efficient than sorting every time.
- **Custom Comparators**: You can modify heap behavior using custom comparators for complex problems (e.g., prioritizing by multiple criteria).

## Sample Notes (Heap Overview)
- **Heap Property**: Parent nodes are greater (max-heap) or smaller (min-heap) than their children.
- **Common Uses**: Priority queues, finding Kth largest/smallest elements, merging lists, and median maintenance.
- **Operations**: Insert, extract, peek, and heapify with logarithmic or constant time complexities.
- **Tricks**:
  - Recognize problems involving "priority" or "selection."
  - Use dual heaps for dynamic median.
  - Optimize with O(N) heap construction.
