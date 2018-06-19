---
layout: post
title: "Finding cycles in linked lists"
comments: false
description: "post 9"
keywords: "Cycles, Linked lists, identify, algorithm"
---

![cycled-linked-list](https://github.com/dherath/WebsiteMaterial/blob/master/2018/Post_9_LinkedList/linked_list_org.jpeg?raw=true){:height="200px"}

Hello Everyone!! Hope everyone is doing ok, the previous semester was pretty hectic with research work and courses so didn't really have time to write anything up. But now I'm back <i class="fa fa-smile-o" style="font-size:20px;"></i> and in todays post I thought of writing something interesting I learned in a course and something that apparently ends up being a common interview question for coding/developing positions--that is to _`"identify cycles in a linked list"`_. If you are from a CS background, you'd probably know that job interviews usually consist of a couple of problems which test a candidates knowledge on algorithms & data structures. If you just stumbled across my post and if you had no idea of this, well now you know.

Anyways, without digressing anymore back to my topic--linked lists are a basic data structure like arrays which are used quite a lot. Now if you have no idea about linked lists and you want to learn about them then this is not the post for that. There are lots of youtube tutorials and posts online which would probably give you a fair understanding on how this data structure works. Click on these links to learn more about linked lists - [[youtube]](https://www.youtube.com/watch?v=NobHlGUjV3g), [[weblink]](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)

### The problem : a cyclic linked list

Now to our problem at hand. I'm assuming you know how a link list works, so basically as depicted above each link would have some storage capability to store data and a pointer to the next link which is the arrow. So if you look at the image above, the linked list starts from the red link at the left end and moves to the right. If you follow through the connectivity of this linked list starting form the red links shown in the image above you would notice that the traversal itself would never stop. Because the green pointer (_the arrow_) of the list would point again to the blue link which in-turn points back to the green links.   

This would be a nightmare in real code because the code will run in an infinite loop. And the worst part is its caused because of the connectivity of the underlining data structure and not an issue with the core programing logic, so figuring it out could be tricky also.  But as it turns out there is a simple algorithm that can check if there are any cycles in a linked list.

````c
// definition for a Node in a link list

typedef struct Node{
	Data value; // the data structure

	struct Node * next; // pointer to next node

}Node;

// definition of the linked list

typedef struct Linkedlist{
	Node * head;
}Linkedlist;
````

Lets consider the above basic **C** declarations for a Node (link) and the linked list. I'll be explaining the working algorithm using a **C** skeleton code so I'm again assuming you have some working knowledge of **C** and pointers. If you don't know much about this, think of `Node` and `Linkedlist` as two classes where the linked list has a reference to its _head_ (i.e. its starting location) and each _Node_ has a reference to the data and the Node connected to it.

### Cycle detection algorithm

````c
int detectCycle(Linkedlist * l)
{
	if (l->head == NULL) return 0;
	Node * s = l->head , * f1 = l->head;
	Node * f2 = f1->next;
	while (s && f1 && f2) {
		s = s->next;
		f1 = f2->next;
		if (f1 != NULL) f2 = f1->next;
		if (s == f1 || s == f2) return 1;
	}
	return 0;
}
````
The algorithm itself isn't pretty long right? But how does this work? I'll explain that next.

##### So until next time,
##### Cheers!

**Prev: [Markov Chains 101]({{site.url}}/2018/Markov-Chains/)**
