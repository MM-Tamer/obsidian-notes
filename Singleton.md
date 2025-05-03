when a class is required to have only one object. So every time you're trying to create an object, that newly created object either creates the object for the first time or returns the already created object.
``` java  title:"Singleton.class"

public class Singleton {
private Singleton object; // equals NULL

// private constructor to restrict creation of new objects
private Singleton(){

}
static Singleton getSingleton(){

	if(object == null){
		object = new Singleton();
		return object;
	} else {
		return object;
	}

}

}
```