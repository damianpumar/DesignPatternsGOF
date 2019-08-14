### Definition

Without violating encapsulation, capture and externalize an object's internal state so that the object can be restored to this state later.

Frequency of use:

![](https://www.dofactory.com/images/use_low.gif)

Low

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/memento.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Memento**  **(Memento)**
    -   stores internal state of the Originator object. The memento may store as much or as little of the originator's internal state as necessary at its originator's discretion.
    -   protect against access by objects of other than the originator. Mementos have effectively two interfaces. Caretaker sees a narrow interface to the Memento -- it can only pass the memento to the other objects. Originator, in contrast, sees a wide interface, one that lets it access all the data necessary to restore itself to its previous state. Ideally, only the originator that produces the memento would be permitted to access the memento's internal state.
-   **Originator**  **(SalesProspect)**
    -   creates a memento containing a snapshot of its current internal state.
    -   uses the memento to restore its internal state
-   **Caretaker**  **(Caretaker)**
    -   is responsible for the memento's safekeeping
    -   never operates on or examines the contents of a memento.

* * * * *

### Structural code in `C#`

This structural code demonstrates the Memento pattern which temporary saves and restores another object's internal state.

    using System;
    
    namespace DoFactory.GangOfFour.Memento.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural 
        /// Memento Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                Originator o = new Originator();
                o.State = "On";
    
                // Store internal state
                Caretaker c = new Caretaker();
                c.Memento = o.CreateMemento();
    
                // Continue changing originator
                o.State = "Off";
    
                // Restore saved state
                o.SetMemento(c.Memento);
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Originator' class
        /// </summary>
        class Originator
        {
            private string _state;
    
            // Property
            public string State
            {
                get { return _state; }
                set
                {
                    _state = value;
                    Console.WriteLine("State = " + _state);
                }
            }
    
            // Creates memento 
            public Memento CreateMemento()
            {
                return (new Memento(_state));
            }
    
            // Restores original state
            public void SetMemento(Memento memento)
            {
                Console.WriteLine("Restoring state...");
                State = memento.State;
            }
        }
    
        /// <summary>
        /// The 'Memento' class
        /// </summary>
        class Memento
        {
            private string _state;
    
            // Constructor
            public Memento(string state)
            {
                this._state = state;
            }
    
            // Gets or sets state
            public string State
            {
                get { return _state; }
            }
        }
    
        /// <summary>
        /// The 'Caretaker' class
        /// </summary>
        class Caretaker
        {
            private Memento _memento;
    
            // Gets or sets memento
            public Memento Memento
            {
                set { _memento = value; }
                get { return _memento; }
            }
        }
    }

##### Output

    State = On\
    State = Off\
    Restoring state:\
    State = On