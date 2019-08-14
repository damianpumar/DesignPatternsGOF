Builder
------

### Definition

Separate the construction of a complex object from its representation so that the same construction process can create different representations.

Frequency of use:

![](https://www.dofactory.com/images/use_medium_low.gif)

Medium low

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/builder.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Builder**  **(VehicleBuilder)**

-   specifies an abstract interface for creating parts of a Product object

-   **ConcreteBuilder**  **(MotorCycleBuilder, CarBuilder, ScooterBuilder)**

-   constructs and assembles parts of the product by implementing the Builder interface
-   defines and keeps track of the representation it creates
-   provides an interface for retrieving the product

-   **Director**  **(Shop)**
    -   constructs an object using the Builder interface
-   **Product**  **(Vehicle)**
    -   represents the complex object under construction. ConcreteBuilder builds the product's internal representation and defines the process by which it's assembled
    -   includes classes that define the constituent parts, including interfaces for assembling the parts into the final result

* * * * *

### Structural code in C#

This structural code demonstrates the Builder pattern in which complex objects are created in a step-by-step fashion. The construction process can create different object representations and provides a high level of control over the assembly of the objects.
    
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

	Product Parts -------\
	PartA\
	PartB

	Product Parts -------\
	PartX\
	PartY