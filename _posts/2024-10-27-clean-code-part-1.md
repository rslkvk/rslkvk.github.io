---
layout: post
title: Clean Code Series Part 1 - Encapsulating State Getters vs. Fields Access
description: Deep dive into accessing data
tags: [java, clean code, spring, testing]
---

### Encapsulating State in Clean Code: When to Use Getters vs. Direct Field Access

In object-oriented programming, Clean Code principles encourage writing code that’s easy to read, maintain, and extend. One key aspect of this is **encapsulation**—keeping a class’s internal data private and accessing it through well-defined methods. However, this often leads to a practical question:

> When should I use a getter method to access a field instead of directly accessing it?
> 

This article explores the principles behind this decision, why getters can be the better approach, and when to access the field directly. We'll go through examples to show the benefits of using getters for encapsulation, testability, and consistent state management.

---

### Why Use Getters Instead of Direct Field Access?

Getters offer a layer of abstraction between a class’s internal fields and the outside world. By encapsulating state access within a getter, you control how data is exposed and create a single, consistent access point for the value.

Here are some reasons why this approach aligns with Clean Code:

1. **Encapsulation and Information Hiding**: Hiding the internal representation of data in a class prevents external code from depending on specific implementation details, which can change over time.
2. **Consistency and Readability**: Using getters consistently promotes a predictable access pattern. Developers reading the code can expect to retrieve values via methods rather than directly accessing variables, which makes intent clearer.
3. **Testability and Flexibility**: Testing becomes more straightforward with getters. Mocking frameworks allow us to stub out methods (like a getter) without exposing the field directly, making it easier to simulate different states.

---

### Example 1: Accessing a Field Directly vs. Using a Getter

Imagine we have a class, `MyClass`, with a boolean field `flagOk`, representing whether certain conditions are met. This flag could be used internally by `MyClass` and also accessed externally.

### Direct Access Approach

In a direct access approach, you would refer to `flagOk` directly within the class and potentially even expose it directly to other classes:

```java
public class MyClass {
    private final boolean flagOk = true;

    public void callSomeMethod(boolean checkFirst) {
        if (checkFirst) {
            new AnotherClass().someMethod(flagOk);  // Direct field access
        }
    }
}

```

This approach works, but it has some downsides:

- If you later add logic to `flagOk` (e.g., dynamically changing it), the direct reference could result in unpredictable behavior.
- Testing becomes less flexible since you’re directly tied to the field without an intermediate layer (like a method) to mock or modify.

### Encapsulated Access with a Getter

Now, let’s modify `MyClass` to use a getter method for `flagOk`:

```java
public class MyClass {
    private final boolean flagOk = true;

    public boolean isOk() {
        return flagOk;
    }

    public void callSomeMethod(boolean checkFirst) {
        if (checkFirst) {
            new AnotherClass().someMethod(isOk());  // Using the getter method
        }
    }
}

```

By using `isOk()`:

- We **encapsulate** access to `flagOk`. If the flag’s internal representation changes, we only need to modify `isOk()`.
- The code is **consistent**. Internally and externally, we access the flag through `isOk()`, making the code more readable.
- **Testing** is easier. If `isOk()` requires special conditions, we can mock or stub this method in tests to simulate different outcomes.

---

### Example 2: Encapsulation for Future Flexibility

Imagine a scenario where `flagOk` may need to change based on complex logic rather than staying constant. With a getter, you can make that change seamlessly without impacting other code that depends on `flagOk`.

Let’s update `MyClass` to include dynamic logic in `isOk()`:

```java
public class MyClass {
    private final boolean flagOk;

    public MyClass(boolean initialFlag) {
        this.flagOk = initialFlag;
    }

    public boolean isOk() {
        // Some additional logic can be added here in the future
        return flagOk;
    }

    public void callSomeMethod(boolean checkFirst) {
        if (checkFirst) {
            new AnotherClass().someMethod(isOk());  // Using the getter, as flagOk logic may change
        }
    }
}

```

In this example:

- **Future-proofing**: If `isOk()` later needs conditional logic, all calls to it will automatically apply this logic. No code changes are required in places where `isOk()` is called, which helps maintain consistent behavior.
- **Simplicity**: By keeping complex logic centralized in `isOk()`, you prevent duplication of logic elsewhere, reducing maintenance efforts.

---

### Testing Example: Benefits of Using Getters

Suppose you’re testing `MyClass` and want to simulate different states of `flagOk`. If you access `flagOk` directly, your test will need to rely on the actual field value. With a getter, however, you can mock its response.

Here’s a test example using Mockito:

```java
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

public class MyClassTest {

    @Test
    public void testCallSomeMethod() {
        // Create a mock of MyClass
        MyClass myClass = mock(MyClass.class);
        AnotherClass anotherClass = mock(AnotherClass.class);

        // Stub the behavior of isOk() to return true
        when(myClass.isOk()).thenReturn(true);

        // Call the method
        myClass.callSomeMethod(true);

        // Verify behavior based on the mocked response
        verify(anotherClass).someMethod(true);
    }
}

```

In this example, we **mock** `isOk()` to return `true`, simulating different states without changing `flagOk` directly. This is not only a powerful testing technique but also improves code flexibility, as you’re not bound to a specific field’s value.

---

### Summary

Using getters instead of direct field access aligns with Clean Code principles by promoting encapsulation, information hiding, and consistent state management. Here’s a quick guide to determine when to use getters:

- **Internal Logic or Conditionals**: If the value may change based on additional logic, use a getter to encapsulate that logic.
- **Consistency**: Always use getters for external access to a field, keeping direct access only within the class for performance when the state doesn’t change.
- **Testing**: Getters make it easier to mock or stub states during testing, giving you more control over how the class behaves in different scenarios.

In summary, encapsulating state through getters helps you build modular, adaptable, and testable code—hallmarks of Clean Code.

---

By consistently using getters to encapsulate field access, your code remains more flexible and easier to maintain over time.
