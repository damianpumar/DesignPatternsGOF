Factory Method
------

### Definition

Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

Frequency of use:

![](https://www.dofactory.com/images/use_high.gif)

High

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/factory.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Product**  **(Page)**
    -   defines the interface of objects the factory method creates
-   **ConcreteProduct**  **(SkillsPage, EducationPage, ExperiencePage)**
    -   implements the Product interface
-   **Creator**  **(Document)**
    -   declares the factory method, which returns an object of type Product. Creator may also define a default implementation of the factory method that returns a default ConcreteProduct object.
    -   may call the factory method to create a Product object.
-   **ConcreteCreator**  **(Report, Resume)**
    -   overrides the factory method to return an instance of a ConcreteProduct.

* * * * *

### Structural code in C#

This structural code demonstrates the Factory method offering great flexibility in creating different objects. The Abstract class may provide a default object, but each subclass can instantiate an extended version of the object.

      using System;

      namespace DoFactory.GangOfFour.Factory.Structural
      {
          /// <summary>
          /// MainApp startup class for Structural 
          /// Factory Method Design Pattern.
          /// </summary>
          class MainApp
          {
          /// <summary>
          /// Entry point into console application.
          /// </summary>
          static void Main()
          {
              // An array of creators
              Creator[] creators = new Creator[2];

              creators[0] = new ConcreteCreatorA();
              creators[1] = new ConcreteCreatorB();

              // Iterate over creators and create products
              foreach (Creator creator in creators)
              {
                  Product product = creator.FactoryMethod();
                  Console.WriteLine("Created {0}",
                      product.GetType().Name);
              }

              // Wait for user
              Console.ReadKey();
          }
      }

      /// <summary>
      /// The 'Product' abstract class
      /// </summary>
      abstract class Product
      {
      }

      /// <summary>
      /// A 'ConcreteProduct' class
      /// </summary>
      class ConcreteProductA : Product
      {
      }

      /// <summary>
      /// A 'ConcreteProduct' class
      /// </summary>
      class ConcreteProductB : Product
      {
      }

      /// <summary>
      /// The 'Creator' abstract class
      /// </summary>
      abstract class Creator
      {
          public abstract Product FactoryMethod();
      }

      /// <summary>
      /// A 'ConcreteCreator' class
      /// </summary>
      class ConcreteCreatorA : Creator
      {
          public override Product FactoryMethod()
          {
              return new ConcreteProductA();
          }
      }

      /// <summary>
      /// A 'ConcreteCreator' class
      /// </summary>
      class ConcreteCreatorB : Creator
      {
          public override Product FactoryMethod()
          {
              return new ConcreteProductB();
          }
      }
  }

##### Output

  Created ConcreteProductA\
  Created ConcreteProductB
