2025-08-30 09:28
Status: #baby
Tags: [[java]]
## Main

Use Exceptions Rather Than Return Codes
```java
public class DeviceController {
...
public void sendShutDown() {
DeviceHandle handle = getHandle(DEV1);
// Check the state of the device
if (handle != DeviceHandle.INVALID) {
// Save the device status to the record field
retrieveDeviceRecord(handle);
// If not suspended, shut down
if (record.getStatus() != DEVICE_SUSPENDED) {
pauseDevice(handle);
clearDeviceWorkQueue(handle);
closeDevice(handle);
} else {
logger.log("Device suspended. Unable to shut down");
}
} else {
logger.log("Invalid handle for: " + DEV1.toString());
}
}
...
}
```
Changed to: 
```java
public class DeviceController {
...
public void sendShutDown() {
try {
tryToShutDown();
} catch (DeviceShutDownError e) {
logger.log(e);
}
}private void tryToShutDown() throws DeviceShutDownError {
DeviceHandle handle = getHandle(DEV1);
DeviceRecord record = retrieveDeviceRecord(handle);
pauseDevice(handle);
clearDeviceWorkQueue(handle);
closeDevice(handle);
}
private DeviceHandle getHandle(DeviceID id) {
...
throw new DeviceShutDownError("Invalid handle for: " + id.toString());
...
}
...
}
```

### Write Your Try-Catch-Finally Statement First
### Use Unchecked Exceptions
### Provide Context with Exceptions
Each exception that you throw should provide enough context to determine the source and
location of an error. In Java, you can get a stack trace from any exception; however, a stack
trace can’t tell you the intent of the operation that failed.
Create informative error messages and pass them along with your exceptions. Men-
tion the operation that failed and the type of failure. If you are logging in your application,
pass along enough information to be able to log the error in your **catch**.

### Deﬁne Exception Classes in Terms of a Caller’s Needs
```java
ACMEPort port = new ACMEPort(12);
try {
port.open();
} catch (DeviceResponseException e) {
reportPortError(e);
logger.log("Device response exception", e);
} catch (ATM1212UnlockedException e) {
reportPortError(e);
logger.log("Unlock exception", e);
} catch (GMXError e) {
reportPortError(e);
logger.log("Device response exception");
} finally {
…
```

TO 
```java
LocalPort port = new LocalPort(12);
try {
port.open();
} catch (PortDeviceFailure e) {
reportError(e);
logger.log(e.getMessage(), e);
} finally {
…
}

public class LocalPort {
private ACMEPort innerPort;
public LocalPort(int portNumber) {
innerPort = new ACMEPort(portNumber);
}
public void open() {
try {
innerPort.open();
} catch (DeviceResponseException e) {
throw new PortDeviceFailure(e);
} catch (ATM1212UnlockedException e) {
throw new PortDeviceFailure(e);
} catch (GMXError e) {
throw new PortDeviceFailure(e);
}
}
…
}
```

### Deﬁne the Normal Flow
Let’s take a look at an example. Here is some awkward code that sums expenses in a
billing application:
```java
try {
MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
m_total += expenses.getTotal();
} catch(MealExpensesNotFound e) {
m_total += getMealPerDiem();
}
```
In this business, if meals are expensed, they become part of the total. If they aren’t, the
employee gets a meal per diem amount for that day. The exception clutters the logic.
Wouldn’t it be better if we didn’t have to deal with the special case? If we didn’t, our code
would look much simpler. It would look like this:
```
MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
m_total += expenses.getTotal();
```

This is called the SPECIAL CASE PATTERN [Fowler]. You create a class or conﬁgure an
object so that it handles a special case for you. When you do, the client code doesn’t have
to deal with exceptional behavior. That behavior is encapsulated in the special case object

### Don’t Return Null
I think that any discussion about error handling should include mention of the things we
do that invite errors. The ﬁrst on the list is returning null
If you are calling a null-returning method from a third-party API, consider wrapping that
method with a method that either throws an exception or returns a special case object.

```java
List<Employee> employees = getEmployees();
if (employees != null) {
for(Employee e : employees) {
totalPay += e.getPay();
}
}
```

Right now, getEmployees can return null, but does it have to? If we change getEmployee so
that it returns an empty list, we can clean up the code:
```java
List<Employee> employees = getEmployees();
for(Employee e : employees) {
totalPay += e.getPay();
}
```
Fortunately, Java has Collections.emptyList(), and it returns a predeﬁned immutable list
that we can use for this purpose:
```java
public List<Employee> getEmployees() {
if( .. there are no employees .. )
return Collections.emptyList();
}
```

### Don't pass null
```java
public class MetricsCalculator
{
public double xProjection(Point p1, Point p2) {
return (p2.x – p1.x) * 1.5;
}
…
}
```
What if we pass null ???  calculator.xProjection(null, new Point(12, 13)); => Exception!

In most programming languages there is no good way to deal with a null that is
passed by a caller accidentally. Because this is the case, the rational approach is to forbid
passing null by default. When you do, you can code with the knowledge that a null in an
argument list is an indication of a problem, and end up with far fewer careless mistakes.

## References### 