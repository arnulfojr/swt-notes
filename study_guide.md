
# Study Guide for Software Eng.


## Development Process

It can be summarized in basically only 4 steps, *ADIT*

1. Analysis
2. Development
3. Implementation
4. Testing


## Analysis

This is the first of the development process, is basically focused on understanding the problem and setting the proper requirements; identifying what can be controllable and what's not controllable by the machine, also what's dependable of the machine and what's not.

### A1 Problem elicitation and description

In this step we use the A1 to extract from the information provided the requirements, knowledge domains, phenomenas and produce a Context Diagram from it.

The requirements and the domain knowledge are in natural language and the diagrams are done using UML.

There's basically 2 components in the system, the *environment* and the *machine*.

The states and behaviour of the environment can be described by *phenomenas*. Then the **machine** can interact with the **environment** by observing certain phenomenas (input) and causing certain phenomenas (output).

TIP: maybe is worth mentioning that the users are part of the environment.

#### Phenomena

Therefore **phenomenas** are events, actions or operations that occure in the enviroment, important for expressing statements and can be observed or controlled by the enviroment or the machine, respectively.

Examples:

1. **Elevator**: Person *presses button,* expects, that the *elevator arrives*.
2. **Bank**: Client gives *withdrawal instruction*, expects a *withdrawal*.

##### Categories
1. Controlled by the environment, not observable by the machine.
2. Controlled by the environment, observable by the machine.
3. Controller by the machine, observable by the environment.


#### Requirements and Domain Knowledge

The characteristics of the environment are **Domain Knowledge** and the desired characteristics of the system are **requirements** and the *machine* should aim to close the gap between this two.

So requiremnts describe the environment after the machine is in place, specifications is how the machine should act for the machine to fulfill the requirements.

*Functional vs Non-Functional Requirements*, functional requirements define how the system should act and the non-functional requirements concern about the quality characteristics as efficiency and user-friendlyness.

#### Types of statements

1. Optative Statements
    * Descrive the env, in the way we expect the env should be after the machine is implemented.
    * therefore **requirements** are optative 
2. Indicative Statements, describe the env., alias the Domain Knowledge
    1. Facts, describe a fixed property of the env.
    2. Assumptions, describes the conditions that are needed, so the requirements are accomplishable.

#### Designations

System descriptinos require *designations* as basic vocabulary, this statements can be wither true or false.
This only expands the vocabulary but *not* its expressiveness and can be absurde or useless but **not** false!

#### Context Diagram (UML too)

* Biddable Domains are **always** an active UML Class.
* Causal Domains are those domains which have predictable behaviour, else they are biddable domains, which trigger events.
* Lexical Domains are a physical representation of data, an online form is one example, a model, too.
* Display Domain is a special causal domain, which serves as an Output device for the machine and provides informations to other problem domains.
* Remember to do Model Driven development when doing the context diagram, as it is not important to include the databases, for instance, only the models and the type of relationship it has to the machine.
    * Normally models/entities are Lexical and Designed Domains!
* Display Domains are only domains that present data to a Biddable Domain!, this are passive classes in UML.
* It is important to define stereotypes in the relationships and inside the classes!
    * They are in the shape of ` <<stereotype_name>> `
* Relationships
    * Simple relationships or assosiations are a line ` ---  `
    * Composition ` <>-----  ` (filled arrow)
    * aggregations ` < >----  ` (empty arrow)
    * generalization ` <¡---- ` (inheritance arrow)



```

// So as we can see, the diagram can have relationship to a biddable domain

                         [1..*]             [1]
  ---------------------                       ---------------
||  <<biddableDomain>> ||--------------------|  <<machine>>  |
  ---------------------     <<connection>>    ---------------
                        BD!{makeSomething, recordSomething}
                        M!{provideFeedback, etc...}  

```



#### A1 Procedure

1. Derive requirements from the given description and collect the needed Domain Knowledge.
    * Requirements (RXX)
    * Assumptions (AXX)
    * Facts (FXX)
