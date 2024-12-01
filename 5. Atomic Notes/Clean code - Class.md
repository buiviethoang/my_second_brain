2024-12-01 21:17
Status: #baby
Tags: [[computer science]] [[clean code]]

## Main
### Class organization 
1. a class should begin with a list of variables
2. Public static constants, if any, should come first
3. Then private static variables follow by private instance variable
4. Public functions should follow the list of variables
5. Private utilities called by a public function should be put right after
#### Encapsulation
- keep our variables and utility functions private
### Class should be small
The name of a class should describe what responsibilities it fulfills. In fact, naming is probably the first way of helping determine class size. If we cannot derive a concise name for a class, then it’s likely too large. The more ambiguous the class name, the more likely it has too many responsibilities.
We should also be able to write a brief description of the class in about 25 words
#### The Single Responsibility Principle
The Single Responsibility Principle (SRP)2 states that a class or module should have one, and only one, reason to change

Every sizable system will contain a large amount of logic and complexity. The pri- mary goal in managing such complexity is to organize it so that a developer knows where
to look to find things and need only understand the directly affected complexity at any given time. In contrast, a system with larger, multipurpose classes always hampers us by insisting we wade through lots of things we don’t need to know right now.
#### Cohesion
Classes should have a small number of instance variables
Each of the methods of a class should manipulate one or more of those variables. In general the more variables a method manipulates the more cohesive that method is to its class. A class in which each variable is used by each method is maximally cohesive
#### Maintaining Cohesion Results in Many Small Classes


### Organizing for Change
For most systems, change is continual. Every change subjects us to the risk that the remainder of the system no longer works as intended. In a clean system we organize our classes so as to reduce the risk of change.

The problem with opening a class is that it introduces risk. Any modifications to the class have the potential of breaking other code in the class. It must be fully retested.

We want to structure our systems so that we muck with as little as possible when we update them with new or changed features. In an ideal system, we incorporate new fea- tures by extending the system, not by making modifications to existing code.

#### Isolating from Change
## References


