Mediator
------

### Definition

Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.

Frequency of use:

![](https://www.dofactory.com/images/use_medium_low.gif)

Medium low

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/mediator.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Mediator**  **(IChatroom)**
    -   defines an interface for communicating with Colleague objects
-   **ConcreteMediator**  **(Chatroom)**
    -   implements cooperative behavior by coordinating Colleague objects
    -   knows and maintains its colleagues
-   **Colleague classes**  **(Participant)**
    -   each Colleague class knows its Mediator object
    -   each colleague communicates with its mediator whenever it would have otherwise communicated with another colleague

* * * * *

### Structural code in `C#`

This structural code demonstrates the Mediator pattern facilitating loosely coupled communication between different objects and object types. The mediator is a central hub through which all interaction must take place.

    using System;
    
    namespace DoFactory.GangOfFour.Mediator.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural 
        /// Mediator Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                ConcreteMediator m = new ConcreteMediator();
    
                ConcreteColleague1 c1 = new ConcreteColleague1(m);
                ConcreteColleague2 c2 = new ConcreteColleague2(m);
    
                m.Colleague1 = c1;
                m.Colleague2 = c2;
    
                c1.Send("How are you?");
                c2.Send("Fine, thanks");
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Mediator' abstract class
        /// </summary>
        abstract class Mediator
        {
            public abstract void Send(string message,
                Colleague colleague);
        }
    
        /// <summary>
        /// The 'ConcreteMediator' class
        /// </summary>
        class ConcreteMediator : Mediator
        {
            private ConcreteColleague1 _colleague1;
            private ConcreteColleague2 _colleague2;
    
            public ConcreteColleague1 Colleague1
            {
                set { _colleague1 = value; }
            }
    
            public ConcreteColleague2 Colleague2
            {
                set { _colleague2 = value; }
            }
    
            public override void Send(string message,
                Colleague colleague)
            {
                if (colleague == _colleague1)
                {
                    _colleague2.Notify(message);
                }
                else
                {
                    _colleague1.Notify(message);
                }
            }
        }
    
        /// <summary>
        /// The 'Colleague' abstract class
        /// </summary>
        abstract class Colleague
        {
            protected Mediator mediator;
    
            // Constructor
            public Colleague(Mediator mediator)
            {
                this.mediator = mediator;
            }
        }
    
        /// <summary>
        /// A 'ConcreteColleague' class
        /// </summary>
        class ConcreteColleague1 : Colleague
        {
            // Constructor
            public ConcreteColleague1(Mediator mediator)
                : base(mediator)
            {
            }
    
            public void Send(string message)
            {
                mediator.Send(message, this);
            }
    
            public void Notify(string message)
            {
                Console.WriteLine("Colleague1 gets message: "
                    + message);
            }
        }
    
        /// <summary>
        /// A 'ConcreteColleague' class
        /// </summary>
        class ConcreteColleague2 : Colleague
        {
            // Constructor
            public ConcreteColleague2(Mediator mediator)
                : base(mediator)
            {
            }
    
            public void Send(string message)
            {
                mediator.Send(message, this);
            }
    
            public void Notify(string message)
            {
                Console.WriteLine("Colleague2 gets message: "
                    + message);
            }
        }
    }

##### Output

    Colleague2 gets message: How are you?
    Colleague1 gets message: Fine, thanks