# Ant Colony
The Ant Colony algorithm is based on the real life example of ants. Ants find the shortest path from the nest to a food source by putting "pheromone" on the ground. When they have to pick a direction, they will now choose the direction with higher probability paths that are marked by stronger pheromone concentrations. A few of the ants will randomly pick other directions, while most of them will follow the pheromone markers.

## Algorithm
1. InitPheromoneValues to a low value
2. for every ant
    2. constructSolution based on the previously deposited pheromone trails. Most ants follow the existing trail, while some ants will follow a new trail. This is computated by a state transition rule.
3. Apply this pheromone trail on the components of their chosen solution
4. The total pheromone trail evaporates a bit based on the evaporation rate


```
/**
 * @author: Xavier Geerinck
 * @title: Heuristic - Ant Colony Optimization
 * @subtitle: 
 * @method: Ants find the shortest path from the nest to a food source by putting "pheromone" on the ground. When they have to pick a direction, they will now choose the direction with higher probabilith paths that are marked by stronger pheromone concentrations. A few of the ants will randomly pick other directions, while most of them will follow the pheromone markers.
 * 
 * @algorithm:
 * 1. InitPheromoneValues to a low value
 * 2. for every ant
 *     i. constructSolution based on the previously deposited pheromone trails. Most ants follow the existing trail, while some ants will follow a new trail. This is computated by a state transition rule.
 * 3. Apply this pheromone trail on the components of their chosen solution
 * 4. The total pheromone trail evaporates a bit based on the evaporation rate
 */
```

