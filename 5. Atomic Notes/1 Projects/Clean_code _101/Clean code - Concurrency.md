## Why Concurrency?
Concurrency is a decoupling strategy. It helps us decouple what gets done from when it
gets done. In single-threaded applications what and when are so strongly coupled that the
state of the entire application can often be determined by looking at the stack backtrace. A
programmer who debugs such a system can set a breakpoint, or a sequence of breakpoints,
and know the state of the system by which breakpoints are hit.

### Myths and Misconceptions
- Concurrency always improves performance. => Concurrency can sometimes improve performance
- Design does not change when writing concurrent programs. => has a
huge effect on the structure of the system.
- Understanding concurrency issues is not important when working with a container
such as a Web or EJB container => 
### Concurrency Defense Principles
#### Single Responsibility Principle
Keep your concurrency-related code separate from other code.
#### Corollary: Limit the Scope of Data
Take data encapsulation to heart; severely limit the access of any
data that may be shared.
#### Corollary: Use Copies of Data
A good way to avoid shared data is to avoid sharing the data in the ﬁrst place. In some sit-
uations it is possible to copy objects and treat them as read-only. In other cases it might be
possible to copy objects, collect results from multiple threads in these copies and then
merge the results in a single thread.
#### Corollary: Threads Should Be as Independent as Possible
Attempt to partition data into independent subsets than can be
operated on by independent threads, possibly in different processors

### Know Your Execution Models
#### Producer-Consumer
#### Readers-Writers
When you have a shared resource that primarily serves as a source of information for read-
ers, but which is occasionally updated by writers, throughput is an issue. Emphasizing
throughput can cause starvation and the accumulation of stale information
#### Dining Philosophers
....

Most concurrent problems you will likely encounter will be some variation of these
three problems. Study these algorithms and write solutions using them on your own so
that when you come across concurrent problems, you’ll be more prepared to solve the
problem.
=> Learn these basic algorithms and understand their solutions.
### Beware Dependencies Between Synchronized Methods
Avoid using more than one method on a shared object.
There will be times when you must use more than one method on a shared object.
When this is the case, there are three ways to make the code correct:
• Client-Based Locking—Have the client lock the server before calling the ﬁrst
method and make sure the lock’s extent includes code calling the last method.
• Server-Based Locking—Within the server create a method that locks the server, calls
all the methods, and then unlocks. Have the client call the new method.
• Adapted Server—create an intermediary that performs the locking. This is an exam-
ple of server-based locking, where the original server cannot be changed.
### Keep Synchronized Sections Small
Keep your synchronized sections as small as possible
### Writing Correct Shut-Down Code Is Hard
Writing a system that is meant to stay live and run forever is different from writing some-
thing that works for awhile and then shuts down gracefully.
Graceful shutdown can be hard to get correct. Common problems involve deadlock,15
with threads waiting for a signal to continue that never comes.
=> Think about shut-down early and get it working early. It’s going to
take longer than you expect. Review existing algorithms because this is probably harder
than you think.
### Testing Threaded Code
Write tests that have the potential to expose problems and then
run them frequently, with different programatic conﬁgurations and system conﬁgurations
and load. If tests ever fail, track down the failure. Don’t ignore a failure just because the
tests pass on a subsequent run
#### Treat Spurious Failures as Candidate Threading Issues
Threaded code causes things to fail that “simply cannot fail.” Most developers do not have
an intuitive feel for how threading interacts with other code (authors included). Bugs in
threaded code might exhibit their symptoms once in a thousand, or a million, executions.
Attempts to repeat the systems can be frustratingly. This often leads developers to write off
the failure as a cosmic ray, a hardware glitch, or some other kind of “one-off.” It is best to
assume that one-offs do not exist. The longer these “one-offs” are ignored, the more code
is built on top of a potentially faulty approach.
Recommendation: Do not ignore system failures as one-offs
#### Get Your Nonthreaded Code Working First
Do not try to chase down nonthreading bugs and threading bugs
at the same time. Make sure your code works outside of threads
#### Make Your Threaded Code Pluggable
Make your thread-based code especially pluggable so that you
can run it in various conﬁgurations
#### Make Your Threaded Code Tunable
Getting the right balance of threads typically requires trial an error. Early on, ﬁnd ways to
time the performance of your system under different conﬁgurations. Allow the number of threads to be easily tuned. Consider allowing it to change while the system is running.
Consider allowing self-tuning based on throughput and system utilization.
#### Run with More Threads Than Processors
Things happen when the system switches between tasks. To encourage task swapping, run
with more threads than processors or cores. The more frequently your tasks swap, the more
likely you’ll encounter code that is missing a critical section or causes deadlock.
#### Run on Different Platforms
Run your threaded code on all target platforms early and often.
#### Instrument Your Code to Try and Force Failures
The reason that threading bugs can be infrequent, sporadic, and hard to repeat, is that
only a very few pathways out of the many thousands of possible pathways through a vul-
nerable section actually fail. So the probability that a failing pathway is taken can be star-
tlingly low. This makes detection and debugging very difﬁcult.
