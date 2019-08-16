Prototype
-------

### Definition

Specify the kind of objects to create using a prototypical instance, and create new objects by copying this prototype.

Frequency of use:

![](https://www.dofactory.com/images/use_medium.gif)

Medium

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/prototype.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Prototype**  **(ColorPrototype)**
    -   declares an interface for cloning itself
-   **ConcretePrototype**  **(Color)**
    -   implements an operation for cloning itself
-   **Client**  **(ColorManager)**
    -   creates a new object by asking a prototype to clone itself

* * * * *

### Structural code in C#

This structural code demonstrates the Prototype pattern in which new objects are created by copying pre-existing objects (prototypes) of the same class.

	using System;
	using System.Collections.Generic;

	namespace DoFactory.GangOfFour.Builder.Structural
	{
	    /// <summary>
	    /// MainApp startup class for Structural
	    /// Builder Design Pattern.
	    /// </summary>
	    public class MainApp
	    {
	        /// <summary>
	        /// Entry point into console application.
	        /// </summary>
	        public static void Main()
	        {
	            // Create director and builders
	            Director director = new Director();

	            Builder b1 = new ConcreteBuilder1();
	            Builder b2 = new ConcreteBuilder2();

	            // Construct two products
	            director.Construct(b1);
	            Product p1 = b1.GetResult();
	            p1.Show();

	            director.Construct(b2);
	            Product p2 = b2.GetResult();
	            p2.Show();

	            // Wait for user
	            Console.ReadKey();
	        }
	    }

	    /// <summary>
	    /// The 'Director' class
	    /// </summary>
	    class Director
	    {
	        // Builder uses a complex series of steps
	        public void Construct(Builder builder)
	        {
	            builder.BuildPartA();
	            builder.BuildPartB();
	        }
	    }

	    /// <summary>
	    /// The 'Builder' abstract class
	    /// </summary>
	    abstract class Builder
	    {
	        public abstract void BuildPartA();
	        public abstract void BuildPartB();
	        public abstract Product GetResult();
	    }

	    /// <summary>
	    /// The 'ConcreteBuilder1' class
	    /// </summary>
	    class ConcreteBuilder1 : Builder
	    {
	        private Product _product = new Product();

	        public override void BuildPartA()
	        {
	            _product.Add("PartA");
	        }

	        public override void BuildPartB()
	        {
	            _product.Add("PartB");
	        }

	        public override Product GetResult()
	        {
	            return _product;
	        }
	    }

	    /// <summary>
	    /// The 'ConcreteBuilder2' class
	    /// </summary>
	    class ConcreteBuilder2 : Builder
	    {
	        private Product _product = new Product();

	        public override void BuildPartA()
	        {
	            _product.Add("PartX");
	        }

	        public override void BuildPartB()
	        {
	            _product.Add("PartY");
	        }

	        public override Product GetResult()
	        {
	            return _product;
	        }
	    }

	    /// <summary>
	    /// The 'Product' class
	    /// </summary>
	    class Product
	    {
	        private List<string> _parts = new List<string>();

	        public void Add(string part)
	        {
	            _parts.Add(part);
	        }

	        public void Show()
	        {
	            Console.WriteLine("\nProduct Parts -------");
	            foreach (string part in _parts)
	                Console.WriteLine(part);
	        }
	    }
	}

##### Output

	Cloned: I\
	Cloned: II