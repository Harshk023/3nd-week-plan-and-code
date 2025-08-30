# 3nd-week-plan-and-code
🚀 3rd-Week-Plan-and-Code

A structured 7-day roadmap covering Stacks, Queues, and Trees (Basics). Includes theory notes, clean Python code snippets, and LeetCode problem solutions to build a strong foundation in linear & hierarchical data structures.

📅 Day-Wise Plan

Day	Focus Area & Questions
Day 15	Stack Basics – Implement a stack using Python list
LeetCode #20 – Valid Parentheses
Day 16	Monotonic Stack – Introduction and applications
LeetCode #739 – Daily Temperatures
Day 17	Queue & Deque – Implement queue and deque in Python
Apply them to BFS traversal
Day 18	Binary Tree Traversals – Preorder, Inorder, Postorder (recursive + iterative)
Day 19	Level Order Traversal
LeetCode #102 – Binary Tree Level Order Traversal
Day 20	Tree Depth & Balance
LeetCode #104 – Maximum Depth of Binary Tree
LeetCode #110 – Balanced Binary Tree
Day 21	Mixed Tree Practice – Solve 3–4 easy/medium tree problems to strengthen traversal and recursion concepts

"""
Day 15: Stack Basics & Valid Parentheses
Author: [Your Name]
Date: [Today's Date]

Topics Covered:
1. Implementing a stack using Python list
2. LeetCode #20 - Valid Parentheses
"""

# ----------------------------------------------------
# 1. Implementing a Stack using Python List
# ----------------------------------------------------
"""
Stack = LIFO (Last In First Out) data structure.
Operations:
- push(x): add element to top
- pop(): remove element from top
- peek(): view top element
- isEmpty(): check if stack is empty
"""

class Stack:
    def __init__(self):
        self.stack = []

    def push(self, x):
        self.stack.append(x)

    def pop(self):
        if not self.isEmpty():
            return self.stack.pop()
        return None

    def peek(self):
        if not self.isEmpty():
            return self.stack[-1]
        return None

    def isEmpty(self):
        return len(self.stack) == 0

    def size(self):
        return len(self.stack)


# Example usage of custom Stack
s = Stack()
s.push(10)
s.push(20)
s.push(30)
print("Stack size:", s.size())       # 3
print("Top element:", s.peek())      # 30
print("Pop element:", s.pop())       # 30
print("Stack after pop:", s.stack)   # [10, 20]


# ----------------------------------------------------
# 2. LeetCode #20 - Valid Parentheses
# ----------------------------------------------------
"""
Problem:
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']',
determine if the input string is valid.

Rules:
- Open brackets must be closed by the same type of bracket.
- Open brackets must be closed in the correct order.

Example:
Input: s = "()[]{}"
Output: True

Input: s = "(]"
Output: False

Approach:
- Use a stack to track opening brackets.
- When a closing bracket is found, check top of stack.
- If mismatched or empty -> invalid.
- If stack empty at end -> valid.

Time Complexity: O(n)
Space Complexity: O(n)
"""

def isValid(s):
    stack = []
    mapping = {")": "(", "}": "{", "]": "["}
    
    for char in s:
        if char in mapping:  # closing bracket
            top = stack.pop() if stack else "#"
            if mapping[char] != top:
                return False
        else:  # opening bracket
            stack.append(char)
    
    return not stack


# Example tests
print("LC #20 Input: '()[]{}' ->", isValid("()[]{}"))  # True
print("LC #20 Input: '(]' ->", isValid("(]"))          # False
print("LC #20 Input: '({[]})' ->", isValid("({[]})"))  # True


# ----------------------------------------------------
# Time Complexity Summary:
# ----------------------------------------------------
# Stack operations: push/pop/peek/isEmpty -> O(1)
# LC #20 Valid Parentheses -> O(n)
# ----------------------------------------------------
