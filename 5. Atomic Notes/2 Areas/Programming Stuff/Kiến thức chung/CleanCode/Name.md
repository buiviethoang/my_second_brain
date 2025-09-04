2025-08-30 09:33
Status: #baby
Tags: [[coding]]
## Main

## Naming
### Use Intention-Revealing Names
`int d; // elapsed time in days`
with 
```
int elapsedTimeInDays;
int fileAgeInDays;
```
```bash
public List<int[]> getThem() {
List<int[]> list1 = new ArrayList<int[]>();
for (int[] x : theList)
if (x[0] == 4)
list1.add(x);
return list1;
}
``` 
with 
```bash
public List<int[]> getFlaggedCells() {
List<int[]> flaggedCells = new ArrayList<int[]>();
for (int[] cell : gameBoard)
if (cell[STATUS_VALUE] == FLAGGED)
flaggedCells.add(cell);
return flaggedCells;
}
```
or even better: 
```bash
public List<Cell> getFlaggedCells() {
List<Cell> flaggedCells = new ArrayList<Cell>();
for (Cell cell : gameBoard)
if (cell.isFlagged())
flaggedCells.add(cell);
return flaggedCells;
}
```
### Avoid Disinformation
**hp** , **aix** , and **sco** would be poor variable names because they are the names of Unix plat-
forms or variants. Even if you are coding a hypotenuse and hp looks like a good abbrevia-
tion, it could be disinformative
Do not refer to a grouping of accounts as an **accountList** unless it’s actually a **List** .
The word list means something speciﬁc to programmers. If the container holding the
accounts is not actually a List , it may lead to false conclusions. So **accountGroup** or
**bunchOfAccounts** or just plain **accounts** would be better.

Beware of using names which vary in small ways. How long does it take to spot the
subtle difference between a **XYZControllerForEfficientHandlingOfStrings** in one module
and, somewhere a little more distant, **XYZControllerForEfficientStorageOfStrings** ? The
words have frightfully similar shapes.

A truly awful example of disinformative names would be the use of lower-case **L** or
uppercase **O** as variable names, especially in combination. The problem, of course, is that
they look almost entirely like the constants one and zero, respectively
```bash
int a = l;
if ( O == l )
a = O1;
else
l = 01;
```

### Make Meaningful Distinctions
Programmers create problems for them-selves when they write code solely to satisfy a compiler or interpreter
Sometimes this is done by misspelling one, leading to the surprising
situation where correcting spelling errors leads to an inability to compile. 
Consider, for example, the truly hideous practice of creating a variable named **klass** just because the name **class** was used
for something else.

Number-series naming **(a1, a2, .. aN)** is the opposite of intentional naming. Such
names are not disinformative—they are noninformative; they provide no clue to the
author’s intention. Consider:
```
public static void copyChars(char a1[], char a2[]) {
for (int i = 0; i < a1.length; i++) {
a2[i] = a1[i];
 }
}
```
This function reads much better when source and destination are used for the argument
names

Noise words are another meaningless distinction. Imagine that you have a **Product**
class. If you have another called **ProductInfo** or **ProductData** , you have made the names dif-
ferent without making them mean anything different. **Info** and **Data** are indistinct noise
words like a , an , and the
Note that there is nothing wrong with using preﬁx conventions like a and the so long
as they make a meaningful distinction. For example you might use a for all local variables
and the for all function arguments. 3 The problem comes in when you decide to call a vari-
able theZork because you already have another variable named zork

`
getActiveAccount();
getActiveAccounts();
getActiveAccountInfo();
`
How are the programmers in this project supposed to know which of these functions to call?
In the absence of speciﬁc conventions, the variable **moneyAmount** is indistinguishable
from **money** , **customerInfo** is indistinguishable from **customer** , **accountData** is indistinguish-
able from **account** , and **theMessage** is indistinguishable from **message** . Distinguish names in
such a way that the reader knows what the differences offer.

### Use Pronounceable Names
```
class DtaRcrd102 {
private Date genymdhms;
private Date modymdhms;
private final String pszqint = "102";
/* ... */
};
``` 
to
```

class Customer {
private Date generationTimestamp;
private Date modificationTimestamp;;
private final String recordId = "102";
/* ... */
};
```

