## Interface
- An interface is essentially a contract that a class will follow in order to standardize an API (think header file)
	```
	interface MyInterface
	{
	   /* compiler will treat them as: 
		* public abstract void method1();
		* public abstract void method2();
		*/
	   public void method1();
	   public void method2();
	}

	class Demo implements MyInterface
	{
		/* This class must have to implement both the abstract methods
		* else you will get compilation error
		*/
		public void method1()
		{
		System.out.println("implementation of method1");
		}
		public void method2()
		{
		System.out.println("implementation of method2");
		}
		public static void main(String arg[])
		{
		MyInterface obj = new Demo();
		obj.method1();
		}
	}
	```

## Singletons
- A class that's set up so there's only one instance of it in the Java virtual machine

## Abstract Methods and Classes
- An abstract class is a class that is declared `abstract`
	— It may or may not include abstract methods
- Abstract classes cannot be instantiated, but they can be subclassed
- "Abstract classes are similar to interfaces. You cannot instantiate them, and they may contain a mix of methods declared with or without an implementation. However, with abstract classes, you can declare fields that are not static and final, and define public, protected, and private concrete methods. With interfaces, all fields are automatically public, static, and final, and all methods that you declare or define (as default methods) are public. In addition, you can extend only one class, whether or not it is abstract, whereas you can implement any number of interfaces." (https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html)

## Factory Pattern
- "...create object without exposing the creation logic to the client and refer to newly created object using a common interface."
- See [here](https://www.tutorialspoint.com/design_pattern/factory_pattern.htm) for an example of a `ShapeFactory`
	- In the example, there are classes for circles, squares, and triangles with a `ShapeFactory` that returns a different class depending on parameter input

### Abstract Factories
- A super-factory creates other factories

## Spring
- Spring is largely used for inversion of control (IoC)
- Spring 5 was just released with a focus on Reactive Programming (https://www.reactivemanifesto.org/)

### Inversion of Control
- If a function needs a dependency, that dependency should be passed in as an argument so that there aren't tight dependencies anywhere:
- Instead of (https://stackoverflow.com/a/3140/3958178):
	```
	public class TextEditor {
		private SpellChecker checker;

		public TextEditor() {
			this.checker = new SpellChecker();
		}
	}
	```
	...do...
	```
	public class TextEditor {
		private IocSpellChecker checker;

		public TextEditor(IocSpellChecker checker) {
			this.checker = checker;
		}
	}

	SpellChecker sc = new SpellChecker; // dependency
	TextEditor textEditor = new TextEditor(sc);
	```
