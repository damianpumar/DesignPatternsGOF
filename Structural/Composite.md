Composite
------

### Definition

Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.

Frequency of use:

![](https://www.dofactory.com/images/patterns/use_medium_high.jpg)

Medium high

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/composite.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Component **  **(DrawingElement)**
    -   declares the interface for objects in the composition.
    -   implements default behavior for the interface common to all classes, as appropriate.
    -   declares an interface for accessing and managing its child components.
    -   (optional) defines an interface for accessing a component's parent in the recursive structure, and implements it if that's appropriate.
-   **Leaf **  **(PrimitiveElement)**
    -   represents leaf objects in the composition. A leaf has no children.
    -   defines behavior for primitive objects in the composition.
-   **Composite **  **(CompositeElement)**
    -   defines behavior for components having children.
    -   stores child components.
    -   implements child-related operations in the Component interface.
-   **Client**  **(CompositeApp)**
    -   manipulates objects in the composition through the Component interface.

* * * * *

### Structural code in `C#`

This structural code demonstrates the Composite pattern which allows the creation of a tree structure in which individual nodes are accessed uniformly whether they are leaf nodes or branch (composite) nodes.

    using System;
    using System.Collections.Generic;
    
    namespace DoFactory.GangOfFour.Composite.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural 
        /// Composite Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                // Create a tree structure
                Composite root = new Composite("root");
                root.Add(new Leaf("Leaf A"));
                root.Add(new Leaf("Leaf B"));
    
                Composite comp = new Composite("Composite X");
                comp.Add(new Leaf("Leaf XA"));
                comp.Add(new Leaf("Leaf XB"));
    
                root.Add(comp);
                root.Add(new Leaf("Leaf C"));
    
                // Add and remove a leaf
                Leaf leaf = new Leaf("Leaf D");
                root.Add(leaf);
                root.Remove(leaf);
    
                // Recursively display tree
                root.Display(1);
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Component' abstract class
        /// </summary>
        abstract class Component
        {
            protected string name;
    
            // Constructor
            public Component(string name)
            {
                this.name = name;
            }
    
            public abstract void Add(Component c);
            public abstract void Remove(Component c);
            public abstract void Display(int depth);
        }
    
        /// <summary>
        /// The 'Composite' class
        /// </summary>
        class Composite : Component
        {
            private List<Component> _children = new List<Component>();
    
            // Constructor
            public Composite(string name)
                : base(name)
            {
            }
    
            public override void Add(Component component)
            {
                _children.Add(component);
            }
    
            public override void Remove(Component component)
            {
                _children.Remove(component);
            }
    
            public override void Display(int depth)
            {
                Console.WriteLine(new String('-', depth) + name);
    
                // Recursively display child nodes
                foreach (Component component in _children)
                {
                    component.Display(depth + 2);
                }
            }
        }
    
        /// <summary>
        /// The 'Leaf' class
        /// </summary>
        class Leaf : Component
        {
            // Constructor
            public Leaf(string name)
                : base(name)
            {
            }
    
            public override void Add(Component c)
            {
                Console.WriteLine("Cannot add to a leaf");
            }
    
            public override void Remove(Component c)
            {
                Console.WriteLine("Cannot remove from a leaf");
            }
    
            public override void Display(int depth)
            {
                Console.WriteLine(new String('-', depth) + name);
            }
        }
    }

##### Output

    -root\
    ---Leaf A\
    ---Leaf B\
    ---Composite X\
    -----Leaf XA\
    -----Leaf XB\
    ---Leaf C