# Queue

## Introduction
A queue is a linear data structure that follows the First In First Out (FIFO) principle. The first element added to the queue is the first one to be removed.

## Basic Operations
1. **Enqueue**: Add an element to the end of the queue.
2. **Dequeue**: Remove the element from the front of the queue.
3. **Peek/Front**: Return the front element without removing it.
4. **IsEmpty**: Check if the queue is empty.

## Tips
- Use a queue when you need to process elements in the order they were added.
- Queues are useful for breadth-first search (BFS) algorithms and scheduling tasks.

## Notes
- Queues can be implemented using arrays, linked lists, or stacks.
- They are used in BFS algorithms, task scheduling, and buffering.

## Frequently Asked Questions
1. **How do you implement a queue using an array?**
   - Use an array to store elements and two variables to track the front and rear indices.

2. **How do you implement a queue using two stacks?**
   - Use one stack for enqueuing and another stack for dequeuing.

3. **What are some real-world applications of queues?**
   - Print spooling, task scheduling, and handling requests in web servers.

## Common Tricks to Identify Patterns
- **Breadth-First Search (BFS)**: Use a queue to explore nodes level by level.
- **Task Scheduling**: Use a queue to manage tasks in the order they arrive.
- **Buffering**: Use a queue to store data temporarily while it is being processed.

## Common Use Cases for Queues
1. **Task Scheduling** (e.g., CPU scheduling, printer queues).
2. **Breadth-First Search (BFS)** in graphs.
3. **Cache Systems** (e.g., FIFO cache replacement policies).
4. **Asynchronous Data Processing**.
5. **Order Processing** in message queues.

## Identifying Queue Problems in Interviews
Look for these patterns or clues:
- **First-Come, First-Served** scenarios.
- **Sequential Processing**: Elements processed in the order they arrive.
- **Level-by-Level Traversals**: BFS traversal of trees or graphs.
- **Sliding Window Problems**: Often involve queues for maintaining the current window.

## Types of Queues
1. **Simple Queue**: Standard FIFO queue.
2. **Deque (Double-Ended Queue)**: Elements can be added/removed from both ends.
3. **Circular Queue**: A queue that wraps around when the end is reached.
4. **Priority Queue**: Elements are dequeued based on priority instead of order.

## Example Problems and Solutions

### 1. Implement Queue using Arrays
**Solution in C#:**
```csharp
public class Queue {
    private int[] elements;
    private int front;
    private int rear;
    private int max;
    private int count;

    public Queue(int size) {
        elements = new int[size];
        front = 0;
        rear = -1;
        max = size;
        count = 0;
    }

    public void Enqueue(int item) {
        if (count == max) {
            throw new InvalidOperationException("Queue overflow");
        }
        rear = (rear + 1) % max;
        elements[rear] = item;
        count++;
    }

    public int Dequeue() {
        if (count == 0) {
            throw new InvalidOperationException("Queue underflow");
        }
        int item = elements[front];
        front = (front + 1) % max;
        count--;
        return item;
    }

    public int Peek() {
        if (count == 0) {
            throw new InvalidOperationException("Queue is empty");
        }
        return elements[front];
    }

    public bool IsEmpty() {
        return count == 0;
    }
}
```

### 2. Implement Queue using Two Stacks
**Solution in C#:**
```csharp
public class MyQueue {
    private Stack<int> stack1;
    private Stack<int> stack2;

    public MyQueue() {
        stack1 = new Stack<int>();
        stack2 = new Stack<int>();
    }

    public void Enqueue(int x) {
        stack1.Push(x);
    }

    public int Dequeue() {
        if (stack2.Count == 0) {
            while (stack1.Count > 0) {
                stack2.Push(stack1.Pop());
            }
        }
        return stack2.Pop();
    }

    public int Peek() {
        if (stack2.Count == 0) {
            while (stack1.Count > 0) {
                stack2.Push(stack1.Pop());
            }
        }
        return stack2.Peek();
    }

    public bool IsEmpty() {
        return stack1.Count == 0 && stack2.Count == 0;
    }
}
```

