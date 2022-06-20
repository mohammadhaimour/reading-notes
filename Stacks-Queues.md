# Stacks and Queues: 
___
## Stack:
 - A stack is a data structure that consists of Nodes. Each Node references the next Node in the stack, but does not reference its previous.

 - Common terminology for a stack :

    1-Push - Nodes or items that are put into the stack are pushed


    2-Pop - Nodes or items that are removed from the stack are popped.When you attempt to pop an empty stack an exception will be raised.


    3-Top - This is the top of the stack.

    4-Peek - When you peek you will view the value of the top Node in the stack. When you attempt to peek an empty stack an exception will be raised.

    5-IsEmpty - returns true when stack is empty otherwise returns false.

- Stacks concepts:

  1 -FILO: First In Last Out
  
  2-LIFO:Last In First Out.

- example of Stacks:
  ![](./image/stack1.PNG)

___
## example Pushing a Node onto a stack:

  ![](./image/stack_push1.PNG)
   ![](./image/stack_push2.PNG)
    ![](./image/stack_push3,4.PNG)
    
 ___
  ## example Popping a Node off a stack:
  
  ![](./image/pop1.PNG)
   ![](./image/pop2.PNG)
    ![](./image/pop3%2C4.PNG)
   
  ___

# Queue :

 - Common terminology for a queue is

   1-Enqueue - Nodes or items that are added to the queue.
   
   2-Dequeue - Nodes or items that are removed from the queue. If called when the queue is empty an exception will be raised.

   3-Front - This is the front/first Node of the queue.

   4-Rear - This is the rear/last Node of the queue.

   5-Peek - When you peek you will view the value of the front Node in the queue. If called when the queue is empty an exception will be raised.

   6-IsEmpty - returns true when queue is empty otherwise returns false.

- FIFO: First In First Out

  This means that the first item in the queue will be the first item out of the queue.

- LILO: Last In Last Out

   This means that the last item in the queue will be the last item out of the queue.

   