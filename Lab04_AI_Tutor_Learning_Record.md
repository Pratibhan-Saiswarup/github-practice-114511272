# AOOP 2026 — Lab 04 AI Tutor Learning Record

## Topic
C++ References, Encapsulation, Constructors, Inheritance, Virtual Functions, and Dynamic Memory

## Part A: True or False

### 1. Check My Understanding

**Question 1:** True or False: If a function parameter is written as `double &v`, changing `v` inside the function can change the original variable passed into the function.

**Answer:** True.

**Reason:** `v` is a reference to the original variable instead of a separate copy.

---

**Question 2:** True or False: A `private` data member can be changed directly by any code outside the class.

**Answer:** False.

**Reason:** Outside code must use the class's public interface instead of directly accessing a private member.

---

**Question 3:** True or False: If a derived class uses `override`, its function can have different parameters from the virtual function in the base class.

**First answer:** True.

**AI hint:** If the parameter list is different, is C++ still replacing the same base-class function?

**Revised answer:** False.

**Reason:** The derived function must correctly match the virtual base-class function. `override` lets the compiler detect a mismatch.

---

**Question 4:** True or False: Memory created with `new double[n]` should be released using `delete p`.

**First answer:** True.

**AI hint:** Does array allocation with `new[]` use the same form of `delete` as a single object?

**Revised answer:** False.

**Reason:** `new[]` must be paired with `delete[]`.

---

**Question 5:** True or False: If a `BaseApp*` points to a `MyApp` object and `Iterate()` is virtual, calling `app->Iterate()` can run `MyApp::Iterate()`.

**Answer:** True.

**Reason:** A virtual function uses the actual object type to select the overridden implementation at runtime.

### Questions completed
5 / 5

### Answers revised after AI hints
2 / 5

---

## 2. My Misconception

**Before: I thought…**

`override` could still work even if the derived function was slightly different from the base-class virtual function, and I thought `delete` and `delete[]` were interchangeable.

**Now: I understand…**

An overridden function must correctly match the base-class virtual function, and memory created with `new[]` must be released with `delete[]`.

---

## 3. Challenge the AI

**One AI-generated question I challenged:**

“True or False: A `private` data member can be changed directly by any code outside the class.”

**Why?**

- [ ] Ambiguous
- [ ] Oversimplified
- [ ] Technically questionable
- [x] Too easy
- [ ] Other

**Brief explanation:**

The meaning of `private` was directly explained in the lecture, so the answer did not require much reasoning. A harder question could ask how a class can safely allow outside code to update private data.

---

## 4. One-Minute Reflection

**One thing I am still unsure about:**

I am still unsure about exactly how `vptr` and `vtable` are used internally when a virtual function is called.

---

# Part B: LeetCode-style Lecture Code Transfer

## 1. Today’s Challenge

**Core concept from today’s OCW lecture:**

Using references to modify original variables, encapsulating data in classes, and using inheritance with virtual functions.

**AI-generated coding challenge title:**

Smart Device Status Tracker

### Problem statement

Create a base class called `Device` with these pure virtual functions:

```cpp
virtual std::string Name() const = 0;
virtual bool Update() = 0;
virtual int Count() const = 0;
```

Create a derived class called `Sensor` that:

- stores a private integer counter,
- starts the counter at `0`,
- returns `"Sensor"` from `Name()`,
- increases the counter by `1` whenever `Update()` is called,
- returns `true` from `Update()`,
- returns the current counter from `Count()`.

Also create:

```cpp
void limit_value(int &value, int min, int max);
```

This function must modify the original value so that it stays between `min` and `max`.

### Input/output specification

There is no keyboard input.

The program should create a `Sensor`, call `Update()` several times, and use `Count()` to verify how many updates occurred.

`limit_value()` modifies the original integer passed to it.

### Constraints

- The counter starts at `0`.
- `limit_value()` must use a reference.
- `Sensor` must inherit publicly from `Device`.
- The three virtual functions in `Sensor` must use `override`.
- Use only concepts covered in the lecture.

### Examples

**Example 1**
```text
Starting count: 0
Update called 3 times
Final count: 3
```

**Example 2**
```text
value = 150
min = 0
max = 100

After limit_value:
value = 100
```

**Example 3**
```text
value = 50
min = 0
max = 100

After limit_value:
value = 50
```

---

## 2. My Initial Approach — Before AI Help

I planned to create the `Device` base class first, then create `Sensor` as a derived class with a private counter. `Update()` would increase the counter, `Count()` would return it, and `Name()` would return `"Sensor"`. For `limit_value()`, I would use a reference so the original variable could be changed.

---

## 3. AI Tutor Help

**Did you ask the AI Tutor for help?**

- [ ] No — I solved it independently
- [x] Yes — I received one or more hints

**The most useful hint/question from AI was:**

“What has to match between the virtual function in the base class and the function marked `override` in the derived class?”

**It helped me realize that:**

The derived function must match the base-class virtual function correctly, including its parameters and `const` qualifier.

---

## 4. My Revision

**Did you change your approach or code after interacting with AI?**

- [ ] No
- [x] Yes

**What did you change, and why?**

I checked the signatures of my overridden functions and made sure `Name()` and `Count()` included `const`. I also used `override` on all three functions so the compiler could check them.

---

## 5. Verification

My final program:

- [x] Passed the provided examples
- [x] Passed additional edge cases
- [ ] Still has unresolved problems

**One edge case I tested:**

Input:
```text
value = -10
min = 0
max = 100
```

Expected output:
```text
0
```

Actual output:
```text
0
```

---

## 6. One-Minute Reflection

**What idea from the OCW lecture did you transfer to this new problem?**

I transferred the use of references to modify the original variable and the use of inheritance and virtual functions to give a derived class its own behavior.

**One thing I understand better now:**

I understand why `override` is useful because the compiler can check whether my derived function really matches a virtual base-class function.

**One thing I am still unsure about:**

I am still unsure about exactly how C++ uses `vtable` and `vptr` internally during virtual function calls.
