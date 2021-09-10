---
layout: default
title: OneMaxProblem
parent: Examples
nav_order: 2
---
# One Max Problem Genetic Algorithm 

### One Max Problem
One Max Problem, also known as "the problem of the max binary vector generation", is a well-known problem in the branch of genetic algorithms.
The purpose of this algorithm is to generate a vector with every element set to 1.

## How to run
In order to correctly run the genetic algorithm, there are some rules that must be respectes:
* The values of the variable __nthread__ and its counterpart in the environment declaration (the __cloud__ variable) must be equal.
* The value of __tournamentSize__ must be less than __dimension__'s one.
* The value of __nThread__, __dimension__, __individualLength__, __tournamentSize__ and __resultSize__ must be greater than 0.
* Each other variable must not be changed.

## Functions

The program is composed by five principal functions:

* **[Initialization Function](#initialization-function)**
* **[Fitness Function](#fitness-function)**
* **[Selection Function](#selection-function)**
* **[Crossover Function](#crossover-function)**
* **[Mutation Function](#mutation-function)**

### Initialization Function 

The initialization function initialize the __population__ with random values between 0 and 1.
The Fly code is the following:

```
func initPopulation(){
	var newPop = Integer[dimension][individualLength]
	population= newPop
	var rand = [type="random"]
	
	for i in [0:dimension]{
		for j in [0:individualLength]{
			var value = 0
			value = rand.nextInt(2)
			
			if(value < 0){
				value = value * -1
			}
			
			population[i][j]= value
		}
	}
}
```

### Fitness Function 

The fitness function evaluates each individual in __population__ or in __newIndividuals__. The evaluation of an individual is the sum of the values of its genes. The function in written in JavaScript.
The code is the following:

``` javascript
  func fitness(populationMatrix){
	native<<<
	console.log(event.data[0])
	var resultJSON = "[" + submatrixIndex + ", " + __populationMatrix_rows + ", "
	
	for(var __i = 0; __i < __populationMatrix_rows; __i++){
		var fitnessValue = 0
		for(var __j = 0; __j < __populationMatrix_cols; __j++){
			if(populationMatrix[__i][__j] == 1){
				fitnessValue += 1
			}
		}
		resultJSON += "" + fitnessValue
		
		if(__i >= 0 && __i < __populationMatrix_rows - 1){
    			resultJSON += ", "
    		}
	}
	
	resultJSON += "]";
	console.log("Result: " + resultJSON)
	__data = await __sqs.getQueueUrl({ QueueName: "ch-'${id}'"}).promise();
		
	__params = {
		MessageBody : JSON.stringify(resultJSON),
		QueueUrl : __data.QueueUrl
	};
		
	__data = await __sqs.sendMessage(__params).promise();
	__data = await __sqs.getQueueUrl({ QueueName: "termination-'${function}'-'${id}'"}).promise();
	>>>
}
```
This funcition is made to evaluate a portion of individuals in a serverless environment. For this reason, results are formatted in a Json string, containing also the number of evaluated individuals and the __submatrixIndex__ number. Results are sent to the client over a channel, ordered by __submatrixIndex__ number and assigned to each evaluated individual.

### Selection Function 

The selection function selects the individuals which can access the crossover phase. The Tournament Selection creates torunaments with __tournamentSize__ different individuals randomly picked from the __population__ and select the best individual, the one with the best fitness. The winner of the tournament is inserted in the __champions__ pool, which is used for the crossover.
The Fly code is the following:

```
func tournamentSelection(){
	var selectedIndividual = -1
	var rand = [type="random"]
	
	var tournament = Integer[tournamentSize]
	
	for j in [0:tournamentSize]{
		var element = 0
		element = rand.nextInt(dimension)
		
		if(element < 0){
			element = element * -1
		}
		
		tournament[j] = element
		
		for i in [0:tournamentSize]{
			if(i != j){
				if(tournament[i] == tournament[j]){
					tournament[j] = -1	
				}
			}
		}
		
		if(tournament[j] == -1){
			j = j - 1
		}
	}
	
	var best = 0
	best = tournament[0]
	
	for j in [1:tournamentSize]{
		if(populationFitness[j] > populationFitness[best]){
			best = tournament[j]
		}
	}
	
	selectedIndividual = best
	return selectedIndividual
}
```

### Crossover Function 

The crossover function combines the genes of two individuals in order to generate one or more new individuals. The One Point Crossover cuts __parent1__ and __parent2__ in two parts, using a randomly generated __crossoverPoint__. Every execution of this function generates two new individuals, __child1__ and __child2__, by swapping the cut parts.
The Fly code is the following:

```
func onePointCrossover(){
	var rand = [type="random"]
	var crossoverPoint = 0
	crossoverPoint = rand.nextInt(individualLength - 1)
	
	while(crossoverPoint == 0){
		crossoverPoint = rand.nextInt(individualLength - 1)
	}
	
	if(crossoverPoint < 0){
		crossoverPoint = crossoverPoint * -1
	}
	
	var p1 = Integer[individualLength]
	var p2 = Integer[individualLength]
	
	for i in [0:individualLength]{
		p1[i] = population[parent1][i]
	}
	
	for i in [0:individualLength]{
		p2[i] = population[parent2][i]
	}
	
	var last2= Integer[individualLength - crossoverPoint]
	var n = 0
	for i in [crossoverPoint:individualLength]{ //Swap 1
		last2[n] = p2[i]
		n++
		p2[i] = p1[i]
	}
	
	var first1 = Integer[crossoverPoint]
	n = 0
	for i in [0:crossoverPoint]{ //Swap 2
		first1[n] = p1[i]
		n++
		p1[i] = p2[i]
	}
	
	n = 0
	var m = 0
	for i in [0:crossoverPoint]{
		if(i < crossoverPoint){
			p2[i] = first1[n]
			n++
		}
		else{
			p2[i] = last2[m]
			m++
		}
	}
	
	for i in [0:individualLength]{
		child1[i] = p1[i]
		child2[i] = p2[i]
	}
}
```

### Mutation Function 

The mutation function randomly changes values in the gene pool of an individual. The Gaussian Mutation is completely based on the probability, in fact it uses the __mutationChance__ variable to decide if a determined gene will be changed or not. Moreover, the access to the mutation process is determined by the value of another randomly generated variable, the __mutationProbability__.
The Fly code is the following:

```
func gaussianMutation(){
	var rand = [type="random"]
	
	for i in [0:individualLength]{
		var mutationChance = 0
		mutationChance = rand.nextInt(2)
		
		if(mutationChance < 0){
			mutationChance = mutationChance * -1
		}
		
		if(mutationChance > 0){
			if(toMutate[i] == 1){
				toMutate[i] = 0
			}
			else{
				toMutate[i] = 1
			}	
		}
	} 
}
```

