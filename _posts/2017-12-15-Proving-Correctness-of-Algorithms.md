---
layout: post
title: "Proving correctness of Algorithms"
comments: false
description: "post 7"
keywords: "Proving, proof, correctness, algorithms, linear search, insertion sort, loop invariants"
---
![queen-of-hearts](https://i.pinimg.com/736x/2d/3f/e5/2d3fe59c74315f74a05b371f67486701.jpg){: height="400px"}
Hello Everyone !! Hope everything is great, the new year is around the corner so I'll be getting couple of days off from work and university, so I thought of writing something interesting I learned in the Algorithms course I took the previous semester. Imagine you have a deck of cards(**which could be incomplete**) in your hand all shuffled together, and someone asks you to find the `Queen of hearts` in it. So how would you go about it... There are two scenarios,

1. The **Queen of Hearts** is in the card deck
2. The **Queen of Hearts** is not in the deck

But since you don't know before hand, the most logical way to go about this problem is to take one card at a time, see if its the queen of hearts, if it is then no point searching further; and if it's not you keep on doing this until you run out of cards where it's safe to say your deck doesn't have that card. This solution seems intuitively correct and the steps seem logical too. So I'm sure you'd agree with me that this method works. But **Imagine** a more complex scenario where _you've_ found a method that can ensure the accurate prediction of the next _flood_ or _hurricane_ or some disaster. Now this is a very serious claim, because human lives depend on your algorithm. So an obvious question that anyone would ask is **`how can you say that your method always gives us the answer we need?`**

Thats where proving algorithms really come into the picture, so today I'll be talking about a technique used to prove the correctness of Algorithms using **Loop Invariants**.

#### Proving Correctness using Loop Invariants

The first question you might have is _"What is a loop invariant?"_ well thats pretty simple, a loop invariant is some condition of a given algorithm that is true before & after an execution of a loop. The loop itself could be anything(_for, while..._). The way to go about proving an algorithm to be correct is by **first** defining a condition that must be true before & after the loop. **Then** we show that condition is true before the execution of the algorithm, while it is executing and **finally** after it's done.  So essentially by induction if an algorithm is correct at its initiation, termination & while its running then the algorithm must be correct. These three cases are called `initialization, maintenance & termination`.

>The tricky part here is not proving the three cases, rather it's selecting/defining a **loop invariant** which can be easily shown to be true in those cases. Depending on how you define the invariant the proof could be simple or complicated, and theres no exact science for it and in my opinion I think it's more of an art :)

In the sections below I'll be showing two basic algorithms(<a href="#ref1">linear search</a> & <a href="#ref2">insertion sort</a>) to be true using loop invariants.

#### <a name="ref1">1) linear search</a>

Linear Search is an easy algorithm and it works the same way as my _finding cards example_ I mentioned above. The pseudocode below describes it in a more formal manner. Instead of searching for cards lets consider a case where the objective is to find some integer value **v** in a Set **A**.

---

|**Input ->**|a set **A** with values {$$ a_1, a_2, a_3,... a_N $$} and **v** the value to be searched|
|**Output ->**|the index **i** of some $$ a_i $$ where $$ a_i=v $$ OR **NILL** if $$ a_i \neq $$ v $$~~\forall~~ i~\in~N $$ |

````
LINEAR-SEARCH(A,v):
// 1-4 are line number
1)  for i = 1 to length[A]
2)    if A[i] == v
3)      then return i
4)  return NILL
````

>**Loop Invariant:**
At the start of each iteration of the for loop in line 1, the subset A[1 ... i-1] would not have the value 'v' in it.

The following section shows how the loop invariant is maintained in the three stages of the algorithm, namely initiation, maintenance & termination.

---

|**I. Initialization:**
Before the first iteration of the loop the subset of A in question would be an empty set. Therefore 'v' would not be in it. Then the loop invariant holds true trivially|
|**II. Maintenance:**
Assuming the subset A[1 ... k-1] does not have the value v, from the comparison in line 2 the loop will transition from the $$ k^{th} $$ iteration to a $$ (k+1)^{th} $$ iteration only if v was not observed. (i.e : $$ A[k] \neq v $$) Therefore at the $$ (k+1)^{th} $$ iteration the subset A[1 ... k] wouldn't have v in it. Which indicates that the loop invariant holds true from a $$k^{th}$$ iteration to a $$(k+1)^{th}$$ iteration|
|**III. Termination:**
At the end of the for loop i = length[A]+1 then the subset would be the complete set 'A' itself. At which point provided 'v' was not found the loop terminates and returns NILL indicating that 'v' is not present within the set 'A'|

From these three cases it's clear that our algorithm is correct and it aligns to our intuitive guess as to why our card searching approach works as well. Now off to a slightly more different problem _insertion sort_.

#### <a name="ref2">2) insertion sort</a>

Like any sorting algorithm, the objective of _insertion sort_ is to sort a given sequence of numbers in some order.(_For our example lets consider ascending_).In a nutshell _insertion sort_ works by taking some element in a set and then finding its desired location to be placed for the set to be sorted and then swapping elements until it's placed in that new location. This process occurs for the entirety of the set. If you are unfamiliar with insertion sort check this [video](https://www.youtube.com/watch?v=i-SKeOcBwko&t=47s){:target="blank"} for more reference.

---

|**Input ->**|a set **A** with a sequence of numbers {$$ a_1, a_2, a_3,... a_N $$} |
|**Output ->**|a permutation **A$$^/$$** with a sequence of numbers {$$ a^/_1, a^/_2, a^/_3,... a^/_N $$} where $$ a^/_i \leq a^/_{i+1}~~\forall~~i~\in~N $$|

````
INSERTION-SORT(A):
// indices of the set start with 1
1)  for j=2 to length[A]
2)    key = A[j]
3)    i = j-1
4)    while i > 0 and A[i] > key
5)      A[i+1] = A[i]
6)      i = i-1
7)    A[i+1] = key
````
>**Loop Invariant:**
At the start of each iteration of the for loop of lines 1-7, the subset A[1 ... j-1] would consist of the elements originally in A[1 ... j-1], but in sorted order.

The following section shows again how the loop invariant is maintained in the three stages of the algorithm, namely initiation, maintenance & termination.

---

|**I. Initialization:**
Before the first iteration of the loop j=2 then the subset of A in question would be a set with only one value. Therefore the loop invariant holds true since trivially A is sorted|
|**II. Maintenance:**
Assuming the loop invariant holds true for the (k-1)$$^{th}$$ iteration then the subset A[1 ... k-1] would be in sorted order. When j = k the while loop starting from line 4 finds the correct position for A[k] such that when swapping is completed A[1 ... k] would be in sorted order. Therefore the loop invariant is maintained from any k$$^{th}$$ iteration to a (k+1)$$^{th}$$ iteration|
|**III. Termination:**
At the end of the for loop j = length[A]+1 then the subset is the set itself, therefore according to the loop invariant the entire set itself would be in sorted order|

So there you have it, two proofs of correctness for two different algorithms using the technique of _loop invariants_. You might have noticed that this technique heavily relies on the algorithms **loop**, what about algorithms without any kind of loop? well there are a bunch of ways to prove correctness of algorithms not just this; however thats a post for another day :).

##### So until next time,
##### Cheers!

**Prev: [From Computational Physics to Computer Science](http://dinalherath.com/2017/Computational-Physics-to-Computer-Science/)**
