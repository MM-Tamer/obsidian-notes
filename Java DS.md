

> [!NOTE] Array
> Arrays in java are a collection of elements. The size of the array must be determined during initialization and is fixed (static) . 
> e.g:
> ```
> int[] myNum = {10, 20, 30, 40};  
> String[] cars = {"Volvo", "BMW", "Ford", "Mazda"}; 
> ```
> Complexity :
> 
> |Insert     |Delete     | Read |
| --- | --- |---|
|  O(n)   |O(n)     | O(1) |






>[!NOTE] ArrayList
> Arrays were introduced to fix the problem of static size of arrays. ArrayLists are Dynamic in size however, there's an overhead introduced in deallocating and reallocating whenever the size of the array is required to change. 
> e.g:
> ```
> ArrayList<String> cars = new ArrayList<String>();

> Complexity :
> 
> |Insert     |Delete     | Read |
| --- | --- |---|
|  O(n)   |O(n)     | O(1) |


>[!NOTE] LinkedList
> A linked list is collection of nodes linked in a sequence. There's a head which is the first node and a tail which is the last node. Every node contains a pointer to the next node 
> e.g:
> ```
> LinkedList<String> cars = new LinkedList<String>(); 
> cars.add("Volvo");
> ```
> Complexity :
> 
> |Insert     |Delete     | Read |
| --- | --- |---|
|  O(1)   |O(1)     | O(n) |



>[!NOTE] Stack
> Stack is LIFO (Last-In-First-Out) data structure and contains two main methods _push_ & _pop_ to add or remove elements at the top of the stack, in addition to _peek_ which returns the element at the top of stack without popping it.






