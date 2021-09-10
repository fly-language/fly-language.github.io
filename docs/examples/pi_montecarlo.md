---
layout: default
title: Pi Montecarlo
parent: Examples
nav_order: 5
---
# Pi estimation algorithm with Monte Carlo method

### Monte Carlo Pi estimation
Pi estimation in one of the main examples of Monte Carlo algorithm. The idea is to simulate random (x, y) points in a 2-D plane with domain as a square of side 1 unit and then to calculate the ratio of number points that lied inside a circle inscribed into the square and total number of generated points.

## How to run
In order to correctly run the algorithm, there are some rules that must be respectes:
* The values of the variable __nthread__ in the environment declararion, the upper bound of the cycle on the variable __i__ in the __estimation__ function and the upper bound in the fly function invocation must be equal.
* The value of __nThread__ must be greater than 0.
* There are multiple declaration of the __cloud__ environment, one for each supported Cloud Provider. Only one of them could not be commented.

## Functions

The program is composed by two functions:

* **[Pi Function](#pi-function)**
* **[Estimation Function](#estimation-function)**
  
### Pi Function 

The pi function can be executed locally or serverless. After generating some random values, it sends an integer on the __ch__ channel. The value sent on __ch__ is 1 if the generated point is into the circle, otherwise it's 0.
The Fly code is the following:

```
func pi(){	
   var r = [type="random"]
   var x = r.nextDouble()
   var y = r.nextDouble()
   var msg = 0
 
   if((x * x)+(y * y) < 1.0){msg = 1}
   ch!msg on cloud
}
```

### Estimation Function 

The estimation function collects the values sent on the __ch__ channel and estimates the value of pi. The __crt__ variable represents the number of generated points, while __sum__ represents the number of points into the circle.
The Fly code is the following:

``` 
  func estimation(){
   var sum = 0
   var crt = 0
   for i in [0:10] {
       sum += ch? as Integer
       crt += 1
   }
   println "pi estimation: " + (sum*4.0) / crt
}
```

