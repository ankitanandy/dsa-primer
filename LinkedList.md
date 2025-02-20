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

