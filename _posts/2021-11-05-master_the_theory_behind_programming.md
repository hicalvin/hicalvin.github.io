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

  ```python
  class Queue:
    def __init__(self, capacity):
      self.front = self.size = 0
      self.rear = capacity -1
      self.Q = [None] * capacity
      self.capacity = capacity

    def isFull(self):
      return self.size == self.capacity

    def enQueue(self, item):
      if self.isFull():
        print("Full)
        return
      self.rear = (self.rear + 1) % (self.capacity)
      self.Q[self.rear] = item
      self.size = self.size + 1
      pritn("%s enqueued to queue" % str(item))
  ```

- Stack and Queue Real World Example
  - Undo and Redo
  - Maze
  - Case learning

    ```python
    We have a stack and queue, [-, -, 4, 3] and [-, -, 2, 1] respectively. When you pop off of the stack, it enqueue on to the queue, implemented as a circular array.(So pop(x) => both pop off the stack and enqueue(x)).

    (Front of the queue is currently on 2, and back on 1. We queue on to the front, and remove from the back. Note: )

    What will the stack and queue look like after: *pop(), push(4), pop(), dequeue(), push(5), push(6), pop(), dequeue(), push(4), pop(), dequeue()
    a. Stack: [-,-,5,3] Queue: [4,-,4,6]
    b. Stack: [-,-,5,3] Queue: [-,-,4,6]
    c. Stack: [-,-,-,5] Queue: [4,-,-,6]
    d. Stack: [-,-,-,-] Queue: [4,-,4,6]
    ```

### Sorting Algorithm

