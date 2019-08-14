###\
Definition

Ensure a class has only one instance and provide a global point of access to it.

Frequency of use:

![](https://www.dofactory.com/images/use_medium_high.gif)

Medium high

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/singleton.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Singleton **  **(LoadBalancer)**
    -   defines an Instance operation that lets clients access its unique instance. Instance is a class operation.
    -   responsible for creating and maintaining its own unique instance.

* * * * *

### Structural code in C#

This structural code demonstrates the Singleton pattern which assures only a single instance (the singleton) of the class can be created.

	using System;

	namespace DoFactory.GangOfFour.Singleton.Structural
	{
	    /// <summary>
	    /// MainApp startup class for Structural
	    /// Singleton Design Pattern.
	    /// </summary>
	    class MainApp
	    {
	        /// <summary>
	        /// Entry point into console application.
	        /// </summary>
	        static void Main()
	        {
	            // Constructor is protected -- cannot use new
	            Singleton s1 = Singleton.Instance();
	            Singleton s2 = Singleton.Instance();

	            // Test for same instance
	            if (s1 == s2)
	            {
	                Console.WriteLine("Objects are the same instance");
	            }

	            // Wait for user
	            Console.ReadKey();
	        }
	    }

	    /// <summary>
	    /// The 'Singleton' class
	    /// </summary>
	    class Singleton
	    {
	        private static Singleton _instance;

	        // Constructor is 'protected'
	        protected Singleton()
	        {
	        }

	        public static Singleton Instance()
	        {
	            // Uses lazy initialization.
	            // Note: this is not thread safe.
	            if (_instance == null)
	            {
	                _instance = new Singleton();
	            }

	            return _instance;
	        }
	    }
	}

##### Output

	Objects are the same instance