2. Set up  a Context Diagram using UML.
    * Nouns are good candidates for the Domains.
    * Verbs are good candidates for the phenomena.
3. Execute Validation Steps.


### A2 Problem Decomposition and problem classification


The objective of this step is to decompose the big-1-problem into several sub-problems, this helps to handle complexity and to ease the comprehension. This step also complements the missing details from the initial domain knowledge and requirements.

Difference in the diagrams between the Context Diagram and the Problem Diagrams are that the Context Diagram asks *Where is the problem located?* and the problem diagram asks *What's the problem?*, therefore the Problem Diagram contains requirements that refer to and constrain the problem domains.

The diagrams *include the requirements from* **A1**, remember that requirements can **NOT** constrain a *Biddable Domain*, but *refersTo* one.

 
```
 // in this diagram a requirement can referTo and constrain some other domains

  ----------------------
 |   <<causalDomain>>   |- - - - - - - -
  ----------------------                |
                                        | <<refersTo>>
                                        |
                                        |            -------------------
                                         - - - - - -|  <<requirement>>  |
                                        |            -------------------
                                        |  <<constrains>>
   -----------------------              |
  |   <<displayDomain>>   |- - - - - - -
   -----------------------


```


#### Approaches to decompositions

* Top-Down decomposition
* Use-case decomposition
    * This approach is usefull when it makes sense to have/think-of the machine as a facility offering discrete services that are used in clearly defined episodes.
* Knowledge-based decomposition through **projection**.
    * decompose into *parallel* subproblems.
    * projection: subproblems are projections of the overall problem, i.e., partial aspects are not considered.

#### Defining problem projections

Since problem diagrams must be consistent with the context diagram, the relation of new elements to existing elements in the *context diagram* must be documented via **mapping diagrams**.

##### Mapping Diagrams

Some operators are:

* Domains are left out, since they are included in the context diagram
* the connection domain between the newly introduced and the domain from the context diagram is done by the stereotype *<<concretizes>>*
    * Introduce designed lexical domain (mapping using aggregations)
    * Remove connection domains use the stereotype *<<concretizes>>*
    * combine domain and splitting domains by using aggregations!


#### Problem frames

This frames are patterns that characterize frequently occuring problems.

* required behaviour
    * the machine needs to control a certain behaviour of the real world
    * usually is used a Causal Domain to control the behaviour
* commanded behaviour
    * There is a domain that a biddable domain needs to control
    * In this case a biddable domain can't be constrained, therefore the causal domain is used to constrain the actions done by the biddable domain.
    * The normal case, where the user controls the machine
* information display
    * in this case the use of a display domain is required!
    * this problem frame is about obtaining this info from the world and present it at the required place in the required form.
* simple workpieces
    + A tool is needed to allow the user to create and edit a certain class of computer processable _process_
        * a text, graphic, or objects
    + important to note: this problem frame does not deal with printing, representing or further processing the workpieces!
    + differences between the workpieces and the commanded behaviour are that the workpieces are lexica and formal whereas the controlled domain is causal and informal.
* transformation
    * Literally only transforms data, is based on I/O.
* simple transformation
    * a file is cyclically or automatically changed.
* query
    * query 1
        + An operator queries information from a database, then the information is displayed.
        - the constrained domain is the Display
    * query 2
        + An alterative, a display domain, a connection domain fwding the request and response can be used.
        - The constriained domain is the Connection domain
    * They both refer to a Biddable or Lexical Domain
* update
    * update 1
        + same as query 1 and as well the information is displayed in a display domain.
        - the constrained is the lexical domain and the display domain
    * update 2
        + instead of the display domain, uses a connection domain
        - the constrained is the lexical domain and the connection domain
    * it refers to the biddable domain!


Normally in web the most common frames are update and query, transformations and *simple transformation*



### A3 Abstract software specifications

So now we take the decomposed sub problems from the A2 and we define specifications.

Where the following states: `Specifications AND Domain knowledge => Requirement `

Steps to execute the A3:

