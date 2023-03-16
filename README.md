# Introduction
This repository provides a brief explanation for the Genetic metaheuristic algorithm for solving Travelling Sales Problem (TSP)

# What is TSP?
![tsp](https://co-enzyme.fr/wp-content/uploads/2020/06/tsp.jpg)

The Travelling Salesman Problem is a classic problem in computer science and optimization. In TSP we're trying to find the shortest route that visits a set of cities  only once then return to the starting point again.

# What is the Genetic-Algorithm?
![image](https://user-images.githubusercontent.com/43891138/225488567-b56c214a-6c63-4982-b8bd-5e30c4096768.png)


Genetic Algorithm (GA) is a metaheuristic algorithm that simulates the process of natural selection by evolving a population of solutions to a problem using some operators such as selection, crossover, and mutation, to generate new solutions. The fittest individuals are selected to reproduce and generate offspring in each generation, with the hope of producing better solutions over time.

## Here is the implementation steps (pipeline):
1. We need to initialize the algorithm paramenters:
    - population_size
    - no_of_iterations / generations count (the Stopping Condition)
    - Elitism percentage(k) of population (best k paths/tours)
    - Crossover probability (generate new 2 tours from 2 older tours)
    - Mutation probability (swapping p of the cities in the same tour)
---------------------------------------------------------------------
2. Create class for Tour and City:
    - Tour class has:
        - list of cities
        - fitness score
        - distance/cost
        
    - City class has:
        - city name
        - x coordinate
        - y coordinate
----------------------------------------------------------------------
3. Initialze Population():
    - Generate tour from permutation(). Note: create deepcopy first
    - Calculate the fitness score (list) for the generated tour (1/tour cost)
        - Ex. c1 --->(2) c3 --->(1) c5 --->(6) c2
        - cost = 2 + 1 + 6 = 9  , ===>  so, fitness = 1/9
    - Add the tour to the population
----------------------------------------------------------------------
4. Fitness_evaluation():
    - calculate the cost of the current tour
    - store the cost
    - calculate the fitness (1/cost)
    - store the fitness
----------------------------------------------------------------------
5. Elitism():
    - caculate the number of elitism we're gonna choose based on the percentage
    - select top fittest tours
    - add elite tour to the new generation list (new pop)
----------------------------------------------------------------------
6. tournament_selection():
    - select random k tours
    - choose the fittest
----------------------------------------------------------------------
7. Crossover():  ---> use partial mapped crossover
    - crossover count (note: we will choose from the population except the elitism) so, count = (pop_size - no_of_elite tours)/2
    - iterate over the crossover count:
        - parent1 = tournament_selection()
        - parent2 = tournament_selection()
        - generate random number rn
            - if rn < crossover prob:
                - apply partial mapped crossover on parent1 and parent2
                - evaluate child1 and child2 fitness
                - insert the childerns to new generation list
            - else:
                - insert the parents to new generation list
     
    ![image](https://user-images.githubusercontent.com/43891138/225487853-3d315492-d34d-4730-a429-bac2d63d5de9.png)
----------------------------------------------------------------------
8. Mutation():  (swap mutation)
    - iterate over the population size:
        - parent1 = select random parent from new generation list
        - generate random double number from 0-->1
        - if the rn < mutation prob:
            - apply the swap mutation to parent1
            - evaluate its fitness
            - replace parent1 by mutated parent1 into the new gen list
            
  ![image](https://user-images.githubusercontent.com/43891138/225488092-c3f3da9e-0a3e-4fab-b990-aac92da6bd18.png)
  
 # How it works

https://user-images.githubusercontent.com/43891138/225491910-3dcd00f4-2f6e-49ce-8d10-dfbaf68d9948.mp4



