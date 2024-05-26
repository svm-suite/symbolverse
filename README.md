```
• • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • •
•                                                                                         •
•   #####                       ##              ##                                        •
•  ##   ##                      ##              ##                                        •
•  ##       ##  ##  ####  ###   #####    ####   ##   ##  ##   ####    ###  #####   ####   •
•   #####   ##  ##  ##  ##  ##  ##  ##  ##  ##  ##   ##  ##  ##  ##  ##   ##      ##  ##  •
•       ##  ##  ##  ##  ##  ##  ##  ##  ##  ##  ##   ##  ##  ######  ##    ####   ######  •
•  ##   ##  ##  ##  ##  ##  ##  ##  ##  ##  ##  ##    ####   ##      ##       ##  ##      •
•   #####    #####  ##  ##  ##  #####    ####    ###   ##     ####   ##   #####    ####   •
•               ##                                                                        •
•            ####                                                                         •
•                                                                                         •
•                         a service virtual machine intended for                          •
•                      workflow programming and automated reasoning                       •
•                                                                                         •
•                                   (PREVIEW DOCUMENT)                                    •
• • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • • •
```

## table of contents

- [symbolverse preview document](#compute-svm-preview-document)
    - [A. LOCAL INSTALLATION (WIP)](#a-local-installation)
    - [B. SERVICES: message passing](#b-services-message-passing)
        - [1. theoretical background](#1-theoretical-background)
            - [1.1. syntax](#11-syntax)
            - [1.2. semantics](#12-semantics)
                - [1.2.1. exchanging messages](#121-exchanging-messages)
                - [1.2.2. memorizing states](#122-memorizing-states)
                - [1.2.3. modularity](#123-modularity)
        - [2. examples (WIP)](#2-examples-wip)
        - [3. afterword](#3-afterword)
    - [C. PROCESSES: workflow programming](#c-processes-workflow-programming)
        - [1. theoretical background](#1-theoretical-background-1)
            - [1.1. syntax](#11-syntax-1)
            - [1.2. semantics](#12-semantics-1)
                - [1.2.1. state flow](#121-state-flow)
                - [1.2.2. variables](#122-variables)
                - [1.2.3. branching](#123-branching)
        - [2. examples (WIP)](#2-examples-wip-1)
        - [3. afterword](#3-afterword-1)
    - [D. RULESETS: automated reasoning](#d-rulesets-automated-reasoning)
        - [1. theoretical background](#1-theoretical-background-2)
            - [1.1. syntax](#11-syntax-2)
            - [1.2. semantics](#12-semantics-2)
                - [1.2.1. rules](#121-rules)
                - [1.2.2. rule systems](#122-rule-systems)
                - [1.2.3. algebraic rules](#123-algebraic-rules)
        - [2. examples (WIP)](#2-examples-wip-2)
        - [3. afterword](#3-afterword-2)
    - [E. IMPLEMENTING A TYPE SYSTEM](#e-implementing-a-type-system-wip)

# symbolverse preview document

*Symbolverse* is a service virtual machine intended for workflow programming and automated reasoning. Its primary focus is on symbolic artificial intelligence programming, but it can be also used for other computation purposes related to back end programming. As a programming framework, *Symbolverse* integrates three paradigms: message exchange between services, sequence processing workflow, and rule based reasoning. Throughout the *Symbolverse* exposure, more experienced readers will perceive similarities between these three paradigms and object oriented structuring, procedural programming, and algebraic term rewriting, respectively.

Following the principles of [service oriented programming](https://en.wikipedia.org/wiki/Service-oriented_programming) (SOP), *Symbolverse* inherits some positive properties from the SOP paradigm. One of those properties is increased code encapsulation which implies a high agility during the programming process. Other positive properties include high level of modularity needed for code reuse, and granular independence between services. The SOP paradigm clearly differentiates between distinct services dedicated to perform given tasks. Such services communicate between each other only by passing messages. Internal processing of messages utilizes a particular *Symbolverse* model of computation.

The model of computation in *Symbolverse* represents an integration of two computing assets: running processes and applying rules. Running processes and applying rules reside on two very distant sides of the known computing spectrum. In *Symbolverse*, while processes can't return values, rules can't run processes. Complementary relation between them is meant to bridge the wide gap between [imperative](https://en.wikipedia.org/wiki/Imperative_programming) (dealing with processes) and [declarative](https://en.wikipedia.org/wiki/Declarative_programming) (dealing with rules) programming paradigms. Different coding purposes may require different approaches to the problems, and in *Symbolverse*, we are able to combine the imperative with the declarative solutions. Message exchange system interwoven into the *Symbolverse* allows us to define any intermediate domain specific solution by integrating components of the two initially contrasting sides.

During the *Symbolverse* creation, guiding thought was aspiration for definitional simplicity since symbolic artificial intelligence, programming which is the main purpose of *Symbolverse*, has to be able to create the *Symbolverse* code. Many aspects of programming constructs (like typing system) are intentionally left out of the *Symbolverse* core definition. Nevertheless, the algorithmic completeness of *Symbolverse* provides us with resources to build up any programming constructs we require on top of the *Symbolverse* core.

In this exposure, we will explain *Symbolverse* message exchange, running processes, and applying rules to expressions, all while exploring a role of versatile workflow programming and automated reasoning framework.

## A. LOCAL INSTALLATION

```
// work in progress //
```

## B. SERVICES: message passing

A service virtual machine (SVM) is an isolated software unit whose purpose is to possibly receive messages from the outer world, perform some inner processes in between, and possibly send messages to the outer world. SVMs are a powerful concept of organizing programming code into separated units, which brings benefits of raising a level of process abstraction, as well as reducing complexity of software integration.

*Symbolverse* is a SVM intended to be a mediator between other SVMs. As a central hub for directing services behavior, *Symbolverse* has abilities to start and stop different SVMs, as well as exchange messages between them during their lifetime. In the process of exchanging messages, *Symbolverse* also embeds an important puzzle piece of intermediate data computation. Data computation may also be placed in the end line of the computation process, providing possibilities to compose a wide range of atomic and compound SVMs suitable for a variety of computing tasks.

### 1. theoretical background

The model of exchanging messages in *Symbolverse* code is based on listening to other services for incoming messages, and igniting processes of invoking other services with outgoing messages. Involved processes may alter the *Symbolverse* local [states](https://en.wikipedia.org/wiki/State_(computer_science)) stored in variables, and they may programmatically invoke a series of services. Although we will use instructions of processes to explain functioning of the *Symbolverse* service message exchange in this section, we will not dive deeper into the details which we will discuss in later, dedicated chapters.

#### 1.1. syntax

[Syntax](https://en.wikipedia.org/wiki/Syntax) of a computer language is the set of rules that defines the combinations of symbols that are considered to be correctly structured statements or expressions in that language. *Symbolverse* language itself resembles a kind of s-expression. S-expressions consist of lists of atoms or other s-expressions where the lists are surrounded by parenthesis. In *Symbolverse* grammar, the first list element to the left determines a type of a list. There are a few predefined list types used to direct data exchange between service virtual machines, depicted by the following relaxed kind of [Backus-Naur form](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form) rules:

```
    <start> := (SERVICE (VAR <ATOM>+)? <statement>+)

<statement> := (MATCH (VAR <ATOM>+) <statement>)
             | (DIRECT (LISTEN <ATOM> <S-EXPR>) <process>)
```

`<process>` rule will be defined in the later chapters.

The above grammar rules define the syntax of *Symbolverse* code. To interpret these grammar rules, we use special symbols: `<...>` for noting identifiers, `... := ...` for expressing assignment, `...+` for one or more occurrences, `...?` for optional appearance, and `... | ...` for alternation between expressions. All other symbols are considered as a part of the *Symbolverse* code.

In addition to the above grammar, user comments have no meaning to the system, but may be descriptive to readers, and may be placed wherever a whitespace is expected. Single line comments begin with `//`, and reach to the end of line. Multiline comments begin with `/*` and end with `*/`, so that everything in between is considered as a comment.

Also, as addition to the grammar, there are a few kinds of functions:

```
(APPLY <S-EXPR> <S-EXPR>) -> <S-EXPR>  // if the first parameter is a service and
                                       // the second parameter is a message

            (FILE <ATOM>) -> <S-EXPR>  // if the parameter is a file name
          
                   <ATOM> -> <S-EXPR>  // if the left hand side is a variable name
```

These function calls are ready to be written where `<S-EXPR>` in the grammar is expected. The functions left hand sides are then automatically replaced by corresponding right hand sides when the code is interpreted.

#### 1.2. semantics

[Semantics](https://en.wikipedia.org/wiki/Semantics), as the meaning of *Symbolverse* code expressions, is presented in this section. Rather than formally defining *Symbolverse* service semantics, we will present a few intuitive examples that characterize coding *Symbolverse* services. We will explain how messages between services are exchanged, how to memorize internal service states, and how to write child services that can be plugged into parent ones.

##### 1.2.1. exchanging messages

Routers are coded within `ROUTER` sections. To receive a message, we need two parameters: a service name and a message. To send a message we also need the same two parameters. The following example represents our first "hello world" example:

```
/*
    hello world example
*/

(
    SERVICE
    (
        DIRECT
        (LISTEN this [start])
        (
            PROCESS
            (NODE BEGIN    (INVOKE parent [console out {hello world}]) (NEXT 1))
            (NODE (CURR 1) (STOP this                                ) END     )
        )
    )
)
```

When a service starts, it is automatically invoked with a message `[start]`. This is internal system behavior, and on receiving this message is a good event to initialize a working environment of the service.

In this example, within the `DIRECT` section, we declare that we `LISTEN` to `this` service (the service controlled by the current code) for such a message, and bind some processing commands to run when the message `[start]` arrives. The `PROCESS` section defines these processes. First, we `INVOKE` the service `parent` with the message `[console out {hello world}]`. Sending this message to the `parent` outputs the text `hello world` to the console. Next, we `STOP` the `this` service, exiting the internal service message listener.

Considering that we started `this` service from a command prompt, thus the command prompt is the root service, it becomes the `parent` service providing a console to read from and write to. To write to the console, we send it a message patterned `[console out <S-EXPR>]`.

The bound `PROCESS` has its own whole little grammar of appearance, and we will analyze it more thoroughly in the later chapters. For now, let's just say that each process has its beginning node, its intermediate nodes and its ending node. The order of nodes executed is determined by matching `NEXT` and `CURR` sections of two distinct nodes. Each `NODE` of the process has an attached instruction to perform in the sequence. In this chapter we will use `INVOKE` instruction for sending messages to different services, `START` and `STOP` for starting and stopping services, and `HOLD` instruction for assigning a content to a variable.

To establish bidirectional communication with the console, we can write something like in the following example:

```
/*
    conversation example
*/

(
    SERVICE
    (
        DIRECT
        (LISTEN this [start])
        (
            PROCESS
            (NODE BEGIN (INVOKE parent [console out {speak to me}]) END)
        )
    )
    (
        DIRECT
        (LISTEN parent [console in {hi}])
        (
            PROCESS
            (NODE BEGIN (INVOKE parent [console out {hello there}]) END)
        )
    )
    (
        DIRECT
        (LISTEN parent [console in {bye}])
        (
            PROCESS
            (NODE BEGIN    (INVOKE parent [console out {good bye}]) (NEXT 1))
            (NODE (CURR 1) (STOP this                             ) END     )
        )
    )
)
```

The example shows that we can have a number of `DIRECT` sections that route messages and execute processes. When the service starts, it prints out `{speak to me}` text. Next, whenever we input `{hi}`, the service greets us with `{hello there}`. Only when we input `{bye}`, the service outputs `{good bye}` and stops.

##### 1.2.2. memorizing states

Each service, during its lifetime, can remember some content states in variables. The variables are declared right ahead the `ROUTER` keyword, putting them within the `VAR` section. There can be any number of variables, and in the following example we take care of only one variable, `<incline>`:

```
/*
    keeping balance example
*/

(
    SERVICE
    (VAR <incline>)
    (
        DIRECT
        (LISTEN this [start])
        (
            PROCESS
            (NODE BEGIN    (HOLD <incline> {standing straight}) (NEXT 1))
            (NODE (CURR 1) (INVOKE this [peek]               ) END     )
        )
    )
    (
        DIRECT
        (LISTEN parent [console in {level out}])
        (
            PROCESS
            (NODE BEGIN    (HOLD <incline> {standing straight}) (NEXT 1))
            (NODE (CURR 1) (INVOKE this [peek]                ) END     )
        )
    )
    (
        DIRECT
        (LISTEN parent [console in {tilt left}])
        (
            PROCESS
            (NODE BEGIN    (HOLD <incline> {leaning right}) (NEXT 1))
            (NODE (CURR 1) (INVOKE this [peek]            ) END     )
        )
    )
    (
        DIRECT
        (LISTEN parent [console in {tilt right}])
        (
            PROCESS
            (NODE BEGIN    (HOLD <incline> {leaning left}) (NEXT 1))
            (NODE (CURR 1) (INVOKE this [peek]           ) END     )
        )
    )
    (
        DIRECT
        (LISTEN parent [console in {peek}])
        (
            PROCESS
            (NODE BEGIN (INVOKE this [peek]) END)
        )
    )
    (
        DIRECT
        (LISTEN parent [console in {exit}])
        (
            PROCESS
            (NODE BEGIN (STOP this) END)
        )
    )
    (
        DIRECT
        (LISTEN this [peek])
        (
            PROCESS
            (NODE BEGIN (INVOKE parent [console out <incline>]) END)
        )
    )
)
```

The example simulates keeping balance while we can tilt the ground beneath it. When this service starts, within the section `HOLD`, it sets the variable `<incline>` contents to `{standing straight}`, and intermediately outputs its contents by sending message `[peek]` to the same service we are defining. We can see the output in the last `DIRECT` section. Next, when we input either `{tilt left}`, `{tilt right}`, or `{level out}`, the `<incline>` variable changes its state to reflect the counterbalance to the ground, and outputs the current state. At any moment, we can input the `{peek}` text to output the current state. When we are done playing with the service, and we want to stop the service, we input `{exit}` to the console.

##### 1.2.3. modularity

As expected, any number of child services may be started within the parent ones, thus forming a hierarchical structure of running services. One such child *Symbolverse* service is depicted by the next example:

```
/*
    child service `car.rt`: responding with sounds example
*/

(
    SERVICE
    (VAR <mark>)
    (
        MATCH
        (VAR <param>)
        (
            DIRECT
            (LISTEN this [start <param>])
            (
                PROCESS
                (NODE BEGIN (HOLD <mark> <param>) END)
            )
        )
    )
    (
        DIRECT
        (LISTEN parent [gas])
        (
            PROCESS
            (NODE BEGIN (INVOKE parent [sound {<mark> goes wrooom!}) END)
        )
    )
    (
        DIRECT
        (LISTEN parent [breaks])
        (
            PROCESS
            (NODE BEGIN (INVOKE parent [sound {<mark> goes skreek!}) END)
        )
    )
    (
        DIRECT
        (LISTEN this [stop])
        (
            PROCESS
            (NODE BEGIN (STOP this) END)
        )
    )
)
```

Let's assume that the service is saved to the `car.rt` file. The service uses the `<param>` pattern matching variable where it passes the value to a `<mark>` state variable of the car we are simulating. Suppose the `<mark>` holds a value `mercedes` after starting the service. Then, upon sending the service a message `[gas]`, it responds to the parent with `[sound {mercedes goes wrooom!}]` message, while sending it `[breaks]`, it responds with `[sound {mercedes goes skreek!}]`.

It is time to introduce a possible parent service that exchanges messages with this service to print out these messages to the console:

```
/*
    parent service: car controlling example
*/

(
    SERVICE
    (
        DIRECT
        (LISTEN this [start])
        (
            PROCESS
            (NODE BEGIN (START mercy [router (FILE car.rt) mercedes]) END)
        )
    )
    (
        DIRECT
        (LISTEN parent [console in {speed up}])
        (
            PROCESS
            (NODE BEGIN (INVOKE mercy [gas]) END)
        )
    )
    (
        DIRECT
        (LISTEN parent [console in {slow down}])
        (
            PROCESS
            (NODE BEGIN (INVOKE mercy [breaks]) END)
        )
    )
    (
        MATCH
        (VAR <snd>)
        (
            DIRECT
            (LISTEN mercy [sound <snd>])
            (
                PROCESS
                (NODE BEGIN (INVOKE parent [console out <snd>]) END)
            )
        )
    )
    (
        DIRECT
        (LISTEN parent [console in {exit}])
        (
            PROCESS
            (NODE BEGIN (STOP this) END)
        )
    )
    (
        DIRECT
        (LISTEN this [stop])
        (
            PROCESS
            (NODE BEGIN (STOP mercy) END)
        )
    )
)
```

The service firstly starts the child service coded within file `car.rt`. To start any process, we use the `(START <instance-name> <parameters>)` pattern. `<instance-name>` will be the instantiated service name, while in the optional `<parameters>` part we set up some parameters. In this case, we state that the name of the new service will be `mercy`, that we start the `router` type of service, that its code is contained in the `car.rt` file, and that we send it a parameter `mercedes`. There may be types of services other than `router` one. We can start any number of child services of the same type, but they have to be named differently. Within parameters, instead of the `(FILE <file-name>)` function call, we can freely copy the entire contents of that file. The passed parameter `mercedes` is intercepted by the child service, and immediately stored in the `<mark>` variable when the service starts.

This parent service serves as a mediator between the console and the `mercy` service. Inputting `{speed up}` outputs the `{mercedes goes wrooom!}`, while inputting `{slow down}` outputs the `{mercedes goes skreek!}`. We stop the service by inputting `{exit}` text.

### 2. examples

```
// work in progress //
```

### 3. afterword

In this section, we saw how messages between services can be exchanged, how we are able to memorize internal service states, and how to write child services controlled from the parent services. Being a service glue element, *Symbolverse* takes a central role among all the service virtual machines in the system. Provided with simple modularity, one may find it easy to imagine a specific system of routers coordinating between different services to perform a diversity of tasks of interest.

## C. PROCESSES: workflow programming

In computing theory, there are two mainstream branches of programming paradigms: declarative and imperative. Declarative programming typically abstracts from states, providing optimized structures for other forms of computations. However, sometimes, when dealing with states seems the most natural thing to do, imperative programming may be a very good fit because dealing with states is what it does the best.

[Finite state machines](https://en.wikipedia.org/wiki/Finite-state_machine), on whose appearance the processes in *Symbolverse* are based, can perform various tasks like driving elevators, traffic lights, combination locks, and many others. The limitations of finite state machines to perform only a subset of all possible tasks is surpassed by reading from and writing to arbitrary variables during program execution. Considering expressiveness, this model of computation is placed side by side with [Turing machines](https://en.wikipedia.org/wiki/Turing_machine) model which is the most expressive model of computation known to us.

A process in *Computing SVM* resembles a sort of [finite state machine](https://en.wikipedia.org/wiki/Finite-state_machine). A program represented by a process is composed of a series of statements which perform instructions in sequence, while the process is running. Each statement marks the current state of the program execution, and points to the next state in the execution sequence. Each instruction, paired with the current state of execution, may input from or output to some variable, or perform operations with services.

### 1. theoretical background

A process combines a kind of deterministic finite state machine model with service operations, variable assignment, and branching choices. Each process can be in exactly one of a finite number of states at any given time. The program begins with the beginning state, changes its state in a controlled manner during the execution, and finally ends with the ending state. As the state changes, instructions associated with the current state are executed.

It is possible to draw a directed graph by connecting nodes where links between nodes are determined by matching states. Specific nodes may also connect in a cyclic manner, thus forming loops necessarily controlled by testing the variables.

#### 1.1. syntax

[Syntax](https://en.wikipedia.org/wiki/Syntax) is the set of rules that defines the combinations of symbols that are considered to be correctly structured statements or expressions. A process code itself resembles a type of s-expression. S-expressions consist of lists of atoms or other s-expressions where lists are surrounded by parenthesis. In the code lists, the first list element to the left determines a type of a list. There are a few predefined list types used for data computing, depicted by the following relaxed kind of [Backus-Naur form](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form) rules:

```
        <process> := (PROCESS (VAR <ATOM>+)? <node>+)

           <node> := (NODE BEGIN <instruction> (NEXT <ATOM>))
                   | (NODE (CURR <ATOM>) <instruction> (NEXT <ATOM>))
                   | (NODE (CURR <ATOM>) <instruction> END)

    <instruction> := SKIP
                   | (TEST <ATOM>)
                   | (HOLD <ATOM> <S-EXPR>)
                   | <service-related>
                   
<service-related> := (START <ATOM>)
                   | (INVOKE <ATOM> <S-EXPR>)
                   | (STOP <ATOM>)
```

The above grammar rules define the syntax of a process code. To interpret these grammar rules, we use special symbols: `<...>` for noting identifiers, `... := ...` for expressing assignment, `...+` for one or more occurrences, `...?` for optional appearance, and `... | ...` for alternation between expressions. All other symbols are considered as parts of the code.

In addition to the above grammar, user comments have no meaning to the system, but may be descriptive to readers, and may be placed wherever a whitespace is expected. Single line comments begin with `//`, and reach to the end of line. Multiline comments begin with `/*` and end with `*/`, so that everything in between is considered as a comment.

#### 1.2. semantics

Word [semantics](https://en.wikipedia.org/wiki/Semantics) is another word for "meaning". In this section, we are dealing with the intuitive semantics of *Compute-stateful.svm* code. Semantics of the code will be explained using a few simplistic examples, describing how to enter and exit the computation, how the current state changes during the process execution, and what instructions are executed in the meanwhile.

##### 1.2.1. state flow

Each process has its `BEGIN` node, its intermediate nodes and its `END` node. Nodes are defined in the `(NODE <current-state> <instruction> <next-state>)` pattern. The order of execution is determined by matching the next and the current state of two distinct nodes. Also, each node of the process corresponds to a single attached instruction. Thus, the following example:

```
...
(
    PROCESS
    (NODE BEGIN    (INVOKE parent [console out {starting the process ...}]  ) (NEXT 1))
    (NODE (CURR 1) (INVOKE parent [console out {... running in between ...}]) (NEXT 2))
    (NODE (CURR 2) (INVOKE parent [console out {... stopping the process}]  ) END     )
)
...
```

outputs to the console the sequence of `{starting the process ...}`, `{... running in between ...}`, and `{... stopping the process}`.

##### 1.2.2. variables

Each process may hold any number of local variables visible only to that process. The variables are created when the process begins, and are forgotten as soon as the process ends. We declare the variables within the `VAR` section, immediately after the `PROCESS` keyword.

The following example:

```
...
(
    PROCESS
    (VAR <happiness> <amount> <lifeMeaning>)
    (NODE BEGIN    (HOLD <happiness> 21                                  ) (NEXT 1))
    (NODE (CURR 1) (HOLD <amount> 2                                      ) (NEXT 2))
    (NODE (CURR 2) (HOLD <lifeMeaning> (APPLY mul {<happiness> <amount>})) (NEXT 3))
    (NODE (CURR 3) (INVOKE parent [console out <lifeMeaning>]            ) END     )
)
...
```

owns local variables `<happiness>`, `<amount>`, and `<lifeMeaning>`. In the first two states, we assign values `21` and `2` to variables `<happiness>` and `<amount>`. In the third state, we assign their product to the `<lifeMeaning>` variable. Here, we applied the rule `mul` to `<happiness>` and `<amount>` to get the result. Finally, we output to the console the value of `<lifeMeaning>` variable.

##### 1.2.3. branching

We can also define multiple `NODE` steps with the same state identifier, which introduces a branching choice. In those cases, the current computing step is determined by the first available node with the same state, whose instruction passes against the `TEST` evaluator. Thus, the example:

```
...
(
    PROCESS
    (VAR <mood>)
    (NODE BEGIN    (HOLD <mood> blue                    ) (NEXT 1))
    (NODE (CURR 1) (TEST (APPLY eq {<mood> gray})       ) (NEXT 2))
    (NODE (CURR 2) (INVOKE parent [console out frowning]) END     )
    (NODE (CURR 1) (TEST (APPLY eq {<mood> blue})       ) (NEXT 3))
    (NODE (CURR 3) (INVOKE parent [console out smiling] ) END     )
)
...
```

has two nodes with the state `1`. After assigning `blue` to the variable `<mood>`, first we `TEST` it for equality with a value `gray`. Equality is tested by applying the `eq` rule to the parameters. Since the first test doesn't pass, next we test it for equality with a value `blue`. This test passes, and we are able to move to the next state `3`, where we output the `smiling` text to the console.

Branching constructs like this one may also be useful in performing loops by employing circular state references. In such cases, branching choices are necessary to exit from the loops to an outer state.

### 2. examples

```
// work in progress //
```

### 3. afterword

In this section we exposed basic constructs of defining processes. Although there are many cases where dealing with states may pose a stumbling stone in writing programs, there are some cases where being able to express states is very desirable. And that is the purpose of processes, to easily express operations with states such as execution in a sequence. Here, we only scratched the surface of what processes are capable of. Since we are dealing with a Turing complete system of processing, we may expect that we are not bound in any way considering the domain of supported computations.

## D. RULESETS: automated reasoning

Characteristic of nowadays widespread [imperative programming](https://en.wikipedia.org/wiki/Imperative_programming) is manual managing of state dynamics by program instructions to produce wanted states. In contrast to imperative, [declarative programming](https://en.wikipedia.org/wiki/Declarative_programming) abstracts from states using descriptions usually represented by rules repeatedly applied to parameters in a goal of producing wanted results. *Rulesets* belong into the category of declarative programming paradigm.

Two most prominent types of declarative programming are [functional](https://en.wikipedia.org/wiki/Functional_programming) and [logic programming](https://en.wikipedia.org/wiki/Logic_programming). Presenting a novel [algebraic](https://en.wikipedia.org/wiki/Algebraic_data_type) [term graph](https://en.wikipedia.org/wiki/Term_graph) [rewriting](https://en.wikipedia.org/wiki/Rewriting) approach, *rulesets* exhibit properties of both functional and logic programming worlds without a special treatment of either paradigm. This is made possible by using rewriting rules in a form of positive [sequents](https://en.wikipedia.org/wiki/Sequent).

Strictly speaking, *rulesets* programming expressions span on a level below functional and logic programming, representing a [rule-based system](https://en.wikipedia.org/wiki/Rule-based_system). We may consider *rulesets* as an "assembler" for declarative programming. Behavior of rewriting rules in *rulesets* is very similar to behavior of [production rules](https://en.wikipedia.org/wiki/Production_(computer_science)) in [parsing](https://en.wikipedia.org/wiki/Parsing) expressions, additionally allowing algebraic expression matching to take a place during the parsing process. Algebraic matching is something that naturally arises from using an extended version of production rules involving [conjunctions](https://en.wikipedia.org/wiki/Logical_conjunction) on the left and [disjunctions](https://en.wikipedia.org/wiki/Logical_disjunction) on the right side of the rules, which are exactly qualities belonging to sequents.

### 1. theoretical background

As a declarative programming paradigm, *rulesets* implement a term graph rewriting system to be a blend of functional and logical inference engine.

Term graph rewriting is a method of reconstructing one form of data from another form of data. In this reconstruction, a new data may be introduced, or existing data may be eliminated or reshaped to suit our requirements. To be able to do this, *rulesets* use a set of user definable rules of a form similar to formulas in mathematics, with the difference that *rulesets* rules may transform not only math expressions, but also any kind of data in a form of s-expressions.

Logical inference in *rulesets* implicitly relates existing rules or their parts by proper logical connectives. Thus, each rule in *rulesets* becomes logical implication, while their mutual interrelation simplifies logical reasoning about different forms of data they operate on. This logical reasoning corresponds to a kind of logic that naturally emerges from the algebraic aspect of rules, which is conveniently captured by [sequent](https://en.wikipedia.org/wiki/Sequent) like rules.

To show a clear correspondence between *rulesets* rules and sequents, we will use an analogy in which *rulesets* may be seen as a form of a [deductive system](https://en.wikipedia.org/wiki/Formal_system#Deductive_system) specifically adjusted to operate on s-expressions. Let's shortly overview the most used deductive systems in area of logical inference. [Hilbert style deduction](https://en.wikipedia.org/wiki/Hilbert_system), [natural deduction](https://en.wikipedia.org/wiki/Natural_deduction), and [sequent calculus](https://en.wikipedia.org/wiki/Sequent_calculus) all belong to a class of deductive systems. They are characterized by respectively increasing number of primitive logical operators. Hilbert style deduction incorporates only [implication](https://en.wikipedia.org/wiki/Material_conditional) where all injected rules take a form of `A -> B`. Natural deduction adds conjunction to the left implication side, so that rules take a form of `A1 /\ A2 /\ ... /\ An -> B`. Sequent calculus further extends the basic language by including right side disjunction, like in `A1 /\ A2 /\ ... /\ An -> B1 \/ B2 \/ ... \/ Bn`.

The price paid for the simple syntax of Hilbert-style deduction is that complete formal proofs tend to get extremely long. In contrast, more complex syntax like in natural deduction or sequent calculus leads to shorter formal proofs. This difference in proof lengths exists because often, on higher levels of abstraction, we would want to use the benefits of conjunction and disjunction constructs. Since Hilbert-style deduction doesn't provide these constructs as primitive operators, we would have to bring their explicit definitions into the implicational proof system, which could be avoided in a case of natural deduction to a certain extent, or sequent calculus to even greater extent.

In contrast to Hilbert style deduction and natural deduction, sequent calculus comes in a package with a full set of mappings from basic [logical connectives](https://en.wikipedia.org/wiki/Logical_connective) to uniform sequents. Logic operators appear natural enough to be fluently used in performing inference, while *sequents* appear simple enough to be reasoned about, which are both important qualities for choosing a base for underlying inference algorithm. One may say that sequent calculus characteristic mappings from logical connectives to sequents may seem imbued with elegant symmetry. In cases of Hilbert style deduction and natural deduction, lack of these mappings is compensated by non-primitive definitions of logical connectives, but we take a stand that those definitions do not reflect the elegance found in sequent calculus mappings.

Although sequent calculus, compared to Hilbert style deduction and natural deduction, may not seem like the simplest solution at first glance, we find it reasonable to base *rulesets* exactly on sequent calculus because, in the long run, benefits may seem to be worth the effort. After all, the simplistic duality elegance of sequent calculus transformations seem too valuable to be left aside in favor of simpler systems. We are taking a stand that the mentioned duality deserves a special treatment which sequent calculus provides us with by its definition. Thus, we choose sequent calculus as a foundation basis for performing inference in *rulesets*.

By the definition, *rulesets* borrow *sequents* from sequent calculus, and extends them by a notion of variables. Although *rulesets* are sharing some primitive foundations with sequent calculus, beyond borrowed sequents they employs their own proving method during logical reasoning process, namely making use of [constructive proofs](https://en.wikipedia.org/wiki/Constructive_proof). This allows us to generate a meaningful s-expression output upon providing a computational rule system and s-expression input.

#### 1.1. syntax

[Syntax](https://en.wikipedia.org/wiki/Syntax) of a computer language is the set of rules that defines the combinations of symbols that are considered to be correctly structured statements or expressions in that language. *rulesets* language itself resembles a kind of s-expression. S-expressions consist of lists of atoms or other s-expressions where lists are surrounded by parenthesis. In *rulesets*, the first list element to the left determines a type of a list. There are a few predefined list types used for data transformation, depicted by the following relaxed kind of [Backus-Naur form](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form) rules:

```
   <ruleset> := (RULESET <expression>+)

<expression> := <binding>
              | <rule>

   <binding> := (MATCH (VAR <ATOM>+) <rule>)
   
      <rule> := (RULE (READ (EXP <S-EXPR>)+) (WRITE (EXP <S-EXPR>)+))
```

The above grammar rules define the syntax of *rulesets*. To interpret these grammar rules, we use special symbols: `<...>` for noting identifiers, `... := ...` for expressing assignment, `...+` for one or more occurrences, and `... | ...` for alternation between expressions. All other symbols are considered as parts of the *rulesets* language.

In addition to the above grammar, user comments have no meaning to the system, but may be descriptive to readers, and may be placed wherever a whitespace is expected. Single line comments begin with `//`, and reach to the end of line. Multiline comments begin with `/*` and end with `*/`, so that everything in between is considered as a comment.

In *rulesets* language, there is no additional type checking, meaning that every expression valid in the above grammar is also valid in *rulesets*. However, we may form *rulesets* valid constructions that regardless of input may never return a successful response. Some of such cases indicate inconsistency in rules and always cause an input or output error.

Other such cases are not indicated by *rulesets* because they may already fall into the category of theoretically undecidable proof constructions. One strategy to deal with these cases is to restrict the rule recursion depth, suppressing further computation if the recursion reaches the posed limit. For more information about this undecidability, interested readers are invited to examine [Gödel's incompleteness theorems](https://en.wikipedia.org/wiki/G%C3%B6del%27s_incompleteness_theorems) and [halting problem](https://en.wikipedia.org/wiki/Halting_problem).

#### 1.2. semantics

[Semantics](https://en.wikipedia.org/wiki/Semantics) is the study of meaning, reference, or truth. In our understanding, semantics is tightly bound to interpretation of syntactically correct expressions. To know what an expression means, it is enough to know how it translates to a form that is already understood by a target environment. In this section, we are dealing with the intuitive semantics of *rulesets*. Semantics of *rulesets* will be explained using various simplistic examples and defining what inputs and outputs the examples accept and generate.

##### 1.2.1. rules

Rules are analogous to implications. They have their input `READ` side and output `WRITE` side, each containing a set of `EXP` sections as conjunction on the `READ` side and a set of `EXP` sections as disjunction on the `WRITE` side.

###### constants

Constants are just that, constant s-expressions without variables:

```
/*
    hello world example
    
     input: `(hello machine)`
    output: `(hello world)`
*/

(
    RULESET
    (RULE (READ (EXP (hello machine))) (WRITE (EXP (hello world))))
)
```

This example inputs s-expression `(hello machine)` and outputs s-expression `(hello world)`.

###### variables

Variables stand for unknown s-expressions that are yet to be specified. The use of variables is noted using `MATCH` and `VAR` sections:

```
/*
    hello entity example
    
     input: `(greet <name>)`
    output: `(hello <name>)`
*/

(
    RULESET
    (
        MATCH
        (VAR <X>)
        (RULE (READ (EXP (greet <X>))) (WRITE (EXP (hello <X>))))
    )
)
```

Within a rule, there can be any number of variables, and we can name them however we want. Thus, if we pass an input `(greet John)` to the above example, we get an output `(ḣello John)`.

##### 1.2.2. rule systems

Rule systems are sets of rules working together to produce some results. In this section we are dealing with untyped rule systems using composite rules. Because types in composite rules always have to be specified, to simulate untyped behavior, we make use of variables in surrounding `READ` and `WRITE` sections, noting generic expressions in a form of `(MATCH (VAR <X>) (EXP <X>))`. These expressions stand for any kind of s-expressions.

###### constants

Let's consider a rule system of constant rules:

```
/*
    toy making decision
    
     input: `(isGood girl/boy)`
    output: `(makeToy doll/car)`
*/

(
    RULESET
    (RULE (READ (EXP (isGood girl))) (WRITE (EXP (makeToy doll))))
    (RULE (READ (EXP (isGood boy) )) (WRITE (EXP (makeToy car) )))
)
```

The root rule has a `CHAIN` section composed of two other rules. What rule will be applied to an input, is determined by pattern matching of the rules `READ` side against the input. Thus, inputting `(isGood girl)` to the above example outputs `(makeToy doll)`, while inputting `(isGood boy)` outputs `(makeToy car)`.

###### variables

And here is another rule system, this time using variables:

```
/*
    job title decision
    
     input: `(isDoing <Name> drivingRocket/healingPeople)`
    output: `(isTitled <Name> astronaut/doctor)`
*/

(
    RULESET
    (
        MATCH
        (VAR <Name>)
        (
            RULE
            (READ (EXP (isDoing <Name> drivingRocket)))
            (WRITE (EXP (isTitled <Name> astronaut)))
        )
    )
    (
        MATCH
        (VAR <Name>)
        (
            RULE
            (READ (EXP (isDoing <Name> healingPeople)))
            (WRITE (EXP (isTitled <Name> doctor)))
        )
    )
)
```

If we, for example, input the expression `(isDoing Jane healingPeople)`, we get the output `(isTitled Jane doctor)`.


###### chaining rules together

Rule systems may be composed of rules that chain their `WRITE` side to other rules' `READ` side in producing results. Thus, the two rules `(RULE (READ (EXP a)) (WRITE (EXP b)))` and `(RULE (READ (EXP b)) (WRITE (EXP c)))` may chain into a new rule `(RULE (READ (EXP a)) (WRITE (EXP c)))` in a process of intermediate pattern matching against the expression `b`.

To show in example:

```
/*
    job title decision
    
     input: `thereIsADoctor`
    output: `peopleAreHealthy`
*/

(
    RULESET
    (
        RULE
        (READ (EXP thereIsADoctor))
        (WRITE (EXP peopleAreHealed))
    )
    (
        RULE
        (READ (EXP peopleAreHealed))
        (WRITE (EXP peopleAreHealthy))
    )
)
```

passing input `thereIsADoctor` chains the two rules, finally producing the output `peopleAreHealthy`.

##### 1.2.3. algebraic rules

Rules stand for implications with conjunctions on the `READ` sides and disjunctions on the `WRITE` sides. Using this feature, we can compose rules in an [algebraic](https://en.wikipedia.org/wiki/Algebraic_data_type) manner.

Having multiple elements on the `WRITE` sides in one rule, each of those elements may be pattern matched against all the elements of any other rule `READ` side. If such a match is met, and the `WRITE` sides of the later rules are all equal, we may produce the `WRITE` sides of the later rules as a result of the chaining process.

This behavior follows from properties of logic implications in proof construction process:

```
 A -> B \/ C,  B -> D,  C -> D
-------------------------------
            A -> D
```

To show it in example:

```
/*
    student decision
    
     input: `(isBeingEducated <Name>)`
    output: `(isAStudent <Name>)`
*/

(
    RULESET
    (
        MATCH
        (VAR <Name>)
        (
            RULE
            (READ (EXP (isBeingEducated <Name>)))
            (
                WRITE
                (EXP (attendsSchool <Name>))
                (EXP (attendsCollege <Name>))
            )
        )
    )
    (
        MATCH
        (VAR <Name>)
        (
            RULE
            (READ (EXP (attendsSchool <Name>)))
            (WRITE (EXP (isAStudent <Name>)))
        )
    )
    (
        MATCH
        (VAR <Name>)
        (
            RULE
            (READ (EXP (attendsCollege <Name>)))
            (WRITE (EXP (isAStudent <Name>)))
        )
    )
)
```

The first rule `WRITE` side holds a disjunction where each element matches against `READ` sides of the second and the third rule. Having the same `WRITE` side in the second and the third rule, the chaining may be performed. Thus, inputting `(isBeingEducated Jane)` in this example results with `(isAStudent Jane)` output.

Similar analogy holds in the symmetric case. Having multiple elements on the `READ` sides in one rule, each of those elements may be pattern matched against all the elements of any other rule `WRITE` side. If the such match is met, and the `READ` sides of the later rules are all equal, we may produce the `WRITE` sides of the former rule as a result of the rule chaining process.

This behavior follows from properties of logic implications in proof construction process:

```
 A -> B,  A -> C,  B /\ C -> D
-------------------------------
            A -> D
```

To show it in example:

```
/*
    computer expert decision
    
     input: `(buildsARobot <Name>)`
    output: `(isAComputerExpert <Name>)`
*/

(
    RULESET
    (
        MATCH
        (VAR <Name>)
        (
            RULE
            (READ (EXP (buildsARobot <Name>)))
            (WRITE (EXP (mastersHardware <Name>)))
        )
    )
    (
        MATCH
        (VAR <Name>)
        (
            RULE
            (READ (EXP (buildsARobot <Name>)))
            (WRITE (EXP (mastersSoftware <Name>)))
        )
    )
    (
        MATCH
        (VAR <Name>)
        (
            RULE
            (
                READ
                (EXP (mastersSoftware <Name>))
                (EXP (mastersHardware <Name>))
            )
            (WRITE (EXP (isAComputerExpert <Name>)))
        )
    )
)
```

The third rule `READ` side holds a conjunction where each element matches against `WRITE` sides of the first and second rule. Having the same `READ` side of the first and second rule, the chaining may be performed. Thus, inputting `(buildsARobot John)` in this example results with `(isAComputerExpert John)` output.

### 2. examples

```
// work in progress //
```

### 3. afterword

If properly performed, there could be numerous kinds of uses of the *rulesets* inference mechanism. One use may be in editing input in sessions that produce some mathematical, logical, or other kinds of computations, while looping back to editing sessions until we are satisfied with the output. Some other, maybe industrial use may involve compiling a program source code to some assembly target code. In other situations, it is also included that we could form a personal, classical business, or even scientific knowledge base with relational algebra rules, so we can navigate, search, and extract wanted information. Ultimately, data from the knowledge base could mutually interact using on-demand learned inference rules, thus developing the entire logical reasoning system ready to draw complex decisions on general system behavior. And this partial sketch of possible uses is just a tip of the iceberg because with a kind of system like *rulesets*, we are entering a nonexhaustive area of general knowledge computing where only our imagination could be a limit.

## E. IMPLEMENTING A TYPE SYSTEM

```
// work in progress //
```
