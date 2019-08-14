### Definition

Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.

Frequency of use:

![](https://www.dofactory.com/images/use_medium_high.gif)

Medium high

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/adapter.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Target **  **(ChemicalCompound)**
    -   defines the domain-specific interface that Client uses.
-   **Adapter **  **(Compound)**
    -   adapts the interface Adaptee to the Target interface.
-   **Adaptee **  **(ChemicalDatabank)**
    -   defines an existing interface that needs adapting.
-   **Client **  **(AdapterApp)**
    -   collaborates with objects conforming to the Target interface.

* * * * *

### Structural code in `C#`

This structural code demonstrates the Adapter pattern which maps the interface of one class onto another so that they can work together. These incompatible classes may come from different libraries or frameworks.

    using System;
    
    namespace DoFactory.GangOfFour.Adapter.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural
        /// Adapter Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                // Create adapter and place a request
                Target target = new Adapter();
                target.Request();
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Target' class
        /// </summary>
        class Target
        {
            public virtual void Request()
            {
                Console.WriteLine("Called Target Request()");
            }
        }
    
        /// <summary>
        /// The 'Adapter' class
        /// </summary>
        class Adapter : Target
        {
            private Adaptee _adaptee = new Adaptee();
    
            public override void Request()
            {
                // Possibly do some other work
                //   and then call SpecificRequest
                _adaptee.SpecificRequest();
            }
        }
    
        /// <summary>
        /// The 'Adaptee' class
        /// </summary>
        class Adaptee
        {
            public void SpecificRequest()
            {
                Console.WriteLine("Called SpecificRequest()");
            }
        }
    }

##### Output

    Called SpecificRequest()