1. Create specifications from the domain knowledge for each sub problem, check if requirements are implementable and identify and use necessary domain knowledge.
2. Create the sequence diagrams per sub-problem.
3. Check correctness of the developed specifications.

#### Specifications

Are descriptions that are sufficient for building the machine and implementable requirements!
Therefore *if the machine fulfills the specifications*, the system fulfills the requirements!

So requirements are not implementable if **constrians a phenomena that are controlled by the env**, refers to phenomena that are not observable by the machine, and makes constraints for the future.

```yaml

R05: If a reserved holiday offer is not paid within 14 days, it is automatically set available again
A04: A staff member records when a payment is received. Staff members are up to date concerning the payment information.
# we can derive the specification:
S05: If no payment is recorded for a reserved holiday offer within 14 days, the reserved holiday offer is automatically set available again.
# preserving the correctness S05 AND A04 = R05

```

#### Sequence Diagrams

Using UML we establish the sequence diagrams per problem frame.

There's different types of operators in the sequence diagrams:

* **alt**, alternative (if statement) 2 or more alternatives are possible
    * alt uses the `[]` brakets to define the expressions.
    * `[n < 3]`, `[else]`, etc..
* **opt**, optional steps
* **loop(x, y)**, loops the nested statements
* *break*, this breaks the steps; mostly usefull in the loop statements
* **par**, parallel independent execution of several operands
* *ignore*, ignores the messages during run time
* *consider*, messages are considered in run time.
* *seq*, weak sequencing, default
* **strict**, strict sequencing
* *neg*, forbidden behaviour
* **critical**,  critical region, non-interruptible behaviour.
* *assert*, to define a message sequence that must occur.


```yaml

S02: If the machine receives the command "getAvailableHolidayOffers", then the available HolidayOffers are returned via the command "showAvailableHolidayOffers".
F05: WebpageGuest mediates between machine and guest.

S03: If the machine receives the command "makeBooking", then it is checked if the holiday offer is available. If the holiday offer is available, then the machin sets it as reserved, sends the command "sendInvoice" to create the invoice email, and informs the user with the command "showOk" to guest's web page about the successful booking process. Otherwise, the machine informs the user with the command "showFail" to the guest's web page about the unsuccessful booking process.
# This is valid because S03 AND F05 AND F06 = R03/R04

```


##### Local attributes
As the UML classes, sequence diagrams can also have attributes, public (+)  and private (-).

##### State predicates
Are called *state invariants* in the standard but are **not** invariant.
State predicates can be expressed as constraints, state symbols or notes.

They are located in top of the time line of the object and use a pill shape or the `{}` brackets.

##### Lost and found messages
used to trigger stuff in the objects/target


### A4 Technical software specification

This is about setting the technologies to use, for instance the database type to use, SQL database or NoSQL database, for example. The server type, Apache 2.4 is the Server which communicates through api to the machine and email using SMTP and IMAP or POP3. Users can use connection domains via gui.

IMPORTANT: is the mappings used to the context diagram! As everything that is set up in this diagram should be represented from the context diagram!



### A5 Operations and data specification

This phase specifies a preliminary class model in UML! And using OCL we are able to desrcibe the pre and post state of the machine/env.

The goal of this Step is to grab the Sequence Diagram (one per sub problem), then setting OCL statements, either class invariants and/or pre/post-conditions. This is for knowing how the machine alters the state of the environment or the machine itself (before vs after).


#### Object Constraint Language OCL

OCL expressions are always bounded to a UML model! Since this language is basically a constraint language, it needs some schema or model to constrain!

1. Class invariant, a constraint that must almost be met by all instances of a class.
2. Pre condition, a constraint that must be true before the execution of an operation.
3. Post condition, a constraint that must be true after the execution of an operation.

Syntax:

```ocl
context <identifier> <constraintType> [<constraintName>]: <boolean expression>
```

* **context** here is a keyword to mark the model element indicated by the *<identifier>* from which other model elements can be referenced, the keyword self can be used within the boolean expression to access the context!
* **<identifier>** is a class or operation name
* **<constraintType>** is one of the keywords **inv**, **pre**, **post**.
* **<constraintName>** is an optional name to assign to the constraint
* **<boolean expression>** just an expression.

