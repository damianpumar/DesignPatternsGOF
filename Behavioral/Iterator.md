### Definition

Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

Frequency of use:

![](https://www.dofactory.com/images/use_high.gif)

High

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/iterator.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Iterator**  **(AbstractIterator)**
    -   defines an interface for accessing and traversing elements.
-   **ConcreteIterator**  **(Iterator)**
    -   implements the Iterator interface.
    -   keeps track of the current position in the traversal of the aggregate.
-   **Aggregate**  **(AbstractCollection)**
    -   defines an interface for creating an Iterator object
-   **ConcreteAggregate**  **(Collection)**
    -   implements the Iterator creation interface to return an instance of the proper ConcreteIterator

* * * * *

### Structural code in `C#`

This structural code demonstrates the Iterator pattern which provides for a way to traverse (iterate) over a collection of items without detailing the underlying structure of the collection.

    using System;
    using System.Collections;
    
    namespace DoFactory.GangOfFour.Iterator.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural 
        /// Iterator Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                ConcreteAggregate a = new ConcreteAggregate();
                a[0] = "Item A";
                a[1] = "Item B";
                a[2] = "Item C";
                a[3] = "Item D";
    
                // Create Iterator and provide aggregate
                ConcreteIterator i = new ConcreteIterator(a);
    
                Console.WriteLine("Iterating over collection:");
    
                object item = i.First();
                while (item != null)
                {
                    Console.WriteLine(item);
                    item = i.Next();
                }
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Aggregate' abstract class
        /// </summary>
        abstract class Aggregate
        {
            public abstract Iterator CreateIterator();
        }
    
        /// <summary>
        /// The 'ConcreteAggregate' class
        /// </summary>
        class ConcreteAggregate : Aggregate
        {
            private ArrayList _items = new ArrayList();
    
            public override Iterator CreateIterator()
            {
                return new ConcreteIterator(this);
            }
    
            // Gets item count
            public int Count
            {
                get { return _items.Count; }
            }
    
            // Indexer
            public object this[int index]
            {
                get { return _items[index]; }
                set { _items.Insert(index, value); }
            }
        }
    
        /// <summary>
        /// The 'Iterator' abstract class
        /// </summary>
        abstract class Iterator
        {
            public abstract object First();
            public abstract object Next();
            public abstract bool IsDone();
            public abstract object CurrentItem();
        }
    
        /// <summary>
        /// The 'ConcreteIterator' class
        /// </summary>
        class ConcreteIterator : Iterator
        {
            private ConcreteAggregate _aggregate;
            private int _current = 0;
    
            // Constructor
            public ConcreteIterator(ConcreteAggregate aggregate)
            {
                this._aggregate = aggregate;
            }
    
            // Gets first iteration item
            public override object First()
            {
                return _aggregate[0];
            }
    
            // Gets next iteration item
            public override object Next()
            {
                object ret = null;
                if (_current < _aggregate.Count - 1)
                {
                    ret = _aggregate[++_current];
                }
    
                return ret;
            }
    
            // Gets current iteration item
            public override object CurrentItem()
            {
                return _aggregate[_current];
            }
    
            // Gets whether iterations are complete
            public override bool IsDone()
            {
                return _current >= _aggregate.Count;
            }
        }
    }

##### Output

    Iterating over collection:\
    Item A\
    Item B\
    Item C\
    Item D