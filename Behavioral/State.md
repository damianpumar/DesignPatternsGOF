State
------

### Definition

Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.

Frequency of use:

![](https://www.dofactory.com/images/patterns/use_medium.jpg)

Medium

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/state.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Context**  **(Account)**
    -   defines the interface of interest to clients
    -   maintains an instance of a ConcreteState subclass that defines the current state.
-   **State**  **(State)**
    -   defines an interface for encapsulating the behavior associated with a particular state of the Context.
-   **Concrete State**  **(RedState, SilverState, GoldState)**
    -   each subclass implements a behavior associated with a state of Context

* * * * *

### Structural code in `C#`

This structural code demonstrates the State pattern which allows an object to behave differently depending on its internal state. The difference in behavior is delegated to objects that represent this state.

    using System;
    
    namespace DoFactory.GangOfFour.State.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural
        /// State Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                // Setup context in a state
                Context c = new Context(new ConcreteStateA());
    
                // Issue requests, which toggles state
                c.Request();
                c.Request();
                c.Request();
                c.Request();
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'State' abstract class
        /// </summary>
        abstract class State
        {
            public abstract void Handle(Context context);
        }
    
        /// <summary>
        /// A 'ConcreteState' class
        /// </summary>
        class ConcreteStateA : State
        {
            public override void Handle(Context context)
            {
                context.State = new ConcreteStateB();
            }
        }
    
        /// <summary>
        /// A 'ConcreteState' class
        /// </summary>
        class ConcreteStateB : State
        {
            public override void Handle(Context context)
            {
                context.State = new ConcreteStateA();
            }
        }
    
        /// <summary>
        /// The 'Context' class
        /// </summary>
        class Context
        {
            private State _state;
    
            // Constructor
            public Context(State state)
            {
                this.State = state;
            }
    
            // Gets or sets the state
            public State State
            {
                get { return _state; }
                set
                {
                    _state = value;
                    Console.WriteLine("State: " +
                        _state.GetType().Name);
                }
            }
    
            public void Request()
            {
                _state.Handle(this);
            }
        }
    }

##### Output

    State: ConcreteStateA\
    State: ConcreteStateB\
    State: ConcreteStateA\
    State: ConcreteStateB\
    State: ConcreteStateA