##### OCL Types

* Predefined Types
    * primitive types: String, Integer, Real, Boolean, etc...
    * collection types: Set, Bag, Sequence, OrderedSet
    * tuple types: Tuple
    * special types: OclAny (supertype for all types except collection and tuples)
* Classifiers
    * classes, enumeration classes, and role names
    * attributes and operations
* Operators
    * boolean: =, <>, and, or, xor, not, implies, if-then-else-endif


This next invariant states all Flight instances have less than 4 units of duration:

```ocl
context Flight
inv: self.duration < 4
```

This is equivalent to

```ocl
context Flight
inv: duration < 4
```

The implies statement is really usefull to use! Class variables are used by ClassType::VARIABLE, or also the enumerations (as they are more properly called)

```ocl

context Passenger
inv: self.age > 90 implies
    self.needsAssistance = Assistance::wheelChair

```

Now having in consideration the following relationship we can now refer to the relationships from their names.

```
                       + origin             + departingFlights
                         [1..*]             [1]
  ---------------------                      ---------------
 |       Airport       |--------------------|     Flight    |
  ---------------------                      ---------------
                      
```

Remember that OCL is **NOT** utf-8 encoding, but rather simple _ASCII_!! The following statement reflects the fact that the origin can not be the destination, according to the requirements or environment.

```ocl
context Flight
inv: origin <> destination
```

Using collections is OCL is sort of using PHP or C++, better PHP! Is used the `->` operator.

```
                       + passengers       + flight
                         [*]             [1]
  ---------------------                     --------------------
 |      Passenger      |--------------------|      Flight      |
  ---------------------         Books       --------------------
                                            | +maxNrPassengers |
                                            --------------------
```

```ocl

context Flight
inv: passengers->size() <= maxNrPassengers

```

###### Collections

1. Set `Set(T)`
    * each element may occur only once
    * single navigation of an association results in a Set
2. Bag `Bag(T)`
    * elements may be present more than once
    * combined navigation results in a Bag
3. OrderedSet `OrderedSet(T)`
    * A set in which the elements are ordered
    * single navigation of an association that is marked as {ordered} results in an OrderedSet
4. Sequence `Sequence(T)`
    * A *Bag* in which the elements are ordered
    * combined navigation of associations, at least one of which is marked as {ordered}, results in a Sequence.
5. Tuple `Tuple(T)`

All collections offer the iterator operations!

* collect, used to query by another collection
    * `collection->collect(collection_2)`
    * the `.` is used to abbreviate this call
    * `collection.collection_2` is the same as using `collection->collect(collection_2)`
* select
    * Specifies a subset of a collection, using a boolean expression as parameter
    * returns a collection with those elements that fulfill the boolean expressiona as **true**.
    * `passengers->select(p: Passenger | p.needsAssistance <> Assistance::noAssistance and ...)`
* reject, same as the *select* but instead of the boolean expression evaluating to true, it agrees on **false**
* forAll
    * evaluates all the instances in the collection, if it evaluates to true for all elements it is true for all, false if at least one does **not** fulfills it!
    * RETURNS A BOOLEAN VALUE, not a collection
    * `Airport.allInstances()->forAll(a1: Airport, a2: Airport | a1 <> a2 implies a1.name <> a2.name)`
    * **shortcut** `Airport.allInstances()->isUnique(name)`
* exists
    * if for at least one element the condition applies it returns a true value, else false.
    * `Airport.allInstances()->exists(a: Airport | a.name = 'Duisburg' )`
* one
    * Specifies that there's only extacly **ONE** instance matching the boolean expression.
    * This statements, tho, does not return a boolean value but rather the matching instance.
    * Uses the same syntax as the *select*
* any
    * This statement returns the **first** matching instance in the source collection.
    * uses the same syntax as the *select*

Usefull methods:

