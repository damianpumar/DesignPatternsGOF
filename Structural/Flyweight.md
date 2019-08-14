### Definition

Use sharing to support large numbers of fine-grained objects efficiently.

Frequency of use:

![](https://www.dofactory.com/images/use_low.gif)

Low

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/flyweight.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Flyweight **  **(Character)**
    -   declares an interface through which flyweights can receive and act on extrinsic state.
-   **ConcreteFlyweight **  **(CharacterA, CharacterB, ..., CharacterZ)**
    -   implements the Flyweight interface and adds storage for intrinsic state, if any. A ConcreteFlyweight object must be sharable. Any state it stores must be intrinsic, that is, it must be independent of the ConcreteFlyweight object's context.
-   **UnsharedConcreteFlyweight **  **( not used )**
    -   not all Flyweight subclasses need to be shared. The Flyweight interface *enables* sharing, but it doesn't enforce it. It is common for UnsharedConcreteFlyweight objects to have ConcreteFlyweight objects as children at some level in the flyweight object structure (as the Row and Column classes have).
-   **FlyweightFactory **  **(CharacterFactory)**
    -   creates and manages flyweight objects
    -   ensures that flyweight are shared properly. When a client requests a flyweight, the FlyweightFactory objects assets an existing instance or creates one, if none exists.
-   **Client **  **(FlyweightApp)**
    -   maintains a reference to flyweight(s).
    -   computes or stores the extrinsic state of flyweight(s).

* * * * *

### Structural code in `C#`

This structural code demonstrates the Flyweight pattern in which a relatively small number of objects is shared many times by different clients.

    using System;
    using System.Collections;
    
    namespace DoFactory.GangOfFour.Flyweight.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural 
        /// Flyweight Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                // Arbitrary extrinsic state
                int extrinsicstate = 22;
    
                FlyweightFactory factory = new FlyweightFactory();
    
                // Work with different flyweight instances
                Flyweight fx = factory.GetFlyweight("X");
                fx.Operation(--extrinsicstate);
    
                Flyweight fy = factory.GetFlyweight("Y");
                fy.Operation(--extrinsicstate);
    
                Flyweight fz = factory.GetFlyweight("Z");
                fz.Operation(--extrinsicstate);
    
                UnsharedConcreteFlyweight fu = new
                    UnsharedConcreteFlyweight();
    
                fu.Operation(--extrinsicstate);
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'FlyweightFactory' class
        /// </summary>
        class FlyweightFactory
        {
            private Hashtable flyweights = new Hashtable();
    
            // Constructor
            public FlyweightFactory()
            {
                flyweights.Add("X", new ConcreteFlyweight());
                flyweights.Add("Y", new ConcreteFlyweight());
                flyweights.Add("Z", new ConcreteFlyweight());
            }
    
            public Flyweight GetFlyweight(string key)
            {
                return ((Flyweight)flyweights[key]);
            }
        }
    
        /// <summary>
        /// The 'Flyweight' abstract class
        /// </summary>
        abstract class Flyweight
        {
            public abstract void Operation(int extrinsicstate);
        }
    
        /// <summary>
        /// The 'ConcreteFlyweight' class
        /// </summary>
        class ConcreteFlyweight : Flyweight
        {
            public override void Operation(int extrinsicstate)
            {
                Console.WriteLine("ConcreteFlyweight: " + extrinsicstate);
            }
        }
    
        /// <summary>
        /// The 'UnsharedConcreteFlyweight' class
        /// </summary>
        class UnsharedConcreteFlyweight : Flyweight
        {
            public override void Operation(int extrinsicstate)
            {
                Console.WriteLine("UnsharedConcreteFlyweight: " +
                    extrinsicstate);
            }
        }
    }

##### Output

    ConcreteFlyweight: 21\
    ConcreteFlyweight: 20\
    ConcreteFlyweight: 19\
    UnsharedConcreteFlyweight: 18