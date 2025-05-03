---

encapsulation
	this keyword, setters and getters private attributes
inheritance 
polymorhpism
abstraction on  classes 
what the final keyword does in inheritance


----
Pillars of *OOP*  
1. [[Encapsulation]]
2. [[ABstraction]]
3. [[Inheritance]]
4. [[Polymorhpism]]

> [!NOTE] Constructors
> Constructors are the methods called to create an instance *Object* of a class.
>  - The Name of the constructor must be exactly the same as the class
>  - They must have no return type.
>  - If no paramaterized constructors are created, a default constructor *(no-argument)* is implicity provided by the compiler. However, when defining paramaterized constructors, the complier does not provide the default constructor and it must be explicitly defined.
>  - The default constructor calls the default constructor of the superclass, so you must verify that the superclass has a defined default constructor or you can override this behaviour by explicitly selecting the which superclass constructor to be called by invoking ```super()```.
