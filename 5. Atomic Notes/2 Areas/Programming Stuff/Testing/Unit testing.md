2025-09-13 22:06
Status: 
Topic: 
Tags: [[testing]]
## Main

### Terminology

| **Term**                          | **Definition**                                                         | **Example (Java / JUnit 5)**                                                                |
| --------------------------------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Unit**                          | Smallest piece of code you test (usually a method or function).        | `int add(int a, int b) { return a + b; }`                                                   |
| **Test Case**                     | A single test that verifies one behavior.                              | `java @Test void testAdd() { assertEquals(5, add(2, 3)); }`                                 |
| **Test Suite**                    | A collection of related test cases.                                    | `java class CalculatorTest { @Test void testAdd() {...} @Test void testSubtract() {...} }`  |
| **Assertion**                     | Statement that checks expected vs actual result.                       | `assertEquals("Positive", classify(5));`                                                    |
| **Fixture**                       | Setup/teardown code before and after tests.                            | `java @BeforeEach void setup() { calc = new Calculator(); }`                                |
| **Mock**                          | A fake object that mimics real dependencies and verifies interactions. | `java PaymentService mock = mock(PaymentService.class); when(mock.pay()).thenReturn("OK");` |
| **Stub**                          | A simple fake object that just returns fixed data (no verification).   | `java class StubService { String getData() { return "stub"; } }`                            |
| **Coverage**                      | % of code executed by tests (statement, branch, path).                 | Tools: JaCoCo, IntelliJ coverage.                                                           |
| **Regression Test**               | Ensures old functionality still works after changes.                   | Old tests kept running when code is updated.                                                |
| **TDD (Test-Driven Development)** | Write test → write code → refactor.                                    | Write `testAdd()`, see it fail, then implement `add()`.                                     |

### Rule of Thumb to write Unit Test

### 1. **Start with Critical Code**

- Don’t aim for 100% coverage everywhere (waste of time).
    
- Focus on code that:
    
    - Contains **business logic** (rules, calculations).
        
    - Is **error-prone** (conditions, loops, data transformations).
        
    - **Interfaces with external systems** (database, API, file).
        

👉 Skip trivial getters/setters unless they contain logic.

### 2. **Think in Terms of Branches**

- For every **decision point (`if`, `switch`, `? :`)**, test all possible outcomes.
    
- This ensures **branch coverage**, which is much more valuable than line coverage.

```java
public String classify(int x) {
    if (x > 0) return "Positive";
    else if (x < 0) return "Negative";
    else return "Zero";
}
```

✅ Write 3 tests: `classify(5)`, `classify(-3)`, `classify(0)`.


### 3. **Use the AAA Pattern (Arrange–Act–Assert)**

Keep your test structure simple and clear:

1. **Arrange** → set up objects/data.
    
2. **Act** → call the method.
    
3. **Assert** → check the result.

```java
@Test
void testAdd() {
    // Arrange
    Calculator calc = new Calculator();
    // Act
    int result = calc.add(2, 3);
    // Assert
    assertEquals(5, result);
}
```

### 4. **Test Edge Cases, Not Just Happy Paths**

- Normal input (expected use).
    
- Edge/boundary values (`0`, empty string, max/min values).
    
- Invalid input (exceptions, nulls, out-of-range).

### 5. **Use Mocks/Stubs to Isolate**

- Don’t hit real databases or APIs in unit tests.
    
- Use **mocks/stubs** to control inputs and outputs.
    
- Example: a fake `PaymentService` that always returns "OK".

### 6. **Measure Coverage (but Don’t Worship It)**

- Use tools like **JaCoCo (Java)**, **pytest-cov (Python)**, or IDE built-in coverage.
    
- Good rule of thumb:
    
    - **70–80%+ coverage** is usually "enough".
        
    - Aim higher (90%+) for core logic.
        
    - Don’t waste effort trying to test trivial code just to hit 100%.

### 7. **Regression Safety Net**

- Keep old tests — they make sure new changes don’t break old behavior.
    
- If a bug appears, **first write a test that reproduces it**, then fix it.
    
- That test stays forever to prevent the bug from coming back.

## 🛠️ Example Workflow

1. Write a failing test for a new feature (TDD style if you like).
    
2. Implement code → make the test pass.
    
3. Add extra tests for edge cases & branches.
    
4. Run coverage → see what’s missing.
    
5. Add tests only if the uncovered parts are **important logic**.

## 🚦 Quick Formula for "Enough Coverage"

- Cover **all branches of logic**.
    
- Cover **happy path + edge cases**.
    
- Cover **critical classes >90%**.
    
- Cover **utility/boilerplate classes ~50-60%** (don’t force it).


# ⚡ Common Edge Cases You Should Always Think About

### 1. **Numerical Boundaries**

- `0`, negative numbers, max/min integer/long/double values.
    
- Example: `divide(10, 0)` → should throw exception.
    

### 2. **Empty Inputs**

- Empty list/array, empty string.
    
- Example: `sum([])` → should return 0, not crash.
    

### 3. **Null / Optional**

- Passing `null` when a value is expected.
    
- Using `Optional.empty()` properly.
    

### 4. **Single Element**

- One item in a list/string (off-by-one bugs).
    
- Example: `max([5])` → should return 5.
    

### 5. **Duplicates**

- Input with repeated values.
    
- Example: `set([1,1,1])` → should handle gracefully.
    

### 6. **Special Characters / Formats**

- Strings with spaces, Unicode, emojis, special symbols.
    
- Example: `" hello "` → trimming?
    

### 7. **Large Inputs**

- Very large collections or max-size strings.
    
- Example: `sort(1_000_000 elements)` → should not timeout.
    

### 8. **Ordering**

- Already sorted vs reverse-sorted inputs.
    
- Example: `binarySearch(sortedArray)` vs unsorted.
    

### 9. **Concurrency / Timing (advanced)**

- Multiple threads using same function.
    
- Delays, timeouts, clock edge cases (e.g., end of month).
    

### 10. **Configuration/Defaults**

- What happens if user doesn’t pass a parameter?
    
- Example: default values vs explicit ones.

# ✅ Unit Test Coverage Checklist

Before you say “done” with testing a function/method, ask:

1. **Happy Path**
    
    -  Does it work with normal/expected input?
        
2. **Branch Coverage**
    
    -  Did I test _all possible outcomes_ of `if/else` / `switch` / ternary conditions?
        
3. **Edge Cases**
    
    -  Did I test boundary values (0, min, max)?
        
    -  Did I test empty collections/strings?
        
    -  Did I test null or optional values?
        
4. **Error Handling**
    
    -  Does it throw the right exception for bad input?
        
    -  Do I test recovery/alternative flows?
        
5. **Regression**
    
    -  If I fix a bug, do I add a test so it never happens again?
        
6. **Isolation**
    
    -  Do I use mocks/stubs for external dependencies (DB, API, filesystem)?
        
7. **Coverage Goal**
    
    -  Is coverage ≥ 80% overall?
        
    -  Is coverage ≥ 90% for critical logic?
## References