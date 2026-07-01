# LeetCode 203 - Remove Linked List Elements

## Problem Statement

Given the `head` of a linked list and an integer `val`, remove all the nodes of the linked list that have `Node.val == val`, and return the new head.

**LeetCode Link:** https://leetcode.com/problems/remove-linked-list-elements/

---

## Approach

To efficiently remove all nodes with the given value, a **dummy node** is created before the head of the linked list. This helps handle cases where the head node itself needs to be removed.

Two pointers are used:

- `prev` – points to the previous valid node.
- `curr` – traverses the linked list.

During traversal:

- If `curr.val == val`, skip the current node by setting `prev.next = curr.next`.
- Otherwise, move `prev` to `curr`.
- Continue until the end of the list.

Finally, return `dummy.next` as the new head.

---

## Algorithm

1. Create a dummy node whose `next` points to the head.
2. Initialize:
   - `prev = dummy`
   - `curr = head`
3. Traverse the linked list:
   - If `curr.val == val`
     - Remove the node by updating `prev.next`.
   - Else
     - Move `prev` to `curr`.
   - Move `curr` to the next node.
4. Return `dummy.next`.

---

## Java Solution

```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode prev = dummy;
        ListNode curr = head;

        while (curr != null) {
            if (curr.val == val) {
                prev.next = curr.next;
            } else {
                prev = curr;
            }
            curr = curr.next;
        }

        return dummy.next;
    }
}
```

---

## Dry Run

### Input

```
head = 1 -> 2 -> 6 -> 3 -> 4 -> 5 -> 6
val = 6
```

### Step 1

```
dummy -> 1 -> 2 -> 6 -> 3 -> 4 -> 5 -> 6
prev = dummy
curr = 1
```

### Step 2

```
curr = 1

1 != 6

prev = 1
curr = 2
```

### Step 3

```
curr = 2

2 != 6

prev = 2
curr = 6
```

### Step 4

```
curr = 6

6 == val

prev.next = curr.next
```

List becomes:

```
dummy -> 1 -> 2 -> 3 -> 4 -> 5 -> 6
```

### Step 5

```
curr = 3

3 != 6

prev = 3
curr = 4
```

### Step 6

```
curr = 4

4 != 6

prev = 4
curr = 5
```

### Step 7

```
curr = 5

5 != 6

prev = 5
curr = 6
```

### Step 8

```
curr = 6

6 == val

prev.next = null
```

### Final Output

```
1 -> 2 -> 3 -> 4 -> 5
```

---

## Complexity Analysis

- **Time Complexity:** `O(n)`
  - Traverse the linked list only once.

- **Space Complexity:** `O(1)`
  - Only constant extra space is used.

---

## Key Takeaways

- Use a **dummy node** to simplify deletion operations.
- Avoid separate handling for deleting the head node.
- Update `prev` only when the current node is **not** removed.
- This is a standard interview pattern for linked list deletion problems.

---
