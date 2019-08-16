Decorator
------

### Definition

Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

Frequency of use:

![](https://www.dofactory.com/images/use_medium.gif)

Medium

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/decorator.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Component **  **(LibraryItem)**
    -   defines the interface for objects that can have responsibilities added to them dynamically.
-   **ConcreteComponent **  **(Book, Video)**
    -   defines an object to which additional responsibilities can be attached.
-   **Decorator **  **(Decorator)**
    -   maintains a reference to a Component object and defines an interface that conforms to Component's interface.
-   **ConcreteDecorator **  **(Borrowable)**
    -   adds responsibilities to the component.

* * * * *

### Structural code in `C#`

This structural code demonstrates the Decorator pattern which dynamically adds extra functionality to an existing object.

    using System;
    
    namespace DoFactory.GangOfFour.Decorator.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural 
        /// Decorator Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                // Create ConcreteComponent and two Decorators
                ConcreteComponent c = new ConcreteComponent();
                ConcreteDecoratorA d1 = new ConcreteDecoratorA();
                ConcreteDecoratorB d2 = new ConcreteDecoratorB();
    
                // Link decorators
                d1.SetComponent(c);
                d2.SetComponent(d1);
    
                d2.Operation();
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Component' abstract class
        /// </summary>
        abstract class Component
        {
            public abstract void Operation();
        }
    
        /// <summary>
        /// The 'ConcreteComponent' class
        /// </summary>
        class ConcreteComponent : Component
        {
            public override void Operation()
            {
                Console.WriteLine("ConcreteComponent.Operation()");
            }
        }
    
        /// <summary>
        /// The 'Decorator' abstract class
        /// </summary>
        abstract class Decorator : Component
        {
            protected Component component;
    
            public void SetComponent(Component component)
            {
                this.component = component;
            }
    
            public override void Operation()
            {
                if (component != null)
                {
                    component.Operation();
                }
            }
        }
    
        /// <summary>
        /// The 'ConcreteDecoratorA' class
        /// </summary>
        class ConcreteDecoratorA : Decorator
        {
            public override void Operation()
            {
                base.Operation();
                Console.WriteLine("ConcreteDecoratorA.Operation()");
            }
        }
    
        /// <summary>
        /// The 'ConcreteDecoratorB' class
        /// </summary>
        class ConcreteDecoratorB : Decorator
        {
            public override void Operation()
            {
                base.Operation();
                AddedBehavior();
                Console.WriteLine("ConcreteDecoratorB.Operation()");
            }
    
            void AddedBehavior()
            {
            }
        }
    }

##### Output

    ConcreteComponent.Operation()\
    ConcreteDecoratorA.Operation()\
    ConcreteDecoratorB.Operation()