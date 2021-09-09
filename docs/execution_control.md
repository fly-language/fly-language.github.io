---
layout: default
title: Execution Control
nav_order: 5
---

# Execution Control
{:.no_toc}

FLY has a lot of different tools to execute functions and blocks of code in different ways. Concurrency, 
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---

## Parallel or Distributed Statements

The definition of FLY functions is the consequence of the explicit parallel execution model of FLY. The language provides the keyword `fly` that enables the user to execute concurrently a set of functions (the number of concurrent functions will depend on the back-end used and the user needs).

The `fly` statement is similar to the `for` statement but the fly statement allows to specify the back-end environment (using the keyword `on`) and, possibly, callback functions.

```js
fly ID in [x:y]|Object|File on Env then ID thenall ID
```

The `fly` statement supports two kinds of function callbacks, declared using the keywords **then** and **thenall**. The *then* callback is executed after each FLY function execution, instead the *thenall* callback is executed after all FLY function executions.
*Then* and *thenall* functions have to take only one input parameter that, for *then* corresponds to the return value of a function execution, while for *thenall* is a FLY  object containing all the return values obtained by all the function executions.

## Asynchronous Execution

FLY explores synchronous and asynchronous execution models. The previous construct defines the synchronous mode, in which the main program waits all functions termination. It is possible to execute functions asynchronously using the keyword `async` before the fly construct.

The async statement returns a special FLY object, named *async-object*, that enables the user to control and interact with the asynchronous execution. 
The `async` FLY constructor invocation immediately returns the control to the main program and the execution can continue. 
The user can control the status of the asynchronous functions invoking the method `status()` on the *async-object* and can wait the termination of all functions using the method `wait()`.

## Types Casting

FLY uses a dynamic type checking, that is variable types are automatically inferred at run time during the first assignment. Moreover, FLY typing is strong, the type of a variable cannot change during the execution time. 
FLY provides support for explicit types casting as in Java and C#. 
Types casting is admitted on basic and domain types, but it is forbidden on environments and channels.

Casting is performed by the keyword `as` followed by the type into be casted.

```js
... // Environments and other stuff initialization
var ch = [type="channel"] on Local

var value = ch? as Integer
```

**Note.** *After getting a value from a channel, it has to be casted. That's because fly can't access to the original type of that value.*

## Native Code

The **native** statement, defined by the keyword `native`, enables the programmers to invoke directly native code in the Fly
functions.

```js
native<<<
    console.log("Hello World!")
>>>
```

FLY is also able to include external libraries (using the keyword `require`, which enables to include and install, in the selected environment, an additional library) and supports the execution of native code (using the keyword `native`). 
For instance, the FLY functions running on the aws back-end are translated in Javascript or Python, which means that it is possible to include in these functions all JS and Python libraries.
