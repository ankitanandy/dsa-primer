# Stack

## Introduction
A stack is a linear data structure that follows the Last In First Out (LIFO) principle. The last element added to the stack is the first one to be removed.

## Basic Operations
1. **Push**: Add an element to the top of the stack.
2. **Pop**: Remove the top element from the stack.
3. **Peek/Top**: Return the top element without removing it.
4. **IsEmpty**: Check if the stack is empty.

## Tips
- Use a stack when you need to reverse elements or when you need to access elements in reverse order.
- Stacks are useful for parsing expressions, backtracking algorithms, and managing function calls.

## Notes
- Stacks can be implemented using arrays or linked lists.
- They are used in depth-first search (DFS) algorithms.
- Stacks are also used in undo mechanisms in text editors.

## Frequently Asked Questions
1. **How do you implement a stack using an array?**
   - Use an array to store elements and a variable to track the index of the top element.

2. **How do you check for balanced parentheses in an expression?**
   - Use a stack to push opening brackets and pop them when a closing bracket is encountered.

3. **What are some real-world applications of stacks?**
   - Function call management, expression evaluation, syntax parsing, and backtracking.

## Common Tricks to Identify Patterns
- **Balanced Parentheses**: Use a stack to ensure every opening bracket has a corresponding closing bracket.
- **Reverse Elements**: Use a stack to reverse the order of elements.
- **Backtracking**: Use a stack to keep track of choices and backtrack when necessary.

## Common Use Cases for Stacks
1. **Expression Evaluation and Conversion** (e.g., infix to postfix).
2. **Balanced Parentheses** (e.g., checking valid brackets).
3. **Undo/Redo Operations** in text editors.
4. **Backtracking** (e.g., Depth-First Search).
5. **Monotonic Stack** for nearest greater/smaller element problems.
6. **Function Call Management** (e.g., recursion).

## Identifying Stack Problems
Look for these clues:
- **LIFO Order**: If the problem processes elements in reverse order of arrival.
- **Nested Structures**: Matching brackets or parenthesis often use stacks.
- **Previous/Next Greater or Smaller Element**: Monotonic stacks are useful here.
- **Undo/Redo Functionality**: Implies a stack usage.

## Example Problems and Solutions

### 1. Implement Stack using Arrays
**Solution in C#:**
```csharp
public class Stack {
    private int[] elements;
    private int top;
    private int max;

    public Stack(int size) {
        elements = new int[size];
        top = -1;
        max = size;
    }

    public void Push(int item) {
        if (top == max - 1) {
            throw new InvalidOperationException("Stack overflow");
        }
        elements[++top] = item;
    }

    public int Pop() {
        if (top == -1) {
            throw new InvalidOperationException("Stack underflow");
        }
        return elements[top--];
    }

    public int Peek() {
        if (top == -1) {
            throw new InvalidOperationException("Stack is empty");
        }
        return elements[top];
    }

    public bool IsEmpty() {
        return top == -1;
    }
}
```

### 2. Valid Parentheses
**Problem:** Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

**Solution in C#:**
```csharp
public bool IsValid(string s) {
    Stack<char> stack = new Stack<char>();
    foreach (char c in s) {
        if (c == '(' || c == '{' || c == '[') {
            stack.Push(c);
        } else {
            if (stack.Count == 0) return false;
            char top = stack.Pop();
            if ((c == ')' && top != '(') ||
                (c == '}' && top != '{') ||
                (c == ']' && top != '[')) {
                return false;
            }
        }
    }
    return stack.Count == 0;
}
```

### 3. Min Stack
**Problem:** Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

**Solution in C#:**
```csharp
public class MinStack {
    private Stack<int> stack;
    private Stack<int> minStack;

    public MinStack() {
        stack = new Stack<int>();
        minStack = new Stack<int>();
    }

    public void Push(int x) {
        stack.Push(x);
        if (minStack.Count == 0 || x <= minStack.Peek()) {
            minStack.Push(x);
        }
    }

    public void Pop() {
        if (stack.Pop() == minStack.Peek()) {
            minStack.Pop();
        }
    }

    public int Top() {
        return stack.Peek();
    }

    public int GetMin() {
        return minStack.Peek();
    }
}
```

### 4. Evaluate Reverse Polish Notation
**Problem:** Evaluate the value of an arithmetic expression in Reverse Polish Notation.

**Solution in C#:**
```csharp
public int EvalRPN(string[] tokens) {
    Stack<int> stack = new Stack<int>();
    foreach (string token in tokens) {
        if (int.TryParse(token, out int num)) {
            stack.Push(num);
        } else {
            int b = stack.Pop();
            int a = stack.Pop();
            switch (token) {
                case "+":
                    stack.Push(a + b);
                    break;
                case "-":
                    stack.Push(a - b);
                    break;
                case "*":
                    stack.Push(a * b);
                    break;
                case "/":
                    stack.Push(a / b);
                    break;
            }
        }
    }
    return stack.Pop();
}
```

### 5. Daily Temperatures
**Problem:** Given a list of daily temperatures, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature.

**Solution in C#:**
```csharp
public int[] DailyTemperatures(int[] T) {
    int[] result = new int[T.Length];
    Stack<int> stack = new Stack<int>();
    for (int i = 0; i < T.Length; i++) {
        while (stack.Count > 0 && T[i] > T[stack.Peek()]) {
            int idx = stack.Pop();
            result[idx] = i - idx;
        }
        stack.Push(i);
    }
    return result;
}
```

### 6. Next Greater Element
**Problem:** For each element in an array, find the next greater element to its right.

**Solution**: Use a monotonic stack to maintain a decreasing sequence.
```csharp
public int[] NextGreaterElement(int[] nums) {
    int n = nums.Length;
    int[] result = new int[n];
    Stack<int> stack = new Stack<int>();

    for (int i = n - 1; i >= 0; i--) {
        while (stack.Count > 0 && stack.Peek() <= nums[i]) {
            stack.Pop();
        }
        result[i] = stack.Count == 0 ? -1 : stack.Peek();
        stack.Push(nums[i]);
    }

    return result;
}
```

### 7. Largest Rectangle in Histogram
**Problem:** Given an array representing histogram bar heights, find the largest rectangle.

**Solution**: Use a stack to maintain bar indices.
```csharp
public int LargestRectangleArea(int[] heights) {
    Stack<int> stack = new Stack<int>();
    int maxArea = 0;
    int n = heights.Length;

    for (int i = 0; i <= n; i++) {
        int height = (i == n) ? 0 : heights[i];
        while (stack.Count > 0 && height < heights[stack.Peek()]) {
            int h = heights[stack.Pop()];
            int width = stack.Count == 0 ? i : i - stack.Peek() - 1;
            maxArea = Math.Max(maxArea, h * width);
        }
        stack.Push(i);
    }

    return maxArea;
}
```

## Tips for Solving Stack Problems
1. **Understand LIFO Behavior**: Visualize how elements are pushed and popped.
2. **Handle Edge Cases**: For parentheses problems, handle empty stacks and leftover symbols.
3. **Use Monotonic Stacks**: Efficient for nearest greater/smaller element problems.
4. **Simulate Step-by-Step**: For expression problems, simulate operations step-by-step to ensure correctness.




