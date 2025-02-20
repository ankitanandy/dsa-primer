# Linked List

## Introduction
A linked list is a linear data structure where each element is a separate object, called a node. Each node contains two items: data and a reference (or link) to the next node in the sequence.

## Types of Linked Lists
1. **Singly Linked List**: Each node points to the next node and the last node points to null.
2. **Doubly Linked List**: Each node has two references, one to the next node and one to the previous node.
3. **Circular Linked List**: The last node points back to the first node, forming a circle.

## Basic Operations
1. **Insertion**: Adding a new node to the list.
2. **Deletion**: Removing a node from the list.
3. **Traversal**: Accessing each node of the list.
4. **Searching**: Finding a node in the list.

## Tips
- Always check for null references to avoid `NullReferenceException`.
- Keep track of the head node to avoid losing the list.
- For doubly linked lists, ensure both next and previous references are updated.

## Notes
- Linked lists are dynamic in size, unlike arrays.
- They allow for efficient insertion and deletion of elements.
- They do not allow random access to elements.

## Frequently Asked Questions
1. **What is the time complexity of insertion in a linked list?**
   - O(1) if inserting at the beginning, O(n) if inserting at the end or at a specific position.

2. **How do you reverse a linked list?**
   - By changing the next pointers of each node to point to the previous node.

3. **What are the advantages of linked lists over arrays?**
   - Dynamic size, ease of insertion/deletion.

## Common Tricks
- **Detecting a cycle in a linked list**: Use Floyd’s Cycle-Finding Algorithm (Tortoise and Hare).
- **Finding the middle of a linked list**: Use two pointers, one moving twice as fast as the other.

## Common Use Cases for Linked Lists
1. **Dynamic Memory Allocation**: Lists that grow or shrink dynamically.
2. **Implementing Stacks and Queues**.
3. **Handling Large Data Streams**.
4. **Chaining in Hash Tables**.

## Identifying Linked List Problems in Interviews
Look for these clues:
- **Sequential Node Connections**: If the problem discusses elements connected via pointers or next references.
- **Insert/Delete at Arbitrary Positions**: Linked lists are ideal for dynamic insertion/deletion.
- **Reversing a List**: Common linked list reversal questions.
- **Loop/Cycle Detection**: If the problem involves identifying cycles in a sequence.

## Example Problems and Solutions

### Problem 1: Reverse a Singly Linked List
**Solution in C#:**
```csharp
public class ListNode {
    public int val;
    public ListNode next;
    public ListNode(int x) { val = x; }
}

public class Solution {
    public ListNode ReverseList(ListNode head) {
        ListNode prev = null;
        ListNode curr = head;
        while (curr != null) {
            ListNode nextTemp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextTemp;
        }
        return prev;
    }
}
```

### Problem 2. Detect a cycle in Linked List
**Solution in C#:**
```csharp
public class ListNode {
    public int val;
    public ListNode next;
    public ListNode(int x) { val = x; }
}

public class Solution {
    public bool HasCycle(ListNode head) {
        if (head == null || head.next == null) return false;
        ListNode slow = head;
        ListNode fast = head.next;
        while (slow != fast) {
            if (fast == null || fast.next == null) return false;
            slow = slow.next;
            fast = fast.next.next;
        }
        return true;
    }
}
```

### Problem 3. Find the Middle of a Linked List
**Solution in C#:**
```csharp
public class ListNode {
    public int val;
    public ListNode next;
    public ListNode(int x) { val = x; }
}

public class Solution {
    public ListNode MiddleNode(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
```

### Problem 4. Merge Two Sorted Linked Lists
**Solution in C#:**
```csharp
public ListNode MergeTwoLists(ListNode l1, ListNode l2) {
    if (l1 == null) return l2;
    if (l2 == null) return l1;

    if (l1.val < l2.val) {
        l1.next = MergeTwoLists(l1.next, l2);
        return l1;
    } else {
        l2.next = MergeTwoLists(l1, l2.next);
        return l2;
    }
}
```

### Problem 5. Remove N-th Node from End of List
**Solution in C#:**
```csharp
public ListNode RemoveNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode first = dummy;
    ListNode second = dummy;

    for (int i = 0; i <= n; i++) {
        first = first.next;
    }

    while (first != null) {
        first = first.next;
        second = second.next;
    }

    second.next = second.next.next;
    return dummy.next;
}
```

## Tips for Solving Linked List Problems
1. **Two Pointers**: Commonly used for problems involving cycles, middle node detection, and N-th node removal.
2. **Dummy Nodes**: Use a dummy node to simplify head insertion/deletion.
3. **Recursive Solutions**: Many linked list problems can be solved recursively.
4. **Edge Cases**: Consider empty lists, single-node lists, and lists with loops.
5. **Cycle Detection**: Use slow and fast pointers to detect loops efficiently.

## Practice Problems
1. **Flatten a Multilevel Doubly Linked List**.
2. **Partition List Around a Value**.
3. **Reorder List (Alternate Front and Back Nodes)**.
4. **Intersection of Two Linked Lists**.
5. **Copy List with Random Pointer**.

