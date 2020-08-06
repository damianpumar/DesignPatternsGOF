Strategy
------

### Definition

Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm vary independently from clients that use it.

Frequency of use:

![](https://www.dofactory.com/images/patterns/use_medium_high.jpg)

Medium high

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/strategy.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Strategy**  **(SortStrategy)**
    -   declares an interface common to all supported algorithms. Context uses this interface to call the algorithm defined by a ConcreteStrategy
-   **ConcreteStrategy**  **(QuickSort, ShellSort, MergeSort)**
    -   implements the algorithm using the Strategy interface
-   **Context**  **(SortedList)**
    -   is configured with a ConcreteStrategy object
    -   maintains a reference to a Strategy object
    -   may define an interface that lets Strategy access its data.

* * * * *

### Structural code in `C#`

This structural code demonstrates the Strategy pattern which encapsulates functionality in the form of an object. This allows clients to dynamically change algorithmic strategies.

    using System;
    
    namespace DoFactory.GangOfFour.Strategy.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural
        /// Strategy Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                Context context;
    
                // Three contexts following different strategies
                context = new Context(new ConcreteStrategyA());
                context.ContextInterface();
    
                context = new Context(new ConcreteStrategyB());
                context.ContextInterface();
    
                context = new Context(new ConcreteStrategyC());
                context.ContextInterface();
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Strategy' abstract class
        /// </summary>
        abstract class Strategy
        {
            public abstract void AlgorithmInterface();
        }
    
        /// <summary>
        /// A 'ConcreteStrategy' class
        /// </summary>
        class ConcreteStrategyA : Strategy
        {
            public override void AlgorithmInterface()
            {
                Console.WriteLine(
                    "Called ConcreteStrategyA.AlgorithmInterface()");
            }
        }
    
        /// <summary>
        /// A 'ConcreteStrategy' class
        /// </summary>
        class ConcreteStrategyB : Strategy
        {
            public override void AlgorithmInterface()
            {
                Console.WriteLine(
                    "Called ConcreteStrategyB.AlgorithmInterface()");
            }
        }
    
        /// <summary>
        /// A 'ConcreteStrategy' class
        /// </summary>
        class ConcreteStrategyC : Strategy
        {
            public override void AlgorithmInterface()
            {
                Console.WriteLine(
                    "Called ConcreteStrategyC.AlgorithmInterface()");
            }
        }
    
        /// <summary>
        /// The 'Context' class
        /// </summary>
        class Context
        {
            private Strategy _strategy;
    
            // Constructor
            public Context(Strategy strategy)
            {
                this._strategy = strategy;
            }
    
            public void ContextInterface()
            {
                _strategy.AlgorithmInterface();
            }
        }
    }

##### Output

    Called ConcreteStrategyA.AlgorithmInterface()\
    Called ConcreteStrategyB.AlgorithmInterface()\
    Called ConcreteStrategyC.AlgorithmInterface()