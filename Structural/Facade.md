Facade
------

### Definition

Provide a unified interface to a set of interfaces in a subsystem. Façade defines a higher-level interface that makes the subsystem easier to use.

Frequency of use:

![](https://www.dofactory.com/images/patterns/use_high.jpg)

High

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/facade.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Facade **  **(MortgageApplication)**
    -   knows which subsystem classes are responsible for a request.
    -   delegates client requests to appropriate subsystem objects.
-   **Subsystem classes **  **(Bank, Credit, Loan)**
    -   implement subsystem functionality.
    -   handle work assigned by the Facade object.
    -   have no knowledge of the facade and keep no reference to it.

* * * * *

### Structural code in `C#`

This structural code demonstrates the Facade pattern which provides a simplified and uniform interface to a large subsystem of classes.

    using System;
    
    namespace DoFactory.GangOfFour.Facade.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural
        /// Facade Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            public static void Main()
            {
                Facade facade = new Facade();
    
                facade.MethodA();
                facade.MethodB();
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Subsystem ClassA' class
        /// </summary>
        class SubSystemOne
        {
            public void MethodOne()
            {
                Console.WriteLine(" SubSystemOne Method");
            }
        }
    
        /// <summary>
        /// The 'Subsystem ClassB' class
        /// </summary>
        class SubSystemTwo
        {
            public void MethodTwo()
            {
                Console.WriteLine(" SubSystemTwo Method");
            }
        }
    
        /// <summary>
        /// The 'Subsystem ClassC' class
        /// </summary>
        class SubSystemThree
        {
            public void MethodThree()
            {
                Console.WriteLine(" SubSystemThree Method");
            }
        }
    
        /// <summary>
        /// The 'Subsystem ClassD' class
        /// </summary>
        class SubSystemFour
        {
            public void MethodFour()
            {
                Console.WriteLine(" SubSystemFour Method");
            }
        }
    
        /// <summary>
        /// The 'Facade' class
        /// </summary>
        class Facade
        {
            private SubSystemOne _one;
            private SubSystemTwo _two;
            private SubSystemThree _three;
            private SubSystemFour _four;
    
            public Facade()
            {
                _one = new SubSystemOne();
                _two = new SubSystemTwo();
                _three = new SubSystemThree();
                _four = new SubSystemFour();
            }
    
            public void MethodA()
            {
                Console.WriteLine("\nMethodA() ---- ");
                _one.MethodOne();
                _two.MethodTwo();
                _four.MethodFour();
            }
    
            public void MethodB()
            {
                Console.WriteLine("\nMethodB() ---- ");
                _two.MethodTwo();
                _three.MethodThree();
            }
        }
    }

##### Output

    MethodA() ----\
    SubSystemOne Method\
    SubSystemTwo Method\
    SubSystemFour Method
    
    MethodB() ----\
    SubSystemTwo Method\
    SubSystemThree Method