* Operations on collection(T)
    * size(): Integer
    * isEmpty(): Boolean
    * notEmpty(): Boolean
    * includes(object: T): Boolean
    * excludes(object: T): Boolean
    * count(object: T): Integer
    * includesAll(c2: Collection(T))
    * excludesAll(c2: Collection(T))
    * sum(): T
    * product(c2: Collection(T)) : Set(Tuple(first: T, second: T2))
* Iterator expressions on collection(T)
    * isUnique(iterators | body): Boolean
* Operations of OrderedSet(T)
    * append(object: T): OrderedSet(T)
    * prepend(object: T): OrderedSet(T)
    * insertAt(index: Integer, object: T): OrderedSet(T)
    * at(i: Integer): T
    * first(): T
    * last(): T
* OclAny
    * OclIsNew(): Boolean
    * allInstaces(): Set(T)

Converting between collections is as easy as calling `asCollectionType()` in the targeted collection.

OrderedSet and Sequence offer the `first()`, `last()` and `at(i: Integer)`


##### pre and post conditions

They are assigned in the OCL statement

```ocl

context ClassType::methodName(**kwargs)
pre: <booleanExpression>
post: <booleanExpression>

```

When using the post statement the conditions from the Pre can be accessed through the `var@pre` statement, where var is the variable name. And the returned value is denoted with the keyword **result**.

All the conditions must always return a boolean value! They describe how was the state **before** and **after** the execution of the statement!

```ocl

context Flight::book(**kwargs)
pre: true
post:
    passengers->size() - passengers@pre->size() = 1
    AND passengers->exists(p: Passenger | p.age = kwargs.age
        AND p.name = kwargs.name
        AND p.needsAssitance = kwargs.assitance
    )    
```

When a call is need to be executed, then the call is done as `observer^callName(args)`.



### A6 Software LifeCycle

The idea is that every sequence diagram, hence every sub problem, is one life cycle.

1. the best approach is to set *one* lifecycle for each biddable domain.
2. Set up exaclty one life-cycle for the machine domain, having all the lifecycle's from the biddable domains for the machine domain, having all the lifecycle's from the biddable domains..

#### Syntax and semantics

1. Each sequence diagram name is a life-cycle expression.
2. let x and y be a lifecycle expression
    * `x:y`, x is follwed by y
    * `x | y`, either x or y
    * `x*`, x is executed 0 or more times
    * `x+`, x is executed at least once
    * `[x]`, x is optional
    * `x || y`, x and y are executed concurrently
3. definitions can also be done
    * `name = life-cycle expression`
    * then name can be used within other lifecycles
    * **RECURSION IS NOT ALLOWED**


```
LCguest = (Browse+; [Book])*
// note that booking is possible only after browsing
LCmember = (Make | (browseBookings; [Pay | Rate]))*
LCvacation_rental = (||n, i=1 LCguest_i) || (||m, j=1 LCmember_j) || Reset*
// where the ||x, x=n LCa_x denotes the parallel composition of n copies of the life-cycle
```

## Design

Consists of the design of the software architecture, inter/intra-component interaction and complete component or class behaviour

### D1

for the D1 we take all Ax and we do the software architecture.

The main difference between the Analysis and the Design phase is that the design pahse is all about structuring and classification of solutions to the problems presented until now.


The machine is composed by **components** and **connectors**.

#### UML

The difference now between the normal UML elements is now it specifies ports of communications between components!

* *parts* are rectangles, denote **components**
    * Parts = Components = Objects or Classes
* *connectors* are lines between 2 ports and may have names
* *ports* are small square/rectangles and denote interactions points of a part with its environment; may have names as well.
    * interfaces detail connectors using the ports
    * ports can be provided or required interfaces
        * The required interfaces are half a circle, this required interfaces are those which the component needs to work or do the job
        * the provided interfaces are a **full** circle, this provided interfaces are those which the component provides for the external component to comunicate, is basically the interface provided so that the components can communicate.
    * Example of provided and required interfaces are
        * Provided `JavaData` as it comes from the external component
        * Required `JavaCommands` and the commands are required to communicate.
    * In the mappings, the required interface the `<<use>>` stereotype in the connection is used.
    * In the mappings, the provided interface is modeled through interface realization. `--|>` (inheritance, generalization)
    * Comming from the problem diagrams, when the machine calls something from another component, then the port interface of the component in the design phase will be a required one.
    * Comming from the PD, when a component calls something from the machine, then the port interface of the component in the design phase will be a provided one.

