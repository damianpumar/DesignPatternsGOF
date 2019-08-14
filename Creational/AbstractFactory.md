Abstract Factory
-------

### Definition

Provide an interface for creating families of related or dependent objects without specifying their concrete classes.

Frequency of use:

![](https://www.dofactory.com/images/use_high.gif)

High

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/abstract.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **AbstractFactory**  **(ContinentFactory)**
    -   declares an interface for operations that create abstract products
-   **ConcreteFactory**   **(AfricaFactory, AmericaFactory)**
    -   implements the operations to create concrete product objects
-   **AbstractProduct**   **(Herbivore, Carnivore)**
    -   declares an interface for a type of product object
-   **Product**  **(Wildebeest, Lion, Bison, Wolf)**
    -   defines a product object to be created by the corresponding concrete factory
    -   implements the AbstractProduct interface
-   **Client**  **(AnimalWorld)**
    -   uses interfaces declared by AbstractFactory and AbstractProduct classes

* * * * *

### Structural code in C#

This structural code demonstrates the Abstract Factory pattern creating parallel hierarchies of objects. Object creation has been abstracted and there is no need for hard-coded class names in the client code.



    using System;
    
    namespace DoFactory.GangOfFour.Abstract.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural
        /// Abstract Factory Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            public static void Main()
            {
                // Abstract factory #1
                AbstractFactory factory1 = new ConcreteFactory1();
                Client client1 = new Client(factory1);
                client1.Run();
    
                // Abstract factory #2
                AbstractFactory factory2 = new ConcreteFactory2();
                Client client2 = new Client(factory2);
                client2.Run();
    
                // Wait for user input
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'AbstractFactory' abstract class
        /// </summary>
        abstract class AbstractFactory
        {
            public abstract AbstractProductA CreateProductA();
            public abstract AbstractProductB CreateProductB();
        }
    
    
        /// <summary>
        /// The 'ConcreteFactory1' class
        /// </summary>
        class ConcreteFactory1 : AbstractFactory
        {
            public override AbstractProductA CreateProductA()
            {
                return new ProductA1();
            }
            public override AbstractProductB CreateProductB()
            {
                return new ProductB1();
            }
        }
    
        /// <summary>
        /// The 'ConcreteFactory2' class
        /// </summary>
        class ConcreteFactory2 : AbstractFactory
        {
            public override AbstractProductA CreateProductA()
            {
                return new ProductA2();
            }
            public override AbstractProductB CreateProductB()
            {
                return new ProductB2();
            }
        }
    
        /// <summary>
        /// The 'AbstractProductA' abstract class
        /// </summary>
        abstract class AbstractProductA
        {
        }
    
        /// <summary>
        /// The 'AbstractProductB' abstract class
        /// </summary>
        abstract class AbstractProductB
        {
            public abstract void Interact(AbstractProductA a);
        }
    
    
        /// <summary>
        /// The 'ProductA1' class
        /// </summary>
        class ProductA1 : AbstractProductA
        {
        }
    
        /// <summary>
        /// The 'ProductB1' class
        /// </summary>
        class ProductB1 : AbstractProductB
        {
            public override void Interact(AbstractProductA a)
            {
                Console.WriteLine(this.GetType().Name +
                    " interacts with " + a.GetType().Name);
            }
        }
    
        /// <summary>
        /// The 'ProductA2' class
        /// </summary>
        class ProductA2 : AbstractProductA
        {
        }
    
        /// <summary>
        /// The 'ProductB2' class
        /// </summary>
        class ProductB2 : AbstractProductB
        {
            public override void Interact(AbstractProductA a)
            {
                Console.WriteLine(this.GetType().Name +
                    " interacts with " + a.GetType().Name);
            }
        }
    
        /// <summary>
        /// The 'Client' class. Interaction environment for the products.
        /// </summary>
        class Client
        {
            private AbstractProductA _abstractProductA;
            private AbstractProductB _abstractProductB;
    
            // Constructor
            public Client(AbstractFactory factory)
            {
                _abstractProductB = factory.CreateProductB();
                _abstractProductA = factory.CreateProductA();
            }
    
            public void Run()
            {
                _abstractProductB.Interact(_abstractProductA);
            }
        }
    }

##### Output

    ProductB1 interacts with ProductA1
    ProductB2 interacts with ProductA2