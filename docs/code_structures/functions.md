---
layout: default
title: Functions
nav_order: 2
parent: Code Structures
---

# Functions
{:.no_toc}

Functions are one of the main aspects of FLY, so let's see how they work.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Introduction

FLY functions are quite different from other scripting languages and follow a functional programming inspired definition. A FLY function represents a task or independent job of the main program and it is defined as a code block that can be executed concurrently.

## Function Declaration

FLY functions are declared using the keyword `func`. Each FLY function can have a set of input parameters and may return a value using the keyword `return`. FLY functions have a private scoping, that is only function parameters and local variable are visible in the body of the function. 

```js
func sum(a, b) {
    return a * b
}
```

## Passing parameters

The input parameters are **passed by copy**, and they are considered as immutable. However, functions can avoid those limitations using *channels* or *constants*. A  *channel* declared in the main program or in a function running on the same environment can be directly used by a function; the same behavior is also defined for the *constants*.

## Invocation

Notice that, the FLY language does not ensure that operations are admitted: if a function is executing on a back-end B, the function can use only channels and objects available on the back-end B. FLY functions can be executed, like for standard languages, using their ID and parameters (in this case functions are executed sequentially). 

```js
var a = 5
var b = 3

println sum(a, b)
```
```
>>> 8
```

## Concurrency

In order to execute functions concurrently, FLY provides the `fly` statement that will be described in the following. The `fly` statement is not admitted in the body of a function (i.e., recursion is not allowed).
