Observer
------

### Definition

Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

Frequency of use:

![](https://www.dofactory.com/images/use_high.gif)

High

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/observer.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Subject**  **(Stock)**
    -   knows its observers. Any number of Observer objects may observe a subject
    -   provides an interface for attaching and detaching Observer objects.
-   **ConcreteSubject**  **(IBM)**
    -   stores state of interest to ConcreteObserver
    -   sends a notification to its observers when its state changes
-   **Observer**  **(IInvestor)**
    -   defines an updating interface for objects that should be notified of changes in a subject.
-   **ConcreteObserver**  **(Investor)**
    -   maintains a reference to a ConcreteSubject object
    -   stores state that should stay consistent with the subject's
    -   implements the Observer updating interface to keep its state consistent with the subject's

* * * * *

### Structural code in `C#`

This structural code demonstrates the Observer pattern in which registered objects are notified of and updated with a state change.

    using System;
    using System.Collections.Generic;
    
    namespace DoFactory.GangOfFour.Observer.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural 
        /// Observer Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                // Configure Observer pattern
                ConcreteSubject s = new ConcreteSubject();
    
                s.Attach(new ConcreteObserver(s, "X"));
                s.Attach(new ConcreteObserver(s, "Y"));
                s.Attach(new ConcreteObserver(s, "Z"));
    
                // Change subject and notify observers
                s.SubjectState = "ABC";
                s.Notify();
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Subject' abstract class
        /// </summary>
        abstract class Subject
        {
            private List<Observer> _observers = new List<Observer>();
    
            public void Attach(Observer observer)
            {
                _observers.Add(observer);
            }
    
            public void Detach(Observer observer)
            {
                _observers.Remove(observer);
            }
    
            public void Notify()
            {
                foreach (Observer o in _observers)
                {
                    o.Update();
                }
            }
        }
    
        /// <summary>
        /// The 'ConcreteSubject' class
        /// </summary>
        class ConcreteSubject : Subject
        {
            private string _subjectState;
    
            // Gets or sets subject state
            public string SubjectState
            {
                get { return _subjectState; }
                set { _subjectState = value; }
            }
        }
    
        /// <summary>
        /// The 'Observer' abstract class
        /// </summary>
        abstract class Observer
        {
            public abstract void Update();
        }
    
        /// <summary>
        /// The 'ConcreteObserver' class
        /// </summary>
        class ConcreteObserver : Observer
        {
            private string _name;
            private string _observerState;
            private ConcreteSubject _subject;
    
            // Constructor
            public ConcreteObserver(
                ConcreteSubject subject, string name)
            {
                this._subject = subject;
                this._name = name;
            }
    
            public override void Update()
            {
                _observerState = _subject.SubjectState;
                Console.WriteLine("Observer {0}'s new state is {1}",
                    _name, _observerState);
            }
    
            // Gets or sets subject
            public ConcreteSubject Subject
            {
                get { return _subject; }
                set { _subject = value; }
            }
        }
    }

##### Output

    Observer X's new state is ABC\
    Observer Y's new state is ABC\
    Observer Z's new state is ABC