### Use Searchable Names
Single-letter names and numeric constants have a particular problem in that they are not
easy to locate across a body of text
One might easily grep for **MAX_CLASSES_PER_STUDENT** , but the number **7** could be more
troublesome. Searches may turn up the digit as part of ﬁle names, other constant deﬁni-
tions, and in various expressions where the value is used with different intent. It is even
worse when a constant is a long number and someone might have transposed digits,
thereby creating a bug while simultaneously evading the programmer’s search.

My personal preference is that single-letter names can ONLY be used as local vari-
ables inside short methods. ***The length of a name should correspond to the size of its scope***

If a variable or constant might be seen or used in multiple places in a body of code,
it is imperative to give it a search-friendly name. Once again compare

`
for (int j=0; j<34; j++) {
s += (t[j]*4)/5;
}
`
to 
```
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
for (int j=0; j < NUMBER_OF_TASKS; j++) {
int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
int realTaskWeeks = (realdays / WORK_DAYS_PER_WEEK);
sum += realTaskWeeks;
}
```

### Avoid Encodings
(Hoi kho hieu)
### Hungarian Notation
(Hoi kho hieu)
### Member Preﬁxes
You also don’t need to preﬁx member variables with m_ anymore. Your classes and func-
tions should be small enough that you don’t need them. And you should be using an edit-
ing environment that highlights or colorizes members to make them distinct.
```
public class Part {
private String m_dsc; // The textual description
void setName(String name) {
m_dsc = name;
 }
}
```
to 
```
public class Part {
String description;
void setDescription(String description) {
this.description = description;
 }
}
```

### Interfaces and Implementations
These are sometimes a special case for encodings. For example, say you are building an
A BSTRACT F ACTORY for the creation of shapes. This factory will be an interface and will
be implemented by a concrete class. What should you name them? **IShapeFactory** and
**ShapeFactory** ?
I prefer to leave interfaces unadorned. The preceding I , so common in
today’s legacy wads, is a distraction at best and too much information at worst. I don’t
want my users knowing that I’m handing them an interface. I just want them to know that
it’s a **ShapeFactory** . So if I must encode either the interface or the implementation, I choose
the implementation. Calling it **ShapeFactoryImp** , or even the hideous **CShapeFactory** , is pref-
erable to encoding the interface

### Avoid Mental Mapping
This is a problem with single-letter variable names. Certainly a loop counter may be
named **i** or **j** or **k** (though never l !) if its scope is very small and no other names can con-
ﬂict with it. This is because those single-letter names for loop counters are traditional.
However, in most other contexts a single-letter name is a poor choice; it’s just a place
holder that the reader must mentally map to the actual concept. There can be no worse rea-
son for using the name **c** than because **a** and **b** were already taken.

### Class Names
Classes and objects should have noun or noun phrase names like **Customer** , **WikiPage** ,
**Account** , and **AddressParser** . Avoid words like **Manager** , **Processor** , **Data** , or **Info** in the name
of a class. A class name should not be a verb

### Method Names
Methods should have verb or verb phrase names like **postPayment** , **deletePage** , or **save** .
Accessors, mutators, and predicates should be named for their value and preﬁxed with **get** ,
**set** , and **is** according to the javabean standard
``` 
string name = employee.getName();
customer.setName("mike");
if (paycheck.isPosted())...
```
When constructors are overloaded, use static factory methods with names that
describe the arguments. For example,
`Complex fulcrumPoint = Complex.FromRealNumber(23.0);`
is generally better than
`Complex fulcrumPoint = new Complex(23.0);`

### Don’t Be Cute
If names are too clever, they will be
memorable only to people who share the
author’s sense of humor, and only as long
as these people remember the joke. Will
they know what the function named
**HolyHandGrenade** is supposed to do? Sure,
it’s cute, but maybe in this case
**DeleteItems** might be a better name.
Choose clarity over entertainment value.

Cuteness in code often appears in the form of colloquialisms or slang. For example,
don’t use the name **whack**() to mean **kill**() . Don’t tell little culture-dependent jokes like
**eatMyShorts**() to mean **abort**()
***Say what you mean. Mean what you say.***

