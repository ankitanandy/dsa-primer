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
