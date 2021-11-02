---
layout: post
title:  "John Washam, Great sample of ABC, Always Being Coding"
date:   2021-10-28 15:03:50 +0800
category: tech
---

This is such a [GREAT github repo](https://github.com/jwasham/coding-interview-university) to share all the content from [**John Washam**](https://github.com/jwasham) when he was pareparing the interview of programming, and eventually became an Engineer of Amazon successfully.

With 196k star, 8.4k watch and 52.7k fork as of now. this was planed just a to-do list of study topcis in the beginning, but now it's such a valuable resource for new software engineers. *To do one normal thing in a extreme way will make the whole thing completedly not normal.*

I really should do better job in CODING by the end of 2021.

### Start from Algorithm

- [x] Harvard CS50 - Asymptotic Notation(video)
- [x] Buy the book of **Data structure and Algorithm in Python**
- [x] Big O Natations (general quick tutorial) (video)
  - [Intro to Big O Notation and Time Complexity](https://www.youtube.com/watch?v=D6xkbGLQesk). :thumbsup: for this video, explained all the stuffs in math.
    - How to idenify
      1. find the fastest growing term
      2. take out the coefficient
    - Time complexity
      - linear time O(n)
      - constant time O(1)
      - quadratic time O(n^2)

### Data Structures

- [x] Arrays
  - [x] About Arrays
    - [x] [Arrays(video)](https://www.coursera.org/lecture/data-structures/arrays-OsBSF). Great video. Understand benefits of using Arrays
    - [x] [CS61B:Data Structures - Iteration and Arrays I by Jonathan Shewchuk from UC-Berkeley](https://archive.org/details/ucberkeley_webcast_Wp8oiO_CZZE)

    ---
    - Notes
      - Array: Contiguous area of memory consisting of equal-size elements indexed by contiguous integers
      - Constant-time access: array_addr+elem_size*(i - first_index)
      - Considering the Time Complexity, Array is great for adding/removing in the end with O(1) complexity, but bad for beginning and middle with O(n). Huge benefit is the constant-time access to elements
      - [Dynamic Arrays](https://www.coursera.org/lecture/data-structures/dynamic-arrays-EwbnV) is to resolve the problem that might not know max size when allocating an array. Instead of direct store, idea is to store a pointer to a dynamically allocated array and replace it with a newly allocated array as needed. In Python, it's **list** Java is **ArrayList** C++ is **Vector**
        - sample code:

          ```c++
            PushBack(val)  
            if size = capacity:  
                allocate new_arr[2*capacity]  
                for i from 0 to size - 1:  
                    new arr[i] = arr[i]  
                free arr  
                arr = new_arr  
                capacity = 2*capacity  
            arr[size] = val  
            size = size + 1
          ```

      - [Jagged Arrays](https://www.youtube.com/watch?v=1jtrQqYpt7g), Aka Array of Arrays

        ```c++
          int[][] mil = new int[4][];  
          mil[0] = new int[6];  
          mil[1] = new int[4];
        ```

      - [HashTable](https://zhuanlan.zhihu.com/p/84327339) is different with Arrays. Arrays can only identify the value with index, but HashTable could use Hash Function with input parameter of *key*. That means, for unsorted Array, the time complexity will be O(n), even for sorted Array, it will be O(log2n). But for HashTable, it's always content time of O(1). That means, almost all the *key-value* containers are using HashTable mindset. Taking product as sample, it's **Redis**.

      

- [] Linked List
  - [x] [Linked List (video)](https://www.coursera.org/lecture/data-structures/singly-linked-lists-kHhgK)
  - [x] [CS 61B Lecture 7 : Linked List I](https://archive.org/details/ucberkeley_webcast_htzJdKoEmO0)
  - [x] [Using C code to create Single Linked List](https://www.youtube.com/watch?v=QN6FPiD0Gzo)

  - Notes
    - [Singly-Linked List](https://www.coursera.org/lecture/data-structures/singly-linked-lists-kHhgK)'s PushBack(no tail) is pretty expense since have to start from beginning and walk through till the end, so it's O(n). Same for PopBack(no tail). But if there's tail, for PushBack(with tail), the time complexity down to O(1). But for PopBack(with tail), it's still O(n) (*think about why*)

      ```java
      public class ListNode{
        int item;
        ListNode next;
      }
      ListNode l1 = ListNode();
      ListNode l2 = ListNode();
      ListNode l3 = ListNode();
      l1.item = 7;
      l2.item = 0;
      l3.item = 6;
      l1.next = l2;
      l2.next = l3;
      l3.next = null;  // In Java, null has to be lower case 
      ```

### Python Basic

- [ ] Python Gramma

### Udemy Courses

- [ ] Computer Science 101: Master the Theory Behind Programming
- [ ] Python Programming Bootcamp
- [ ] Complete Python Developer in 2021: Zero to Mastery
- [ ] 100 Days of Code - The complete Python Programming

### Resources

- [emoji shortcuts](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md) could be well used in Markdown documentation, and IF you want to apply into Jekyll like this site, you need to update *_config.yml* to apply by adding *plugins*.
- Use [Jupyter Notebook](https://jupyter.org/) to take as notebook since it can either run Python and can also using Markdown to take notes. Github.io is that just for tracking the progress. **AMAZING !!**