[Visualgo.net](https://visualgo.net/en/sorting) shows all the sorting algorithm with visualized motional graphs. Very useful resoruce.

- Bubble Sort (冒泡排序)
  - Bubble Sort is arguably the simplest sorting algorithm. It works by repeatedly swapping adjacent elements that are in the wrong order.
  - Easy to implement, but **bad algorithm**
  - Run Time:
    - O(n^2)

    ```c
    do
      swapped = false
      for i = 1 to idnexOfLastUnsortedElement - 1
        if leftElement > rightElement
          swap(leftElement, rightElement)
          swapped = true
    while swapped
    ```

    - *Code Sample*

    ```python
    def bubbleSort(arr):
    n = len(arr)

    for i in range(0, n-1):
      for j in range(0, n-i-1):
        if arr[j] > arr[j+1]:
          arr[j], arr[j+1] = arr[j+1], arr[j]
    ```

- Selection Sort (选择排序)
  - Run Time: O(n^2). Even the best run time is also n^2
  - The **most inefficient** sort algorithm
  - Code Sample

    ```python
    def selectionSort(arr):
      n = len(arr)
      for i in range(0, n-1):
        min_index = i
        for j in range(i+1, n-1):
          if arr[min_index] > arr[j]
            min_index = j

        arr[i], arr[min_index] = arr[min_index], arr[i]
    ```

- Insertion Sort (插入排序法)
  - The selection sort is very similar to that of bubble sort. Instead of finding a max however, It repeatedly finds the minimum element from the unsorted portion, and puts it into a "sorted portion".
  - Run time: O(n^2) (identical to bubble sort)
  
- Recursion
  *Sample*

  ```java
  int sumBy3(int n, int x)
  {
    print("We are at: " + n)
    if(n < = 1) // base case
      return x;
    else
      return sumBy3(n-3, x+n)
  }
  ```

- Quick Sort
  - Quick Sort works off picking a “pivot” point. All numbers less than the pivot point go to the left, and all numbers greater than the pivot point go to the right. It then reapplies this algorithm to each side of the pivot
  - Run time: average case is O(nlogn)
  - [A Complete Overview of Quicksort](https://www.youtube.com/watch?v=0SkOjNaO1XY) worth to figure out, which can clearly explained the source codes.
  - Example

    ```python
    def quicksort(arr, low, high):
      if low < high:  # base case to exit from recursion

        #create our pivot array
        partitionIndex = partition(arr, low, high)

        quickSort(arr, low, partitionIndex -1 )
        quickSort(arr, partitionIndex + 1, high)
    
    def partition(arr, low, high):
      i = (low - 1)  # index of smaller elelment
      pivot = arr[high]  # pivot
      for j in range(low, high):

        # If curent elelment is smaller than the pivot
        if arr[j] < pivot:

          # increment index of smaller element
          i = i + 1
          arr[i], arr[j] = arr[j], arr[i]
      
      arr[i+1], arr[high] = arr[high], arr[i+1]
      return (i+1)

    arr = [55, 44, 10, 30, 15, 35]
    quickSort(arr, 0, len(arr)-1)
    ```

- Merge Sort (归并排序)
  - Merge Sort is the fastest algorithm we are going to be analyzing. (Fastest on average, quicksort is technically faster, but has the problem of the n^2 worst case).  It has a way of dividing the data up like in quick sort, except that it doesn’t require selecting a pivot point to get the nlogn run times
  - Kind of the fastest algorithm. Recommend [Merge Sort - Data Structure & algorithms Tutorial Python](https://www.youtube.com/watch?v=nCNfu_zNhyI) which tell the merge sort with Python clearly. 
  - Run Time: O(nlogn)

    ```pseudocode
    MergeSort(arr[], l, r)
    if r > 1
      1. Find the pivot. We are choosing the array.:
         1. middle m = (1+r)/2
      2. Call mergeSort recursively for first half:
         1. Call mergeSort(arr, 1, m)
      3. Call mergeSort recursively for second half:
         1. Call mergeSorge(arr, m+1, r)
      4. Merge the two halves sorted in step 2 and 3:
         1. Call merge(arr, 1, m, r)
    ```

    *Code Sample*
    ```python
    def merge_sort(arr):
      if len(arr) <= 1:
        return arr
      
      mid = len(arr)//2

      left = arr[:mid]
      right = arr[mid:]

      left = merge_sort(left)
      right = merge_sort(right)

      return merge_two_sorted_lists(left, right)
    
    def merge_two_sorted_lists(a, b):
      sorted_list = []
      len_a = len(a)
      len_b = len(b)
      i = j = 0  # i is the index of a, j is the index of b

      while i < len_a and j < len_b:
        if a[i] <= b[j]:
          sorted_list.append(a[i])
          i+ = 1
        else:
          sorted_list.append(b[j])
          j+ = 1
      
      while i < len_a:
        sorted_list.append(a[i])
        i+ = 1

      while j < len_b:
        sorted_list.append(b[j])
        j+ = 1

      return sorted_list

    if __name__ == '__main__':
      arr = [5, 8, 23, 56, 89, 100, 7, 9, 52, 45]
      sorted_arr = merge_sort(arr)

      print(sorted_arr)
    ```

    *Optimized Code Sample by saving memory*
    ```python
    def merge_sort(arr):
      if len(arr) <= 1:
        return
      
      mid = len(arr)//2

      left = arr[:mid]
      right = arr[mid:]

      left = merge_sort(left)
      right = merge_sort(right)

      merge_two_sorted_lists(left, right, arr)
    
    def merge_two_sorted_lists(a, b, arr):

      len_a = len(a)
      len_b = len(b)
      i = j = k = 0  # i is the index of a, j is the index of b, k point to the postion of new sorted array

      while i < len_a and j < len_b:
        if a[i] <= b[j]:
          arr[k] = a[i]
          i+ = 1
        else:
          arr[k] = b[j]
          j+ = 1
        k+ = 1

      while i < len_a:
        arr[k] = a[i]
        i+ = 1
        k+ = 1

      while j < len_b:
        arr[k] = b[j]
        j+ = 1
        k+ = 1

    if __name__ == '__main__':
      arr = [5, 8, 23, 56, 89, 100, 7, 9, 52, 45]
      merge_sort(arr)

      print(arr)
    ```

- Stable and Non-Stable
  - Sometimes the order of data within data structures is important. Certain sorting algorithms adhere to this importance, while others don’t. If a data structure takes order in to account, we call it stable, if it doesn’t, we call it not stable or non-stable.  
  - Selection Sort and Quick Sort is NOT stable (Quick Sort happens when picking the pivot. Selection Sort happends when it swap)
  - Bubble, Insertion and Merge Sort is stable

- Trees
  - Binary Search Tree (BST)
    - Each node can only have at most two children  
    - All right children must be greater than  
    - All left children must be less than or equal to. (You can put the equal to on the right or left)  
  - Trees are some of the most used data structures in computer science. They link information together in a relational way. You can use them to sort, to store information, to make inferences, and so much more. They are even used in databases to help index (find) the data in the database.  
  - Parents are the nodes that are directly above another node, while children are ones that are directly below

  ```python
  class Node:
    def __init__(self, key):
      self.left = None
      self.right = None
      self.val = key

    def insert(root, key):
      if root is None:
        return Node(key)
      else 
        if root.val == key:
          return root
        elif root.val < key:
          root.right = insert(root.right, key)
        else:
          root.left = insert(root.left, key)
      return root
    
    def search(root, key):
      if root is None or root.val = key:
        return root
      
      if root.val < key:
        return search(root.right, key)
      
      return search(root.left, key)
  ```

  - Tree Traversals
    - InOrder: Left, Root, Right
    - PreOrder: Root, Left, Right
    - PostOrder: Left, Right Root
    - Tree Example:
      <img src='https://g.gravizo.com/svg?
 digraph G {
   20 -> 10;
   20 -> 25;
   10 -> 5 -> 7;
   10 -> 13;
   7 -> 6
   7 -> 8;
   25 -> 23 -> 24;
 }
'/>
      - InOrder: L, Ro, R:  5, 6, 7, 8, 10, 13 20, 23, 24, 25

      - PreOrder: Ro, L, R: 20, 10, 5, 7, 6, 8, 13, 25, 23, 24

      - PostOrder: L, R, Ro: 6, 8, 7, 5, 13, 10, 24, 23, 25, 20

      - LevelOrder: 20, 10, 25, 5, 13, 23, 7, 24, 6, 8

  - Tree Real World Examples
    - Tree Directory
    - Database Indexing
    - Decision Trees

- Heap
  - Sub-devision of Tree
  - Heap property is sort of Level Property, and the parent nodes has relationship (either **Greater(max)** or **Less Than(min)**)
  - Run Time:
    - Insert: O(logn)
    - Remove