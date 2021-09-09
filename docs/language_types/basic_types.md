---
layout: default
title: Basic Types
nav_order: 1
parent: Language Types
---

# Basic Types
{:.no_toc}

## Table of Contents 
{: .no_toc .text-delta }
1. TOC
{:toc}

---

## Overview

FLY provides a set of types named _basic types_. Basic types are inherted by Java, and comprises boolean, integer, real (double point precision float) and string.
Moreover, FLY supports one/bi/three-dimensionale array definition for basic types.

## Atomic Types

An atomic type is a basic type on which other basic types relies.
The following table contains all FLY's atomic types and its literals.

|Type|Literal|Examples|
|:---:|:---:|:---:|
|_Integer_  |Can be any digit, or group of digits followed by a white character. Can be negative.|__1__, __-12__, __392__, __-034__|
|_Boolean_  |Can be __true__ or __false__.|__true__, __false__|
|_Real_     |Can be any decimal digit on wich the integer and decimal separator is the dot character. Can be negative.|__0.134__, __42.594__, __-1.0__|
|_String_   |Can be any kind of character wrapped in a double quotes characters. Can be also the empty string. Moreover, all Java escapes characters are supported.|__""__, __"Hello World!"__, __"c\n\n"__, __"S1t24"__|

Each of those basic types is inherited by Java atomic types (_Real_ matches to _Double_).

## Collections

A _collection_ is just a group of atomic types, that are enclosed in a single variable or literal. Also the _collection_ type in FLY are inherited by Java.

### Array

#### Definition
{:.no_toc}

Array basic type. We have introduced the array type. A Fly array is a collection of __homogeneous__ basic types laid on a tabular form having one, two, or three dimensions. The declaration of an array is described in the following:

```js
var arr = Integer|Real|Boolean|String [N][M][K]
```
where N, M and K are the array dimensions. If one of those dimension is 0, is just need to be omitted in the definition.

Arrays has also a literal definition:

```js
var arr_1d = { 1, 2, 3 }
var arr_2d = { { 1, 2, 3 }, { 10, 20, 30 } }
var arr_3d = { { {1, 2, 3}, { 10, 20, 30 } }, { { 4, 5, 6 }, { 40, 50, 60 } } }
```

#### Access
{:.no_toc}

FLY provides the brackets notation to access to an array element.
```js
println arr_1d[0]
println arr_2d[1][0]
```

Also, arrays indexes can be a left-value of an expression.
```js
arr_1d[0] = 101
arr_2d[0][1] = 241
```

### Map

Fly __maps__ are declared using braces ({…}) and can contains values ​​of heterogeneous types The mapping between object IDs and values are made using the assignment (=) symbol.
For instance:

```js
var ID = {?ID1=VALUE, ?ID2=VALUE, ...}
```

For example:
```js
var map = {n=42, s="Universe Answare"}
```

To access to objects, the brackets notation is needed:
```js
println map[n]
println map[s]
map[n] = "24"
map[s] = "Ciao"
map[new_id] = 24.5
```
We can add new elements to our map even after the declaration.
Moreover the mapping is between a key and an object, so each object doesn't need to be of the same type of the initialization one.

Object ID can be also omitted. In this case can access to that object trhough a positional index key:
```js
var map = {"Hello!", "World!"}
println map[0], map[1]
```

Also we can use either positional index keys, or ID index keys:
```js
var map = {"Hello", n=42, "World!", s="Universe Answare"}
```

## Other Basic Types

FLY provides two more basic types, which are _Datetime_ and _Random_.
Those types are also inherited by Java, even if they are not basic types, FLY manages them as basic types.

### Datetime

TODO

### Random

The __random object__ definitions reminds to Domain Object declaration.
In formal way:
```js
var rand = [type="random"]
```

Random objects can generates random values as the following:
```js
rand.nextBoolean() // generates Booleans
rand.nextDouble() // generates Real numbers
rand.nextInt(MAX RAND) // generates Integer numbers
```