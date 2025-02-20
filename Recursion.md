### **Recursion: Complete Interview Guide**

Recursion is a powerful concept where a function calls itself to solve smaller instances of the same problem. Many problems are elegantly solved with recursion, especially when they involve dividing the problem into smaller, repetitive subproblems.

---

### **Basic Terminology**

- **Base Case**: The condition under which the recursive function stops calling itself.
- **Recursive Case**: The part of the function that continues the recursion.
- **Stack Overflow**: Occurs when recursion is too deep or lacks a base case.

---

### **How to Identify Recursion Problems**
Look for the following cues in a problem:

1. **Subproblem Structure**: The problem can be broken into smaller versions of itself.
2. **Divide-and-Conquer**: Problems that can be split into independent subproblems.
3. **Tree-Like Structures**: Problems involving hierarchical data structures like trees.
4. **Backtracking**: Solving problems with multiple choices (e.g., permutations and combinations).
5. **Dynamic Programming (Top-Down)**: Problems solvable by memoization often start with recursion.

---

### **Common Recursion Patterns**

1. **Factorial of a Number**
   **Problem**: Calculate the factorial of a number using recursion.

   **C# Code:**
   ```csharp
   public int Factorial(int n) {
       if (n == 0) return 1; // Base case
       return n * Factorial(n - 1); // Recursive case
   }
   ```

2. **Fibonacci Sequence**
   **Problem**: Find the N-th Fibonacci number.

   **C# Code:**
   ```csharp
   public int Fibonacci(int n) {
       if (n <= 1) return n; // Base case
       return Fibonacci(n - 1) + Fibonacci(n - 2); // Recursive case
   }
   ```

3. **Binary Search (Recursive)**
   **Problem**: Perform binary search on a sorted array.

   **C# Code:**
   ```csharp
   public int BinarySearch(int[] arr, int target, int left, int right) {
       if (left > right) return -1; // Base case

       int mid = left + (right - left) / 2;

       if (arr[mid] == target) return mid;
       else if (arr[mid] > target) return BinarySearch(arr, target, left, mid - 1);
       else return BinarySearch(arr, target, mid + 1, right);
   }
   ```

4. **Permutations**
   **Problem**: Generate all permutations of a given string.

   **C# Code:**
   ```csharp
   public void Permute(string str, int left, int right) {
       if (left == right) {
           Console.WriteLine(str);
       } else {
           for (int i = left; i <= right; i++) {
               str = Swap(str, left, i);
               Permute(str, left + 1, right);
               str = Swap(str, left, i); // Backtrack
           }
       }
   }

   private string Swap(string str, int i, int j) {
       char[] charArray = str.ToCharArray();
       char temp = charArray[i];
       charArray[i] = charArray[j];
       charArray[j] = temp;
       return new string(charArray);
   }
   ```

---

### **Advanced Recursion Concepts**

1. **Tail Recursion**
   - A form of recursion where the recursive call is the last operation in the function.
   - Can be optimized by some compilers to avoid using additional stack space.

   **C# Code (Tail Recursion Example):**
   ```csharp
   public int TailRecursiveFactorial(int n, int accumulator = 1) {
       if (n == 0) return accumulator; // Base case
       return TailRecursiveFactorial(n - 1, n * accumulator); // Recursive call
   }
   ```

2. **Memoization**
   - Technique to optimize recursion by caching the results of subproblems.

   **C# Code (Fibonacci with Memoization):**
   ```csharp
   private Dictionary<int, int> memo = new Dictionary<int, int>();

   public int FibonacciMemo(int n) {
       if (n <= 1) return n;
       if (memo.ContainsKey(n)) return memo[n];

       int result = FibonacciMemo(n - 1) + FibonacciMemo(n - 2);
       memo[n] = result;
       return result;
   }
   ```

3. **Backtracking**
   - A problem-solving technique that incrementally builds candidates and abandons those that fail to satisfy constraints.

   **Example: N-Queens Problem**
   ```csharp
   public bool SolveNQueens(int[,] board, int col) {
       if (col >= board.GetLength(0)) return true; // All queens placed

       for (int i = 0; i < board.GetLength(0); i++) {
           if (IsSafe(board, i, col)) {
               board[i, col] = 1;

               if (SolveNQueens(board, col + 1)) return true;

               board[i, col] = 0; // Backtrack
           }
       }

       return false;
   }

   private bool IsSafe(int[,] board, int row, int col) {
       for (int i = 0; i < col; i++) {
           if (board[row, i] == 1) return false;
       }

       for (int i = row, j = col; i >= 0 && j >= 0; i--, j--) {
           if (board[i, j] == 1) return false;
       }

       for (int i = row, j = col; i < board.GetLength(0) && j >= 0; i++, j--) {
           if (board[i, j] == 1) return false;
       }

       return true;
   }
   ```

---

### **Common Recursion Problems**
1. **Power Function**: Calculate `x^n` using recursion.
2. **Tower of Hanoi**: Move N disks from one peg to another using a helper peg.
3. **Combination Sum**: Find all combinations of numbers that sum to a target.
4. **Word Search**: Find a word in a 2D grid using backtracking.
5. **Subsets**: Generate all subsets of a given set.

---

### **Tips for Solving Recursion Problems**
1. **Define the Base Case Clearly**: Ensure there is a stopping condition.
2. **Avoid Stack Overflow**: Ensure your recursive depth is manageable.
3. **Memoize to Optimize**: Use caching to store results of subproblems.
4. **Trace Function Calls**: For complex problems, use diagrams to trace recursive calls.
5. **Think Iteratively First**: Sometimes visualizing the iterative solution helps in writing the recursive function.

---
