# Garbage Collection in Java

## What is Garbage Collection?
Garbage Collection (GC) is an automatic memory management mechanism in Java that removes objects from memory when they are no longer needed by the program.

In Java, objects are created dynamically during runtime and stored in heap memory.

```java
Student s = new Student();
```

If unused objects were never removed, memory would keep filling up and the application could eventually crash due to lack of memory.

---

# Why is it needed?
Garbage Collection is needed to:

- Free unused memory automatically
- Prevent memory leaks
- Improve memory utilization
- Reduce programmer burden
- Make Java programs safer and more reliable

Without garbage collection, programmers would need to manually free memory like in C/C++.

---

# Why is it called “automatic”?
It is called automatic because the JVM (Java Virtual Machine) itself handles memory cleanup.

The programmer does not manually delete objects.

In C/C++:

```c
free(ptr);
```

In Java:

```java
Student s = new Student();
s = null;
```

The JVM automatically decides:

- when memory should be cleaned
- which objects are unused
- when to remove them

This automatic cleanup system is called Garbage Collection.

---

# Real meaning of “reachable”
An object is considered reachable if it can still be accessed through some active reference.

Example:

```java
Student s = new Student();
```

Memory representation:

```text
s ───► Student Object
```

The object is reachable because the reference variable `s` points to it.

The JVM checks reachability using references like:

- local variables
- instance references
- static references
- active threads

If no active reference can access the object anymore, the object becomes unreachable.

---

# Eligible for Garbage Collection
An object becomes eligible for garbage collection when no live reference points to it anymore.

Example:

```java
Student s = new Student();
s = null;
```

Now:

```text
s = null

Student Object ← no reference
```

Since no reference can access the object now, it becomes eligible for garbage collection.

---

# Eligible does NOT mean: immediately deleted
A very important point:

Eligible for garbage collection does NOT mean the object is instantly removed from memory.

It only means:

> The JVM is now allowed to remove the object whenever required.

The JVM decides the actual cleanup timing based on:

- memory requirements
- JVM optimization
- system performance

So garbage collection happens during runtime, but not at a fixed time.

---

# Reassigning references
An object can also become eligible when its reference is reassigned.

Example:

```java
Student s = new Student();
s = new Student();
```

Step 1:

```text
s ───► Object1
```

Step 2:

```text
s ───► Object2
```

Now no reference points to Object1.

So Object1 becomes eligible for garbage collection.

---

# Important Difference

## Garbage Value vs Garbage Collection

### Garbage Value
A random uninitialized memory value.

Java generally prevents this.

### Garbage Collection
Automatic removal of unused objects from memory.

These two concepts are completely different.

---

# Final Summary

- Garbage Collection is automatic memory cleanup in Java.
- It happens during runtime, not compile time.
- JVM removes objects that are no longer reachable.
- Objects first become eligible for garbage collection.
- Eligible does not mean immediately deleted.
- Java handles memory management automatically, making programs safer and easier to manage.