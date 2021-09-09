---
layout: default
title: Control Flow
nav_order: 1
parent: Code Structures
---

# Control Flow
{:.no_toc}

The control flow (or flow of control) is the order in which individual statements, instructions or function calls of an imperative program are executed or evaluated.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Introduction

Since FLY is based on Java, it supports the three main control flow structures of Java, which are: __if/else__, __while__ and __for__.

Each control structure has the main purpose of the Java corrispective, but it's syntax can be different.


__Note.__ _In this guide we are not going to explain the purpose of each control flow structure since it should be already known by the reader._

## Branching with If/Else

The main structure of the *If/Else* control flow structure is as the following:
```js
if (expression) {
    statements
} else if (expression) {
    statements
} else {
    statements
}
```

The _else if_ and the _else_ branches are optional, so can be skipped.

The __expressions__ inside the round brackets must return a __Boolean__ value.

## Looping with For

The *for* expression is specified by the following syntax:

```js
for INDEX in OBJECT ?(by DELIMITER) {
    statements
}
```

This structure can be not familiar for Java users, that's why we are going to explain all the components of that structure:
1. **INDEX**: _INDEX_ is just one or more variable which will assume the iteration value of the iterator.
2. **OBJECT**: _OBJECT_ is where the _INDEX_ needs to iterate. _OBJECT_ can be an **array**, a **map**, a **dataframe**, or a **range object** (later on we will explain the range object).
3. **DELIMITER**: the DELIMITER can assume three different values, which are **row**, **col** or **delimiter** followed by a string. Essentially, a delimiter tells how the _OBJECT_ must be iterated by the _INDEX_.

### Range Object
{:.no_toc}

A range object is just a simple way to iterate over a range of values.
The syntax of a range object literal is the following `[V1 : V2]`
where V1 and V2 can be **Integers** variable, constants or literals.

### Examples
{:.no_toc}

The following example shows how to iterate an houndred times over the index i:
```js
for i in [0:100] {
    println i
}
```

The following example shows how to iterate over an array:
```js
var arr = {1, 2, 3, 4, 5}

for i in arr {
    println i
}
```

The following example shows how to iterate over a dataframe given a certain delimiter:
```js
var dat = [type="dataframe", ...]

for i in dat by row {
    println i
}
```

## Looping with While

A *while* expression is defined by the following syntax:

```js
while (condition) {
    statements
}
```

*While* expression doesn't need examples since is simple as it seems.