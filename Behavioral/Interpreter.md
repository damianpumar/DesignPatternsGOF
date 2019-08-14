### Definition

Given a language, define a representation for its grammar along with an interpreter that uses the representation to interpret sentences in the language.

Frequency of use:

![](https://www.dofactory.com/images/use_low.gif)

Low

* * * * *

### UML class diagram

![](https://www.dofactory.com/images/diagrams/net/interpreter.gif)

* * * * *

### Participants

    The classes and objects participating in this pattern are:

-   **AbstractExpression**  **(Expression)**
    -   declares an interface for executing an operation
-   **TerminalExpression**  **( ThousandExpression, HundredExpression, TenExpression, OneExpression )**
    -   implements an Interpret operation associated with terminal symbols in the grammar.
    -   an instance is required for every terminal symbol in the sentence.
-   **NonterminalExpression**  **( not used )**
    -   one such class is required for every rule R ::= R1R2...Rn in the grammar
    -   maintains instance variables of type AbstractExpression for each of the symbols R1 through Rn.
    -   implements an Interpret operation for nonterminal symbols in the grammar. Interpret typically calls itself recursively on the variables representing R1 through Rn.
-   **Context**  **(Context)**
    -   contains information that is global to the interpreter
-   **Client**  **(InterpreterApp)**
    -   builds (or is given) an abstract syntax tree representing a particular sentence in the language that the grammar defines. The abstract syntax tree is assembled from instances of the NonterminalExpression and TerminalExpression classes
    -   invokes the Interpret operation

* * * * *

### Structural code in `C#`

This structural code demonstrates the Interpreter patterns, which using a defined grammer, provides the interpreter that processes parsed statements.

    using System;
    using System.Collections;
    
    namespace DoFactory.GangOfFour.Interpreter.Structural
    {
        /// <summary>
        /// MainApp startup class for Structural 
        /// Interpreter Design Pattern.
        /// </summary>
        class MainApp
        {
            /// <summary>
            /// Entry point into console application.
            /// </summary>
            static void Main()
            {
                Context context = new Context();
    
                // Usually a tree 
                ArrayList list = new ArrayList();
    
                // Populate 'abstract syntax tree' 
                list.Add(new TerminalExpression());
                list.Add(new NonterminalExpression());
                list.Add(new TerminalExpression());
                list.Add(new TerminalExpression());
    
                // Interpret
                foreach (AbstractExpression exp in list)
                {
                    exp.Interpret(context);
                }
    
                // Wait for user
                Console.ReadKey();
            }
        }
    
        /// <summary>
        /// The 'Context' class
        /// </summary>
        class Context
        {
        }
    
        /// <summary>
        /// The 'AbstractExpression' abstract class
        /// </summary>
        abstract class AbstractExpression
        {
            public abstract void Interpret(Context context);
        }
    
        /// <summary>
        /// The 'TerminalExpression' class
        /// </summary>
        class TerminalExpression : AbstractExpression
        {
            public override void Interpret(Context context)
            {
                Console.WriteLine("Called Terminal.Interpret()");
            }
        }
    
        /// <summary>
        /// The 'NonterminalExpression' class
        /// </summary>
        class NonterminalExpression : AbstractExpression
        {
            public override void Interpret(Context context)
            {
                Console.WriteLine("Called Nonterminal.Interpret()");
            }
        }
    }

##### Output

    Called Terminal.Interpret()\
    Called Nonterminal.Interpret()\
    Called Terminal.Interpret()\
    Called Terminal.Interpret()