### 3. Implement Circular Queue
**Solution in C#:**
```csharp
public class CircularQueue {
    private int[] elements;
    private int front;
    private int rear;
    private int max;
    private int count;

    public CircularQueue(int size) {
        elements = new int[size];
        front = 0;
        rear = -1;
        max = size;
        count = 0;
    }

    public bool Enqueue(int item) {
        if (count == max) {
            return false;
        }
        rear = (rear + 1) % max;
        elements[rear] = item;
        count++;
        return true;
    }

    public bool Dequeue() {
        if (count == 0) {
            return false;
        }
        front = (front + 1) % max;
        count--;
        return true;
    }

    public int Front() {
        if (count == 0) {
            throw new InvalidOperationException("Queue is empty");
        }
        return elements[front];
    }

    public int Rear() {
        if (count == 0) {
            throw new InvalidOperationException("Queue is empty");
        }
        return elements[rear];
    }

    public bool IsEmpty() {
        return count == 0;
    }

    public bool IsFull() {
        return count == max;
    }
}
```

### 4. Binary Tree Level Order Traversal
**Problem:** Given a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

**Solution in C#:**
```csharp
public IList<IList<int>> LevelOrder(TreeNode root) {
    IList<IList<int>> result = new List<IList<int>>();
    if (root == null) return result;
    Queue<TreeNode> queue = new Queue<TreeNode>();
    queue.Enqueue(root);
    while (queue.Count > 0) {
        int levelSize = queue.Count;
        IList<int> currentLevel = new List<int>();
        for (int i = 0; i < levelSize; i++) {
            TreeNode currentNode = queue.Dequeue();
            currentLevel.Add(currentNode.val);
            if (currentNode.left != null) queue.Enqueue(currentNode.left);
            if (currentNode.right != null) queue.Enqueue(currentNode.right);
        }
        result.Add(currentLevel);
    }
    return result;
}
```

### 5. Implement Stack using Queues
**Problem:** Implement a stack using queues.

**Solution in C#:**
```csharp
public class MyStack {
    private Queue<int> queue1;
    private Queue<int> queue2;

    public MyStack() {
        queue1 = new Queue<int>();
        queue2 = new Queue<int>();
    }

    public void Push(int x) {
        queue2.Enqueue(x);
        while (queue1.Count > 0) {
            queue2.Enqueue(queue1.Dequeue());
        }
        Queue<int> temp = queue1;
        queue1 = queue2;
        queue2 = temp;
    }

    public int Pop() {
        return queue1.Dequeue();
    }

    public int Top() {
        return queue1.Peek();
    }

    public bool IsEmpty() {
        return queue1.Count == 0;
    }
}
```

### 6. Sliding Window Maximum
**Problem:** Given an array and a window size `k`, find the maximum for each window.

**Solution**: Use a deque to store indices and maintain the window.
```csharp
public int[] MaxSlidingWindow(int[] nums, int k) {
    if (nums == null || nums.Length == 0) return new int[0];
    LinkedList<int> deque = new LinkedList<int>();
    int[] result = new int[nums.Length - k + 1];

    for (int i = 0; i < nums.Length; i++) {
        // Remove elements outside the window
        if (deque.Count > 0 && deque.First.Value < i - k + 1) {
            deque.RemoveFirst();
        }

        // Remove smaller elements from the back
        while (deque.Count > 0 && nums[deque.Last.Value] < nums[i]) {
            deque.RemoveLast();
        }

        deque.AddLast(i);

        // Add the maximum element for the window
        if (i >= k - 1) {
            result[i - k + 1] = nums[deque.First.Value];
        }
    }

    return result;
}
```

### 7. BFS Traversal of a Graph
**Problem:** Traverse a graph using Breadth-First Search.

**Solution**: Use a queue to explore nodes level-by-level.
```csharp
public void BFS(int startNode, Dictionary<int, List<int>> graph) {
    Queue<int> queue = new Queue<int>();
    HashSet<int> visited = new HashSet<int>();

    queue.Enqueue(startNode);
    visited.Add(startNode);

    while (queue.Count > 0) {
        int node = queue.Dequeue();
        Console.WriteLine(node);

        foreach (int neighbor in graph[node]) {
            if (!visited.Contains(neighbor)) {
                queue.Enqueue(neighbor);
                visited.Add(neighbor);
            }
        }
    }
}
```

## Tips for Solving Queue Problems
1. **Think FIFO**: If the problem involves processing in the order of arrival, a queue is likely involved.
2. **Sliding Window/Fixed-Length Processing**: Consider using deques for optimization.
3. **Tree or Graph Level Traversals**: BFS typically uses queues to explore level-by-level.
4. **Circular Behavior**: Use circular queues to handle wrapping-around scenarios.
5. **Cache Management**: Many cache algorithms (e.g., FIFO cache) are queue-based.