### Pick One Word per Concept
Pick one word for one abstract concept and stick with it. For instance, it’s confusing to
have **fetch** , **retrieve**, and **get** as equivalent methods of different classes. How do you
remember which method name goes with which class? Sadly, you often have to remember
which company, group, or individual wrote the library or class in order to remember which
term was used. Otherwise, you spend an awful lot of time browsing through headers and
previous code samples.
it’s confusing to have a controller and a manager and a driver in the same
code base. What is the essential difference between a DeviceManager and a Protocol-
Controller ? Why are both not controller s or both not manager s? Are they both Drivers
really? The name leads you to expect two objects that have very different type as well as
having different classes.
A consistent lexicon is a great boon to the programmers who must use your code
### Don’t Pun
Avoid using the same word for two purposes. Using the same term for two different ideas
is essentially a pun.
If you follow the “one word per concept” rule, you could end up with many classes
that have, for example, an add method. As long as the parameter lists and return values of
the various add methods are semantically equivalent, all is well

### Use Solution Domain Names
Remember that the people who read your code will be programmers. So go ahead and use
computer science (CS) terms, algorithm names, pattern names, math terms, and so forth. It
is not wise to draw every name from the problem domain because we don’t want our
coworkers to have to run back and forth to the customer asking what every name means
when they already know the concept by a different name
The name AccountVisitor means a great deal to a programmer who is familiar with
the V ISITOR pattern. What programmer would not know what a JobQueue was? There are
lots of very technical things that programmers have to do. Choosing technical names for
those things is usually the most appropriate course

### Use Problem Domain Names
When there is no “programmer-eese” for what you’re doing, use the name from the prob-
lem domain. At least the programmer who maintains your code can ask a domain expert
what it means.

### Add Meaningful Context
Imagine that you have variables named firstName , lastName , street , houseNumber , city ,
state , and zipcode . Taken together it’s pretty clear that they form an address. But what if
you just saw the state variable being used alone in a method? Would you automatically
infer that it was part of an address?
You can add context by using preﬁxes: addrFirstName , addrLastName , addrState , and so
on. At least readers will understand that these variables are part of a larger structure. Of
course, a better solution is to create a class named Address . Then, even the compiler knows
that the variables belong to a bigger concept.
**Variables with unclear context**
```
private void printGuessStatistics(char candidate, int count) {
String number;
String verb;
String pluralModifier;
if (count == 0) {
number = "no";
verb = "are";
pluralModifier = "s";
} else if (count == 1) {
number = "1";
verb = "is";
pluralModifier = "";
} else {
number = Integer.toString(count);
verb = "are";
pluralModifier = "s";
}
String guessMessage = String.format(
"There %s %s %s%s", verb, number, candidate, pluralModifier
);
print(guessMessage);
}
```
**Variables have a context**
```
public class GuessStatisticsMessage {
private String number;
private String verb;
private String pluralModifier;
public String make(char candidate, int count) {
createPluralDependentMessageParts(count);
return String.format(
"There %s %s %s%s",
verb, number, candidate, pluralModifier );
}
private void createPluralDependentMessageParts(int count) {
if (count == 0) {
thereAreNoLetters();
} else if (count == 1) {
thereIsOneLetter();
} else {
thereAreManyLetters(count);
}
}
private void thereAreManyLetters(int count) {
number = Integer.toString(count);
verb = "are";
pluralModifier = "s";
}
private void thereIsOneLetter() {
number = "1";
verb = "is";
pluralModifier = "";
}
private void thereAreNoLetters() {
number = "no";
verb = "are";
pluralModifier = "s";
}
}
```

### Final Words
The hardest thing about choosing good names is that it requires good descriptive skills and
a shared cultural background. This is a teaching issue rather than a technical, business, or
management issue. As a result many people in this ﬁeld don’t learn to do it very well.
People are also afraid of renaming things for fear that some other developers will
object. We do not share that fear and ﬁnd that we are actually grateful when names change
(for the better). Most of the time we don’t really memorize the names of classes and meth-
ods. We use the modern tools to deal with details like that so we can focus on whether the
code reads like paragraphs and sentences, or at least like tables and data structure (a sen-
tence isn’t always the best way to display data). You will probably end up surprising some-
one when you rename, just like you might with any other code improvement. Don’t let it
stop you in your tracks.
Follow some of these rules and see whether you don’t improve the readability of your
code. If you are maintaining someone else’s code, use refactoring tools to help resolve these
problems. It will pay off in the short term and continue to pay in the long run.

## References
