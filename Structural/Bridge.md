Bridge
------

### Definition

Decouple an abstraction from its implementation so that the two can vary independently.

Frequency of use:

![](https://www.dofactory.com/images/use_medium.gif)

Medium

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/bridge.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Abstraction **  **(BusinessObject)**
    -   defines the abstraction's interface.
    -   maintains a reference to an object of type Implementor.
-   **RefinedAbstraction **  **(CustomersBusinessObject)**
    -   extends the interface defined by Abstraction.
-   **Implementor **  **(DataObject)**
    -   defines the interface for implementation classes. This interface doesn't have to correspond exactly to Abstraction's interface; in fact the two interfaces can be quite different. Typically the Implementation interface provides only primitive operations, and Abstraction defines higher-level operations based on these primitives.
-   **ConcreteImplementor **  **(CustomersDataObject)**
    -   implements the Implementor interface and defines its concrete implementation.

* * * * *

### Structural code in `C#`

This structural code demonstrates the Bridge pattern which separates (decouples) the interface from its implementation. The implementation can evolve without changing clients which use the abstraction of the object.

    using System;
    
    namespace DoFactory.GangOfFour.Bridge.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural
        /// Bridge Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                Abstraction ab = new RefinedAbstraction();
    
                // Set implementation and call
                ab.Implementor = new ConcreteImplementorA();
                ab.Operation();
    
                // Change implemention and call
                ab.Implementor = new ConcreteImplementorB();
                ab.Operation();
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Abstraction' class
        /// </summary>
        class Abstraction
        {
            protected Implementor implementor;
    
            // Property
            public Implementor Implementor
            {
                set { implementor = value; }
            }
    
            public virtual void Operation()
            {
                implementor.Operation();
            }
        }
    
        /// <summary>
        /// The 'Implementor' abstract class
        /// </summary>
        abstract class Implementor
        {
            public abstract void Operation();
        }
    
        /// <summary>
        /// The 'RefinedAbstraction' class
        /// </summary>
        class RefinedAbstraction : Abstraction
        {
            public override void Operation()
            {
                implementor.Operation();
            }
        }
    
        /// <summary>
        /// The 'ConcreteImplementorA' class
        /// </summary>
        class ConcreteImplementorA : Implementor
        {
            public override void Operation()
            {
                Console.WriteLine("ConcreteImplementorA Operation");
            }
        }
    
        /// <summary>
        /// The 'ConcreteImplementorB' class
        /// </summary>
        class ConcreteImplementorB : Implementor
        {
            public override void Operation()
            {
                Console.WriteLine("ConcreteImplementorB Operation");
            }
        }
    }

##### Output

    ConcreteImplementorA Operation\
    ConcreteImplementorB Operation