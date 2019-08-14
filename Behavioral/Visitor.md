### Definition

Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.

Frequency of use:

![](https://www.dofactory.com/images/use_low.gif)

Low

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/visitor.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Visitor**  **(Visitor)**
    -   declares a Visit operation for each class of ConcreteElement in the object structure. The operation's name and signature identifies the class that sends the Visit request to the visitor. That lets the visitor determine the concrete class of the element being visited. Then the visitor can access the elements directly through its particular interface
-   **ConcreteVisitor**  **(IncomeVisitor, VacationVisitor)**
    -   implements each operation declared by Visitor. Each operation implements a fragment of the algorithm defined for the corresponding class or object in the structure. ConcreteVisitor provides the context for the algorithm and stores its local state. This state often accumulates results during the traversal of the structure.
-   **Element**  **(Element)**
    -   defines an Accept operation that takes a visitor as an argument.
-   **ConcreteElement**  **(Employee)**
    -   implements an Accept operation that takes a visitor as an argument
-   **ObjectStructure**  **(Employees)**
    -   can enumerate its elements
    -   may provide a high-level interface to allow the visitor to visit its elements
    -   may either be a Composite (pattern) or a collection such as a list or a set

* * * * *

### Structural code in `C#`

This structural code demonstrates the Visitor pattern in which an object traverses an object structure and performs the same operation on each node in this structure. Different visitor objects define different operations.

    using System;
    using System.Collections.Generic;
    
    namespace DoFactory.GangOfFour.Visitor.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural 
        /// Visitor Design Pattern.
        /// </summary>
        class MainApp
        {
            static void Main()
            {
                // Setup structure
                ObjectStructure o = new ObjectStructure();
                o.Attach(new ConcreteElementA());
                o.Attach(new ConcreteElementB());
    
                // Create visitor objects
                ConcreteVisitor1 v1 = new ConcreteVisitor1();
                ConcreteVisitor2 v2 = new ConcreteVisitor2();
    
                // Structure accepting visitors
                o.Accept(v1);
                o.Accept(v2);
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Visitor' abstract class
        /// </summary>
        abstract class Visitor
        {
            public abstract void VisitConcreteElementA(
                ConcreteElementA concreteElementA);
            public abstract void VisitConcreteElementB(
                ConcreteElementB concreteElementB);
        }
    
        /// <summary>
        /// A 'ConcreteVisitor' class
        /// </summary>
        class ConcreteVisitor1 : Visitor
        {
            public override void VisitConcreteElementA(
                ConcreteElementA concreteElementA)
            {
                Console.WriteLine("{0} visited by {1}",
                    concreteElementA.GetType().Name, this.GetType().Name);
            }
    
            public override void VisitConcreteElementB(
                ConcreteElementB concreteElementB)
            {
                Console.WriteLine("{0} visited by {1}",
                    concreteElementB.GetType().Name, this.GetType().Name);
            }
        }
    
        /// <summary>
        /// A 'ConcreteVisitor' class
        /// </summary>
        class ConcreteVisitor2 : Visitor
        {
            public override void VisitConcreteElementA(
                ConcreteElementA concreteElementA)
            {
                Console.WriteLine("{0} visited by {1}",
                    concreteElementA.GetType().Name, this.GetType().Name);
            }
    
            public override void VisitConcreteElementB(
                ConcreteElementB concreteElementB)
            {
                Console.WriteLine("{0} visited by {1}",
                    concreteElementB.GetType().Name, this.GetType().Name);
            }
        }
    
        /// <summary>
        /// The 'Element' abstract class
        /// </summary>
        abstract class Element
        {
            public abstract void Accept(Visitor visitor);
        }
    
        /// <summary>
        /// A 'ConcreteElement' class
        /// </summary>
        class ConcreteElementA : Element
        {
            public override void Accept(Visitor visitor)
            {
                visitor.VisitConcreteElementA(this);
            }
    
            public void OperationA()
            {
            }
        }
    
        /// <summary>
        /// A 'ConcreteElement' class
        /// </summary>
        class ConcreteElementB : Element
        {
            public override void Accept(Visitor visitor)
            {
                visitor.VisitConcreteElementB(this);
            }
    
            public void OperationB()
            {
            }
        }
    
        /// <summary>
        /// The 'ObjectStructure' class
        /// </summary>
        class ObjectStructure
        {
            private List<Element> _elements = new List<Element>();
    
            public void Attach(Element element)
            {
                _elements.Add(element);
            }
    
            public void Detach(Element element)
            {
                _elements.Remove(element);
            }
    
            public void Accept(Visitor visitor)
            {
                foreach (Element element in _elements)
                {
                    element.Accept(visitor);
                }
            }
        }
    }

##### Output

    ConcreteElementA visited by ConcreteVisitor1\
    ConcreteElementB visited by ConcreteVisitor1\
    ConcreteElementA visited by ConcreteVisitor2\
    ConcreteElementB visited by ConcreteVisitor2