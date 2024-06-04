---
layout: post
title: "Understanding Memory and Data in C: A Foundation for Programming"
feature_image: /assets/images/posts/2024-05-29-Understanding_Memory_and_Data/stack_and_heap.png
categories: misc
---


I’ve been re-visiting the content of C language - something I haven't seen for a while. I’m trying to better understand how data structures work because I believe that will make the effort of learning new programming languages easier. While syntax and some language-specific features may vary, the core concepts of data manipulation often remain consistent across languages like Java, Go, and others. This shared understanding I believe will give me a significant advantage when learning new languages, as I'll already have a solid foundation to build upon.

C is a low-level programming language, which means it deals with memory in a lower level as well. Getting in touch with concepts such as pointers and memory allocation are fundamental for understanding the inner workings of many other programming languages. I’ve once heard from an experienced programmer that we all should learn what goes “under the hood”. We should see ourselves as Mechanics, trying to understand the intricacies of how engines operate as it will be a valuable knowledge when the time comes to fix issues efficiently. My goal learning of data structures in C is follows the same line: understand the inner workings of data structures in order to gather a deeper understanding of how data is stored, accessed, and manipulated in memory. This fine-grained control over memory usage can give us the power to write more efficient code, debug problems effectively, and optimize performance when necessary. On top of that is the fact that many other languages, including higher-level ones, are implemented in or interact with C. Examples include: Python, PHP, Ruby, among others.

To start with we have to understand how the memory is allocated. Whenever a process needs to run on our computer,it needs memory to store its instructions. Who’s responsible for making such allocations? The operating system (OS) - this memory management is crucial for the stability, security, and performance of a computer system. Once the OS allocates the desirable memory for the given process it is time to think on how data and variables of this process will be stored. Data can actually be stored in different ways depending on factors such as programming language, scope and memory management. The most common ways to store data are:

<ul>

<li>Continuous: arrays and vectors are examples of data that is stored continuously. If we have a vector of four positions, we know that one position is continuously placed at the side of the other. It follows a sequence. This is why it is easier to access the elements of an array, all we need is its index.</li>
<li>Non-continuous: here the data is placed in different parts of the memory. To access it we will use the infamous “pointers”.</li>
<li>Static: whenever we have data allocated since the beginning of the program we say that this data is allocated statically in RAM.</li>
<li> Dynamic: it means the memory will be allocated dynamically by demand, which means that the data will be allocated as the program needs it. In general it refers to data that is non-continuous stored.</li>

</ul>

<br>

![Image of my newly create API route]({{site.url}}/assets/images/posts/2024-05-29-Understanding_Memory_and_Data/memory_allocation.png){: style="display: block; margin: 0 auto"}

<br>

At the base of the diagram is the Static Variables - these are already allocated since the beginning of the program. We can change its value, but not its structure. Along with the Instructions and Local Variables, they collectively form what is referred to as Fixed Storage Data. All three are allocated when the program starts running.

And at the top of my diagram lies the Stack and Heap memory. What are the differences between them? Let’s think about functions. When a function is called, space for its local variables and parameters is allocated on the Stack. This memory is automatically freed when the function returns. In a nutshell, Stack Memory is usually responsible for keeping in memory the variables of our functions. The Heap Memory, on the other hand, stores the structures that are allocated in the runtime.  Structures allocated in heap memory are usually referred to as dynamically allocated structures.To allocate Heap Memory dynamically in C we can use functions like ‘malloc()’, ‘calloc()’ or ‘realloc(). Heap-allocated structures are useful when you need data that persists beyond the scope of a function. However, it’s important to manage this memory properly to avoid memory leaks or other issues. 

<br>

![Image of my newly create API route]({{site.url}}/assets/images/posts/2024-05-29-Understanding_Memory_and_Data/stack_and_heap.png){: style="display: block; margin: 0 auto"}


<br>

What should I do then? Allocate memory in a continuous manner or dynamically given the demand? Well, it actually depends. Both strategies have its ups and downs. Is it possible to know everything that is going to be allocated before running the program? If yes, then we should try to allocate the memory continuously. If we don't know that for sure, then we better allocate dynamically as the program needs it. Structures such as trees, graphs, and linked lists often benefit from dynamic memory allocation because their size and structure can vary dynamically based on program inputs and operations.These are all non-linear structures. And what does that mean? It means that the data of these structures are not arranged in a sequential or linear manner. And here is where Pointers become handy, they are the ones responsible for making the “links” between each of the elements of the structure.

In conclusion, going through the dynamics of memory allocation and data structures in C not only equip us with a deeper understanding of programming fundamentals but also lays a solid base for understanding other programming languages. Whether we choose to allocate memory continuously or dynamically, understanding the trade-offs of each approach will guide us into making more informed decisions - which will eventually bring more efficiency to our code. 