#### Architectural Styles

1. Pipes and filters, from the UNIX programming environment.
    * Pipes move data from a filter output to a filter input
    * filters transform streams of input data into streams of output data in an incermental way
    * Fits better in the transformation problem frame
2. Repository architecture
    * The integration of data in an important goal, as they all share a common data.
    * query and update problem frames fit the best in this case
3. Layered architecture
    * only connected to adjacent layers and shuold not have layer bridging at all!
    * ISO/OSI reference model for communication protocols.

#### Making the Diagrams and mappings

It is important to set the mappings from the Ax to D1!

This is made by setting up the architectural diagram and then mapping it, it is important to tell what phenomenas are used in the **ports** and which of them they can relate from the A3 (sequence diagrams), this is called refining `app_if`.

If the phenomena is a required one, then use the `<<use>>` stereotype. else use the inheritance (the generalization).

`tech_if`...

Summary:

* Always when having ports, "refine" them means that it has to be mapped to which phenomenas is being related (use A3)
* Do mappings when introducing new components.


### D2 - Inter

Inter component interaction.

Uses the OCL code and the D1 + A3. Remember to define the SQL commands executed against a database!

This phase is about doing sequence diagrams to explain the interaction between the components, the calls shall implement all the parameters from the function already, consistent with the preliminary class in A5, I think...

Is weirdly the largest chapter but I dont have anything to say...

### D3 - Intra

something about the intra-components, never did it heard no one doing it; mock exam didnt had it...

You know what it means, but is usually defined if no ORM is used for instance.

### D4 - State Machines!

Consists of states and transitions between these states.

* A transition is a basic `--->` arrowed line with `e[g]/a` on top.
    * A transition is taken when g is true and e occurs. then a is sent/executed.
    * `in1/out1`
* The initial state is a black circle. `•-->`.
* The final state is a cross `---> X` or a black circle inside a circle `-->@`.
* `back` is a trigger for a transition to move back to the default state.

Simple example

```
      ----------
     |   Idle   |-----------------------
      ----------                        |
                                        | doGet(new Request('def'))/response.println(defaultWebpage())
                                        |
                                        |             ----------
                                         ----------->| default  |
                                        |             ----------
                                        | back/response.println(defaultWebpage())
   -------------                        | 
  |   Another   |<----------------------
   ------------- doGet(new Request('another))/response.println(anotherWebPage())


```


## Implementation and testing

### Implementation

Testing software:

* Unit testing
* Component Test/Integration Test
    * Goal: examine whether the components cooperate according to the architecture and reduce the number of the stubs to be implemented.
    * Two ways, top-down or bottom-up-integration
    * top-down requires more test stubs which simulate the activity of the missing components; implementation can be critical
    * bottom-up requires test drivers, which call a particular component and pass test cases to it, generally easy to implement.
* System Test
* Acceptance Test


* **Failure** software does not do what the specification describes.
* **Error, fault** cause of failure, error: mistake by a human when programming some software activity. can lead to a fault

### Testing
There's a lot of testing involved but no idea of what the fuck is going on there in the slides.
Basically explain how to do unit tests, integration tests and system tests, and somehow acceptance test.


## Correct Algorithms

proving a loop of `{Q} init; while b do S od {R}`

1. Show that P is true before the loop begins: `{Q} init {P}`
2. Show `{P and b} S {P}`, i.e. P is indeed an invariant
3. Show `P and not b => R`, i.e. when the loop terminates the postcondition is fulfilled.
4. Show `P and b => t > 0`, i.e. as long as the loop has not terminated, t is bounded from below
5. Show `{P and b} t1 := t; S {t < t1}`, i.e. each loop iteration is guarateed to decrease the boud function. the variable t1 must be new











