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

"""
Day 16: Monotonic Stack Intro & Daily Temperatures
Author: [Your Name]
Date: [Today's Date]

Topics Covered:
1. What is a Monotonic Stack?
2. LeetCode #739 - Daily Temperatures
"""

# ----------------------------------------------------
# 1. Monotonic Stack Intro
# ----------------------------------------------------
"""
A Monotonic Stack is a stack that is either entirely
- Increasing (each new element >= top) OR
- Decreasing (each new element <= top)

Use cases:
- Next Greater Element
- Daily Temperatures
- Stock Span problems
"""

# Simple Example: Next Greater Element
def next_greater_element(arr):
    stack = []
    result = [-1] * len(arr)
    for i in range(len(arr)-1, -1, -1):
        while stack and stack[-1] <= arr[i]:
            stack.pop()
        if stack:
            result[i] = stack[-1]
        stack.append(arr[i])
    return result

print("Next Greater Element Example:", next_greater_element([2,1,2,4,3]))
# Output: [4,2,4,-1,-1]


# ----------------------------------------------------
# 2. LeetCode #739 - Daily Temperatures
# ----------------------------------------------------
"""
Problem:
Given an array of daily temperatures T, return an array answer such that
answer[i] is the number of days you have to wait after the i-th day to get a warmer temperature.
If there is no future day, put 0.

Example:
Input: T = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]

Approach:
- Use a monotonic decreasing stack that stores indices.
- While the current temperature is greater than the stack’s top index temperature,
  update result[stack_top] = current_index - stack_top.
- Push current index into stack.

Time Complexity: O(n)
Space Complexity: O(n)
"""

def dailyTemperatures(temperatures):
    n = len(temperatures)
    answer = [0] * n
    stack = []  # stores indices

    for i, temp in enumerate(temperatures):
        # while stack not empty and current temp > top's temp
        while stack and temperatures[i] > temperatures[stack[-1]]:
            prev_index = stack.pop()
            answer[prev_index] = i - prev_index
        stack.append(i)

    return answer


# Example test
temps = [73,74,75,71,69,72,76,73]
print("LC #739 Input:", temps)
print("LC #739 Output:", dailyTemperatures(temps))
# Expected: [1,1,4,2,1,1,0,0]


# ----------------------------------------------------
# Time Complexity Summary:
# ----------------------------------------------------
# Next Greater Element: O(n)
# LC #739 Daily Temperatures: O(n)
# ----------------------------------------------------

# ----------------------------------------------------
# Time Complexity Summary:
# ----------------------------------------------------
# Stack operations: push/pop/peek/isEmpty -> O(1)
# LC #20 Valid Parentheses -> O(n)
# ----------------------------------------------------

"""
Day 17: Queue, Deque & BFS
Author: [Your Name]
Date: [Today's Date]

Topics Covered:
1. Implementing Queue using collections.deque
2. Implementing Deque (double-ended queue)
3. BFS Traversal (on graphs and binary trees)
"""

from collections import deque

# ----------------------------------------------------
# 1. Queue using deque
# ----------------------------------------------------
"""
Queue = FIFO (First In, First Out)
Operations:
- Enqueue (append at right)
- Dequeue (pop from left)
"""

queue = deque()

# Enqueue
queue.append(10)
queue.append(20)
queue.append(30)
print("Queue after enqueues:", list(queue))

# Dequeue
print("Dequeued element:", queue.popleft())
print("Queue after dequeue:", list(queue))


# ----------------------------------------------------
# 2. Deque (Double-Ended Queue)
# ----------------------------------------------------
"""
Deque allows insertion and deletion from both ends.
Useful for sliding window and BFS problems.
"""

dq = deque([1, 2, 3])

# Insert at both ends
dq.appendleft(0)
dq.append(4)
print("Deque after insertions:", list(dq))

# Remove from both ends
dq.popleft()
dq.pop()
print("Deque after removals:", list(dq))


# ----------------------------------------------------
# 3. BFS Traversal in Graph
# ----------------------------------------------------
"""
Breadth-First Search (BFS) explores level by level.

Steps:
1. Use a queue to process nodes
2. Mark visited nodes
3. Traverse neighbors

Time Complexity: O(V + E)
"""

def bfs_graph(adj_list, start):
    visited = set()
    q = deque([start])
    order = []

    while q:
        node = q.popleft()
        if node not in visited:
            visited.add(node)
            order.append(node)
            for neighbor in adj_list[node]:
                if neighbor not in visited:
                    q.append(neighbor)
    return order

# Example graph (adjacency list)
graph = {
    0: [1, 2],
    1: [2, 3],
    2: [4],
    3: [4],
    4: []
}

print("BFS on graph starting from node 0:", bfs_graph(graph, 0))
# Output: [0, 1, 2, 3, 4]


# ----------------------------------------------------
# 4. BFS Traversal in Binary Tree
# ----------------------------------------------------
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def bfs_tree(root):
    if not root:
        return []
    
    result = []
    q = deque([root])
    
    while q:
        node = q.popleft()
        result.append(node.val)
        if node.left:
            q.append(node.left)
        if node.right:
            q.append(node.right)
    
    return result

# Example tree:
#       1
#      / \
#     2   3
#    / \
#   4   5
root = TreeNode(1)
root.left = TreeNode(2, TreeNode(4), TreeNode(5))
root.right = TreeNode(3)

print("BFS on binary tree:", bfs_tree(root))
# Output: [1, 2, 3, 4, 5]


# ----------------------------------------------------
# Time Complexity Summary:
# ----------------------------------------------------
# Queue/Deque operations: O(1)
# BFS on Graph: O(V + E)
# BFS on Binary Tree: O(n)
# ----------------------------------------------------
