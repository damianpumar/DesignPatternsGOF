Chain of Responsibility
------

### Definition

Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.

Frequency of use:

![](https://www.dofactory.com/images/use_medium_low.gif)

Medium low

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/chain.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Handler **  **(Approver)**
    -   defines an interface for handling the requests
    -   (optional) implements the successor link
-   **ConcreteHandler **  **(Director, VicePresident, President)**
    -   handles requests it is responsible for
    -   can access its successor
    -   if the ConcreteHandler can handle the request, it does so; otherwise it forwards the request to its successor
-   **Client **  **(ChainApp)**
    -   initiates the request to a ConcreteHandler object on the chain

* * * * *

### Structural code in `C#`

This structural code demonstrates the Chain of Responsibility pattern in which several linked objects (the Chain) are offered the opportunity to respond to a request or hand it off to the object next in line.

    using System;
    
    namespace DoFactory.GangOfFour.Chain.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural
        /// Chain of Responsibility Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                // Setup Chain of Responsibility
                Handler h1 = new ConcreteHandler1();
                Handler h2 = new ConcreteHandler2();
                Handler h3 = new ConcreteHandler3();
                h1.SetSuccessor(h2);
                h2.SetSuccessor(h3);
    
                // Generate and process request
                int[] requests = { 2, 5, 14, 22, 18, 3, 27, 20 };
    
                foreach (int request in requests)
                {
                    h1.HandleRequest(request);
                }
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Handler' abstract class
        /// </summary>
        abstract class Handler
        {
            protected Handler successor;
    
            public void SetSuccessor(Handler successor)
            {
                this.successor = successor;
            }
    
            public abstract void HandleRequest(int request);
        }
    
        /// <summary>
        /// The 'ConcreteHandler1' class
        /// </summary>
        class ConcreteHandler1 : Handler
        {
            public override void HandleRequest(int request)
            {
                if (request >= 0 && request < 10)
                {
                    Console.WriteLine("{0} handled request {1}",
                        this.GetType().Name, request);
                }
                else if (successor != null)
                {
                    successor.HandleRequest(request);
                }
            }
        }
    
        /// <summary>
        /// The 'ConcreteHandler2' class
        /// </summary>
        class ConcreteHandler2 : Handler
        {
            public override void HandleRequest(int request)
            {
                if (request >= 10 && request < 20)
                {
                    Console.WriteLine("{0} handled request {1}",
                        this.GetType().Name, request);
                }
                else if (successor != null)
                {
                    successor.HandleRequest(request);
                }
            }
        }
    
        /// <summary>
        /// The 'ConcreteHandler3' class
        /// </summary>
        class ConcreteHandler3 : Handler
        {
            public override void HandleRequest(int request)
            {
                if (request >= 20 && request < 30)
                {
                    Console.WriteLine("{0} handled request {1}",
                        this.GetType().Name, request);
                }
                else if (successor != null)
                {
                    successor.HandleRequest(request);
                }
            }
        }
    }

##### Output

    ConcreteHandler1 handled request 2\
    ConcreteHandler1 handled request 5\
    ConcreteHandler2 handled request 14\
    ConcreteHandler3 handled request 22\
    ConcreteHandler2 handled request 18\
    ConcreteHandler1 handled request 3\
    ConcreteHandler3 handled request 27\
    ConcreteHandler3 handled request 20