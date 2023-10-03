Original: [Queues: A Tale of Two Stacks](https://www.hackerrank.com/challenges/ctci-queue-using-two-stacks/problem?h_r=internal-search)

## Problem
A queue is an abstract data type that maintains the order in which elements were added to it, allowing the oldest elements to be removed from the front and new elements to be added to the rear. This is called a First-In-First-Out (FIFO) data structure because the first element added to the queue (i.e., the one that has been waiting the longest) is always the first one to be removed.

A basic queue has the following operations:
- Enqueue: add a new element to the end of the queue.
- Dequeue: remove the element from the front of the queue and return it.

In this challenge, you must first implement a queue using two stacks. Then process <i>q</i> queries, where each query is one of the following <i>3</i> types:
1. ``1 x``: Enqueue element <i>x</i> into the end of the queue.</li>
1. ``2``: Dequeue the element at the front of the queue.
1. ``3``: Print the element at the front of the queue.


## Code
```java
class MyQueue<T> {
    private Stack<T> stackin = new Stack<>();
    private Stack<T> stackout = new Stack<>();
    
    public void enqueue(T n) {
        stackin.push(n);
    }
    
    public void dequeue() {
        if(stackout.isEmpty()) {
            while(!stackin.isEmpty())
                stackout.push(stackin.pop());
        }
        stackout.pop();    
    }
    
    public T peek() {
        if(stackout.isEmpty()) {
            while(!stackin.isEmpty())
                stackout.push(stackin.pop());
        }
        
        return stackout.peek();
    }
}
```
