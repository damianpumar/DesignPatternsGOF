Command
------

### Definition

Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

Frequency of use:

![](https://www.dofactory.com/images/patterns/use_medium_high.jpg)

Medium high

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/command.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **Command**  **(Command)**
    -   declares an interface for executing an operation
-   **ConcreteCommand**  **(CalculatorCommand)**
    -   defines a binding between a Receiver object and an action
    -   implements Execute by invoking the corresponding operation(s) on Receiver
-   **Client**  **(CommandApp)**
    -   creates a ConcreteCommand object and sets its receiver
-   **Invoker**  **(User)**
    -   asks the command to carry out the request
-   **Receiver**  **(Calculator)**
    -   knows how to perform the operations associated with carrying out the request.

* * * * *

### Structural code in `C#`

This structural code demonstrates the Command pattern which stores requests as objects allowing clients to execute or playback the requests.

    using System;
    
    namespace DoFactory.GangOfFour.Command.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural 
        /// Command Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                // Create receiver, command, and invoker
                Receiver receiver = new Receiver();
                Command command = new ConcreteCommand(receiver);
                Invoker invoker = new Invoker();
    
                // Set and execute command
                invoker.SetCommand(command);
                invoker.ExecuteCommand();
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Command' abstract class
        /// </summary>
        abstract class Command
        {
            protected Receiver receiver;
    
            // Constructor
            public Command(Receiver receiver)
            {
                this.receiver = receiver;
            }
    
            public abstract void Execute();
        }
    
        /// <summary>
        /// The 'ConcreteCommand' class
        /// </summary>
        class ConcreteCommand : Command
        {
            // Constructor
            public ConcreteCommand(Receiver receiver) :
                base(receiver)
            {
            }
    
            public override void Execute()
            {
                receiver.Action();
            }
        }
    
        /// <summary>
        /// The 'Receiver' class
        /// </summary>
        class Receiver
        {
            public void Action()
            {
                Console.WriteLine("Called Receiver.Action()");
            }
        }
    
        /// <summary>
        /// The 'Invoker' class
        /// </summary>
        class Invoker
        {
            private Command _command;
    
            public void SetCommand(Command command)
            {
                this._command = command;
            }
    
            public void ExecuteCommand()
            {
                _command.Execute();
            }
        }
    }

##### Output

    Called Receiver.Action()