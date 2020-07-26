
---

**Travelling Salesman Problem using Genetic Algorithm**

---

A basic implementation of genetic algorithm for traveling salesman problem


**Introduction**
Travelling salesman problem is a combinatorial optimization problem. Which in terms of problem classification falls into NP-hard problem. A general problem of TSP is "Given a list of cities and the distances between each pair of cities, what is the shortest possible route that visits each city and returns to the origin city?". Here we will be solving this problem using a genetic algorithm in python. 
It's kind of basic implementation of genetic algorithm.

First task to import libraries.
```python
import numpy as np, random, operator, pandas as pd
import matplotlib.pyplot as plt
```
Creating CityList i.e (X, Y) for every city
```python
cityList = []
for i in range(0,25):
    x=int(random.random() * 200)
    y=int(random.random() * 200)
    cityList.append((x,y))
```
From here the genetic algorithm starts
1. Creating a starting population of solution. In order to create a starting population, we need to create individual members.

```python
def create_starting_population(size,Number_of_city):
    '''Method create starting population 
    size= No. of the city
    Number_of_city= Total No. of the city
    '''
    population = []
    
    for i in range(0,size):
        population.append(create_new_member(Number_of_city))
        
    return population
 ```
2. Now ranking the routes i.e finding the best fit. Fitness function is being used to find the fitness of an individual route.
```python
def fitness(route,CityList):
    '''Individual fitness of the routes is calculated here
    route= 1d array
    CityList = List of the cities
    '''
    #Calculate the fitness and return it.
    score=0
    #N_=len(route)
    for i in range(1,len(route)):
        k=int(route[i-1])
        l=int(route[i])

        score = score + distance(CityList[k],CityList[l])
        
        
    return score
def rankRoutes(population,City_List):
    fitnessResults = {}
    for i in range(0,len(population)):
        fitnessResults[i] = fitness(population[i],City_List)
    return sorted(fitnessResults.items(), key = operator.itemgetter(1), reverse = False)
```
3. Selecting the best fit among the population.
```python
def selection(popRanked, eliteSize):
    selectionResults=[] 
    result=[]
    for i in popRanked: 
        result.append(i[0])
    for i in range(0,eliteSize):                                                                                                                                         selectionResults.append(result[i])
 return selectionResults
```
4. Creating a mating pool so that the best individual among the population can breed and produce a better solution.
```python
def matingPool(population, selectionResults):
    matingpool = []
    for i in range(0, len(selectionResults)):
        index = selectionResults[i]
        matingpool.append(population[index])
    return matingpool
 ```   
5. Making them breed to produce offsprings.
```python
def breedPopulation(mating_pool):
    children=[]
    for i in range(len(mating_pool)-1):
                children.append(crossover(mating_pool[i],mating_pool[i+1]))
    return children
 ```
6. Mutation of population
```python
def mutatePopulation(children,mutation_rate):
    new_generation=[]
    for i in children:
        muated_child=mutate(i,mutation_rate)
        new_generation.append(muated_child)
    return new_generation
 ```
7. Finally, we have one generation of routes. Repeat it until the solution converges.
I have provided the necessary function that is required for a genetic algorithm.
Full Notebook of the code is available  [Link](http://github.com/avitomar12/TSP-using-Genetic-Algorithm)

Article about the notebook is published on https://medium.com/thecyphy/travelling-salesman-problem-using-genetic-algorithm-130ab957f165

