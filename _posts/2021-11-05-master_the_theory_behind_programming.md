---
layout: post
title:  "Master The Theory Behind Programming"
date:   2021-11-05 09:40:50 +0800
category: tech
---

### Section 1 - Introduction

- Binary Data System
  - How to convert between binary and deca

### Section 2 - Analyzing Algorithms

- Time Complexity
  - Standard way of analyzing and comparing different algorithms. e.g. Big O Notation.
- Math Refresher
  - Logarithmic Functions
    - ```Logx(Y) = A: x^A = Y```
  - Factorial Functions
    - ```3! = 1*2*3```
  - Algebraic Expression
    - ```nlog2(n)```
- n Notation
  - An analysis of how the algorithm will scale with more and more data. It's represented as a function of n.
  - Look for large patterns
    - Dont care about multiples. e.g. sqat(n) equals 3*sqat(n)
    - Just take the lastest in an equation. e.g. -> sqat(n) -> sqat(n) -> nlogn ---> sqat(n) as the lastest one
    - Typical pattern: n, N!, 2^N, n^2, Nlog(N), sqat(N), log(N), 1
  - n Notation example:
    - Every cycle of a program takes .001 sec, how much faster will nlog(n) taek than n^2 if 1,000 pieces of data are input?

    ```javascript
    nlogn = 1000log(1000) = 9960*0.001 = 9.96 seconds
    n^2 = 1000^2 = 1,000,000 * 0.001 = 1,000 seconds = 16 minutes

    nlogn = 25000log(25000) = 365,000*0.001 = 6 minutes 5 seconds
    n^2 = 25000^2 = 625,000,000*0.001 = 7 days 5 hours
    ```

- Big O Notation
  - O(nlogn) means **at worst**, it will be nlogn. Cause it means at worst, that give guidance to evalute how fast the programe will run.It gives us a bound. e.g.
  1. Load: O(n^2)
  2. Execute Step 1: O(nlogn)
  3. Execute Step 2: O(n)
  4. Save: O(1)
  Time Complexity is biggest one as O(n^2) as worst case.
  - Big O Real-world Example

    ```java
    for each data "N" in data list
    {
      //Check if Data is in List
      For each data "W" in data list{
        if N == W, print True
      }
    }
    ```

    Time complexity is: n * n = n^2

### Section 3: Arrays

- Fixed Arrays
  - Collection of data together with fixed size
  - Run time
    - Insert(Rand) - O(n)
    - Insert(Front) - O(n)
    - Insert(Back) - O(1)
    - Delete(Front) - O(n)
    - Delete(Back) - O(1)
    - Search(Unsorted) - O(n)
    - Search(Sorted) - O(logn) -- Binary Search (L+R)/2

- Circular Array
  - Never *Out of bound* issue. Length == mod

    ```python
    def printCircularArray(array, size, ind):
    i = ind
    
    #print from ind-th index to (size+i)th index
    while i < size + ind:
        print(a[(i % size)], end = " ")
        i = i + 1

    a = ['A', 'B', 'C', 'D', 'E', 'F']
    n = len(a);
    printCircularArray(a, n, 3)
    ```

- Dynamic Arrays
  - Why double the array when allocating new array instead of add extra one box every time?

- Approximity
  - When data size growth, in some cases, why O(n) -> O(1) by taking dynamic array as sample.

### Section 4: Linked Lists

- Nodes
  - Composed by 3 parts: Data itself of address, Prev pointer, and Next pointer. 

- Linked List
  - A bunch of Nodes
  - Singly Linked List(单向链表): One way. Pointing to NULL means it's the end of the list.
  - No need to allocate space ahead of time, which might be benefit comparing with Arrays by saving space. E.g. Satalite.
  - Run Time
    - Insert(Rand): O(n)
    - Insert(Front): O(1)
    - Insert(Back): O(n)
    - Delete(Front): O(1)
    - Delete(Back): O(n)
    - Search(Unsorted): O(n)
    - Search(Sorted): O(n)
    - Access Time: O(n)
  - Code Example

    ```python
    class Node:
      def __init__(self, data):
        self.data = data
        self.next = None
    
    class LinkedList:
      def __init__(self):
        self.head = None
    
      def __init__(self, head):
        self.head = head
    
      def __iter__(self):
        node = self.head
        while node is not None:
          yield node
          node = node.next

      def add(self, new_data):
        new_node = Node(new_data)
        new_node.next = self.head
        self.head = new_node  #run time to add at front is O(1) versus adding to the end

    ```

    *Run Code as below*

    ```python
    a = Node("a")
    l = LinkedList(a)
    l.add("b")
    l.add("c")
    for node in l:
      print(node.data)
    ```

  - Doubly Linked List (双向链表)
    - Add a *Prev* pointer
    - Benefit comparing with Singly Linked List is, when deleting a node, Singly Linked List will need run time as: Search O(n) + Delete O(n), total run time will be O(2n)  With *Prev* pointer, it can improve to O(n).
    - Tail Pointer
      - Keep track the last node
      - Optimize **Insert(Back) and Delete(Back)** from O(n) to O(1)

  - Example
    - Web page history in web browser

### Section 5: Stacks and Queues

- Stacks
  - Think about trays in the cafeteria
  - Using **Pop()** to get the top element, and use **Push()** to put elements. This is called LIFO(Last In First Out, or Most Recent IN, First Out)
  - Trying to Pop from an empty stack will cause an error
  - Examples

    ```python
    def createStack():
      stack = []
      return stack
    
    def isEmpty(stack):
      return len(stack) == 0
    
    def push(stack, item):
      stack.append(item)
      print(item + " pushed to stack")

    def pop(stack):
      if(isEmpty(stack)):
        return str("Null")
      
      return stack.pop()

    stack = createStack()
    push(stack, str(10))
    print(pop(stack) + " from stack")
    print(pop(stack))
    ```

    ```python
    stacks = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
    print(stacks)
    stacks.pop()
    stacks.pop()
    stacks.append('coconut')
    print(stacks)
    print(type(stacks))
    ```

- Queues
  - FIFO (First In, First Out).
  - Using a Circular Array or Doubly Linked List with Tail Pointer to implement
  - E.g. How cpu process the tasks.

  - *Code Snippet*

  ```python
  from collections import deque
  queue = deque(["Eric", "John", "Michael"])
  queue.append("Smith")
  queue.append("Tony")
  print(queue)
  queue.pop()
  print(queue)
  queue.popleft()
  print(queue)
  ```
