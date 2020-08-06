Proxy
------

### Definition

Provide a surrogate or placeholder for another object to control access to it.

Frequency of use:

![](https://www.dofactory.com/images/patterns/use_medium_high.jpg)

Medium high

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/proxy.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Proxy **  **(MathProxy)**
    -   maintains a reference that lets the proxy access the real subject. Proxy may refer to a Subject if the RealSubject and Subject interfaces are the same.
    -   provides an interface identical to Subject's so that a proxy can be substituted for for the real subject.
    -   controls access to the real subject and may be responsible for creating and deleting it.
    -   other responsibilites depend on the kind of proxy:
        -   *remote proxies* are responsible for encoding a request and its arguments and for sending the encoded request to the real subject in a different address space.
        -   *virtual proxies* may cache additional information about the real subject so that they can postpone accessing it. For example, the ImageProxy from the Motivation caches the real images's extent.
        -   *protection proxies* check that the caller has the access permissions required to perform a request.
-   **Subject **  **(IMath)**
    -   defines the common interface for RealSubject and Proxy so that a Proxy can be used anywhere a RealSubject is expected.
-   **RealSubject **  **(Math)**
    -   defines the real object that the proxy represents.

* * * * *

### Structural code in `C#`

This structural code demonstrates the Proxy pattern which provides a representative object (proxy) that controls access to another similar object.

    using System;
    
    namespace DoFactory.GangOfFour.Proxy.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural
        /// Proxy Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                // Create proxy and request a service
                Proxy proxy = new Proxy();
                proxy.Request();
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Subject' abstract class
        /// </summary>
        abstract class Subject
        {
            public abstract void Request();
        }
    
        /// <summary>
        /// The 'RealSubject' class
        /// </summary>
        class RealSubject : Subject
        {
            public override void Request()
            {
                Console.WriteLine("Called RealSubject.Request()");
            }
        }
    
        /// <summary>
        /// The 'Proxy' class
        /// </summary>
        class Proxy : Subject
        {
            private RealSubject _realSubject;
    
            public override void Request()
            {
                // Use 'lazy initialization'
                if (_realSubject == null)
                {
                    _realSubject = new RealSubject();
                }
    
                _realSubject.Request();
            }
        }
    }

##### Output

    Called RealSubject.Request()